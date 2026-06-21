# splunk-soc-lab-03-apache-reconnaissance-detection

## Overview

This lab demonstrates how to detect reconnaissance activity within Apache HTTP access logs using Splunk Search Processing Language (SPL).

Reconnaissance is often the first phase of an attack lifecycle. Attackers commonly scan web servers for hidden pages, administrative interfaces, backup files, and vulnerable applications before attempting exploitation.

The objective of this lab is to identify suspicious web activity and develop foundational threat hunting and detection engineering skills.

---

# Lab Environment

- Windows 10/11 Host
- Splunk Enterprise
- Search & Reporting App
- Apache Access Log Dataset

---

# Scenario

The SOC team has observed an increase in web server activity and suspects that an external actor may be performing reconnaissance against a public-facing web application.

As a SOC Analyst, your task is to analyze Apache access logs and determine whether evidence of scanning or enumeration activity exists.

---

# Objectives

- Detect web reconnaissance activity
- Identify repeated requests from the same IP
- Investigate excessive 404 errors
- Detect requests for sensitive resources
- Analyze traffic spikes
- Develop detection logic using SPL
- Build threat hunting skills

---

# MITRE ATT&CK Mapping

| Technique | Description |
|------------|------------|
| T1595 | Active Scanning |
| T1590 | Gather Victim Network Information |
| T1190 | Exploit Public-Facing Application |

---

# Severity

**Medium**

Reconnaissance activity frequently precedes exploitation attempts and should be investigated.

---

# Detection Logic

## Top Requesting IP Addresses

```spl
index=main
| stats count by clientip
| sort -count
```

---

## Excessive Requests from Same IP

```spl
index=main
| stats count by clientip
| where count > 100
```

---

## Multiple 404 Errors

```spl
index=main
status=404
| stats count by clientip
| sort -count
```

---

## Requests for Administrative Pages

```spl
index=main
"/admin"
```

---

## Requests for Login Pages

```spl
index=main
"/login"
```

---

## Requests for Backup Files

```spl
index=main
("/backup" OR ".bak")
```

---

## Requests for Configuration Files

```spl
index=main
("/config" OR ".conf")
```

---

## Traffic Timeline Analysis

```spl
index=main
| timechart count
```

---

# False Positives

- Search engine crawlers
- Internal vulnerability scanners
- Monitoring services
- Authorized penetration tests
- Internal administrators

---

# Recommended Containment

Investigate the source IP, validate request patterns, block confirmed malicious hosts, enable WAF protections, and review additional logs for related activity.

---

# Step 1: Count Total Events

```spl
index=main
| stats count
```

---

# Step 2: Identify Top Requesting IP Addresses

```spl
index=main
| stats count by clientip
| sort -count
```

---

# Step 3: Identify High-Volume Clients

```spl
index=main
| stats count by clientip
| where count > 100
```

---

# Step 4: Investigate 404 Errors

```spl
index=main
status=404
| stats count by clientip
| sort -count
```

---

# Step 5: Hunt for Administrative Page Access

```spl
index=main
"/admin"
```

---

# Step 6: Hunt for Login Page Access

```spl
index=main
"/login"
```

---

# Step 7: Hunt for Backup Files

```spl
index=main
("/backup" OR ".bak")
```

---

# Step 8: Hunt for Configuration Files

```spl
index=main
("/config" OR ".conf")
```

---

# Step 9: Analyze Traffic Trends

```spl
index=main
| timechart count
```

---

# Step 10: Correlate Findings

Review:

- Top requesting IPs
- High-volume clients
- 404 activity
- Sensitive URL access
- Traffic spikes
- Overall evidence of reconnaissance

---



---

# Skills Demonstrated

- Splunk SPL
- Threat Hunting
- Detection Engineering
- Web Log Analysis
- SIEM Investigation
- Security Monitoring
- Apache Log Analysis

---

# Lessons Learned

This lab improves understanding of:

- Web reconnaissance techniques
- Active scanning detection
- Threat hunting methodology
- Detection development
- SPL aggregation commands
- SOC investigation workflows
