# AWS-enterprise-network-lab


Simulated enterprise network architecture in AWS demonstrating subnet segmentation, security access control , DMZ web hosting


![VPC Flow Screenshot](./screenshots/aws-console/VPC-Flow.png)


## 📋 Project Overview

Enterprise network simulation demonstrating:
- **5 Segmented Subnets** (Management, IT, Sales, HR, DMZ)
- **Multi-layer Security** (Security Groups + NACLs)
- **Bastion Host Architecture**
- **Department-level Isolation**

## 🏗️ Network Architecture

**VPC:** 10.10.0.0/16

| Subnet | CIDR | Type | Purpose |
|--------|------|------|---------|
| Management | 10.10.0.0/27 | Public | Bastion, NAT Gateway |
| IT | 10.10.0.64/26 | Private | DNS, AD, File Server |
| Sales | 10.10.0.128/26 | Private | CRM, Applications |
| HR | 10.10.0.192/26 | Private | Payroll, HR Portal |
| DMZ | 10.10.1.0/26 | Public | Web Server |

![VPC Flow Screenshot](./screenshots/aws-console/ascii-art-image.png)

# 🖥️ AWS EC2 Instances Setup

As part of this project, three EC2 instances were created in the AWS console to simulate a segmented network environment. Each instance serves a different purpose and resides in a designated subnet.

### Instances Overview

| Instance Name | Purpose | Network Zone | Description |
|----------------|----------|---------------|--------------|
| **mgmt** | Management Server | Management Subnet | Used for administrative access and centralized management of other instances. |
| **dmz** | Web/DMZ Server | DMZ Subnet | Exposed to the internet to host public-facing applications or web services. |
| **hr** | Internal Application Server | Internal Subnet | Hosts HR or internal business applications not directly accessible from the internet. |

![DMZinstance](./screenshots/aws-console/DMZ-instance.png)
![HR-instance](./screenshots/aws-console/HR-instance.png)
## 🔒 Security Implementation

## Security Groups

![Management SG](./screenshots/security-groups/MG-security.png)
![DMZ SG](./screenshots/security-groups/DMZ-Security.png)

  Internal-SG [HR,IT,Sales]
  
![Interna-SG](screenshots/security-groups/Internal-Security.png)

## 🚦 Routing Configuration

**Public Route Table** (Management & DMZ):
- 10.10.0.0/16 → local
- 0.0.0.0/0 → Internet Gateway

**Private Route Table** (IT, Sales, HR):
- 10.10.0.0/16 → local
- 0.0.0.0/0 → NAT Gateway

![Private-Route Table](./screenshots/aws-console/routing-PV.png)
![Public-Route Table](./screenshots/aws-console/routing-public.png)


### Test Evidence
![Local to Management](./screenshots/testing/Mgmt-Test.png)
![Management to HR](./screenshots/testing/Mgmt-HR.png)
![Management to DMZ](./screenshots/testing/Mgmt-DMZ.png)

## 🌐 Web Application Deployment

### Apache Web Server in DMZ

A functional web server was deployed in the DMZ subnet to demonstrate public-facing infrastructure:
![DMZ web page](./screenshots/aws-console/DMZ-Web.png)

## 🎯 Key Achievements

✅ Enterprise-grade VPC with proper CIDR allocation  
✅ Multi-layer security (Security Groups + NACLs)  
✅ Department isolation preventing lateral movement  
  

## 🛠️ Technologies Used

- AWS VPC, EC2, Internet Gateway, NAT Gateway
- Security Groups & Network ACLs
- Amazon Linux 2
- SSH/SCP for secure access

## 🚀 Future Enhancements

- [ ] Grafana monitoring dashboards
- [ ] VPC Flow Logs integration
- [ ] Application Load Balancer
- [ ] Auto Scaling Groups
- [ ] CloudWatch alarms
