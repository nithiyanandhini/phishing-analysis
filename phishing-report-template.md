# Phishing Analysis Report: Case [number]

**Date analyzed:** [date]
**Source of sample:** [e.g. LetsDefend alert, phishing_pot sample, own mailbox spam folder]
**Analyst:** Nithiya Nandhini Dass
**Verdict:** [Malicious / Suspicious / Benign]
**Severity:** [Low / Medium / High]

## 1. Summary
[2 to 3 sentences: what the email pretends to be, what it asks the user to do, and your verdict.]

## 2. Email details
| Field | Value |
|---|---|
| Subject | |
| From (display name) | |
| From (actual address) | |
| Reply-To | |
| Return-Path | |
| Date sent | |
| Sending IP (from headers) | |

## 3. Header checks
| Check | Result | Notes |
|---|---|---|
| SPF | pass / fail / none | |
| DKIM | pass / fail / none | |
| DMARC | pass / fail / none | |
| Display name vs actual domain match? | yes / no | |
| Sending IP reputation (AbuseIPDB) | | |

## 4. Body and link analysis
- **Social engineering tactic:** [urgency, fear, reward, authority, etc.]
- **Links found (defanged, e.g. hxxps://example[.]com):**
  - 
- **URL scan result (URLScan.io / VirusTotal):**
- **Domain age and registrar (WHOIS):**

## 5. Attachment analysis (only inside an isolated VM)
| File name | File type | SHA-256 | VirusTotal result |
|---|---|---|---|
| | | | |

## 6. Indicators of compromise (IOCs)
| Type | Value |
|---|---|
| Sender address | |
| Sender domain | |
| Sending IP | |
| URL | |
| File hash | |

## 7. MITRE ATT&CK mapping
- T1566.001 Spearphishing Attachment, or T1566.002 Spearphishing Link (keep the one that applies)
- [Any other technique the sample shows]

## 8. Recommended actions
1. [e.g. Block sender domain and URL at the email gateway]
2. [e.g. Search mailboxes for the same subject and sender]
3. [e.g. If a user clicked or opened the file: reset password, isolate the device, escalate to Tier 2]
4. [e.g. Notify the user and report to the security team]

## 9. Escalation note (written for a Tier 2 analyst)
[3 to 5 lines: what you found, evidence, what you already did, what you need from the next person.]
