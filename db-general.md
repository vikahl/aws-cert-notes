# Databases

## Relation database services (RDS)  

- RDS is _not_ serverless, it runs on virtual machines, but it's not possible to log in to these machine.  
  _Exception is Aurora serverless which is a serverless RDS_
- Don't have to worry about OS or patching, Amazon takes care of that.
- Amazon supports: Microsoft SQL server, Oracle, MySQL, PostgreSQL, Amazon Aurora, MariaDB
- Encryption at rest is supported and will encrypt everything (backups, snapshots, …)

Key features

- Multi-AZ, for _disaster recovery_
  - Allows an exact copy of a db in another AZ, which will be automatically synchronized
  - If failure, maintenance or similar, Amazon will _automatically_ fail over to the standby
  - Disaster recovery only, will not increase performance

- Read replicas, for _scaling/performance_
  - No automatic fail-over, the DNS needs to be updated manually
  - Example of usage: half the EC2 instances can point to the read replica and the other half to the primary, thus increasing performance
  - Possible to have 5 read replicas for one database (and read replicas of read replicas, but that might increase latency)
  - Automatic backups must be turned on
  - Read replicas can have multi-AZ turned on
  - Read replicas can be promoted to their own database (breaks replication)
  - Do not need to be in the same region as the primary database.
  - Force switching AZ is possible by rebooting the instances (just as EC2 instances)

Two types of backups

- Automated backups
  - Allows recovery of the database to any point in time within a "retention period" (1–35 days)
  - Will take full daily snapshots and store transactions logs during the day
  - When restoring, the most recent daily backup will be used as a base and the transactions will then be applied
  - Stored in S3, free storage equal to the size of the database (10 GB RDS instance = 10 GB free backup)
  - During the defined backup window, storage io might be suspended
- Snapshots
  - Taken manually
  - Still stored after the original RDS is deleted

- When database is restored (snapshot or automatic), it will be a new RDS instance with a new DNS endpoint

### Amazon Aurora

- MySQL/PostgreSQL compatible relational database, up to 5 times better performance than MySQL
- Migrating is easy by creating read-replicas of MySQL/PostgreSQL and then promote to standalone database

- Starts with 10 GB, scales with 10 GB increments to 64 Tb (storage autoscaling)
- Compute resources can scale up to 32vCPU and 244 GB memory
- 2 copies of data is contained in each AZ (for regions with minimum of 3 AZ) (= 6 copies of data)
- Designed to transparently handle loss of 2 copies without affecting write availability and 3 copies without affecting read
- Self-healing, data blocks and disks are scanned for errors and repaired automatically
- Two types of replicas: Aurora replicas (up to 15) and MySQL replicas (up to 5)
- Automated backups are always enabled and neither automatic or manual backups affects performance

## DynamoDB, Amazons non-relation database (NoSQL)

_Uses collection (table) > document (row) > key-value pairs (fields/columns) and (key-value pairs does not need to exist in all records in non-relation databases)_

- Supports both documents and key-value
- Stored on ssd across three geographical distinct data centres (both speed and redundancy)
- The db is partitioned across a number of nodes, each responsible for a defined block of data (in SQL syntax it's called sharding)
- Two consistency models possible
  - eventual consistent read (default)  
    consistency is usually reached within a second, best read performance
  - strongly consistent read  
    a read returns a result that reflects all writes that recieved a successful response prior to the read

## Amazon Redshift

- Data warehouse service used for complex queries
- Can start small and scales to petabytes
- Only supports single-AZ deployments

- Two configurations
  - Single node (160 GB)
  - Multi node
    - Leader node, manages client connections and receives queries
    - Compute node, store data and perform computation and queries. Up to 128 compute nodes.
- Uses advanced compression techniques to achieve significant compression compared to RDS.
- Does not require indexes or materialized views = even less space
- Massively parallel processing (MPP), automatically distributes data and query loads across all nodes.
- Backup is enabled by default with 1 day retention period (supports up to 35 days)
- Attempts to maintain at least three copies of the data (original, replica on compute nodes, backup in S3)
- Can asynchronously replicate across multiple regions

### Pricing

- Compute node hours (1 unit per node per hour). Leader node is not charged.
- Backup
- Data transfer within a VPC

### Security

- Encrypted in transit with SSL
- Encrypted at rest using AES-256
- RedShift takes case of key management (but it can be customized)

## Other database services

- Elasticache, an in-memory cache
  - In memory cache with Memcached or Redis
  - Memcached, scales horizontally, multi-threaded, no persistence, no backup/restore
  - Redis, advanced data types, pub/sub, persistence, backup/restore, multi-AZ
