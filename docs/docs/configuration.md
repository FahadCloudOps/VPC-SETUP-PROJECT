


 **Configuration Details**
 
 ***Creating a Custom VPC and Accessing Windows Server on AWS***



This project involves configuring a custom VPC with subnets, route tables, security groups, and an Internet Gateway to launch and access a Windows Server EC2 instance securely. Below are the key configuration details:

1️⃣ VPC Configuration
VPC Name: Custom-VPC
IPv4 CIDR Block: 10.0.0.0/16
IPv6 CIDR Block: Not used
Tenancy: Default


2️⃣ Subnet Configuration
Public Subnet

Name: Public-Subnet
CIDR Block: 10.0.1.0/24
Availability Zone: (e.g., us-east-1a)
Auto-assign Public IP: Enabled
Private Subnet (Optional)

Name: Private-Subnet
CIDR Block: 10.0.2.0/24
Auto-assign Public IP: Disabled


3️⃣ Internet Gateway (IGW)
Name: Custom-IGW
Attached to VPC: Custom-VPC


4️⃣ Route Table Configuration
Public Route Table (Public-RT)

Associated with: Public-Subnet
Routes:
0.0.0.0/0 → Custom-IGW (for internet access)
Private Route Table (Optional, for Private-Subnet)

Not configured for internet access unless NAT Gateway is added


5️⃣ Security Group Configuration (Windows-SG)
VPC: Custom-VPC
Inbound Rules:
RDP (Port 3389) → Source: My IP (Restrict access for security)
HTTP (Port 80, optional) → Source: 0.0.0.0/0 (For web server access)
Outbound Rules:
Allow all traffic (0.0.0.0/0)


6️⃣ EC2 Instance Configuration (Windows Server)
AMI: Windows Server 2022
Instance Type: t2.micro (Free Tier eligible)
Network: Custom-VPC
Subnet: Public-Subnet
Auto-assign Public IP: Enabled
Security Group: Windows-SG
Storage: 30GB EBS (Default)
Key Pair: Download and store .pem file safely for RDP access


7️⃣ Remote Desktop (RDP) Access
Retrieve Public IP from EC2 instance
Open Remote Desktop Connection (RDP)
Enter:
Username: Administrator
Password: Retrieved from "Get Windows Password" (using .pem key)
Verify successful login and test internet connectivity (ping google.com)

###**This configuration ensures a secure and functional AWS network with a Windows Server accessible via RDP, following best practices for VPC, subnets, routing, and security rules**### 🚀