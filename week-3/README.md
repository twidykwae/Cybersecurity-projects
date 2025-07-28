# Network Security & Intrusion Detection Systems

An exploration of network intrusion detection and directory traversal attack analysis using industry-standard tools

## Project Overview

This repository demonstrates practical cybersecurity skills through hands-on network security analysis, focusing on Snort intrusion detection system (IDS) configuration, custom rule development, and forensic analysis of directory traversal attacks. The projects simulate real-world scenarios where security professionals monitor network traffic and investigate security breaches.

## Key Learning Outcomes

- **Intrusion Detection Systems**: Configuration and deployment of Snort NIDS
- **Custom Rule Development**: Writing Snort rules for specific threat detection
- **Network Traffic Analysis**: Real-time monitoring and packet analysis
- **Directory Traversal Attacks**: Understanding and executing file system vulnerabilities
- **Forensic Investigation**: Analyzing network traffic to identify unauthorized access

## Technologies & Tools Used

- **Snort**: Network Intrusion Detection System (NIDS)
- **Docker**: Containerized testing environment with pytbull-ng
- **pytbull-ng**: Network security testing framework for attack simulation
- **Node.js**: FTP server implementation for vulnerability testing
- **Wireshark**: Network protocol analyzer for .pcap file analysis
- **Linux/Ubuntu**: Primary operating environment
- **Bash Scripting**: Automation and attack simulation
- **Vim**: Text editor for configuration and rule files

### Project: Directory Traversal Attack Investigation

**Scenario**: Forensic investigation of Fairly Oddparents Corp. suspected of financial fraud

**Objective**: Execute directory traversal attacks on FTP server and analyze network traffic to identify unauthorized file access

#### Technical Implementation:

**Phase 1: FTP Server Deployment**
- Started FTP server using provided Node.js script
- Prepared attack automation script

**Phase 2: Directory Traversal Attack Execution**
- Modified `attack.sh` bash script to automate directory traversal
- Implemented attack.js to navigate restricted file systems
- Targeted hidden financial reports in personal directories

**Phase 3: Network Traffic Analysis**
- Analyzed `server.pcapng` file containing network traffic
- Identified unauthorized file access patterns
- Documented compromised files and data exfiltration

#### Key Findings:
- **Unauthorized Access**: Successfully accessed restricted company directories
- **Data Discovery**: Located hidden financial reports outside public folders
- **Security Breach Documentation**: Identified specific files accessed without permission
- **Evidence Collection**: Three distinct files compromised through directory traversal

#### Files Compromised:
1. Personal directory financial reports
2. Alternative versions of general/reports.txt
3. Original earnings data contradicting public statements

## Real-World Applications

This project demonstrates skills directly applicable to:

- **SOC Analyst Roles**: Real-time network monitoring and intrusion detection
- **Digital Forensics**: Network traffic analysis and incident investigation
- **Penetration Testing**: Directory traversal vulnerability assessment
- **Incident Response**: Attack pattern identification and evidence collection
- **Compliance Monitoring**: Security rule implementation and threat detection

## Security Concepts Demonstrated

### Intrusion Detection:
- Signature-based detection using custom Snort rules
- Real-time network traffic monitoring
- Attack pattern recognition and alerting
- Rule validation and testing procedures

### Vulnerability Assessment:
- Directory traversal attack execution
- FTP server security weaknesses
- File system access control bypass
- Network forensics and evidence gathering

### Network Security:
- Packet analysis and traffic inspection
- Protocol-specific rule development
- Live attack simulation and detection
- Security breach investigation

## Technical Skills Demonstrated

- **Network Security Analysis**: Deep understanding of network protocols and attack vectors
- **Intrusion Detection Systems**: Snort configuration, rule development, and deployment
- **Bash Scripting**: Automation of security testing and attack simulation
- **Network Forensics**: Packet capture analysis and incident investigation
- **Linux System Administration**: Command-line proficiency and system configuration
- **Vulnerability Assessment**: Directory traversal attack execution and analysis

## Professional Development Alignment

This project aligns with industry certifications and roles:
- **CompTIA Security+**: Network security monitoring and incident response
- **GCIH (GIAC Certified Incident Handler)**: Forensic investigation procedures
- **CEH (Certified Ethical Hacker)**: Penetration testing and vulnerability assessment
- **SOC Analyst**: Real-time threat detection and network monitoring

## Key Deliverables

### Lab 3 Deliverables:
- Functional Snort IDS configuration
- Custom detection rules for ICMP and HTTPS traffic
- Real-time attack detection capabilities
- Rule validation and testing documentation

### Project 3 Deliverables:
- Completed attack.sh script for automated directory traversal
- Network traffic analysis of server.pcapng file
- Documentation of three compromised files
- Evidence of unauthorized access to restricted directories

## Conclusion

This comprehensive cybersecurity project demonstrates practical skills in network intrusion detection, attack simulation, and forensic investigation. The hands-on experience with industry-standard tools like Snort IDS and network analysis techniques provides essential foundation for cybersecurity professionals. The combination of defensive monitoring through intrusion detection and offensive security testing through directory traversal attacks showcases a well-rounded understanding of network security principles and practices.