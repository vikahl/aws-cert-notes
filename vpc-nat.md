# NAT instances & NAT gateways

- Solves the problem of instances in the private net needing to communicate out to Internet (for example to do updates)

## NAT instances

NAT instances are launched as ec2, search for _nat_ under _Community AMIs_. More information can be found in Amazon NAT instance help.

- Launch into public subnet
- Disable _source/destination check_
- Create route in main route table, destination: `0.0.0.0/0` -> instance (nat instance)

Not ideal solution, one single instance handles all forwarding and if that instance is crashed (overloaded, terminated, …) outbound connections will no longer work.
Possible to account of bottleneck issues by creating high availability using autoscaling groups, multiple subnets in different AZ's and scripts to automate failovers.

## NAT gateway

Better solution to NAT instance.

- Redundant inside AZ
- No need to patch/update the os
- Not associated with security groups and automatically assigned a public ip
- No need to disable source/destination checks
- Note: if resources in multiple AZ share one NAT gateway, in the event of the NAT gateways AZ is down, all instances will lose Internet access.  
  To create an AZ-independent architecture, create a NAT gateway in each AZ (and configure the routing to use the GW in same AZ)

Create new NAT gateway

- Create NAT gateway (under NAT gateways)
- Create route table entry `0.0.0.0/0 -> nat gateway`
