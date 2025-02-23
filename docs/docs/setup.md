
**PROJECT SETUP**:

**📌INSTRUCTIONS** :

###
• Create a custom VPC with subnets, route tables, and security groups.
• Launch a Windows Server EC2 instance in the VPC.
• Connect to the Windows Server using RDP (Remote Desktop Protocol).
• Test internet connectivity from the Windows Server.
###


🔹 Step 1: Create a Custom VPC
1️⃣ Login to AWS Console
1. Open AWS Management Console → Navigate to VPC service.


2️⃣ Create a VPC
1. Click "Create VPC" → Choose "VPC only" option.
2. Enter: 
a. VPC Name: Custom-VPC
b. IPv4 CIDR block: 10.0.0.0/16
c. Leave IPv6 and other options as default.
3. Click Create VPC.
🔹 Step 2: Create Subnets


3️⃣ Create a Public Subnet
1. Go to Subnets → Click "Create subnet".
2. Select: 
a. VPC: Custom-VPC
b. Subnet Name: Public-Subnet
c. Availability Zone: Choose any (e.g., us-east-1a)
d. IPv4 CIDR block: 10.0.1.0/24
3. Click Create Subnet.


4️⃣ Create a Private Subnet (Optional)
1. Repeat the above steps but with: 
a. Subnet Name: Private-Subnet
b. CIDR Block: 10.0.2.0/24
c. No Auto-assign public IP.
🔹 Step 3: Create and Attach an Internet Gateway (IGW)


5️⃣ Create an Internet Gateway (IGW)
1. Navigate to Internet Gateways → Click Create Internet Gateway.
2. Enter Name: Custom-IGW → Click Create.
3. Select Custom-IGW → Click Actions → Attach to VPC → Select Custom-VPC → 
Click Attach.
🔹 Step 4: Configure Route Tables


6️⃣ Create a Route Table for Public Subnet
1. Navigate to Route Tables → Click Create Route Table.
2. Enter: 
a. Name: Public-RT
b. VPC: Custom-VPC
3. Click Create Route Table.
4. Select Public-RT → Click Routes → Edit Routes → Add Route: 
a. Destination: 0.0.0.0/0
b. Target: Custom-IGW
5. Click Save Changes.


7️⃣ Associate Route Table to Public Subnet
1. Go to Subnet Associations → Edit Subnet Associations.
2. Select Public-Subnet → Click Save Changes.
🔹 Step 5: Create a Security Group for Windows Server


8️⃣ Create a Security Group (SG)
1. Navigate to Security Groups → Click Create Security Group.
2. Enter: 
a. Name: Windows-SG
b. VPC: Custom-VPC
3. Under Inbound Rules → Click Add Rule: 
a. RDP (Port 3389) → Source: My IP (your current public IP)
b. HTTP (Port 80) → Source: Anywhere (0.0.0.0/0) (optional, for web server 
access)
4. Click Create Security Group

.
🔹 Step 6: Launch Windows Server in the VPC
9️⃣ Launch an EC2 Instance
1. Navigate to EC2 → Click Launch Instance.
2. Choose AMI: 
a. Windows Server 2022
3. Choose Instance Type: 
a. t2. micro (Free Tier eligible).
4. Configure Instance Details: 
a. Network: Custom-VPC
b. Subnet: Public-Subnet
c. Auto-assign Public IP: Enable
5. Add Storage: Keep default (30GB).
6. Configure Security Group: Select Windows-SG.
7. Launch Instance and Download Key Pair (.pem).
🔹 Step 7: Connect to Windows Server via RDP


🔟 Get the Public IP
1. Navigate to EC2 → Select your Windows instance.
2. Copy the Public IP.
1️⃣1️⃣ Connect via Remote Desktop (RDP)
1. Open Remote Desktop Connection on your PC.
2. Enter Public IP and click Connect.
3. Enter Username: Administrator.
4. Get Password from AWS: 
a. Click EC2 Instance → Actions → Get Windows Password.
b. Upload the .pem key and decrypt the password.
5. Login to Windows Server. 


🔹 Step 8: Check Internet Connectivity
1️⃣2Test Internet in Windows Server
1. Open Command Prompt (cmd) → Type: ping google.com
2. If successful, internet is working.
3. failed, check Security Groups, Route Table, or Subnet Settings 