# Amazon Aurora

- MySQL/PostgreSQL compatible relational database, up to 5 times better performance than MySQL
- Aurora read replicas can be made from MySQL databases (which can be promoted to a standalone database and thus migrate from MySQL to Aurora)

- Start with 10 Gb, scales with 10 Gb increments to 64 Tb (storage autoscaling)
- Compute resources can scale up to 32vCPU and 244 Gb memory
- 2 copies of data is contained in each AZ (for regions with minimum of 3 AZ) (= 6 copies of data)
- Designed to transparently handle loss of 2 copies without affecting write availability and 3 copies without affecting read
- Self-healig, datablock and disks are scanned for errors and repaired automatically
- Two types of replicas: Aurora replicas (up to 15) and MySQL replicas (up to 5)

- Automated backups are always enabled and do not impact performance
- Snapshots can be taken manually (does not impact performance)
- Snapshots can be shared with other AWS accounts
