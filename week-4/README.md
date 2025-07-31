# DoS Attack Mitigation with NGINX

## Project Overview

This project lab focused on understanding and mitigating **Denial of Service (DoS) attacks** using the Slowloris attack tool against a local NGINX server. The project involved implementing DoS mitigation rules in NGINX configuration and analyzing network traffic to distinguish between vulnerable and protected servers.

**Tools Used**: NGINX, Slowloris, NGINX Amplify, Wireshark

---

## Learning Objectives

- Understand how Slowloris DoS attacks work
- Configure NGINX DoS mitigation rules  
- Monitor server performance using NGINX Amplify dashboard
- Analyze network traffic patterns in Wireshark to identify attack signatures

---

## Lab Environment Setup

### Pre-installed Tools Verification
- **NGINX web server**: Verified with `nginx -v`
- **Slowloris attack tool**: Verified with `slowloris -v`

### Initial Setup Steps
```bash
# Stop Apache2 if running (conflicts with NGINX)
sudo service apache2 stop

# Start NGINX service
sudo systemctl start nginx
```

---

## NGINX Amplify Monitoring Setup

### Dashboard Configuration
1. **Created free NGINX Amplify account** for real-time server monitoring
2. **Installed Amplify agent** on the VM using provided commands
3. **Configured metrics collection** by creating `/etc/nginx/conf.d/stub_status.conf`

```nginx
# Added to stub_status.conf for monitoring
server {
    listen 127.0.0.1:80;
    server_name 127.0.0.1;
    location /nginx_status {
        stub_status on;
        access_log off;
        allow 127.0.0.1;
        deny all;
    }
}
```

4. **Reloaded NGINX configuration**:
```bash
sudo kill -HUP `cat /var/run/nginx.pid`
```

---

## Initial Attack Analysis

### Slowloris Attack Execution - Pre-Mitigation
```bash
# Launch Slowloris attack against local server
slowloris 127.0.0.1
```

**Attack Results (10-minute duration):**
- NGINX Amplify dashboard showed uncontrolled connection growth
- Server became unresponsive to legitimate traffic
- Connections remained open indefinitely, exhausting server resources

---

## DoS Mitigation Implementation

### NGINX Configuration Changes

I modified `/etc/nginx/conf.d/default.conf` with DoS mitigation rules (shown in screenshot)


### Configuration Applied
```bash
sudo systemctl restart nginx
```

---

## Post-Mitigation Attack Testing

### Second Attack Execution
```bash
# Re-run Slowloris attack with mitigation rules active
slowloris 127.0.0.1
```

**Attack Results with Mitigation (10-minute duration):**

The NGINX Amplify dashboard clearly demonstrates the effectiveness of our DoS mitigation rules:

**Connection Management Analysis:**
- The "NGINX Current Connections" graph shows controlled connection spikes that quickly drop back to zero
- Peak connections reached approximately 150-160 concurrent connections before being terminated
- Connection patterns show regular "sawtooth" behavior. Connections spike up then immediately drop, indicating timeout rules are working
- No sustained connection buildup, preventing resource exhaustion

**Key Evidence of Successful Mitigation:**
- Connection graphs show controlled spikes rather than exponential growth

The mitigation rules successfully limited concurrent connections per IP address and implemented timeout values that prevented Slowloris from maintaining persistent connections, as evidenced by the regular connection termination patterns in the dashboard.

---

## Network Traffic Analysis with Wireshark

To further validate the effectiveness of our DoS mitigation, we analyzed network packet captures from both vulnerable and protected servers.

### Packet Capture Analysis Method

**Objective**: Compare traffic patterns between vulnerable and protected server configurations

**Analysis Approach**: Used Wireshark filters to examine TCP connection behavior patterns in pcap files

```
# Filter for connection reset packets
tcp.flags.reset == 1

# Filter for connection termination packets  
tcp.flags.fin == 1
```

### Traffic Pattern Comparison

#### File A Analysis (Protected Server Traffic)
- **High number of RST (reset) packets** - indicating the server actively terminated malicious connections
- **Short connection durations** - evidence that timeout configurations were working effectively
- **Active connection management** - server forcefully closed slow connections before resource exhaustion

#### File B Analysis (Vulnerable Server Traffic)  
- **Long-lasting connections** without proper termination
- **Absence of RST packets** - server failed to close malicious connections
- **Attack success pattern** - connections remained open indefinitely, consuming server resources

### Network Analysis Conclusion
- **File A represents the protected server** with active connection management and mitigation rules
- **File B represents the vulnerable server** without protection mechanisms

The packet analysis confirmed that our NGINX mitigation rules were effectively detecting and terminating malicious Slowloris connections, as evidenced by the increased presence of TCP reset packets in the protected server traffic.

---

## Lab Cleanup

### Environment Teardown
```bash
# Stop NGINX Amplify agent
sudo service amplify-agent stop

# Remove NGINX Amplify agent
sudo apt-get remove nginx-amplify-agent

# Delete resource from Amplify web dashboard
```

---

## Technical Learning Outcomes

### DoS Attack Types Studied
- **Slowloris**: Application-layer attack exploiting HTTP connections by sending partial requests
- **SYN floods**: Network-layer attack overwhelming TCP handshake process  
- **HTTP floods**: Volumetric attack using legitimate HTTP requests at high volume

### Key Security Concepts
- **Connection limiting** as an effective DoS mitigation strategy
- **Timeout configurations** for preventing resource exhaustion
- **Traffic pattern analysis** for identifying malicious activity
- **Real-time monitoring** for attack detection and validation

This lab demonstrated the practical implementation of server hardening techniques and the importance of combining configuration-based defenses with network traffic analysis for comprehensive DoS protection.