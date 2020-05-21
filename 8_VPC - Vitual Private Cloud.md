# VPC - Virtual Private Cloud

- AZ scoped
- Can have multiple subnets. Subnets are AZ scoped
- Public subnet can access the internet (through a Internet Gateway)
- Private subnet cannot access the internet
- Route tables are used to define access to the internet and between subnets
- 1 default VPC per Region

## NAT - Network Address Translation

Allow the private subnets to access the internet, while remaining private.

It's placed at the public subnet and communicates directly with the Internet Gateway, to access the internet.

Can be:
- NAT Gateways (AWS managed)
- NAT Instances (self-managed)

## Network ACL

- Firewall which controls traffica from and to the subnet
- Can have ALLOW and DENY rules
- Are attached at <u>Subnet</u> level
- Rules only include IP addresses

## VPC Flow Logs

Can capture information about IP traffic of:
- VPC
- Subnet
- Elastic Network Interface

## VPC Peering
Way of connecting two VPC with non overlaping IP ranges

## VPC Endpoint
Provide private access to AWS Services within VPC

## Site to Site VPN

- Connect an on-premises VPN to AWS
- Connectio is automatically encrypted
- Goes over the public internet

## Direct Connect (DX)

- Physical connection between on-premises and AWS
- Connection is private, secure and fast
- Goes over a private network
- Takes at least a month to establish
