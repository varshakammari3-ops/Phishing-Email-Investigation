# Phishing Email Investigation Report

## Investigation Scope

This investigation analyzed two raw email samples to identify phishing, spam-style, and suspicious characteristics using email headers, authentication results, sender infrastructure, message content, and extracted indicators of interest (IOCs).

### Emails Investigated

- Email 01 — Promotional/Spam-style
- Email 02 — Likely Phishing

### Safety Controls

- Raw email content was analyzed as text.
- Links were not opened or resolved.
- URLs were defanged in the investigation notes.
- No email attachments were opened.

## Investigation Methodology

The investigation followed a structured email-analysis process:

1. Review the raw email headers.
2. Identify the sender, Return-Path, sending host, and sending IP.
3. Review SPF, DKIM, and DMARC authentication results.
4. Examine the email body for social-engineering indicators.
5. Extract URLs, domains, IP addresses, and email addresses as IOCs.
6. Keep URLs defanged and do not access their destinations.
7. Assess the available evidence and assign a classification with confidence.
8. Map confirmed phishing behavior to the relevant MITRE ATT&CK technique where supported by the evidence.
## Email 01 — Promotional/Spam-style

### Header and Authentication Findings

- From: `132784@534617.vav.proo55.us.com`
- Return-Path: `bounce@vav.proo55.us.com`
- Sending Host: `vav.proo55.us.com`
- Sending Server: `vps-b3328616.vps.ovh.net`
- Sending IP: `141.95.0.46`
- SPF: **PASS**
- DKIM: **PASS**
- DKIM: **NEUTRAL (expired)** for `googlemail.com`
- DMARC: **Not reported** in the supplied Authentication-Results

The sender and Return-Path domains are structurally related. No obvious display-name/domain mismatch was identified from the supplied headers.

### Content Findings

- Promotional casino/gambling content.
- "50 Spins On Us" promotional offer.
- "Start Spinning Now" call-to-action.
- Shortened TinyURL used for the call-to-action.
- The same shortened URL was also used for the unsubscribe and terms links.

### IOCs

- Domain: `vav.proo55.us.com`
- Domain: `534617.vav.proo55.us.com`
- Domain: `vps-b3328616.vps.ovh.net`
- IP: `141.95.0.46`
- URL: `hxxps://tinyurl[.]com/mrymsuhv`
- Email: `132784@534617.vav.proo55.us.com`
- Email: `bounce@vav.proo55.us.com`

### Classification

**Promotional/Spam-style**

**Confidence: Moderate**

The available evidence supports a promotional/spam-style classification. SPF and the primary DKIM result passed, while another DKIM result was expired/neutral. The shortened URL requires caution, but its destination was not accessed or resolved.

### MITRE ATT&CK Assessment

No MITRE ATT&CK phishing technique is assigned at this stage because the available evidence does not establish a confirmed phishing behavior.

## Email 02 — Likely Phishing

### Header and Authentication Findings

- From: `noreply@microsoftonline-verify.com`
- Return-Path: `noreply@microsoftonline-verify.com`
- Sending Host: `mail.microsoftonline-verify.com`
- Sending Server: `vps-291847.contabo.net`
- Sending IP: `178.238.225.91`
- SPF: **FAIL**
- DKIM: **FAIL**
- DMARC: **FAIL**
- DMARC Policy: `p=NONE`

The display name claims to be "Microsoft Account Team", but the sender domain is `microsoftonline-verify.com`, not `microsoft.com`.

### Content and Social-Engineering Findings

- Subject uses urgent language: `[Action Required]`.
- The message claims unusual sign-in activity.
- Claimed sign-in location: Russia.
- Claimed sign-in IP: `91.234.99.42`.
- The recipient is instructed to secure the account immediately if the activity was not theirs.
- The "Review recent activity" button uses a shortened Bitly URL.
- The message uses Microsoft branding and a Microsoft-related sender identity.

### IOCs

- Domain: `microsoftonline-verify.com`
- Domain: `mail.microsoftonline-verify.com`
- Domain: `contabo.net`
- IP: `178.238.225.91`
- IP: `91.234.99.42`
- Email: `noreply@microsoftonline-verify.com`
- URL: `hxxps://bit[.]ly/3vF9xKz`

### Classification

**Likely Phishing**

**Confidence: High**

The combination of a Microsoft-themed identity, non-Microsoft sender domain, SPF failure, DKIM failure, DMARC failure, urgent account-security language, and a shortened Bitly URL supports the phishing classification.

The shortened URL was not opened or resolved, so the final destination was not independently analyzed.

### MITRE ATT&CK Mapping

**T1566.002 — Phishing: Spearphishing Link**

Evidence:

- Account-security lure.
- Recipient is instructed to "Review recent activity".
- A shortened Bitly URL is provided as the call-to-action.

The observed behavior is consistent with a phishing link technique.
## Comparative Analysis

| Indicator | Email 01 | Email 02 |
|---|---|---|
| Primary theme | Casino promotion | Account security |
| Sender domain | `534617.vav.proo55.us.com` | `microsoftonline-verify.com` |
| SPF | PASS | FAIL |
| DKIM | PASS | FAIL |
| DMARC | Not reported | FAIL |
| Shortened URL | TinyURL | Bitly |
| Urgency | Low | High |
| Social-engineering pressure | Limited | Strong |
| Classification | Promotional/Spam-style | Likely Phishing |
| Confidence | Moderate | High |
| MITRE ATT&CK | None assigned | T1566.002 |

### Key Observations

Email 01 primarily presents promotional content and does not provide sufficient evidence to establish phishing behavior.

Email 02 combines sender-identity concerns, authentication failures, urgency, account-security theming, and a shortened link. These indicators collectively support its classification as likely phishing.

## Final Conclusion

Based on the available evidence:

- **Email 01:** Promotional/Spam-style — Moderate confidence
- **Email 02:** Likely Phishing — High confidence

Email 01 contains promotional content and a shortened URL, but the available authentication evidence does not establish malicious intent.

Email 02 contains multiple indicators associated with phishing, including a Microsoft-themed sender identity using a non-Microsoft domain, SPF/DKIM/DMARC failures, urgent account-security language, and a shortened URL used as the call-to-action.

No links were opened or resolved during the investigation. Therefore, the analysis does not make any claim about the final destination of either shortened URL.

The classifications are based only on the evidence available in the supplied email samples.
## Evidence References

### Email 01

- Raw email: `evidence/email-01/email-01.eml`
- Header analysis: `evidence/email-01/header-analysis.txt`
- IOC analysis: `evidence/email-01/iocs.txt`
- Investigation summary: `evidence/email-01/summary.txt`

### Email 02

- Raw email: `evidence/email-02/email-02.eml`
- Header analysis: `evidence/email-02/header-analysis.txt`
- IOC analysis: `evidence/email-02/iocs.txt`
- Investigation summary: `evidence/email-02/summary.txt`

### Screenshots

Screenshots are stored under the `screenshots/` directory and are intended to provide visual evidence of the investigation workflow where applicable.