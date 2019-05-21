# Load balancers

## Exam tips

- Read the ELB faq for classic load balancers

## General

- If responding with 504 (Gateway timeout) it means that the _application_ is having issues (web server, database …)
- `X-Forwarded-For` header  
  When user hits LB and is forwarded to web server, that requests origins from the LB ip address.
  However, the `X-Forwarded-For` header still contains the original (user) ip.

## Load balancer types

- Application load balancer (ALB)
  - application-aware, can for example detect a changed language on a website
  - suited for http/https
  - operate at layer 7
- Network load balancer (NLB)
  - suited for tcp traffic where extreme performance is required
  - operate at layer 4 (connection layer)
  - capable of handling millions of requests per second, while maintaining ultra-low latency
  - have a fixed ip address
- Classic load balancer (CLB)
  - legacy load balancer
  - can balance http/https
  - can use layer 7 features but not application aware
  - can also use strict layer 4

## Creating load balancers

- Classic load balancer is quite straightforward, just follow the guide.
- Application load balancer; first create a target group that can target instances and register instances in the target group.  
  (optional) create advanced rules from the _Listeners_ > _View/edit rules_

## Sticky sessions

- CLB routes each request independently to the ec2 with smallest load
- Sticky sessions allows to bind a user's session to a specific ec2 instance
- Can be enabled for ALB, but will operate on target group
- If there is an EC2 instance that don't get any traffic, try disabling sticky sessions

## Cross zone load balancing

- With cross zone load balancing disabled (no cross zone…) load balancers can not send traffic across AZ.
- Default is to have it disabled.
- Example: Route 53 routes 50%/50% of traffic between two AZ. One AZ has 4 ec2 instances, the other has 1.  
  Result is that the 4 instances will split 50% => 12.5% per instance while the other will get 50% of traffic.  
  With cross zone enabled, each instance will get 20% of traffic.

## Path patterns

- A listener with rules to forward requests based on the URL path.
- For microservices, traffic can be routed to multiple backends based on paths (for example general request to one target group and requests to generate images to another)
