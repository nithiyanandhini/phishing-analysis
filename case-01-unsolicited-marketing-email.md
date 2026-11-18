# Phishing Analysis Report: Case 01

**Date analyzed:** November 18, 2026
**Source of sample:** Personal Gmail spam folder (received November 13, 2026)
**Analyst:** Nithiya Nandhini Dass
**Verdict:** Benign: unsolicited marketing email (no malicious indicators found)
**Severity:** Low

## 1. Summary
An email titled "Your first lesson is on us!" from a music academy in Brampton, Ontario advertised a Black Friday offer (free first lesson and a waived first-year membership fee, valid until November 30, 2026). It was sent in bulk through an email marketing platform whose sending IP has three old spam reports. The sender domain is almost five years old and passes SPF, DKIM and DMARC. Every link goes through one tracking domain and then to the academy's own registration page. No malware, credential harvesting or brand impersonation was found. I classify it as unsolicited marketing.

## 2. Email details
| Field | Value |
|---|---|
| Subject | Your first lesson is on us! |
| From (display name) | Synergy Music Academy |
| From (actual address) | info@synergymusicacademy[.]com |
| To | [redacted]@gmail.com |
| Reply-To | Not present |
| Return-Path | bounces+[tracking-id]@sendersrv[.]com |
| Date sent | Fri, Nov 13, 2026, 19:43 UTC (2:43 PM Eastern), delivered after 25 seconds |
| Message-ID domain | sendersrv[.]com |
| Sending host / IP | mail11.sendersrv3[.]com / 185.3.229[.]155 |
| Transport | TLS 1.3 |

## 3. Header checks
| Check | Result | Notes |
|---|---|---|
| SPF | Pass | 185.3.229[.]155 is an allowed sender for the Return-Path domain sendersrv[.]com |
| DKIM | Pass (two signatures) | One signed by sendersrv[.]com and one by synergymusicacademy[.]com, so the From domain is properly signed |
| DMARC | Pass | Policy is p=NONE (monitoring only), which is common but weaker than quarantine or reject |
| Display name vs actual domain match? | Yes | Name and domain match. The footer says "SYNERGY Performing Arts Academy", a small naming difference that matches a business with more than one program |
| Sending IP reputation (AbuseIPDB) | 0% confidence score, 3 reports | All 3 reports are from September 2022 and mention spam from sendersrv[.]com. None in the last 60 days. ISP UAB Synergia, Lithuania |

**Bulk-mail markers:** `Precedence: bulk`, `List-Unsubscribe` with one-click unsubscribe, and `Feedback-ID` all point to a marketing platform. Image and tracking URLs (`stats.sender[.]net`, `cdn.sender[.]net`) suggest the platform is Sender.net.

Passing SPF, DKIM and DMARC shows the sender is authenticated. It does not prove the email is wanted or safe.

## 4. Body and link analysis
- **Social engineering tactic:** Free offer with a deadline ("Register by November 30th"). Mild urgency, no request for credentials or payment.
- **Content:** Black Friday offer for private music lessons or an Academic Art program. The footer lists two Brampton locations and phone numbers, and the landing page title matches ("SYNERGY Music Academy, Brampton").
- **Tracking and hidden content:** The email contains a 1x1 tracking pixel (`stats.sender[.]net/email_open/...`) and hidden preheader text padded with invisible characters. Both are standard marketing techniques, not signs of an attack.
- **Links found (defanged):**
  - REGISTER NOW button: hxxps://campaign-statistics[.]com/link_click/[tracking-id]/[hash] (HTTP 302 redirect)
  - 4 social media icons (Instagram, Facebook, one other, YouTube): all through campaign-statistics[.]com/link_click/...
  - Unsubscribe: hxxps://stats.sender[.]net/unsubscribe/[tracking-id]
  - Final page after redirect: hxxps://synergymusicacademy[.]com/register?utm_campaign=...&utm_medium=email
- **URL scan result (URLScan.io):** No classification. Page title "Register for Lessons | SYNERGY Music Academy, Brampton". Landing IP 147.93.42[.]57 (Hostinger, Boston). 49 requests to 11 domains, 96% HTTPS. Detected technologies: Google Analytics, Google Tag Manager, DoubleClick Floodlight and reCAPTCHA, all normal for a marketing site. TLS certificate issued November 6, 2026.
- **Link scan on VirusTotal:** No security vendor flagged the link as malicious or phishing (Google Safe Browsing, OpenPhish, Phishtank and URLhaus all Clean).
- **Sender domain age and registrar (WHOIS):** synergymusicacademy[.]com created December 2021, registrar Tucows, expires December 2027. Last updated November 12, 2026, the day before the email was sent. I noted this but found no other sign of compromise.
- **Sending service domain:** sendersrv[.]com had no vendor detections on VirusTotal (zero malicious or phishing flags from the major engines, including Google Safe Browsing, OpenPhish and Phishtank). Creation date not checked.

## 5. Attachment analysis
No attachment.

## 6. Indicators of compromise (IOCs)
None malicious. Observed indicators, for reference only:
| Type | Value |
|---|---|
| Sender domain | synergymusicacademy[.]com |
| Bulk sender domain | sendersrv[.]com |
| Sending host / IP | mail11.sendersrv3[.]com / 185.3.229[.]155 |
| Tracking domain | campaign-statistics[.]com |
| Tracking / unsubscribe host | stats.sender[.]net |
| Landing IP | 147.93.42[.]57 |

## 7. MITRE ATT&CK mapping
No technique observed. If the link had led to a fake login page, this would map to T1566.002 (Spearphishing Link).

## 8. Recommended actions
1. No block needed. Mark the message as spam or use the unsubscribe link if the user did not sign up.
2. If this sender appears often, consider filtering the bulk-sender domain sendersrv[.]com at the email gateway, because of its history of spam reports.
3. No user action needed. Remind users to check the real domain before clicking an offer they don't recognize.

## 9. Escalation note (written for a Tier 2 analyst)
No escalation needed. Bulk marketing email from a 5-year-old business domain. Passes SPF, DKIM (two signatures) and DMARC (p=NONE). All links go through one tracking domain and land on the sender's own registration page. The sending IP has 3 old spam reports (Sept 2022) and none in the last 60 days. No malicious detections on VirusTotal for the sender domain, the sending service or the link, and no classification on urlscan.io. The domain's WHOIS was updated one day before sending, which I noted but found no other sign of compromise. Classified as unsolicited marketing, low severity.
