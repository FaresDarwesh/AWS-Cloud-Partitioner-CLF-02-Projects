# Project 7: VPC Networking 🌐

## Objective
Design and build a custom AWS VPC with public/private subnets, secure routing, and test connectivity between resources.

## AWS Services Used
- VPC (Virtual Private Cloud)
- Subnets (Public + Private across 2 AZs)
- Internet Gateway (IGW)
- NAT Gateway
- Route Tables
- Security Groups
- EC2 (Bastion Host + Private Instance)

## Architecture Overview
![VPC Architecture](screenshots/vpc-architecture.png)

## Steps

### Step 1: Create VPC
1. Go to **VPC Console** → **Create VPC**
2. Select **"VPC and more"** (الأفضل عشان يعمل حاجات كتير مع بعض)
3. Configure:
   - **Name tag:** `my-vpc-project7`
   - **IPv4 CIDR:** `10.0.0.0/16`
   - **Number of AZs:** 2
   - **Number of public subnets:** 2
   - **Number of private subnets:** 2
   - **NAT gateways:** 1 per AZ (أو 1 بس لو عاوز توفر)
   - **VPC endpoints:** None
   - **Enable DNS hostnames:** ✅ Yes
4. Click **Create VPC**

### Step 2: Verify Subnets
After creation, you'll see 4 subnets:
| Subnet Name | AZ | CIDR | Type |
|-------------|-----|------|------|
| public-1a | us-east-1a | 10.0.1.0/24 | Public |
| public-1b | us-east-1b | 10.0.2.0/24 | Public |
| private-1a | us-east-1a | 10.0.3.0/24 | Private |
| private-1b | us-east-1b | 10.0.4.0/24 | Private |

Rename them to meaningful names if needed.

### Step 3: Verify Internet Gateway
- Go to **Internet Gateways** in VPC Console
- You should see `igw-xxxxxxxx` attached to `my-vpc-project7`

### Step 4: Verify NAT Gateway
- Go to **NAT Gateways** in VPC Console
- Should be in `public-1a` with an **Elastic IP**
- State: `Available`

### Step 5: Verify Route Tables
**Public Route Table:**
- Destination: `10.0.0.0/16` → Target: `local`
- Destination: `0.0.0.0/0` → Target: `igw-xxxxxxxx`
- Associated with: public-1a, public-1b

**Private Route Table:**
- Destination: `10.0.0.0/16` → Target: `local`
- Destination: `0.0.0.0/0` → Target: `nat-xxxxxxxx`
- Associated with: private-1a, private-1b

### Step 6: Create Security Groups

**Bastion-SG:**
- Inbound: SSH (22) from `My IP`
- Outbound: All traffic

**Private-SG:**
- Inbound: SSH (22) from `Bastion-SG` (اختر الـ SG مش IP!)
- Outbound: All traffic

### Step 7: Launch EC2 Instances

**Bastion Host (Public Subnet):**
- Name: `bastion-host`
- AMI: Amazon Linux 2
- Instance type: t2.micro
- Network: `my-vpc-project7`
- Subnet: `public-1a`
- Auto-assign public IP: **Enable**
- Security Group: `Bastion-SG`
- Key pair: Create new or use existing

**Private Instance (Private Subnet):**
- Name: `private-instance`
- AMI: Amazon Linux 2
- Instance type: t2.micro
- Network: `my-vpc-project7`
- Subnet: `private-1a`
- Auto-assign public IP: **Disable**
- Security Group: `Private-SG`
- Key pair: **Same key pair as Bastion**

### Step 8: Test Connectivity

**Test 1: SSH into Bastion**
```bash
ssh -i "your-key.pem" ec2-user@<BASTION-PUBLIC-IP>
