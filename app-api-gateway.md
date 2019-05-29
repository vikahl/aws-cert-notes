# API gateway

- Service making it easy to publish, maintain, monitor and secure API´s
- Connects to Lambda, DynamoDB, EC2
- Can send each endpoint to a different target
- Scale effortlessly (no autoscaling groups or similar)
- Can throttle requests to prevent overflow attacks
- Can be monitored via CloudWatch
- Supports endpoint caching (with a set TTL)
- _Error: Origin policy cannot be read at the remote resource_ ⇒ CORS needs to be enabled on API gateway

## How to configure and deploy

1. Define an API
2. Define resources and nested resources (URL paths)
   1. Select supported http methods
   2. Set security
   3. Set target (EC2, Lambda, DynamoDB, …)
