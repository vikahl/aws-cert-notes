# Load balancers

## General

- If responding with 504 (Gateway time-out) it means that the _application_ is having issues (web server, database …)
- `X-Forwarded-For` header  
  When user hits LB and is forwarded to web server, that requests origins from the LB IP address.
  However, the `X-Forwarded-For` header contains the original (user) IP.
- All LB supports both IPv4 and IPv6, however, in a VPC, only IPv4 is supported.
- All LB supports https termination.

## Load balancer types

- _Application load balancer_ (ALB)
  - application-aware, e.g. can detect a changed language on a website
  - suited for http/https
  - operates at layer 7 (only)
  - supports websockets, http2 and is aware of the protocols
- _Network load balancer_ (NLB)
  - suited for TCP traffic where extreme performance is required
  - operate at layer 4 (connection layer)
  - capable of handling millions of requests per second, while maintaining ultra-low latency
  - have a fixed IP address
- _Classic load balancer_ (CLB)
  - legacy load balancer
  - can balance http/https
  - can use layer 7 features but is not application aware
  - can also use strict layer 4

## Creating load balancers

- Classic load balancer is quite straightforward, just follow the guide.
- Application load balancer
  - first create a target group that can target instances and register instances in the target group.
  - (optional) create advanced rules from the _Listeners_ > _View/edit rules_

## Sticky sessions

- By default CLB routes each request independently to the instance with smallest load
- Sticky sessions allows to bind a user's session to a specific EC2 instance
- Can be enabled for ALB, but will instead operate on target group (rather than instance)
- Troubleshooting: If there is an EC2 instance that don't get any traffic, try disabling sticky sessions

## Cross zone load balancing

- With cross zone load balancing disabled (no cross zone…) load balancers can not send traffic across AZ.
- Default is to have it disabled.
- Example: Route 53 routes 50%/50% of traffic between two AZ. One AZ has 4 EC2 instances, the other has 1. Result is that the 4 instances will split 50% => 12.5% per instance while the other will get 50% of traffic. With cross zone enabled, each instance will get 20% of traffic.

## Path patterns

- A listener with rules to forward requests based on the URL path.
- For microservices, traffic can be routed to multiple backends based on paths (for example general request to one target group and requests to generate images to another
