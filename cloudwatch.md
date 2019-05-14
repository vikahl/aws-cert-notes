# Cloudwatch

- Monitoring service to monitor AWS resources as well as the applications run on AWS.
- Host level metrics accessable from the hypervisor, consists of
  - CPU
  - Network
  - Disk
  - Status check
  - but not memory usage, that is handled by the OS
- With EC2 will monitor events every 5 minutes (by default)
- With detailed monitoring, 1 minute intervals (enabled for new EC2 by checking _Enable Cloudwatch detailed monitoring_)
- Dashboards to visualize what is happening.
- Alarms to notify when a threshold is hit.
- Events helps responding to state changes in AWS resources.
- Logs helps to aggregate, monitor and store logs.

## Cloudwatch or Cloudtrail

- Cloudwatch is about _performance_, Cloudtrail is about _auditing_ (API calls in the AWS platform).
- Usual question on exam trying to confuse cloudwatch or cloudtrail.
- Cloudtrail records management console actions and api calls to identify which users and accounts called aws and their source ip.

## Lab: Create a billing alarm

Note: Billing alarms are not global, but it uses a global metric (bill). All billing data in AWS is stored in US East.

1. Enable billing e-mails in _My billing dashboard_.
2. Go to CloudWatch and set up a new billing alarm.
3. ?
4. Profit (or at least less loss)
