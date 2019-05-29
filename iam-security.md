# AWS Identity Access Management

- Manage users and their level of access
- AWS IAM offers
  - centralized control of your AWS account
  - shared access to your AWS account
  - granular permissions
  - provides temporary access for users/devices
  - identity federation (including active directory, Facebook, Linkedin, …)
- IAM is universal, it does not apply to regions.
- New users has _no_ permissions when created, all permissions needs to be assigned.

## Key terminology

- _Users_, end users.
- _Groups_, a collection of users with shared permissions
- _Policies_, gives permissions on what to do
- _Roles_, added to AWS resources and allows using other resources (for example allowing EC2 to communicate with S3)

## Best practices

- Always set up MFA on root account
- Do not use access keys on root account.

## IAM roles instead of AWS access keys

- Attaching a role to EC2 instance allows for cli access from that EC2 instance with the permissions of the role, without having to store credentials on the machine itself.
- Roles are easier to manage, access keys needs to be updated on every machine while roles can just be updated centrally
- Roles can be assigned to EC2 instance after it is created.

## Amazon Cognito

- Web identity federation service: Let users access resources after successfully authenticated with Amazon, Facebook or Google.
- Provides temporary credentials, mapped to IAM role, allowing access to resources without application needing to embed or store credentials locally.
- Synchronizes user data for multiple services (using SNS push), if user updates something on web it will be instantly synced to apps.
- Recommended for all mobile AWS services

[Illustration of authentication in action](assets/app-cognito-pools.png)

## User pools

- User based, handles user registration, authentication, account recovery, …
- Cognito acts as an identity broker between identity provider and AWS
- Successful auth generates JWT

## Identity pools

- Actual granting of permissions to use resources
- Provide temporary credentials to access AWS services (S3, DynamoDB, …)
