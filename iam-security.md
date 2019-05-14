# AWS Identity Access Management

- Manage users and their level of access
- AWS IAM offers
  - centralized control of your aws account
  - shared access to your aws account
  - granular permissions
  - provides temporary access for users/devices
  - identity federation (including active directory, facebook, linkedin, …)
- IAM is universal, it does not apply to regions.
- New users has _no_ permissions when created, all permissions needs to be assigned.

## Key terminology

- Users, end users.
- Groups, a collection of users with shared permissions
- Policies, gives permissions on what to do
- Roles, added to aws resources to allow using other resources (for example allowing ec2 to communicate with s3)

## Best practices

- Always set up MFA on root account
- Do not use access keys on root account.

## IAM roles instead of AWS access keys

- Attaching a role to EC2 instance allows for cli access from that EC2 instance with the permissions of the role, without having to store credentials on the machine itself.
- Roles are easier to manage, access keys needs to be updated on every machine while roles can just be updated.
- Roles can be assigned to EC2 instance after it is created.
