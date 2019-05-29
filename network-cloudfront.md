# Cloudfront

- Content delivery network (CDN)
- User requesting content from edge locations, which either has it cached or retrieves it (and then caches)

## Terminology and concepts

- _Edge location_, location where the content will be cached. Separate to an AWS region/AZ.
  - Not read only, it's possible to write/put to them to.
- _Origin_, origin of the file, can be a S3 bucket, EC2 instance, elastic load balancer, Route53.
- _Distribution_, the CDN, consisting of a collection of edge nodes.
- Two types of distributions
  - _Web distribution_, typically used for websites
  - RTMP, used for media streaming
- Objects are cached for the time to live (TTL)
- Cached objects can be cleared, but it will be charged.
- Access can be restricted to signed URL or signed cookies.
