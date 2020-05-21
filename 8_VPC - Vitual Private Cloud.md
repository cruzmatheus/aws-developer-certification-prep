# VPC - Virtual Private Cloud

- AZ scoped
- Can have multiple subnets. Subnets are AZ scoped
- Public subnet can access the internet (through a Internet Gateway)
- Private subnet cannot access the internet
- Route tables are used to define access to the internet and between subnets

## NAT - Network Address Translation
---
Allow the private subnets to access the internet, while remaining private.

It's placed at the public subnet and communicates directly with the Internet Gateway, to access the internet.

Can be:
- NAT Gateways (AWS managed)
- NAT Instances (self-managed)

## Network ACL
---
- Firewall which controls traffica from and to the subnet
- Can have ALLOW and DENY rules
- Are attached at <u>Subnet</u> level
- Rules only include IP addresses

## VPC Flow Logs
---
Can capture information about IP traffic of:
- VPC
- Subnet
- Elastic Network Interface