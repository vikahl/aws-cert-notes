# Virtual private cloud (VPC)

_Important part of the exam, you need to be able to build VPC from memory_

- Logically isolated section of AWS where resources can be launched in a virtual network that you define (think of it as locial datacenters in AWS)
- Consists of IGWs (or virtual private gateways), route tables, network access control list, subnets and security groups.
- 1 subnet = 1 availability zone (you can have multiple subnets in same AZ, but not one subnet across multiple AZ)
- Allows for (for example) to create a public-facing subnet for webservers with Internet access and a private-facing subnet (without Internet) for backend system.
- Additionally, can create a hardware virtual private network (VPN) between datacenter and VPC and leverage the AWS cloud as an extension to the datacenter
- Network ACL are stateless (they can have both allow and deny rules)
- Security groups are stateful (they can only allow)
- Default VPC is user friendly, allowing to immediately deploy instances
  - All subnets in default VPC have a route out to Internet
  - Each EC2 instance has both public and private ip address

## VPC peering

- Connect one VPC with another via a direct network route using private ip addresses.
- Instances behaves as if they were on the same private network.
- VPC's can be peered with other aws accounts or other vpcs within same account.
- Peering is star configuration, i.e. 1 central vpc peers with 4 others.
- No transative peering, all vpcs needs to be paired on a 1-1 basis.
- Can peer across regions.

## Network ranges

- Useful resource for ip addresses and cidr range [CIDR.xyz](https://cidr.xyz)
- Private network ranges (by IANA), `10.0.0.0—10.255.255.255`, `172.16.0.0—172.31.255.255`, `192.168.0.0—192.168.255.255`
- Amazon reserves five addresses in the block
  - `.0` network address
  - `.1` vpc router
  - `.2` dns server
  - `.3` reserved for future use
  - `.255` network broadcast is not supported, so the address is reserved.

## Creating VPCs

- When a VPC is created, it also creates a default route table, network access control list and a default security group.
- No subnets nor default internet gateway are automatically created

- Enable auto-assign ip public ip addresses to allow launching publicly accessable ec2 instances into the subnet.
- Add internet gateway under "Internet gateways" and attach to VPC to enable a gateway into the subnet.
  - Only one Internet gateway can be added to a vpc
- Do not add route out to Internet to main route table since all new subnets will be automatically added to main route table and thus will all be accessable from Internet.
- Route tables out to the Internet
  - created with destination `0.0.0.0/0` (ipv4) and `::/0` (ipv6) and target of the Internet gateway.
  - associate subnet with the route table
- Launch ec2 instances with selecting the vpc under _network_ and the subnet under _subnet_

### Remember

- Security groups can't span VPCs
- Different security groups do not have access to each other (by default)
- Add a security group with open ports and source of the gateway to allow tunneling in

## VPC flow log

- Feature enabling capturing information about ip traffic to/from network interfaces in VPC
- Stored using Cloudwatch log
- Log group needs to be created in cloudwatch
- IAM group can be created automatically
- When a flow log has been created, it cannot be updated.
- Not all ip traffic is monitored, the following is not logged
  - traffic to amazon dns
  - Amazon Windows license activation
  - traffic to/from 169.254.169.254 (for metadata)
  - dhcp traffic
  - traffic to the reserved ip address for the default vpc router
