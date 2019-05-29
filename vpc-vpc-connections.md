# VPC connections

## Network access control lists (NACL)

- VPC automatically comes with a default network ACL that allows _all_ inbound/outbound
- Custom network ACL by default _deny_ all inbound/outbound
- Associates subnets with inbound and outbound rules
- Amazon recommends rules to be numbered in increments of 100, i.e. `100 TCP 80`, `200 TCP 22`, …
  - Rules are evaluated in numerical order, so for blocking 80 on a specific IP that rule needs to be lower than the rule allowing everyone on port 80.
- Open ephemeral ports are short lived ports used for outbound communication and needs to be allowed out in the rules
  - A NAT gateway uses ports 1 024—65 535
- Network ACL acts before security groups (so if a port is denied in network ACL it will never reach the SG)
- Network ACLs can block IP addresses (security groups can't)
- A network ACL can be associated with multiple subnets, however, a subnet can only be associated with one network ACL.
- Network ACL are stateless: responses to allowed inbound traffic are subject to rules for outbound traffic (and vice versa)

### NACL or security groups (SG)

- SG operate at instance level
- NACL are stateless, SG are stateful
- SG evaluates all rules before deciding traffic

## Bastion hosts

- Special purpose computer on a network specifically designed and configured to withstand attacks.
- Generally hosts a single application, such as proxy server, and everything else is removed to reduce threat.
- Specific AMI's suitable for bastion hosts exists.

## AWS Direct connect

- Directly connects data centres to AWS
- Useful for high throughput workloads (= lots of network traffic) or if a stable and reliable secure station is needed

## VPC endpoints

- Enables privately connect a VPC to supported AWS services without requiring Internet gateway or similar.
- Endpoints are virtual devices, horizontally scaled
- Allows for example an EC2 instance to connect to S3 without needing outbound traffic to Internet  
  note: if the S3 connection is hanging it's because the region needs to be specified in the cli (`--region eu-west-1`)

Two types of VPC endpoints

- Interface endpoints
  - supported for a load of services
- Gateway endpoints
  - supported for S3 and DynamoDB
