# Route 53

- Managed DNS domain
- Global service (does not rely on AZs)
- Most common records:
    - A: hostname to IPv4
    - AAAAA: hostname to IPv6
    - CNAME: hostname to hostname
    - Alias: hostname to AWS resource
- Can use:
    - public domain names
    - private domain names that can be resolved by VPC
- Has:
    - Load balancing
    - Health checks
    - Routing policy

## TTL - Time to Live
---
It's a value (int) configured in Route53 and used by the browser to cache the result of the DNS resolve result

## CNAME
---
- AWS resource (Load Balancer, CloudFront...) expose an AWS hostname
- Only work for non root domain (ex: <u>something</u>.mydomain.com)

## Alias
---
- Points a hostname to an AWS Resource (app.mydomain.com => blabla.amazonaws.com)
- Works for root domain and non toor domain (ex: mydomain.com)
- Free of charge
- Native health check

## Weighted Routing Policy
- Control de percentage of the requests that go specific endpoint
- Helpful for:
    - Testing 1% of traffic on new app version
    - Split traffic between two regions
- Can be associated with Health Checks