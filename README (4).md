# Automated Backup Solution

This project provides a simple automated backup solution using a python script. The script compresses a specified directory and uploads it to an AWS S3 bucket. After the backup, it generates a log file that reports the success or failure of the operation.

---

## Prerequisites

1. **AWS Account**  
   Make sure you have an AWS account with access to S3.

2. **AWS CLI Installed**  
   Install AWS CLI on your instance:
   ```bash
   sudo apt update && sudo apt install -y awscli
   ```

3. **Configure AWS CLI**  
   Run the following command and provide your AWS Access Key, Secret Key, and default region:
   ```bash
   aws configure
   ```

4. **S3 Bucket**  
   Create an S3 bucket where backups will be stored:
   ```bash
   aws s3 mb s3://your-backup-bucket-name
   ```

---

## Backup Script

Create a file called `backup.sh` and paste the following script:

```bash
#!/bin/bash

# Variables
SOURCE_DIR="/home/ubuntu/data"        # Directory to backup
BUCKET_NAME="your-backup-bucket-name" # Replace with your S3 bucket name
TIMESTAMP=$(date +%F-%H-%M-%S)
BACKUP_FILE="backup-$TIMESTAMP.tar.gz"
LOG_FILE="/home/ubuntu/backup.log"

# Create backup
tar -czf $BACKUP_FILE $SOURCE_DIR

# Upload to S3
aws s3 cp $BACKUP_FILE s3://$BUCKET_NAME/

# Check if upload was successful
if [ $? -eq 0 ]; then
    echo "$(date): Backup successful. File $BACKUP_FILE uploaded to S3." >> $LOG_FILE
    rm $BACKUP_FILE
else
    echo "$(date): Backup failed." >> $LOG_FILE
fi
```

Make the script executable:
```bash
chmod +x backup.sh
```

Run the script:
```bash
./backup.sh
```

---

## Automating Backups with Cron

To schedule daily backups at midnight, add a cron job:

```bash
crontab -e
```

Add the following line:
```bash
0 0 * * * /home/ubuntu/backup.sh
```

---

## Logs

Backup logs will be stored in `/home/ubuntu/backup.log`.

---

## Example Log

```
2025-09-18 00:00:00: Backup successful. File backup-2025-09-18-00-00-00.tar.gz uploaded to S3.
```

---

## Notes

- Replace `/home/ubuntu/data` with the directory you want to back up.
- Ensure your S3 bucket name is unique.
- Monitor your S3 storage usage to avoid unexpected costs.
