# Cloudwatch

- Monitoring service to monitor AWS resources as well as the applications run on AWS.
- Host level metrics accessible from the hypervisor, consists of
  - CPU
  - Network
  - Disk
  - Status check
  - _but not memory usage_, that is handled by the OS
- EC2 instances will be monitored every 5 minutes by default
- Detailed monitoring (1 min interval) can be enabled, for new instances check _Enable Cloudwatch detailed monitoring_
- Alarms can notify when a threshold is hit and events helps responding to state changes in AWS resources.

## Cloudwatch or Cloudtrail

- Cloudwatch is about _performance_, Cloudtrail is about _auditing_ (API calls in the AWS platform).
- Often questions on exam trying to confuse Cloudwatch or Cloudtrail.
- Cloudtrail records management console actions and API calls to identify which users and accounts called AWS and their source IP.

## Lab: Create a billing alarm

Note: Billing alarms are not global, but uses a global metric (bill). All billing data in AWS is stored in US East.

1. Enable billing e-mails in _My billing dashboard_.
2. Go to CloudWatch and set up a new billing alarm.
3. ?
4. Profit (or at least less loss)
