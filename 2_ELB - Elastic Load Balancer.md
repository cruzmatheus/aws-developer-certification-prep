# ELB - Load Balancer

Can scale but it is not instantaneous.

## Classic Load Balancer - 2009 (CLB)
* HTTP, HTTPS, TCP

## Application Load Balancer - 2016 (ALB)
* HTTP, HTTPS, WebSocket
* Great fit for microservices
* Can route based on:
    * URL path (/users, /posts)
    * hostname (one.example.com, other.example.com)
    * Query Strings (?id=123&order=false)
* Target groups:
    * EC2 instances
    * EC2 tasks
    * Lambda functions
    * Ip addresses
* Can map to multiple target groups
* Health check are at the target group level

## Network Load Balancer - 2017 (NLB)
* TCP, TLS (secure TCP) & UDP
* Forward TCP & UDP traffic to instances
* Handle millions of request per second
* Less latency ~ 100ms (vs 400ms ALB)
* Has one static IP per AZ (support Elastic IP)
* Used for extreme performances
* Not included in free tier


## Stickiness
---
* Works for Classic and Application Load Balancers
* The "cookie" user for stickiness has an expiration date manueally controlled
* May bring imbalance to the load

## Cross-Zone Load Balancing
---
* Will distribute traffic through all Availability Zones
* If it isn't enable, the traffic will be distributed only inside the current AZ

For Classic Load Balancer:
* It is disabled by default
* Has no charge enabling Cross-Zone, if enabled

For Application Load Balancer:
* Always on (can't be disabled)
* Has no changes

For Network Load Balancer
* Disabled by default
* It is charged for Cross-Zone balacing, if enabled

## SSL/TLS Certificates
---
* The load balancer user an X.509 certificate (SSL/TLS server certificate)
* It is possible to manage certificates using ACM (AWS Certificate Manager)
* It is possible to upload my own certificate

### SNI - Server Name Indication

* Used to load multiple SSL certificates onto one web server
* Requires the client to indicate the hostname of the target server
* Only works for ALB and NLB
* Does not work for CLB (suports only one certificate)

## Connection Draining
---

Time to complete "in-flight requests" while the instance is de-registering or unhealthy


It makes ELB stop sending new requests to the instance which is de-registering.

Delay:
* Can be between 1 to 3600 seconds (default is 300 seconds)
* Can be disabled (set value to 0)

Feature naming:
* CLB: Connection Draining
* Target Group: Deregistration Delay (for ALB & NLB)

## ASG - Auto Scaling Group
---
* Scaling policies can be on CPU, Network... and can even be omn custom metrics or based on a schedule
* Uses launch configurations or launch templates
* To update a ASG, a new launch configuration/template is needed
* IAM roles attached to an ASG will get assigned to EC2 instances
* ASG are free. The payment is for the resource being launched
* Having instances over ASG means that if they get terminated, for whatever reason, the ASG will automatically create new ones as a replacement
* ASG can terminate instances marked as unhealthy by LB (and replace them)

### Scaling Policies

* Target Tracking Scaling
    * Most simple and easy to set-up
    * Example: I want the average ASG CPU to stay at aroung 40%

* Simple / Step Scaling
    * When a CloudWatch alarm is triggered (example CPU > 70%)    , then add 2 unit
    * When a CloudWatch alarm is triggered (example CPU < 30%)    , then remove 1 unit

* Scheduled Actions
    * Anticipate a scaling based on known usage patterns
    * Example: Increase the min capacity to 10 at 5 pm on Fridays    