# Project 6: Flask App with AWS RDS

## Objective
Create an Amazon RDS database and connect a Flask application to it.

## AWS Services Used
- RDS (Relational Database Service)
- EC2 (for hosting Flask app)
- VPC / Security Groups

## Steps

### 1. Create RDS Instance
- Go to RDS Console → Create database
- Engine: MySQL
- Template: Free tier
- DB instance identifier: `my-flask-db`
- Master username: `admin`
- Master password: (set strong password)
- Instance class: db.t3.micro
- Storage: 20 GB

### 2. Configure Security Group
- Inbound rules:
  - Type: MySQL/Aurora
  - Port: 3306
  - Source: My EC2 Security Group (or My IP)

### 3. Launch EC2 for Flask
- Amazon Linux 2
- Install Python & Flask:
```bash
sudo yum update -y
sudo yum install python3 python3-pip -y
pip3 install flask pymysql
