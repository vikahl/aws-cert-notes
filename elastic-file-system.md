# Elastic file system (EFS)

- Elastic file storage for EC2 instances, using NFSv4 to enable sharing
- No pre-provisioning required (only pay for the storage used), and can scale to Pb
- Supports thousands of concuccernt NFS connections.
- Data is stored across multiple AZ within a region.
- Read after write consistency
- Amazon EFS utils tool can be installed with bootstrap script (in amazon linux: `yum install -y amazon-efs-utils`
- EFS and EC2 needs to be in the same security group
- Mount instructions can be found when checking the EFS system in the web console
