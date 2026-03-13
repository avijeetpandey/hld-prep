## Distributed logging system

Functional requirements
- Ingestion -  Ability to collect logs from various microservices 
- Storage - Persist logs for a pre defined retention period ( Eg 30 days)
- Search / Analysis - users should be able to query logs by type, timestamp or keyword
- Realtime  - should be able to view logs near-real time

Non functional requirements
- Highly availble
- Highly scalable
- Low latency ingestion
- Fault tolerant