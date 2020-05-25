# ECS - Elastic Container Service

Has 3 flavors:
- ECS Classic
- Fargate
- EKS (Kubenetes)

## ECS Task Definition

- JSON form containing info on how to run a Docker container

## ECR - Elastic Container Registry

## IAM Roles

- EC2 instance profile is user by ECS agent
- Makes API call to ECS service
- Send container logs to CloudWatch Logs
- Pull Docker image from ECR

## ECS Task Role

- Allow each task to have a specific role
- Use different roles for the different ECS Services
- Task Role is defined in the task definition

## ECS Task Placement Strategies

- Binpack: Place tasks based on the least available amount of CPU or memory
- Random: Place the task randomly
- Spread: Place the task evenly based on the specified value (e.g. instanceId, attribute:ecs.availability-zone)

## ECS Task Placement Constraints

- distinctInstance: place each task on a different container instance
- memberOf: places task on instances that satisfy an expression

## ECS - Service Auto Scaling

- Target Tracking: target a specific average CloudWatch metric
- Step Scaling: scale based on CloudWatch alarms
- Scheduled Scaling: based on predictable changes
- ECS Service Scale (task level) differs from EC2 Auto Scaling (instance level)
- Fargate Auto Scaling is much easier to setup