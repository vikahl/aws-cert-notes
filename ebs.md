# Elastic block store (EBS)

## Five different types

- General purpose (SSD). IOPS/volume: 16 000  
  Balances price and performance for a wide variety of transactional workloads
- Provisioned IOPS (SSD). IOPS/volume: 64 000  
  Highest performance SSD designed for mission-critical applications, i.e. databases.
- Throughput optimized (HDD). IOPS/volume: 500  
  Low cost for frequently accessed, throughput intensive workloads, i.e. big data and data warehouse
- Cold (HDD). IOPS/volume: 250  
  Lowest cost designed for less frequent access, i.e. file servers
- EBS magnetic. IOPS/volume: 40-200 
  Previous generation HDD, used where data is infrequently accessed.

## Key topics

- EBS is always in the same available zone as the instance.
- Volumes can be resized or volume type can be changed on the fly (the instance does not need to be stopped).
- Terminating instance (by default) terminates root instance. Additional volumes are however kept.

## Moving between available zones

Moving a volume (and instance) can be achieved by:

1. Creating a snapshot of the volume  
  Can be done when the instance is running, but to ensure consistency the instance should be stopped.
2. Create an image (AMI) from the snapshot
3. Use that image to launch a new EC2 instance

That AMI can be copied to another region to start a new instance in another region.

## Instance store vs EBS

- All AMIs are categorized as either backed by EBS or instance store.
- The root device for instance launched from  
  - EBS AMI is created from an EBS snapshot
  - instance store AMI is created from a template stored in S3
- Instance store is ephemeral storage and do not persist between reboots

## Encrypt root device volumes & snapshots

- Normally the root device cannot be encrypted when creating an instance through the web ui launch.
- Snapshots of encrypted volumes are encrypted automatically.
- Volumes restored from encrypted snapshots are encrypted automatically.
- Snapshots can be shared, but not if they are encrypted.

### Creating an encrypted root volume

1. Create a snapshot of the volume
2. Copy the snapshot and select to encrypt this copy
3. Create AMI (image) from the snapshot, resulting in an encrypted image
4. Launch a new instance which will have the root device encrypted.

