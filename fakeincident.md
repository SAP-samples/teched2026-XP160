# 🛡️ NORDIC-CERT Advisory NCERT-2024-001

**Computer Emergency Response Team — Nordic Region**

---

> **⚠️ CRITICAL ALERT — ACTIVE CAMPAIGN**
>
> **Ransomware Group "NorthernStorm" Targeting Nordic Retail Sector**
>
> Advisory ID: `NCERT-2024-001` | Published: January 16, 2024 09:00 CET | Last Updated: January 16, 2024 14:30 CET

| Confirmed Victims | Campaign Duration | Threat Level | Target Sector |
|:-:|:-:|:-:|:-:|
| 3 | 48h | **HIGH** | Retail |

---

## Table of Contents

1. [Executive Summary](#1-executive-summary)
2. [Technical Analysis](#2-technical-analysis)
3. [Indicators of Compromise](#3-indicators-of-compromise-iocs)
4. [Recommendations & Mitigation](#4-recommendations--mitigation)

---

## 1. Executive Summary

NORDIC-CERT has identified an active ransomware campaign targeting retail and e-commerce organizations in the Nordic region. The threat actor, identified as **"NorthernStorm"**, has successfully compromised three organizations running SAP S/4HANA systems in the past 48 hours.

### Affected Organizations

---

**Monday, January 15, 2024 — 14:00 CET**

#### RetailHub A/S (Denmark)

| Field | Details |
|---|---|
| **Industry** | E-commerce / Electronics Retail |
| **Systems Affected** | SAP S/4HANA 2021, SAP Fiori, Gateway |
| **Impact** | Complete system encryption, 12-hour outage |
| **Ransom Demand** | 100,000 EUR (Bitcoin) |
| **Status** | Systems restored from backup (48-hour recovery) |

---

**Tuesday, January 16, 2024 — 06:00 CET**

#### ShopNordic AS (Norway)

| Field | Details |
|---|---|
| **Industry** | Fashion / Apparel Retail |
| **Systems Affected** | SAP S/4HANA 2022, SAP HANA DB, Backup Infrastructure |
| **Impact** | Production and backup systems encrypted |
| **Ransom Demand** | 150,000 EUR (Bitcoin) |
| **Data Exfiltration** | Confirmed — 87 GB customer and financial data |
| **Status** | Currently offline, negotiating recovery options |

---

**Tuesday, January 16, 2024 — 08:00 CET**

#### BuyItNow AB (Sweden)

| Field | Details |
|---|---|
| **Industry** | Multi-Category E-commerce |
| **Systems Affected** | SAP S/4HANA 2020, SAP Gateway, Fiori Launchpad |
| **Impact** | Partial encryption (40% of database tables) |
| **Ransom Demand** | 200,000 EUR (Bitcoin) |
| **Data Exfiltration** | Suspected — under investigation |
| **Status** | Emergency incident response in progress |

---

> **⚠️ Active Campaign Warning:** Based on the geographic and temporal pattern, NORDIC-CERT assesses with HIGH CONFIDENCE that additional attacks are imminent. Organizations in Finland, Iceland, and remaining Scandinavian countries are at elevated risk.

---

## 2. Technical Analysis

### Attack Vector & Initial Access

#### Primary Entry Point

| Field | Details |
|---|---|
| **Vulnerability** | CVE-2024-0847 (SAP Gateway Remote Code Execution) |
| **CVSS Score** | **9.8 (Critical)** |
| **Affected Versions** | SAP Gateway 7.5, 7.53, 7.54 (unpatched) |
| **Patch Available** | Yes — SAP Security Note 3411067 (Dec 2023) |

#### Secondary Access Method

In addition to the SAP Gateway vulnerability, the threat actor utilized stolen VPN credentials obtained through previous phishing campaigns. Analysis of artifacts suggests credentials were harvested 2–3 weeks prior to the attacks.

```
VPN Username Format: firstname.lastname@company.com
Authentication:      RADIUS (no MFA detected on victim networks)
VPN Solution:        FortiClient, Cisco AnyConnect
Access Hours:        22:00–05:00 CET (outside business hours)
```

### Attack Timeline & TTPs

#### Phase 1: Initial Access — Day 0 (Hour 0–2)

- **T1190:** Exploit Public-Facing Application (SAP Gateway)
- **T1078:** Valid Accounts (Stolen VPN credentials)
- Establishment of reverse shell connection
- Deployment of persistence mechanism (SAP RFC backdoor)

#### Phase 2: Reconnaissance — Day 0–1 (Hour 2–24)

- **T1087:** Account Discovery (SU01 enumeration)
- **T1083:** File and Directory Discovery
- **T1046:** Network Service Scanning
- Mapping of SAP landscape (systems, databases, backup infrastructure)
- Identification of high-value data tables

#### Phase 3: Privilege Escalation — Day 1–2 (Hour 24–48)

- **T1078.003:** Creation of SAP administrative accounts
- Username patterns: `SAP_SUPPORT_TEMP`, `BASIS_ADMIN_02`
- Assignment of SAP_ALL profile
- Reactivation of dormant privileged accounts

#### Phase 4: Lateral Movement — Day 2–3 (Hour 48–72)

- **T1021.004:** Remote Services (SAP RFC)
- Movement from application layer to database layer
- Access to SAP HANA database servers
- Compromise of backup systems (NetBackup, Veeam)

#### Phase 5: Data Exfiltration — Day 3–4 (Hour 72–96)

- **T1567.002:** Exfiltration to Cloud Storage
- Destinations: mega.nz, anonfiles.com
- Data volume: 45–87 GB per victim
- Exfiltration timing: 23:00–04:00 CET (off-hours)
- Tables targeted: `KNA1`, `LFA1`, `BSEG`, `USR02`

#### Phase 6: Encryption — Day 4–5 (Hour 96–120)

- **T1486:** Data Encrypted for Impact
- Ransomware variant: Custom (likely LockBit 3.0 derivative)
- File extension: `.locked` or `.nstorm`
- Encryption speed: ~500 GB/hour
- Ransom note: `RESTORE_YOUR_FILES.txt`

> **🔍 Analyst Insight:** The 4–5 day dwell time between initial access and encryption deployment is consistent with professional ransomware operators conducting thorough reconnaissance. This patience increases impact by ensuring backup systems are compromised before encryption begins.

---

## 3. Indicators of Compromise (IoCs)

> **Note:** Organizations should search logs and systems for the following indicators. Presence of ANY indicator warrants immediate investigation.

### Network Indicators

| Type | Indicator | Description | First Seen |
|---|---|---|---|
| IP Address | `185.220.101.47` | Command & Control server (Romania) | 2024-01-10 |
| IP Address | `45.142.214.89` | Data exfiltration destination (Netherlands) | 2024-01-12 |
| IP Address | `23.95.67.134` | Secondary C2 server (United States) | 2024-01-14 |
| Domain | `sap-update-service[.]com` | Phishing domain (credential harvesting) | 2024-01-05 |
| Domain | `northdata-backup[.]net` | Data staging/exfiltration | 2024-01-11 |
| URL | `hxxps://mega[.]nz/folder/Xy7R2JbK` | Exfiltrated data storage | 2024-01-13 |

### SAP-Specific Indicators

| Type | Indicator | Description | Detection Method |
|---|---|---|---|
| Username | `SAP_SUPPORT_TEMP` | Malicious admin account | Transaction: SU01 |
| Username | `BASIS_ADMIN_02` | Unauthorized privileged account | Transaction: SU01 |
| Username | `EMERGENCY_ACCESS` | Backdoor account with SAP_ALL | Transaction: SU01 |
| RFC Connection | `Z_REMOTE_CONN_01` | Malicious RFC destination | Transaction: SM59 |
| File Path | `/usr/sap/trans/tmp/.system32` | Hidden malware staging directory | OS-level file system scan |
| Process | `sapstartsrv_backup.exe` | Renamed malicious executable | Process monitoring (ps, tasklist) |

### File Hashes (Malware Samples)

| Algorithm | Hash | Description |
|---|---|---|
| SHA256 | `a7f8e4c9b2d1f6e3a5c8b9d2e4f7a1c3b5d8e2f4a6c9b1d3e5f8a2c4b6d9e1f3` | Ransomware payload (nstorm_encryptor.exe) |
| SHA256 | `b3e7f2a8c5d9e1f4a6c8b2d5e7f9a1c4b6d8e3f5a7c9b1d4e6f8a3c5b7d9e2f4` | Data exfiltration tool (nordex.dll) |
| MD5 | `e4f6a8c2b5d7e9f1a3c5b7d9e2f4a6c8` | PowerShell credential stealer |

### YARA Rules

```yara
rule NorthernStorm_Ransomware {
    meta:
        description = "Detects NorthernStorm ransomware variant"
        author = "NORDIC-CERT"
        date = "2024-01-16"
        hash = "a7f8e4c9b2d1f6e3a5c8b9d2e4f7a1c3b5d8e2f4a6c9b1d3e5f8a2c4b6d9e1f3"

    strings:
        $s1 = "RESTORE_YOUR_FILES.txt" ascii wide
        $s2 = "NorthernStorm" ascii wide
        $s3 = ".locked" ascii wide
        $s4 = "Your files have been encrypted" ascii wide
        $hex1 = { 4D 5A 90 00 03 00 00 00 04 00 00 00 FF FF }
        $hex2 = { 89 E5 83 EC 40 48 89 4D F0 }

    condition:
        uint16(0) == 0x5A4D and
        filesize < 5MB and
        3 of ($s*) and 1 of ($hex*)
}

rule NorthernStorm_SAP_Backdoor {
    meta:
        description = "Detects SAP RFC backdoor used by NorthernStorm"
        author = "NORDIC-CERT"
        date = "2024-01-16"

    strings:
        $sap1 = "SAP_SUPPORT_TEMP" ascii wide
        $sap2 = "Z_REMOTE_CONN" ascii wide
        $sap3 = "BASIS_ADMIN" ascii wide
        $func1 = "RFC_SYSTEM_INFO" ascii
        $func2 = "SXPG_COMMAND_EXECUTE" ascii

    condition:
        2 of ($sap*) and 1 of ($func*)
}
```

---

## 4. Recommendations & Mitigation

### 🚨 Immediate Actions (Next 24 Hours)

**1. Apply SAP Security Patch**

Install SAP Security Note 3411067 to remediate CVE-2024-0847 on ALL SAP Gateway instances. Verify patch level using transaction SYSTEM → Status.

```
SPAM/SAINT → Load Support Packages → SAPKB75054
```

**2. Audit SAP Administrative Accounts**

Review all accounts with SAP_ALL or SAP_NEW profiles using SU01. Disable any unrecognized accounts immediately.

```
SE16 → USR02 → Filter: PROFN = 'SAP_ALL'
```

**3. Review RFC Connections**

Check for unauthorized remote connections using SM59. Delete any suspicious RFC destinations, especially those created in the last 30 days.

**4. Enable MFA on VPN**

If not already enabled, enforce multi-factor authentication for all VPN access immediately. Reset all VPN passwords.

**5. Search Logs for IoCs**

Query firewall, SAP security audit logs (SM20), and SIEM for the IP addresses and domains listed in the IoC section above.

---

### ⚠️ Short-Term Actions (Next 7 Days)

**1. Conduct Security Audit**

Perform comprehensive SAP security assessment focusing on dormant/orphaned accounts, accounts with unchanged passwords >90 days, overly permissive role assignments, and unencrypted RFC connections.

**2. Implement Network Segmentation**

Isolate SAP landscape from general corporate network. Implement firewall rules restricting SAP Gateway access to known IP ranges only.

**3. Backup Verification**

Test restoration from backups. Ensure backup infrastructure is isolated from production network and cannot be accessed via compromised SAP accounts.

**4. Enable Enhanced Logging**

Configure SAP Security Audit Log (RSAU_CONFIG) to capture all RFC calls, user administration changes, critical transaction execution, and failed login attempts (>3 per hour).

**5. Incident Response Planning**

Update IR playbooks to include SAP-specific procedures. Conduct tabletop exercise simulating this attack scenario.

---

### 📋 Strategic Actions (Next 30 Days)

**1. Deploy SAP-Aware Security Monitoring**

Implement solutions capable of detecting SAP-specific attack patterns (e.g., Onapsis, SecurityBridge, or native SAP Enterprise Threat Detection).

**2. Establish Threat Intelligence Sharing**

Join industry ISACs and information sharing groups (FS-ISAC, Retail Cyber Intelligence Sharing Center).

**3. Security Awareness Training**

Conduct phishing simulation campaigns focusing on SAP-themed lures ("Security Patch Required", "System Maintenance").

**4. Third-Party Risk Assessment**

Audit all vendors with RFC or VPN access to SAP systems. Implement least-privilege access principles.

**5. Cyber Insurance Review**

Verify coverage for ransomware incidents, data exfiltration, and business interruption. Ensure compliance with policy security requirements.

---

### Detection Queries

#### SAP Security Audit Log (SM20/SM21)

```sql
-- Suspicious RFC Activity
SELECT * FROM RSAUPROF
WHERE
    TCODE IN ('SM59', 'RFC1', 'SM69')
    AND MANDT = '100'
    AND DATUM >= '20240101'
    AND UZEIT BETWEEN '220000' AND '050000'
    AND TERMINAL NOT IN (SELECT TERMINAL FROM KNOWN_ADMIN_IPS)
ORDER BY DATUM DESC, UZEIT DESC;

-- New Administrative Accounts
SELECT BNAME, ERDAT, UFLAG, CLASS
FROM USR02
WHERE
    ERDAT >= '20240101'
    AND (BNAME LIKE '%TEMP%' OR BNAME LIKE '%ADMIN%' OR BNAME LIKE '%SUPPORT%')
    AND EXISTS (
        SELECT 1 FROM AGR_USERS
        WHERE USR02.BNAME = AGR_USERS.UNAME
        AND AGR_USERS.AGR_NAME = 'SAP_ALL'
    );
```

#### Splunk SPL Queries

```spl
/* Network Connections to Known IoCs */
index=firewall OR index=proxy
| search dest_ip IN ("185.220.101.47", "45.142.214.89", "23.95.67.134")
    OR dest_domain IN ("*sap-update-service.com*", "*northdata-backup.net*")
| stats count by src_ip, dest_ip, dest_domain, dest_port
| where count > 1
| sort - count

/* Off-Hours Large Data Transfers */
index=netflow
| eval hour=strftime(_time, "%H")
| where (hour >= 22 OR hour <= 5)
| stats sum(bytes) as total_bytes by src_ip, dest_ip
| where total_bytes > 1073741824
| eval total_gb=round(total_bytes/1073741824, 2)
| sort - total_gb
| table src_ip, dest_ip, total_gb
```

---

**Advisory ID:** NCERT-2024-001 | **TLP:** AMBER — Share with sector peers only | **Classification:** RESTRICTED

Report incidents: incident@nordic-cert.eu | Hotline: +47 800 CERT-NO

*This is a fictional advisory created for training purposes.*
