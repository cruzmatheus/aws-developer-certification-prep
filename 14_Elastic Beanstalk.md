# Elastic Beanstalk

## Deployment modes

### All at once

- Fastest deployment
- Application has downtime
- Great for quick iteractions in development environment
- No additional cost

### Rolling

- Application is running bellow capacity
- Can set the bucket size
- Application, at some point, is running bothe versions simultaneously
- No additional cost
- Long deployment

### Rolling with additional batches

- Same as Rolling but runs at full capacity
- Small additional cost
- Good for prod

### Immutable

- Zero downtime
- New code is deployed to new instances on a temporary ASG
- High cost
- Double capacity
- Quick rollback in case of failures
- Great for prod

### Blue / Green deployment

- Zero downtime and release facility
- Create a new stage environment and deploy v2 there
- Route 53 can be setup using weghted policies to redirect a little bit of traffic to the stage environemnt

## Lifecycle policy
- Elastic Beanstalk can store at most 1000 application versions
- When the limit of application versions is reached, it is not possible to deploy additional versions
- There are 2 policies:
    - Based on time: older versions are removed first
    - Based on space: when having too many versions
- Versions that are currently used won't be deleted