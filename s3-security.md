# AWS S3 Security and Encryption

- Bucket acess is controlled by bucket policies and access control list (ACL).
- Access logs can be configured, showing all requests made to the bucket. These logs can be sent to another bucket (even another account).

## Encryption types

- Encryption in transit is achieved by SSL/TLS
- Encryption at rest (server side) is achieved by:
  - S3 managed keys (SSE-S3)
  - AWS key management service, managed keys (SSE-KMS/AWS-KMS)
  - Server side encryption with customer provided keys (SSE-C)
- Client side encryption, encrypt file on client side before upload
