
#  **Phase 3 — Part 1: EC2 + EBS Storage Architecture**

##  Project Overview  
This project demonstrates how to build and manage EC2 compute resources, attach and configure EBS storage, create AMIs, use IAM roles, and automate EC2 using User Data.  
I performed hands‑on tasks including disk formatting, mounting, snapshot creation, IAM role usage, and troubleshooting.  
This represents real cloud engineering work done inside AWS.

---

##  What I Built  
- Launched an EC2 instance (Amazon Linux 2023)  
- Created a gp3 EBS volume  
- Attached the volume to EC2  
- Identified NVMe device mapping  
- Formatted the disk using XFS  
- Mounted the disk at `/data`  
- Made the mount persistent using `/etc/fstab`  
- Created snapshots for backup  
- Restored volumes from snapshots  
- Created custom AMIs  
- Attached IAM role to EC2  
- Accessed S3 using the IAM role  



##  Architecture Diagram  

+--------------------------------------------------+
|                    EC2 Instance                  |
|              Amazon Linux 2023 (t2.micro)        |
|                                                  |
|  - IAM Role Attached (EC2-S3-Access)             |
|  - User Data (optional automation)               |
+---------------------------+----------------------+
                            |
                            v
+--------------------------------------------------+
|                    EBS Volume                    |
|                gp3 - 4 GiB - /dev/nvme1n1        |
|                                                  |
|  - Formatted with XFS                            |
|  - Mounted at /data                              |
|  - Persistent mount via /etc/fstab               |
+--------------------------------------------------+




##  Commands I Used (Proof of Hands‑On Work)

```bash
ssh -i phase3-key.pem ec2-user@<public-ip>
lsblk
sudo mkfs.xfs /dev/nvme1n1
sudo mkdir /data
sudo mount /dev/nvme1n1 /data
df -h




## ⭐ Expected Output (Screenshot Replacement)

### `lsblk`

nvme0n1     259:0    0   10G  0 disk
└─nvme0n1p1 259:1    0   10G  0 part  /
nvme1n1     259:2    0    4G  0 disk
```

### `df -h`

Filesystem      Size  Used Avail Use% Mounted on
/dev/nvme1n1    4.0G   33M  3.9G   1% /data
```

### IAM Role Verification

{
  "UserId": "AROA123456789:ec2-instance",
  "Account": "123456789012",
  "Arn": "arn:aws:sts::123456789012:assumed-role/EC2-S3-Access/i-0abc123def456"
}
```

### S3 Access

2024-05-01  bucket-name
2024-05-01  another-bucket




## ⭐ Troubleshooting  
- **EBS not mounting** → fixed `/etc/fstab` entry  
- **Wrong device name** → learned Nitro → NVMe mapping  
- **AccessDenied from S3** → fixed IAM policy  
- **Mount not persistent** → corrected XFS mount options  


## ⭐ What I Learned  
- How EC2 uses EBS as persistent block storage  
- How Nitro instances map EBS volumes to NVMe devices  
- How to format and mount Linux filesystems  
- How `/etc/fstab` controls persistent mounts  
- How snapshots provide backup and recovery  
- How IAM roles give EC2 secure access to S3  
- How AMIs allow custom server images  

---

## ⭐ Skills Gained  
- EC2  
- EBS  
- IAM Roles  
- S3 Access  
- Linux Filesystems  
- Disk Mounting  
- Snapshots  
- AMIs  
- Troubleshooting  
- Cloud Architecture Documentation  



