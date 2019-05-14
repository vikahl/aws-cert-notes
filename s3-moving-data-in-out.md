# Moving data in and out of AWS

## Snowball

- Petabyte-scale data transport solution that uses secure appliances to transfer data in/out of AWS.
- Can import to S3 and export to S3.
- Uses multiple layers of security to protect the data and device is securely erased after use.
- Snowball Edge is a combined compute and storage device, can for example run Lambda functions.  
  Used also as a temporary storage tier or support local workloads in remote of offline locations (e.g. airplane testing)
- AWS Snowmobile is a shipping container, on a truck.

## Storage gateway

- Provides seamless and secure integration between on-site it-environment and aws storage infrastructure.
- Three different types
  - File gateway, stores flat files. Accessed through NFS, when files are transfered to S3 they can be managed with normal life cycles et c.
  - Volume gateway, disk volumes using iSCSI. Asynchronously backed up as snapshots and stored as EBS snapshots (snapshots are incremental backups that captures only changed blocks). 
    - Stored volumes, primary data locally backing up to AWS. Entire dataset is available locally and offline.
    - Cached volumes, primary data in S3 while frequently accessed data is cached locally. Still provides access to all data, without needing to scale the on-premise storage infrastructure.
  - Tape gateway (VTL), virtual tapes that allows for leverage existing tape-based backup infrastructure.
