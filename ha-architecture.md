# HA architecture

## Autoscaling

- Launch configuration are configurations on how instances should be launched into autoscaling groups
- Set a desired group size (i.e. _start with 3 instances_)
- Can use policies to scale between _n₁_ and _n₂_ instances based on different metrics (cpu, …)
- Specify how many seconds instances need to warm up after scaling

## Architecture

- Always plan for failure
- Use multiple az's and multiple regions if possible
- Know the difference between _multi-AZ_ (disaster recovery) and _read replicas_ for RDS (performance)
- Know the difference between _scaling out_ (add new instances to autoscaling group) and _scaling up_ (increase resources in ec2, micro -> small, …)
- Know the different S3 classes

## Cloudformation

- A way to completely script the cloud environment (db servers, ec2 instances, …)
- Quick start templates allows for creating complex environments based on already built templates.

## Elastic beanstalk (ELB)

- Found under compute services
- Easier/different front end for deploying applications to cloud without knowing aws or worrying about infrastructure
- Uses cloud formation in the back
- Can use autoscaling, health monitoring, load balancing, …
