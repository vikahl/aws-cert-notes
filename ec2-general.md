# Elastic compute cloud (EC2)

- Provides resizable compute capacity in the cloud.
- Underlying hypervisors are Xen, or recently Nitro

## Pricing models

- On demand, pay a fixed rate by the hour (or second) with no commitment.
- Reserved, capacity reservation at a significant discount. Contract is 1 year or 3 year.
  - Standard reserved instances, up to 75% off. Does not allow converting instance type.
  - Convertible reserved instances, allows converting from t2 to r4 or similar.
  - Scheduled reserved instances, available to launch within a specific time window.
- Spot, enables bidding on excessive instance capacity, where the price fluctuates depending on supply and demand.  
  Instances will be terminated if price exceeds the set limit.  
  If Amazon terminates the instance you will not be charged for a partial hour of usage, however, if you terminate the instance you will be charged for any hour in which the instance ran.
- Dedicated hosts, physical ec2 server dedicated for your use.

## Fight Dr McPixie in Australia, instance type mnemonic

Not required for this certificate, but useful to know.

- F, FPGA
- I, IOPS
- G, graphics
- H, high disk throughput
- T, cheap general purpose
- D, density
- R, RAM
- M, main choice for general purpose apps
- C, compute
- P, graphics (pics)
- X, extreme memory
- Z, extreme memory _and_ cpu
- A, arm-based workloads
- U, bare metal

## Exam tips

- Termination protection is turned off by default, must be enabled.
- On EBS-backed instance, the default action for the root EBS is to be deleted when instance is terminated.
- EBS root volumes of default AMI's cannot be encrypted. Third party tools can be used, or done when creating AMI's in the AWS console or API.
- Additional volume can be encrypted.

## Security groups

- Groups can be edited in the _Security groups_ tab under _Network & security_.
- Changes in security group takes effect immediately.
- Inbound rules are stateful, if an inbound rule is allowing traffic in, that traffic is automatically allowed out again.
- Multiple security groups can be assigned to a specific instance.
- All inbound traffic is blocked by default. All outbound traffic is allowed by default.
- Rules can allow, but not deny, nor block specific ip addresses (instead use network access control lists)
- Instead of IP addresses, ports can be opened for another security group

## Placement group

- Clustered placement group
  - Groupment of instances within a _single_ AZ
  - Recommended for applicatinos that needs low network latency or high network throughput (or both)
  - Only certain instances can be launched into clustered placement group
- Spread placement group
  - Each instance is placed on a distinct hardware
  - Recommended for applications that have a small number of critical instances
  - Can span multiple AZ
- AWS recommends homogenous instances within placement groups
- Placement groups can be merged
- Existing instances can't be moved into a placement group. Instead, create an AMI from an existing instance and launch a new instance from the AMI into the group.














