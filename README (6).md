# System Health Monitoring Script (Python)

This project provides a Python script to monitor the health of a Linux system.  
It checks **CPU usage, memory usage, disk space, and running processes**. If any of these metrics exceed predefined thresholds, the script sends an alert to the console.

---

## ✅ Features
- Monitors **CPU usage**, **memory usage**, and **disk usage**.  
- Verifies if a critical process (default: `sshd`) is running.  
- Prints **alerts** if thresholds are exceeded or processes are missing.  
- Easy to extend for logging to a file or sending alerts via email/Slack.  

---

## 🛠️ Prerequisites
- Python 3.x installed.  
- Install the `psutil` library:
```bash
pip3 install psutil
```

---

## 📦 Installation
1. Clone or copy the script to your Linux system:
```bash
nano system_health_monitor.py   # paste the script
```

2. Make it executable:
```bash
chmod +x system_health_monitor.py
```

---

## ▶️ Usage
Run the script manually:
```bash
./system_health_monitor.py
```
or
```bash
python3 system_health_monitor.py
```

---

## ⚙️ Configuration
Thresholds and process name can be updated inside the script:

```python
CPU_THRESHOLD = 80
MEMORY_THRESHOLD = 80
DISK_THRESHOLD = 80
PROCESS_NAME = "sshd"   # change this to nginx, mysql, etc.
```

---

## 📊 Example Output
Normal case:
```
--- System Health Check: 2025-09-18 20:15:10 ---
CPU Usage: 12.0%
Memory Usage: 65.4%
Disk Usage: 72.1%
Process 'sshd': Running
Check complete.
```

Alerts:
```
--- System Health Check: 2025-09-18 20:20:33 ---
CPU Usage: 91.2%
[ALERT] High CPU usage detected: 91.2%
Memory Usage: 84.5%
[ALERT] High Memory usage detected: 84.5%
Disk Usage: 81.3%
[ALERT] Low Disk Space detected: 81.3% used
Process 'sshd': Not Running
[ALERT] Process 'sshd' not running!
Check complete.
```

---

## 🚀 Bonus Ideas
- Schedule periodic runs with **cron jobs**:
```bash
*/5 * * * * /usr/bin/python3 /home/ubuntu/system_health_monitor.py >> /var/log/system_health.log 2>&1
```
- Redirect alerts to a log file.  
- Extend the script to send **email, SMS, or Slack alerts**.  
