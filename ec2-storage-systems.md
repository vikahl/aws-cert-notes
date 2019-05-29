# File storage for EC2

## Elastic block store (EBS)

### Five different types

- _General purpose_ (SSD). IOPS/volume: 16 000  
  Balances price and performance for a wide variety of transactional workloads
- _Provisioned_ IOPS (SSD). IOPS/volume: 64 000  
  Highest performance SSD designed for mission-critical applications, i.e. databases.
- _Throughput optimized_ (HDD). IOPS/volume: 500  
  Low cost for frequently accessed, throughput intensive workloads, i.e. big data and data warehouse
- _Cold_ (HDD). IOPS/volume: 250  
  Lowest cost designed for less frequent access, i.e. file servers
- _EBS magnetic_. IOPS/volume: 40-200  
  Previous generation HDD, used where data is infrequently accessed.

### Key topics

- EBS is always in the same available zone as the instance.
- Volumes can be resized or type can be changed on the fly (the instance does not need to be stopped).
- Terminating instance (by default) terminates root instance. Additional volumes are by default kept.

### Moving between regions

Moving a volume (and instance) can be achieved by:

1. Creating a snapshot of the volume  
   Can be done when the instance is running, but to ensure consistency the instance should be stopped.
2. Create an image (AMI) from the snapshot
3. Use that image to launch a new EC2 instance

That AMI can be copied to another region and used to start copies of the instance

### Instance store or EBS

- All AMI's are categorized as either backed by EBS or instance store.
- The root device for instance launched from:  
  - EBS AMI is created from an EBS snapshot
  - instance store AMI is created from a template stored in S3
- Instance store is ephemeral storage (RAM) and do not persist between reboots

### Encrypt root device volumes & snapshots

- Snapshots of encrypted volumes are encrypted automatically.
- Volumes restored from encrypted snapshots are encrypted automatically.
- Snapshots can be shared, but not if they are encrypted.
- Normally root volumes cannot be encrypted, but they can be created by:
  1. Create a snapshot of the volume
  2. Copy the snapshot and select to encrypt this copy
  3. Create AMI (image) from the snapshot, resulting in an encrypted image
  4. Launch a new instance which will have the root device encrypted.

## Elastic file system (EFS)

- Elastic file storage for EC2 instances, using NFSv4 to enable sharing
- No pre-provisioning required (only pay for the storage used), and can scale to Pb
- Supports thousands of concurrent NFS connections.
- Data is stored across multiple AZ within a region.
- Read after write consistency
- Amazon EFS utilities tool can be installed with bootstrap script (in Amazon Linux: `yum install -y amazon-efs-utils`
- EFS and EC2 needs to be in the same security group
- Mount instructions can be found when checking the EFS system in the web console
