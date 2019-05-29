# Moving data in and out of AWS or accessing it from on-site

## Snowball

- Petabyte-scale data transport solution that uses secure appliances to transfer data in/out of AWS.
- Can import to S3 or export from S3.
- Uses multiple layers of security to protect the data and device is securely erased after use.
- Snowball Edge is a combined compute and storage device, can for example run Lambda functions.  
  Used also as a temporary storage tier or support local workloads in remote of offline locations (e.g. airplane testing)
- AWS Snowmobile is a shipping container, on a truck.

## Storage gateway

- Provides seamless and secure integration between on-site it-environment and AWS storage infrastructure.
- Three different types
  - _File gateway_, stores flat files. Accessed through NFS, when files are transferred to S3 they can be managed with normal life cycles etc.
  - _Volume gateway_, disk volumes using iSCSI. Asynchronously backed up as snapshots and stored as EBS snapshots (snapshots are incremental backups that captures only changed blocks).
    - _Stored volumes_, primary data locally backing up to AWS. Entire dataset is available locally and offline.
    - _Cached volumes_, primary data in S3 while frequently accessed data is cached locally. Still provides access to all data, without needing to scale the on-premise storage infrastructure.
  - _Tape gateway_ (VTL), virtual tapes that allows for leverage existing tape-based backup infrastructure.
