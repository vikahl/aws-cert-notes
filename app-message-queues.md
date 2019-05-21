# Message queues

## SQS

- Distributed queue system that enables web applications to get access to a message queue
- Allows for decoupling infrastructure
- Pull based, ec2 instances needs to go in and pull messages from the queue
- Messages are 256 Kb in size (can be larger but then S3 is used)
- Messages can be kept in queue from 1 minute to 14 days, default is 4 days
- Visibility time out: the time that the message is invisible in the queue after a reader picks up the message  
  If the job is not processed within the visibility time, the message will be come visible again and another reader will process it
  Useful since it allows messages to be processed even if ec2 instances dies.  
  Maximum 12 hours
- Short polling returns immediately
- Long polling allows to poll and wait until message arrives (or poll times out)
- Two types of queues
  - Standard queues (default)
    - High capacity
    - Guarantee of message delivery
    - However, messages might be delivered multiple times and might be out of order
  - First in first out (IFO) queues
    - Order is preserved and no duplications
    - Supports message groups, allowing multiple ordered message groups within a queue
    - Limited to 300 transactions per second (TPS)

## Simple work flow service (SWF)

- Web service making it easy to coordinate work across distributed application components
- Used to coordinate tasks
- Tasks represents invocations of various processing steps in an application which can be performed by code, web service calls, human actions
- Example: used by Amazon when ordering from the web store. Multiple processing steps (place order, deduct credit card) and _human actions_ (pick order in warehouse)
- Workflow executions can last up to 1 year
- Presents a task oriented API (whereas SQS offers a message-oriented API)
- Ensures that a task is assigned only once and never duplicated
- Keeps track of all the tasks and events in an application (in SQS application-level tracking needs to be implemented by yourself)

- SWF actors
  - Workflow starters, an application that can initiate a workflow. Example: web shop following the placement of an order
  - Deciders, controls the flow of activity tasks in a workflow execution. If something has finished or failed, decider decides what to do next.
  - Activity workers, carries out the task

# Simple notification service (SNS)

- Web service allowing push notifications to mobile devices, sms, email, SQS queues, HTTP endpoint
- Instantaneous push-based delivery (no polling)
- Pub/sub using topics
- Inexpensive, pay-as-your-go model with no upfront
- Easy configured in the web console

## SNS vs SQS

- Both are message services
- SNS: push
- SQS: pull/poll
