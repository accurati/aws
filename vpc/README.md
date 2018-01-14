
# Cloud Formation - Default VPC

This cloud formation script defines a default VPC in AWS. The VPC defines 4 subnet groups:
- DMZ - Internet facing Subnet
- Frontend (FE) - Used for web-servers
- Backend (BE) - User for service layer servers
- Database (DB) - For database layer services

Each subnet group is created in 3 different Availability Zones (AZ): a, b and c.

## VPC Cidr block

The VPN cidr block is `/16`, which means you should select the `x.y.0.0/16` subnet at
the setup moment.

## Subnet blocks

It defines three blocks:

### DMZ
- `x.y.10.0/24` (Availability Zone a)
- `x.y.20.0/24` (Availability Zone b)
- `x.y.30.0/24` (Availability Zone c)


### Front End (FE)
- `x.y.11.0/24` (Availability Zone a)
- `x.y.21.0/24` (Availability Zone b)
- `x.y.31.0/24` (Availability Zone c)


### Back End (BE)
- `x.y.12.0/24` (Availability Zone a)
- `x.y.22.0/24` (Availability Zone b)
- `x.y.32.0/24` (Availability Zone c)

### Database (DB)
- `x.y.13.0/24` (Availability Zone a)
- `x.y.23.0/24` (Availability Zone b)
- `x.y.33.0/24` (Availability Zone c)


## Routing table

+ Only the DMZ subnet group has access to the internet gateway placed on Availability Zone a.
+ All other subnets have routing to the internet through the Nat Gateway placed on AZ a as well.


## Access Control List details

Only DMZ is exposed to the internet and only port 22 is open to the world. Also the ephemeral ports egress traffic is allowed only from the world to the DMZ area.

All other networks can talk each other without any restriction yet. It will be changed in the future.


## Bastion Host

This script also creates a bastion host which should be used to access all hosts in the private networks without exposing them to the Internet. At the end of the CloudFormation script execution, the bastion public IP address will be provided in the Output section.
