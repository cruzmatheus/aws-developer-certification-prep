# RDS - Relational Database Service
Managed SQL database. The following databases can be created:

- Postgres
- MySQL
- MariaDB
- Oracle
- Microsoft SQL Server
- Aurora (AWS proprietary database)

## Advantages
---
- Automated provisioning, OS patching
- Continuous backups and restore to specific timestamp (Poing in Time Restore)
- Monitoring dashboards
- Read replicas for improved read performance
- Multi AZ setup for Disaster Recovery
- Maintenance windows for upgrades
- Scaling capability (vertical and horizontal)
- Storage backend by EBS (gp2 or io1)

NOTE: It is not possible to SSH into it!

## Backups
---
- Enabled by default
- Automated backups:
    - Daily full backup of the database (during maintenance window)
    - Transaction logs are backed-up every 5 minutes
    - Ability to restore to any point in time (from oldest backup to 5 minutes ago backup)
    - 7 days retation period (can be increased to 35 days)

## Snapshots
---

- Manually triggered by the user
- Retention of backup for as long as the user wants

## Read Replicas
---

- Up to 5 Read Replicas
- Within AZ, Cross AZ and Cross Region
- Replication is ASYNC, so reads are enventually consistent
- Replicas can be promoted to their own DB
- Applications must update the connection string to leverage read replicas
- Can be setup as Multi AZ for Disaster Recovery
- Cannot execute INSERT, UPDATE and DELETE

Use case: Reporting application that performs a lot of READ operations

### Read Replicas - Network Cost

- There is a network cost when data goes from one AZ to another (due to replication process)
- If the Read Replica remains in the AZ, there is no charges

## Multi AZ for Disaster Recovery
---
- SYNC Replication
- One DNS name - automatic app failover to stand by database
- Failover in case of loss of AZ, loss of network, instance or storage failover
- No manual intervention in apps
- Not used for scaling

## Encryption
---
- Possible to encrypt the master & Read Replicas with AWS KMS - AES-256 encryption
- Is defined at launch time
- If the master is not encrypted, the Read Replicas <u>CANNOT</u> be encrypted

### In-flight encryption

- SSL certificates to encrypt data to RDS in flight
- Provide SSL options with trust certificate when connecting to database

### Encrypt operations

- Snapshot of un-encrypted RDS databases are un-encrypted
- Snapshots of encrypted RDS database are encrypted
- It is possible to copy a snapshot into an encrypted one

## IAM Authentication
---
- Only for MySQL and Postgres
- Just the IAM token is needed