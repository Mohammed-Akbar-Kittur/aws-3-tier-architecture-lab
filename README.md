# 3-Tier Web Architecture on AWS

<img width="1920" height="1280" alt="IMG-20261004-WA8491" src="https://github.com/user-attachments/assets/e4c1a1fa-2377-407a-b3fd-3ee3f60f67b2" />

> **Lab Status:** Built and tested in lab VPC 10.0.0.0/16, decommissioned after.

## Overview
Industry-standard 3-tier architecture with strict security and separation of concerns - presentation, application, and database layers isolated.

## Architecture
- Tier 1 Presentation: ALB in Public Subnets 10.0.1.0/24, 10.0.2.0/24
- Tier 2 Application: EC2 Apache in Private App Subnets 10.0.3.0/24, 10.0.4.0/24 (2 AZs)
- Tier 3 Database: RDS MySQL in Private DB Subnets 10.0.5.0/24, 10.0.6.0/24

## Security - Layered SGs
- ALB-SG: Inbound 80,443 from 0.0.0.0/0
- App-SG: Inbound 80 from ALB-SG only
- DB-SG: Inbound 3306 from App-SG only
- NAT Gateway for private subnets outbound only

## Tech Stack
VPC, ALB, EC2, RDS MySQL, IGW, NAT GW, Route Tables, Security Groups

## Validation
- Curl test: `curl http://ALB-DNS/` -> Apache page from private EC2 via ALB
- SG test: Direct curl to EC2 private IP from internet -> Timeout (secure as expected)
- DB test: `mysql -h RDS-endpoint -u admin -p` from App EC2 -> Connected, from bastion -> Timeout
- AZ failure: Terminated App EC2 in 1a -> ALB routed all traffic to 1b, no downtime
- 3-tier flow validated: User -> ALB -> App -> DB -> App -> User

## Outcome
- Enterprise-grade secure architecture implemented
- 100% isolated tiers - meets security best practices
- Scalable - each tier can scale independently
- Production-ready design used by real companies

---
## Author
**Mohammed Akbar Kittur**
DevOps Engineer | AWS | Linux | Terraform | Docker | Kubernetes
📍 Bangalore, Karnataka
🔗 [GitHub](https://github.com/Mohammed-Akbar-Kittur) | [LinkedIn](https://linkedin.com/in/mohammed-akbar-kittur)
