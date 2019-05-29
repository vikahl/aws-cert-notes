# Virtual private cloud (VPC)

_Important part of the exam, you need to be able to build VPC from memory_

- Logically isolated section of AWS where resources can be launched in a virtual network that you define (think of it as local datacenters in AWS)
- Consists of IGW's (or virtual private gateways), route tables, network access control list, subnets and security groups.
- 1 subnet = 1 availability zone (you can have multiple subnets in same AZ, but not one subnet across multiple AZ)
- Allows (for example) to create a public-facing subnet for web servers with Internet access and a private-facing subnet (without Internet) for back end system.
- Additionally, can create a hardware virtual private network (VPN) between datacenter and VPC and leverage the AWS cloud as an extension to the datacenter
- Default VPC is user friendly, allowing to immediately deploy instances
  - All subnets in default VPC have a route out to Internet
  - Each EC2 instance has both public and private IP address

## VPC peering

- Connect one VPC with another via a direct network route using private IP addresses.
- Instances behaves as if they were on the same private network.
- VPC's can be peered with other AWS accounts or other VPC's within same account.
- Peering is star configuration, i.e. 1 central VPC peers with 4 others.
- No transitive peering, all VPC's needs to be paired on a 1-1 basis.
- Peering can be done across regions.

## Network ranges

- Useful resource for IP addresses and CIDR range [CIDR.xyz](https://cidr.xyz)
- Private network ranges (by IANA), `10.0.0.0—10.255.255.255`, `172.16.0.0—172.31.255.255`, `192.168.0.0—192.168.255.255`
- Amazon reserves five addresses in the block
  - `.0` network address
  - `.1` VPC router
  - `.2` DNS server
  - `.3` reserved for future use
  - `.255` network broadcast is not supported, so the address is reserved.

## Creating VPC's

- When a VPC is created, by default the following components are created:
  1. default route table
  2. network access control list (NACL)
  3. default security group
- No subnets nor default Internet gateway are automatically created

- Enable auto-assign IP public IP addresses to allow launching publicly accessible EC2 instances into the subnet.
- Add Internet gateway under "Internet gateways" and attach to VPC to enable a gateway into the subnet.
  - Only one Internet gateway can be added to a VPC
- Do not add route out to Internet to main route table since all new subnets will be automatically added to main route table and thus will all be accessible from Internet.
- Launch EC2 instances with selecting the VPC under _network_ and the subnet under _subnet_

## Enable Internet access to VPC

- Attach an Internet gateway to the VPC
- Add a route table out to the Internet, either globally scoped (`0.0.0.0/0` or `::/0`) or scoped to a narrower range if needed.
- Ensure that the instances in the subnet have a globally unique IP address (public IPv4, Elastic IP or IPv6)  
  _All instances has a private IPv4 address and the instance itself is only aware of the IPv4 address_
- Ensure that the NACL and SG rules allows relevant traffic to and from instances

## VPN connections

- When connecting a VPN between AWS and a third party site, the customer gateway is created within AWS but contains information about the third party site (IP address and type of routing)
- Virtual private gateway has information regarding the AWS side of the VPN and connects a specific VPC to VPN
- AWS transit gateway is a transit hub that can be used to interconnect the VPC and on-premise network

## Remember

- Security groups can't span VPC's
- Different security groups do not have access to each other (by default)
- Add a security group with open ports and source of the gateway to allow tunnelling in

## VPC flow log

- Feature enabling capturing information about IP traffic to/from network interfaces in VPC
- Stored using Cloudwatch log
- Log group needs to be created in Cloudwatch
- IAM group can be created automatically
- When a flow log has been created, it cannot be updated.
- Not all IP traffic is monitored, the following is not logged
  - Traffic to Amazon DNS
  - Amazon Windows license activation
  - Traffic to/from 169.254.169.254 (for metadata)
  - DHCP traffic
  - Traffic to the reserved IP address for the default VPC router
