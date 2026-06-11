# 🛡️ Cybersecurity Portfolio — Shakhawat Hossain Refat

A collection of hands-on cybersecurity labs, incident response exercises, and coursework.

---

## 📁 Labs & Projects

### Week 10 — Containment, Eradication & Recovery
**Tool:** Splunk (BOTSv1 dataset)  
**Scenario:** Investigated a real-world attack on `imreallynotbatman.com` (Wayne Enterprises)

**Outcome:**
https://youtu.be/A2qVXn7mj8o

**What I did:**
- Identified victim server `192.168.250.70` and two attacker IPs
- Traced the full kill chain: reconnaissance → SQL injection → brute-force → Joomla defacement
- Wrote a containment decision memo to the CISO recommending isolation strategy
- Completed a chain of custody form for forensic memory evidence
- Applied NIST SP 800-88 to five sanitization scenarios (Clear / Purge / Destroy)
- Built a recovery validation checklist covering accounts, logging, config, and vulnerability state

## 🖥️ Splunk Commands Used

### 🔍 Finding the Victim Server
```spl
index=botsv1 sourcetype=stream:http
| stats count by dest_ip
| sort -count
```

### 👾 Identifying Attacker IPs
```spl
index=botsv1 sourcetype=stream:http
| stats count by src_ip
| sort -count
```

### 🔎 Investigating SQL Injection
```spl
index=botsv1 sourcetype=stream:http dest_ip=192.168.250.70
| search uri_query=*select* OR uri_query=*union* OR uri_query=*drop*
```

### 🔑 Brute Force Authentication Analysis
```spl
index=botsv1 sourcetype=stream:http dest_ip=192.168.250.70
| stats count by src_ip, uri_path
| where count > 10
```

### 📁 Finding the Defacement File
```spl
index=botsv1 sourcetype=stream:http dest_ip=192.168.250.70
| search uri_path=*.jpeg OR uri_path=*.php
```

### 🚨 Checking Attacker IPs in Firewall Logs
```spl
index=botsv1 sourcetype=suricata
| stats count by src_ip, dest_ip, alert.signature
| sort -count
```

### 📊 Full Kill Chain Timeline
```spl
index=botsv1 (src_ip=40.80.148.42 OR src_ip=23.22.63.114)
| table _time, src_ip, dest_ip, uri_path, status
| sort _time
```

**Skills demonstrated:**
`Splunk` `NIST SP 800-61` `NIST SP 800-88` `Digital Forensics` `Incident Response` `Chain of Custody` `Log Analysis`

---

## 🧰 Tools & Frameworks
- Splunk SIEM
- NIST SP 800-61 Rev. 2 (Incident Handling)
- NIST SP 800-88 Rev. 1 (Media Sanitization)
- RFC 3227 (Evidence Collection)
- FTK Imager

