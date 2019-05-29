# AWS S3

_Simple, storage service_

IMPORTANT: Read the S3 FAQ before the exam, S3 takes up a large part of the exam.

- Object based ― i.e. allows for uploading files
  - _key_: name of the object
  - _value_: data, made up of a sequence of bytes
  - _version id_, used for versioning
  - _metadata_
  - _sub resources_
    - access control list (permissions to that object)
- Files can be from 0 B to 5 TB
- Multipart uploads is recommended for >100 MB and required for >5 GB
- Uploads returns a HTTP 200
- REST API is available for interaction

_S3 only supports object based storage. An alternative is blocked based storage, which is supported by EBS/EFS_

## Data consistency for S3

- Read after write consistency for new objects (PUT)
- Eventual consistency for overwrite (PUT) and deletes (DELETE), can take some time to propagate.  
  Means that if a file is updated/deleted and read immediately, you might get the new one or you might get the old one.

## Durability

- 11 x 9s, Amazon guarantees 99.99999999999% durability for the information  
  If stored 10 million objects, you can expect lose 1 object every 10 000 years.
- Best practices includes secure access permissions, cross-region replication, versioning and functioning, regularly tested backup.

## Features of S3

- Tiered storage available
- Life cycle management
- Versioning
- Encryption
- MFA delete
- Data is secured by Access control lists (ACL) and Bucket policies

## S3 storage classes

IMPORTANT: Knowledge about the different storage classes and the usage.

All storage classes except _one zone-IA_ is stored across multiple devices spanning at least three AZ. One zone-IA is stored redundantly within a single AZ.

- _Standard_, 99.99% availability, 11x9 durability
  - Stored redundantly across multiple devices in multiple facilities and designed to sustain the loss of two facilities concurrently
- _Infrequently accessed_ (IA), 99.9% availability
  - For data access less frequently, but requires rapid access when needed. Lower fee, but charges retrieval fee.
  - Data deleted within 30 days will be charged for full 30 days.
- _One zone infrequently accessed_, 99.5% availability
  - Lower-cost option for IA data and do not require the multiple availability zone data resilience.
- _Intelligent tiering_ (released in 2018)
  - Optimizing costs by using machine learning to move the data between tiers.
- _Glacier_  
  - Secure, durable and low-cost storage.
  - Data can be retrieved within 1-5 minutes (but at cost)
  - If data is deleted within 90 days of uploading, there will be an early deletion fee
- _Glacier deep archive_
  - Lowest cost storage class where a retrieval time of 12 hours is acceptable.
  - Very cheap, about $1 per TB-month.

## S3 billing and charging

- Storage
- Requests
- Storage management pricing
- Data transfer pricing
- Transfer acceleration  
  Uses CloudFront for fast, easy and secure transfer of files over long distances to end users.
- Cross region replication pricing  
  Replicate objects from one bucket to another in different regions (from US to AUS for example)

## S3 transfer acceleration and caching

- Transfer acceleration utilises the CloudFront edge network to accelerate uploads to S3.  
  Instead of uploading directly to the bucket, a distinct URL to upload to an edge location is used, which will then be transferred to the bucket.
- Speedtest tool to check which regions that are fastest to your current location

## S3 security and encryption

- Access logs can be configured, showing all requests made to the bucket. These logs can be sent to another bucket (even another account).
- Access can be controlled with four mechanisms
  1. IAM policies
  2. Bucket policies  
     Defines rules that applies broadly across all requests and can grant access such as write privilegies to a subset of S3 resources. Can also restrict access based on an aspect of the request such as HTTP referrer and IP address.
  3. Access control lists (ACL)  
     Can grant specific permissions (READ, WRITE, FULL_CONTROL, …) to specific users for a bucket/object.
  4. Query string authentication  
     An URL can be created that is only available for a limited time.

## Encryption types

- Encryption in transit is achieved by SSL/TLS
- Encryption at rest (server side) is achieved by:
  - S3 managed keys (SSE-S3)  
    Amazon handles key management
  - AWS key management service, managed keys (SSE-KMS/AWS-KMS)  
    Uses AWS key management service for managing keys.
  - Server side encryption with customer provided keys (SSE-C)  
    Customer provides/manages keys, but encryption is done server side.
- Client side encryption, encrypt file on client side before upload (for example by using Amazon S3 encryption client)

## Various S3 things

- Query in place  
  Run queries against data stored without the need to move data into a separate analytics platform, ⇒ enables the use of S3 as a data-lake.
- S3 select  
  Retrieve specific data from contents of an object using a SQL subset without having to retrieve the whole object. For example, using SELECT, WHERE from objects stored as csv, json. Can be integrated with Lambda or big data frameworks.
- Athena  
  Serverless, interactive query service for analysing data in S3 using SQL. Integrates with QuickSight for visualisation.
- Redshift Spectrum  
  Feature of Redshift for running queries against exabyte of unstructured data.
