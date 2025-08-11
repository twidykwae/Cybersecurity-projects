# SIEM Security Analysis

## Executive Summary

Thisproject  demonstrates Security Information and Event Management (SIEM) analysis using Splunk Enterprise. For this project, I analyzed Netflix metadata and conducted a malware breach investigation, that shows real-world cybersecurity analyst capabilities including log correlation, threat hunting, and incident response.

## Project Overview

**Focus:** SIEM Operations and Threat Detection  
**Platform:** Splunk Enterprise  
**Investigation Types:** Data analytics and security incident response

### Key Competencies Demonstrated
- Advanced Splunk SPL (Search Processing Language) query construction
- Multi-source log correlation and threat attribution  
- IOC (Indicators of Compromise) based threat hunting
- Behavioral analysis and anomaly detection

---

## Investigation 1: Netflix Content Analytics

### Objective
Demonstrate structured data analysis capabilities using Splunk.

**Dataset:** `index=main host=Netflix`

### Completed Analysis

| Challenge | Finding | SPL Query |
|-----------|---------|-----------|
| **Turkish Content Inventory** | 210 titles | `index="main" host="Netflix" country="Turkey" \| stats count` |
| **2020 Movie Releases** | 1,034 movies | `index="main" host="Netflix" type="Movie" release_year="2020" \| stats count` |
| **Content Duration Analysis** | 9 seasons (TV-14, TV-PG, TV-MA) | `index="main" host="Netflix" type="TV Show" \| stats max(duration) as longest_duration by rating \| sort -longest_duration` |

### Technical Skills Applied
- **Data Aggregation:** Used `stats count` for inventory analysis
- **Filtering:** Applied multiple field conditions for precise results
- **Statistical Analysis:** Implemented `max()` function with grouping
- **Result Optimization:** Utilized `sort` command for meaningful data presentation

---

## Investigation 2: Malware Incident Response

### Incident Profile
**Threat Classification:** Advanced Persistent Threat (APT)  
**Primary IOC:** MD5 Hash `3AADBF7E527FC1A050E1C97FEA1CBA4D`  
**Attack Vector:** Credential compromise → Malicious file upload  
**Investigation Scope:** Multi-host log correlation across 4 data sources

### Data Sources Architecture
```
├── BlueCoatProxy01    → Web proxy traffic logs
├── failedlogins64     → Authentication failure tracking  
├── uploadedhashes     → File upload monitoring system
└── webserver02        → HTTP server access logs
```

### Investigation Timeline & Attribution

#### Phase 1: Initial Threat Detection
**Challenge:** What was the IP address that uploaded the malware?
```spl
host="BlueCoatProxy01" OR host="failedlogins64" OR host="uploadedhashes" OR host="webserver02" EvilScript.exe
```
**Critical Finding:** Source IP `192.168.1.10` identified as upload origin

#### Phase 2: Attack Pattern Analysis  
**Challenge:** What usernames did that IP address try to login as? Which one uploaded the file?
```spl
host="BlueCoatProxy01" OR host="failedlogins64" OR host="uploadedhashes" OR host="webserver02" 192.168.1.10
```
**Behavioral Pattern:** Systematic brute force targeting usernames:
- `Admin` (Administrative account targeting)
- `Pi` (Default system account exploitation)
- `ABurke` (Successful compromise vector - uploaded the file)

#### Phase 3: Technical Fingerprinting
**Challenge:** What was the User Agent String of the attacker?
```spl
host="BlueCoatProxy01" OR host="failedlogins64" OR host="uploadedhashes" OR host="webserver02" 192.168.1.10
```
*Note: Analyzed user_agent field from results*
**Technical Attribution:** `Opera/75.0.3969.218` browser fingerprint

---

## Advanced SIEM Techniques Demonstrated

### Log Correlation Methodology
- **Cross-Host Analysis:** Successfully correlated events across 4 distinct log sources
- **Temporal Correlation:** Linked authentication failures to successful file uploads
- **IOC Tracking:** Used hash-based indicators for precise threat identification

### Splunk Query Optimization
```spl
# Multi-host threat hunting approach
host="BlueCoatProxy01" OR host="failedlogins64" OR host="uploadedhashes" OR host="webserver02" EvilScript.exe

# IP-based behavioral analysis
host="BlueCoatProxy01" OR host="failedlogins64" OR host="uploadedhashes" OR host="webserver02" 192.168.1.10

# User agent extraction from results
# (Analyzed user_agent field manually from query results)
```

### Threat Hunting Capabilities
- **Proactive IOC Searching:** Identified compromise before impact assessment
- **Behavioral Anomaly Detection:** Recognized brute force patterns in authentication logs
- **Attribution Analysis:** Built comprehensive attacker profile through log correlation

---

## SIEM Concepts Applied

### Security Information Management (SIM)
- **Historical Analysis:** Leveraged retained log data for forensic investigation
- **Compliance Reporting:** Demonstrated audit trail reconstruction capabilities
- **Long-term Storage:** Accessed historical authentication and file transfer records

### Security Event Management (SEM)  
- **Real-time Detection:** Identified active threats through live log analysis
- **Alert Correlation:** Connected disparate security events into coherent incident narrative
- **Incident Response:** Provided actionable intelligence for containment strategies

### User and Entity Behavior Analytics (UEBA) Concepts
- **Baseline Deviation:** Identified abnormal authentication patterns
- **Risk Scoring:** Evaluated threat severity through multi-factor analysis
- **Behavioral Profiling:** Analyzed attacker techniques and operational patterns

---

## Professional Impact & Learning Outcomes

### Technical Proficiencies Gained
- **Splunk Enterprise:** Advanced SPL query construction and optimization
- **SIEM Operations:** End-to-end incident investigation workflow
- **Threat Intelligence:** IOC analysis and attribution methodologies
- **Digital Forensics:** Timeline reconstruction and evidence correlation

### Cybersecurity Analyst Skills
- **Threat Hunting:** Proactive search for compromise indicators
- **Incident Response:** Structured investigation and documentation
- **Risk Assessment:** Threat severity evaluation and impact analysis
- **Communication:** Technical findings presentation for stakeholder consumption

---

## Key SPL Commands Reference

```spl
# Content analysis and business intelligence
index="main" host="Netflix" country="Turkey" | stats count

# Statistical aggregation with sorting
index="main" host="Netflix" type="TV Show" 
| stats max(duration) as longest_duration by rating 
| sort -longest_duration

# Multi-host malware investigation
host="BlueCoatProxy01" OR host="failedlogins64" OR host="uploadedhashes" OR host="webserver02" EvilScript.exe

# IP-based threat correlation
host="BlueCoatProxy01" OR host="failedlogins64" OR host="uploadedhashes" OR host="webserver02" 192.168.1.10
```

---

## Conclusion

This project demonstrated core SIEM analyst competencies through application of Splunk Enterprise in both business analytics and security operations contexts. The investigation shows critical cybersecurity skills including threat detection, incident response, and forensic analysis while highlighting the strategic importance of centralized logging and correlation analysis in modern security operations.
