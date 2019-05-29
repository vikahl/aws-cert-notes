# NAT instances & NAT gateways

- Solves the problem of instances in the private net needing to communicate out to Internet (for example to do updates)

## NAT instances

NAT instances are launched as EC2, search for _nat_ under _Community AMIs_. More information can be found in Amazon NAT instance help.

- Launch into public subnet
- Disable _source/destination check_
- Create route in main route table, destination: 0.0.0.0/0 ⇒ instance (NAT instance)

Not an ideal solution, one single instance handles all forwarding and if that instance is crashed (overloaded, terminated, …) outbound connections will no longer work.
Possible to account of bottleneck issues by creating high availability using autoscaling groups, multiple subnets in different AZ and scripts to automate failover.

## NAT gateway

Better solution than NAT instance.

- Redundant inside AZ
- No need to patch/update the OS
- Not associated with security groups and automatically assigned a public IP
- No need to disable source/destination checks
- Note: if resources in multiple AZ share one NAT gateway, in the event of the NAT gateways AZ is down, all instances will lose Internet access.  
  To create an AZ-independent architecture, create a NAT gateway in each AZ (and configure the routing to use the gateway in same AZ)

Create new NAT gateway

- Create NAT gateway (under NAT gateways)
- Create route table entry 0.0.0.0/0 ⇒ NAT gateway

## Egress-only Internet gateway

- Used for IPv6 (NAT instances/gateways are used for IPv4)
- IPv6 addresses are globally unique and therefore public by default
- Stateful
