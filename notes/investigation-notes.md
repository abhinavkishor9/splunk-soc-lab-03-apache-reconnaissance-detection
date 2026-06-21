# Investigation Notes

## Overview

This document records observations and findings from the Apache Web Reconnaissance Detection investigation.

---

# Dataset Information

| Field | Value |
|---------|---------|
| Log Source | Apache HTTP Access Logs |
| SIEM | Splunk Enterprise |
| Index | main |

---

# Queries Executed

## Top Requesting IPs

```spl
index=main
| stats count by clientip
| sort -count
```

---

## High-Volume Clients

```spl
index=main
| stats count by clientip
| where count > 100
```

---

## 404 Error Analysis

```spl
index=main
status=404
| stats count by clientip
| sort -count
```

---

## Administrative Page Access

```spl
index=main
"/admin"
```

---

## Login Page Access

```spl
index=main
"/login"
```

---

## Backup File Access

```spl
index=main
("/backup" OR ".bak")
```

---

## Configuration File Access

```spl
index=main
("/config" OR ".conf")
```

---

## Traffic Timeline

```spl
index=main
| timechart count
```

---

# Findings

## Top Requesting IP

```
Document Results
```

---

## High-Volume Clients

```
Document Results
```

---

## 404 Errors

```
Document Results
```

---

## Sensitive URL Access

```
Document Results
```

---

## Traffic Spikes

```
Document Results
```

---

# Analyst Assessment

Document whether the activity appears to be:

- Normal Web Traffic
- Search Engine Crawling
- Vulnerability Scanning
- Potential Reconnaissance
- Requires Further Investigation

---

# Conclusion

Summarize the findings and determine whether evidence of reconnaissance activity exists within the dataset.
