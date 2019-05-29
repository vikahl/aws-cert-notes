# Elastic compute cloud (EC2)

## Exam tips

- Termination protection is turned off by default, must be enabled.
- On EBS-backed instance, the default action for the root EBS is to be deleted when instance is terminated.
- EBS root volumes of default AMI's cannot be encrypted, but can be encrypted in the OS. Alternatively, an encrypted AMI can be created ⇒ new instances will be encrypted.
- Non-root volumes can always be encrypted

- Provides resizeable compute capacity in the cloud.
- Underlying hypervisors are Xen, or recently Nitro

## Pricing models

Four different pricing models available

1. _On demand_, pay a fixed rate by the hour (or second) with no commitment.
2. _Reserved_, capacity reservation at a significant discount. Contract is 1 year or 3 year.
   - _Standard reserved_ instances, up to 75% off. Does not allow converting instance type.
   - _Convertible reserved_ instances, allows converting between instance types
   - _Scheduled reserved_ instances, available to launch within a specific time window.
3. _Spot_, enables bidding on excessive instance capacity, where the price fluctuates depending on supply and demand.  
  Instances will be terminated if price exceeds the set limit. If Amazon terminates the instance you will not be charged for a partial hour of usage, however, if you terminate the instance you will be charged for any hour in which the instance ran.
4. _Dedicated hosts_, physical EC2 server dedicated for your use.

## Fight Dr McPixie in Australia, instance type mnemonic

Not required for this certificate, but useful to know and required for more advanced certificates.

- F, FPGA
- I, IOPS
- G, graphics
- H, high disk throughput
- T, cheap general purpose
- D, density
- R, RAM
- M, main choice for general purpose apps
- C, compute
- P, graphics (pictures)
- X, extreme memory
- Z, extreme memory _and_ CPU
- A, ARM-based workloads
- U, bare metal

## Security groups

- Groups can be edited in the _Security groups_ tab under _Network & security_.
- Changes in security group takes effect immediately.
- Inbound rules are stateful, if an inbound rule is allowing traffic in that traffic is automatically allowed out again.
- Multiple security groups can be assigned to a specific instance.
- All inbound traffic is blocked by default. All outbound traffic is allowed by default.
- Rules can only allow traffic, use NACL for blocking ports or IP addresses.
- Ports could be opened for specific security groups apart for specifying IP addresses.

## Placement group

- _Clustered_ placement group
  - Groupment of instances within a _single_ AZ
  - Recommended for applications that needs low network latency or high network throughput
  - Only some instance types can be launched into clustered placement group
- _Spread_ placement group
  - Each instance is placed on a distinct hardware
  - Recommended for applications that have a small number of critical instances
  - Can span multiple AZ
  - Maximum of 7 instances per AZ
- AWS recommends homogeneous instances within placement groups
- Placement groups can be merged
- Existing instances cannot be moved into a placement group.  
  Instead, create an AMI from an existing instance and launch a new instance from the AMI into the group.

## Bootstrap scripts

- Scripts that are run when EC2 instances are _launched_
- Entered under _configure instance_ > _user data_
- Start with shebang, i.e. `#!/bin/bash`

## EC2 instance metadata

- Local API on `http://169.254.169.254` (private IP address space)
- List of metadata endpoints found on `/latest/meta-data/`
- Bootstrap script from `/latest/user-data/`
