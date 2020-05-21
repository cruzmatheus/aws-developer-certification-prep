# Amazon Aurora
---

- Proprietary AWS technology
- Cloud optimized
- Has 5x better performance over MySQL and 3x over Postgres
- Storage automatically grows in increments of 10GB, up to 64 TB
- Can have 15 replicas (MySQL can only have 5)
- Failover is instantaneous. It is High Availability native
- Has a higher cost - 20% more

## High Availability and Read Scaling
---

- 6 copies of data across 3 AZ
- Self healing
- Auto expanding


## Failover
---
- One instance takes writes (master)
- Automatic failover for master in less than 30 seconds
- Supports Cross Region replication

## Cluster
----
- The master is the only instance that writes in the cluster
    - This is done via "Writer endpoint" (always point to the master even in failover)
- Since the Read Replicas can scale, there is a "Reader endpoint" that act as a Load Balancer between these Replicas

## Aurora Serverless
---

- Automated database instantiation and auto-scaling based on actual usage
- Good for infrequent, intermittnet or unpredictable workloads
- No capacity planning needed
- Pay per second, can be more cost-effective

## Global Aurora
---

- Cross Region Read Replicas
    - Useful for disaster recovery
- Aurora Global Database (recommended)
    - 1 Primary region (read / write)
    - Up to 5 secondary (read-only) regions, replication lag is less than 1 second
    - Up to 16 Read Replicas per secondary region
    - Helps for decreasing latency
    - Async replication