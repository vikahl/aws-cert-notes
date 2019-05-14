# Cloudfront

- Content delivery network (CDN)
- User requesting content from the edge location, either it is cached or it will be retrieved.

## Terminology and concepts

- Edge location, location where the content will be cached. Separate to an AWS region/AZ.
- Origin, origin of the file, can be a S3 bucket, EC2 instance, elastic load balancer, Route53.
- Distribution, the CDN, consisting of a collection of edge nodes.
- Two types of distributions
  - Web distribution, typically used for websites
  - RTMP, used for media streaming
- Edge locations are not just read only, it's possiblet to write/put to them to.
- Objects are cached for the time to live (ttl)
- Cached objects can be cleared, but it will be charged.
- Accessed can be restricted to signed urls or signed cookies.
