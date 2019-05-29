# Route53 routing policies

## Simple routing  

- One record with multiple IP addresses. Records will be returned in random order.

## Weighted routing

- Traffic is split based on different weights
- For multiple IP for one domain, create multiple records with one IP in each one, as well as the weight and set id (custom name unique within weight group)
- Records can be automatically omitted based on Route53 health checks (health checks can also trigger an alarm)
- Weights are arbitrary, all weights in the record set is added and requests are ported accordingly.

## Latency-based routing

- Traffic is routed based on lowest network latency for end users, which might be the nearest region but can also be one further away
- A latency resource record set for EC2/ELB resource in each region that hosts the website and Route53 selects the region with lowest latency

## Failover routing

- Used to create active/passive set up, e.g. primary site in _eu-west-2_ and secondary site in _ap-southeast-2_.
- Endpoints are monitored with Route53 health checks and if active goes down passive will be used

## Geolocation routing

- Traffic is routed based on geographical location (continent or countries)
- A default record can handle both queries from IP addresses that aren't mapped to any location and queries that come from locations that have no specific record.
- Results will only be returned if record exists

## Geoproximity routing

_Not in scope for the solutions architect associate_

- Only used in conjunction with Route 53 traffic flow
- Traffic to resources are routed based on geographical location of users and resources
- Optionally, biased can be used to route more or less traffic to a given resource

## Multivalue answer routing

- Like simple routing, but allows for health check to only return healthy resources.
- Create one record for each resource (EC2/…)
