# Message queues

## SQS

- Distributed queue system that enables web applications to get access to a message queue
- Pull based, consumers (EC2 instances, …) needs to pull messages from the queue
- Size limit of 256 KB per message (larger messages are possible, but then S3 is used for storage)
- Messages can be kept in queue from 1 minute to 14 days, default is 4 days
- The time the message is invalid in the queue after a reader picks up the message is called _visibility time out_. Maximum of 12 hours.  
  If the job is picked up, but not processed within the visibility time, the message will be visible on the queue again (dead letter queue, DLQ) and another reader will process it.

Two polling strategies:

- Short polling, messages are returned immediately. If queue is empty, nothing will be returned.
- Long polling, allows for polling empty queues and wait until message arrives (or polling times out)

Two types of queues

- Standard queues (default)
  - High capacity
  - Guarantee of message delivery
  - Drawback: messages might be delivered multiple times and might be out of order
- First in first out (FIFO) queues
  - Order is preserved and no duplications will occur
  - Supports message groups, allowing multiple ordered message groups within a queue
  - Limited to 300 transactions per second

## Simple work flow service (SWF)

- Used to coordinate work (tasks) across distributed application components
- Tasks are steps that can be performed by code, remote web calls or _human action_.  
  Example: a web store which has multiple processing steps (place order, deduct credit card) and _human actions_ (pick order in warehouse)
- Workflow executions can last up to 1 year
- Presents a task oriented API (whereas SQS offers a message-oriented API)
- Ensures that a task is assigned only once and never duplicated
- Keeps track of all the tasks and events in an application (in SQS application-level tracking needs to be implemented by yourself)

- SWF actors
  - _Workflow starters_, an application that can initiate a workflow, e.g. web shop when order is placed.
  - _Deciders_, controls the flow of activity tasks in a workflow execution, decides what to do if task has finished or failed.
  - _Activity workers_, carries out the work.

## Simple notification service (SNS)

- Web service allowing push notifications to mobile devices, sms, e-mail, SQS queues, HTTP endpoints
- Instantaneous push-based delivery (no polling)
- Pub/sub using topics
- Inexpensive, pay-as-your-go model with no upfront
- Easy configured in the web console

## SNS or SQS or SWF

- SNS and SQS are both message services
  - SNS: push
  - SQS: pull/poll
- SWF is task oriented
