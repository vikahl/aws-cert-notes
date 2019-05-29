# HA architecture

## Autoscaling

- Launch configuration are configurations on how instances should be launched into autoscaling groups
- Set a desired group size (i.e. _3 instances_)
- Can use policies to scale between _n₁_ and _n₂_ instances based on different metrics (CPU, …)
- Specify how many seconds instances need to warm up after scaling
- Useful even without policies since it can monitor and start new instances if they crashes.

## Architecture

- Always plan for failure
- Use multiple AZ and multiple regions if possible
- Know the difference between _multi-AZ_ (disaster recovery) and _read replicas_ for RDS (performance)
- Know the difference between _scaling out_ (add new instances to autoscaling group) and _scaling up_ (increase resources for instance)
- Know the different S3 classes

## Cloudformation

- A way to completely script the cloud environment (db servers, EC2 instances, …)
- Quick start templates allows for creating complex environments based on already built templates.

## Elastic beanstalk (ELB)

- Found under compute services
- Easier/different frontend for deploying applications to cloud without needing to know AWS
- Uses Cloudformation in the back
- Can use autoscaling, health monitoring, load balancing, …
