# codepath-cyb-102
# Week 1: Blue Team Defense Concepts

---

## 🧠 Topics Covered:
- Defensive cybersecurity
- Red Team vs. Blue Team roles
- NIST cybersecurity framework and controls
- Common blue team tools: SIEM, IDS, antivirus, packet sniffers
- Security Operations Center (SOC) structure and purpose
- Cyber Fusion Centers
- Key defensive skills: risk assessment, monitoring, hardening, threat intelligence

---


## 🧰 Tools Used:
- Wireshark (network packet analyzer)

---

## 💡 Key Takeaways:
- Blue Teams focus on protecting systems from attackers by monitoring, analyzing, and responding to threats.
- SOCs and Cyber Fusion Centers help companies defend against modern threats in real time.
- Tools like Wireshark help analyze traffic and investigate incidents.
- Risk management and threat intelligence are critical skills for defenders.

---

### 🎯 Project 1
- **Goal:** Identify phishing emails in `.pcap` files and find the malicious actor.
- **Tools Used:** Wireshark, SMTP filters, TCP Stream Analysis
- **How I Did It:**  
  Used Wireshark filters like `smtp contains "FROM"` across all pcap files. Found high SMTP traffic in `C.pcap`, followed TCP streams, and identified malicious content in the emails.

---
