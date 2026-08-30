# Project 4: Mounting an EBS Volume

## Objective
Attach and mount an EBS volume to an EC2 instance for persistent storage.

## AWS Services Used
- EC2 (Elastic Compute Cloud)
- EBS (Elastic Block Store)

## Steps
1. Create EC2 Instance (if not exists)
2. Create EBS Volume (same Availability Zone!)
3. Attach Volume to EC2 Instance
4. SSH into the Instance
5. Format the Volume (`sudo mkfs -t ext4 /dev/xvdf`)
6. Create Mount Point (`sudo mkdir /mnt/myvolume`)
7. Mount the Volume (`sudo mount /dev/xvdf /mnt/myvolume`)
8. Verify (`df -h`)

## Commands Used
```bash
lsblk
sudo mkfs -t ext4 /dev/xvdf
sudo mkdir /mnt/myvolume
sudo mount /dev/xvdf /mnt/myvolume
df -h
