# Automated Backup Solution:

This project contains a Python script that automatically backs up files from an EC2 instance to an Amazon S3 bucket. Each backup is stored in a **timestamped folder** inside the bucket for versioning.

---

## 🚀 Features
- Uploads all files from a local directory to an S3 bucket.  
- Organizes backups into timestamped folders (`backups/YYYY-MM-DD_HH-MM-SS`).  
- Simple and lightweight – uses `boto3` (AWS SDK for Python).  
- Error handling for missing directories and failed uploads.  

---

## 📋 Requirements
- Python 3.x installed  
- `boto3` library  
- AWS CLI installed and configured **OR** an EC2 IAM Role with S3 permissions  

Install dependencies:
```bash
sudo apt update -y
sudo apt install python3-pip -y
pip3 install boto3
```

---

## ⚙️ Configuration
1. **Set your source directory** (files to back up):
   ```python
   SOURCE_DIR = "/home/ubuntu/data"
   ```

2. **Set your S3 bucket name**:
   ```python
   BUCKET_NAME = "my-ubuntu-backups-12345"
   ```

3. Ensure your EC2 instance has access to S3:
   - **Option 1 (Best Practice):** Attach an IAM Role with `AmazonS3FullAccess` or custom S3 policy.  
   - **Option 2:** Configure AWS CLI with your credentials:
     ```bash
     aws configure
     ```

---

## ▶️ Usage
Run the script manually:
```bash
python3 backup_to_s3.py
```

You’ll see logs for each uploaded file:
```
--- Backup Operation: 2025-09-19_18-30-12 ---
Uploaded: backups/2025-09-19_18-30-12/file1.txt
Uploaded: backups/2025-09-19_18-30-12/file2.txt
[SUCCESS] Backup to S3 bucket 'my-ubuntu-backups-12345' completed.
```

---

  
