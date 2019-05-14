# Amazon Redshift

- Data warehouse service, used for complex querys
- Can start small, scale to petabytes
- Only available in 1 AZ

- Single node (160 Gb)
- Multi node
  - Leader node, manages client connections and receives queries
  - Compute node, store data and perform computation and queries. Up to 128 compute nodes.
- Uses advanced compression and multiple compression techniques to achieve significant compression compared to RDS.
- Does not require indexes or materialized views = even less space
- Massively parallel processing (MPP), automatically distributes data and query loads across all nodes.
- Backup is enabled by default with 1 day retention period (supports up to 35 days)
- Attempts to maintain at least three copies of the data (original, replica on compute nodes, backup in s3)
- Can asynchronously replica across multiple regions

## Priced as

- Compute node hours (1 unit per node per hour). Leader node is not charged.
- Backup
- Data transfer within a VPC

## Security

- Encrypted in transit with SSL
- Encrypted at rest using AES-256
- RedShift takes case of key management (but it can be customized)
