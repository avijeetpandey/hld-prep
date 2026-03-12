# FAQ's


1. How the System Works (The Flow)
Entry Point: Users (Buyers, Sellers, Admins) hit a Load Balancer, which distributes traffic to the API Gateway.

Orchestration: The Gateway routes requests to specific microservices:

Users/Items: Standard CRUD operations.

Bidding/Auction: The "hot" path where the real action happens.

The Bidding Loop: * When a bid is placed, the Bidding Service likely validates it and pushes an event to Kafka.

The Auction Processor Service (the brain) consumes from Kafka, determines the winner or the next highest bid, and updates the state.

Data Storage: * Metadata goes to RDS (Relational).

Item details/images go to S3/MongoDB.

Bidding history/state goes to DynamoDB and Redis.

Output: Results are pushed to a Notification Service (via Kafka) to alert users of outbids or wins.

2. Reasoning for Architectural Choices
Why MongoDB for Items Service?
Reasoning: Item descriptions change based on category (e.g., a "Car" has mileage; "Jewelry" has carats).

Pros: Flexible schema; easy to store unstructured blobs.

Cons: Not great for complex relational joins across many categories.

Why DynamoDB for Bidding/Auction?
Reasoning: Bidding requires extreme scale and low latency.

Pros: Seamless horizontal scaling (no downtime) and predictable millisecond performance. It handles the "write-heavy" nature of auctions better than standard SQL.

Cons: Limited querying capabilities compared to SQL.

Why Redis Cluster?
Reasoning: Likely used as a Distributed Lock or a Leaderboard.

Pros: In-memory speed. You need to know the "Current Highest Bid" instantly.

Cons: Data is volatile; if it crashes and isn't backed up, you lose the "instant" state (though DynamoDB acts as the persistent backup here).

3. The Kafka Cluster: The Core Engine
In this HLD, Kafka isn't just a "pipe"; it's the buffer and truth-sequencer.

Role: It decouples the Bidding Service (which accepts bids) from the Auction Processor (which validates them).

Why it's vital here: If 10,000 people bid on a rare item in 1 second, the DB might crash if hit directly. Kafka "absorbs" the spike, allowing the Processor to chew through bids at its own pace.

Order Matters: Kafka ensures that bids are processed in the order they were received (per auction ID using Partition Keys).

Scaling Kafka: You scale it by adding more Partitions. Each partition can be read by one consumer in a group, allowing you to parallelize the "Auction Processor Service."

Bottleneck: If a single auction becomes "too hot," one partition might get overloaded, leading to Consumer Lag (where the UI shows an old bid because the processor hasn't reached the latest message yet).