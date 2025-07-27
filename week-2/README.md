# CodePath CYB102 – Week 2: Endpoint Monitoring

A cybersecurity lab demonstrating Host-based Intrusion Detection Systems (HIDS) implementation using Linux's `auditd` for endpoint monitoring 

## Topics Covered
- Host Event Logs & System Monitoring
- Host Vulnerability Scanning Techniques
- Host Intrusion Prevention/Detection Systems
---

## Lab: 

###  Objective
Configure `auditd` to monitor file modifications and demonstrate incident investigation capabilities using audit log analysis.

### Implementation Steps

1. **File Setup & Initialization**
   ```
   # Create target file with initial content
   echo "Initial test data" > /home/codepath/unit2_lab.txt
   vim /home/codepath/unit2_lab.txt
   ```

2. **Audit Rule Configuration**
   ```
   # Configure monitoring rule for write operations
   sudo auditctl -w /home/codepath/unit2_lab.txt -p w -k unit2_lab_changes
   ```

3. **Service Management**
   ```
   # Apply configuration changes
   sudo systemctl restart auditd
   ```

4. **Event Generation**
   ```
   # Trigger monitored activity
   echo "Modified content" >> /home/codepath/unit2_lab.txt
   ```

5. **Forensic Analysis**
   ```
   # Investigate modifications using audit logs
   sudo ausearch -ts today -k unit2_lab_changes
   ```

### 📊 Expected Output
- Detailed modification timestamps
- User attribution and process identification
- File access patterns and permission changes
- Complete audit trail for forensic investigation

---

##  Main Project

### Scenario Overview
This exercise simulated an attack against a protected file system. The challenge involved detecting and unauthorized modifications over data files using monitoring techniques.

### Technical Architecture

**Challenge**: Implement comprehensive monitoring for 10+ files and correlate attacks through log analysis

**Solution Components**:
- **Audit Rules**: Individual monitoring configurations per target file
- **Filter Keys**: Distinct audit keys enabling precise log correlation
- **Attack Attribution Engine**: Custom `ausearch` queries for forensic investigation

---


### 🗂 Monitored Files

The following files in the `protected_files` directory were monitored for write activity using audit rules:

- car_sales.csv  
- cloudia.txt  
- dolly.txt  
- earthquakes.csv  
- loggy.txt  
- oakley.txt  
- precipitation.csv  
- squeaky.txt  
- tosty.txt  

---

### ⚙️ Audit Rule Implementation

```bash
sudo auditctl -w /home/codepath/project2-main/protected_files/car_sales.csv -p wa -k car_sales_monitor
sudo auditctl -w /home/codepath/project2-main/protected_files/earthquakes.csv -p wa -k earthquakes_monitor
sudo auditctl -w /home/codepath/project2-main/protected_files/precipitation.csv -p wa -k precipitation_monitor
sudo auditctl -w /home/codepath/project2-main/protected_files/cloudia.txt -p wa -k cloudia_monitor
sudo auditctl -w /home/codepath/project2-main/protected_files/loggy.txt -p wa -k loggy_monitor
sudo auditctl -w /home/codepath/project2-main/protected_files/oakley.txt -p wa -k oakley_monitor
sudo auditctl -w /home/codepath/project2-main/protected_files/dolly.txt -p wa -k dolly_monitor
sudo auditctl -w /home/codepath/project2-main/protected_files/squeaky.txt -p wa -k squeaky_monitor
sudo auditctl -w /home/codepath/project2-main/protected_files/tosty.txt -p wa -k tosty_monitor
sudo auditctl -w /home/codepath/project2-main/protected_files/website.js -p wa -k website_monitor
```

---

## 🧠 Key Learning Outcomes

### Technical Skills Developed
- **Linux System Administration**: Advanced `auditd` configuration and management
- **Security Rule Engineering**: Custom audit policy development and deployment
- **Incident Response**: Real-time threat detection and forensic investigation
- **Log Analysis**: Advanced filtering and correlation techniques using `ausearch`
- **Attack Attribution**: Correlating malicious activities to specific threat vectors

### Cybersecurity Principles Applied
- **Defense in Depth**: Multi-layered monitoring approach
- **Continuous Monitoring**: Real-time security event detection
- **Forensic Readiness**: Comprehensive audit trail maintenance
- **Threat Intelligesnce**: Attack pattern recognition and attribution

---

### Command Reference
```bash
# System monitoring
sudo auditctl -l                    # List active rules
sudo systemctl status auditd        # Service health check
sudo ausearch -x attack-a           # Search by executable name
sudo ausearch -k precipitation_monitor | grep "exe=" 
tail -f /var/log/audit/audit.log    # Real-time monitoring
```

---


