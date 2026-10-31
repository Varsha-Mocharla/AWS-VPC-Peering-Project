# AWS VPC Peering – Secure Communication Between Two VPCs

## Project Overview

This project demonstrates how to establish secure network communication between two separate Amazon Virtual Private Clouds (VPCs) using **AWS VPC Peering**.

The project uses private EC2 instances in two VPCs and a Bastion Host to provide controlled SSH access. Route tables and security groups are configured to enable communication between the private instances.

## AWS Architecture

**AWS Region:** Asia Pacific (Sydney) – `ap-southeast-2`

| Component | Configuration |
|---|---|
| VPC A | `10.10.0.0/16` |
| VPC B | `10.20.0.0/16` |
| VPC A public subnet | `10.10.1.0/24` |
| VPC A private subnet | `10.10.2.0/24` |
| VPC B private subnet | `10.20.1.0/24` |
| Bastion Host | Public subnet in VPC A |
| App-A | Private subnet in VPC A |
| App-B | Private subnet in VPC B |
| Connectivity | AWS VPC Peering |

## AWS Services Used

- Amazon VPC
- VPC Peering
- Amazon EC2
- Subnets (Public and Private)
- Route Tables
- Internet Gateway
- Security Groups
- SSH and ICMP connectivity testing

## Implementation Steps

1. Created two VPCs with non-overlapping CIDR ranges.
2. Created public and private subnets.
3. Configured an Internet Gateway for public connectivity in VPC A.
4. Launched a Bastion Host in the public subnet.
5. Launched App-A and App-B in private subnets.
6. Created and accepted a VPC Peering connection.
7. Added routes to the relevant route tables in both VPCs.
8. Configured security groups to allow required SSH and ICMP traffic.
9. Connected to private EC2 instances through the Bastion Host.
10. Tested communication between App-A and App-B in both directions.

## Connectivity Testing

The following tests were performed:

| Test | Result |
|---|---|
| SSH from Bastion to App-A | Successful |
| SSH from Bastion to App-B | Successful |
| Ping from App-A to App-B | Successful |
| Ping from App-B to App-A | Successful |
| Security Group restriction test | Expected traffic blocking observed |
| Connectivity after restoring the rule | Successful |

The bidirectional ping tests completed with 4 packets transmitted and 4 received, with 0% packet loss.

## Security Configuration

- Private EC2 instances do not have public IPv4 addresses.
- SSH access to private instances is routed through the Bastion Host.
- SSH access to the Bastion Host is restricted to the configured source.
- Security groups allow only the required traffic for this lab.
- ICMP access is restricted to the specified private instance addresses.

## Project Evidence

The detailed project report includes the architecture, AWS configuration screenshots, route table settings, security group rules, SSH access, connectivity tests, and troubleshooting evidence.

**[View the Project Report (PDF)](Varsha_EWB_VPC_Peering_Project_Report.pdf)**

## Learning Outcomes

- Understanding AWS VPC networking.
- Configuring public and private subnets.
- Implementing VPC Peering.
- Configuring route tables and security groups.
- Accessing private EC2 instances through a Bastion Host.
- Testing private network connectivity.
- Troubleshooting routing and security group configurations.

## Conclusion

Successfully implemented and tested private communication between two AWS VPCs using VPC Peering. The project demonstrates network routing, controlled access, and secure communication between private EC2 instances.

---

**Project Type:** AWS Cloud Networking  
**Status:** Completed
