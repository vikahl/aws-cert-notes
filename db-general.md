# Databases

## Relation database services (RDS)  

- "Normal" database: _database > tables > roles_
- RDS runs on virtual machines, but you cannot log in to these machines
- Patching of the RDS OS is Amazons responsibility
- RDS is _not_ serverless (exept for Aurora serverless)
- Amazon supports: Microsoft SQL server, Oracle, MySQL server, PostgreSQL, Amazon Aurora, MariaDB

Two key features

- Multi-AZ, for disaster recovery
  - Allows an exact copy of a db in another AZ, which will be automatically synchronized
  - If failure, maintenance or similar, Amazon will _automatically_ failover to the standby
  - Disaster recovery only, will not increase performance

- Read replicas, for scaling/performance
  - Primarily for very read-heavy database workloads  
  - No automatic fail-over, the dns needs to be updated manually
    Half the EC2 instances can point to the read replica and the other to the primary to increase performance
  - Can have 5 read replicas for a database (and read replicas of read replicas, but that might increase latency)
  - Automatic backups must be turned on
  - Read replicas can have Multi-AZ turned on
  - Can be promoted to their own database (breaks replication)
  - Can exist in another region from the primary
  - Possible to force a failover from one AZ to another by rebooting the instance

## Non-relation databases

- _Collection (table) > document (row) > key-value pairs (fields/columns)_ (key-value pairs does not need to exist in all records in non-relation databases)
- DynamoDB (Amazons NoSQL solution)
  - supports both documents and key-value
  - stored on ssd across three geographical distinc data centers (both speed and redundancy)
  - database is partitioned across a number of nodes, each responsible for a defined block of data (in SQL syntax it's called sharding)
  - two consistency models
    - eventual consistent read (default)  
      consistency is usually reached within a second, best read performance
    - strongly consistent read  
      a read returns a result that reflects all writes that recieved a successful response prior to the read

## Other services

- Redshift, data warehousing
- Elasticache, an in-memory cache
  - In memory cache with Memcached or Redis
  - Memcached, scales horizontally, multi-threaded, no persistence, no backup/restore
  - Redis, advanced data types, pub/sub, persistence, backup/restore, multi-AZ

## Backups

Two types of backups

- Automated backups
  - Allows recovery of the database to any point in time within a "retention period" (1–35 days)
  - Will take full daily snapshots and store transactions logs during the day
  - When restoring, the most recent daily backup will be used as a base and the transactions will then be applied
  - Stored in S3, free storage equal to the size of the database (10 Gb RDS instance = 10 Gb free backup)
  - During the defined backup window, storage i/o might be suspended
- Snapshots
  - Taken manually
  - Stored after the original RDS is deleted

- When database is restored (snapshot or automatic), it will be a new RDS instance with a new DNS endpoint

## Encryption

- Encryption at rest is supported for MySQL, Oracle, SQL server, PostgreSQL, MariaDB and Aurora.
- With encryption turned on, everything will be encrypted (backups, snapshots, …)
