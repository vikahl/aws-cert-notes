# Route53 routing policies

## Simple routing  

- One record with multiple ip addresses. Records will be returned in random order.

## Weighted routing

- Traffic is split based on different weights
- Multiple records are created with one ip in each one, as well as the weight and set id (custom name unique within weight group)
- Records can be automatically omitted based on Route53 healthchecks (health checks can also send a notice)
- Adds up all weights in the record set, then ports the request accordingly.

## Latency-based routing

- Traffic is routed based on lowest network latency for end users (which might be the nearest region but can also be one further away)
- A latency resource record set for EC2/ELB resource in each region that hosts the website and Route53 selects the region with lowest latency

## Failover routing

- Used to create active/passive set up, e.g. primary site in eu-west-2 and secondary site in ap-southeast-2.
- Endpoints are monitored with Route53 healthchecks
- If active goes down, passive will be used

## Geolocation routing

- Traffic is routed based on geographical location (continent or countries)
- A default record can handle both queries from ip addresses that aren't mapped to any location and queries that come from locations that have no specific record.
- If no record exist for location, no result will be returned

## Geoproximity routing

_Not in scope for the solutions architect associate_

- Only used in conjunction with Route 53 traffic flow
- Traffic to resources are routed based on geographical location of users and resources 
- Optionally, biased can be used to route more or less traffic to a given resource

## Multivalue answer routing

- Like simple routing, but allows for healthcheck to only return healthy resources.
- Create one record for each resource (EC2/…)
