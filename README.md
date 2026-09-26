# Phishing Email Investigation

## Project Overview

This project documents a practical email-security investigation of two raw email samples.

The investigation focuses on identifying phishing and spam-style indicators through:

- Email header analysis
- SPF, DKIM, and DMARC authentication checks
- Sender and sending-infrastructure analysis
- Social-engineering indicators
- URL and IOC extraction
- Evidence-based email classification
- MITRE ATT&CK mapping where applicable

The investigation was performed using raw email data, with potentially unsafe links kept defanged and not accessed.
## Investigation Results

| Email | Classification | Confidence |
|---|---|---|
| Email 01 | Promotional/Spam-style | Moderate |
| Email 02 | Likely Phishing | High |

### Email 01

Key observations:

- Promotional casino/gambling content
- SPF: PASS
- DKIM: PASS
- DMARC: Not reported
- Shortened TinyURL
- No confirmed malicious behavior established

### Email 02

Key observations:

- Microsoft-themed sender identity
- Sender domain: `microsoftonline-verify.com`
- SPF: FAIL
- DKIM: FAIL
- DMARC: FAIL
- Urgent account-security language
- Shortened Bitly URL
- MITRE ATT&CK: `T1566.002 — Phishing: Spearphishing Link`
- 

 ## Project Structure

```text
Phishing-Email-Investigation/
├── evidence/
│   ├── email-01/
│   │   ├── email-01.eml
│   │   ├── header-analysis.txt
│   │   ├── iocs.txt
│   │   └── summary.txt
│   └── email-02/
│       ├── email-02.eml
│       ├── header-analysis.txt
│       ├── iocs.txt
│       └── summary.txt
├── screenshots/
│   ├── email-01/
│   │   └── email-01-header-analysis.png
│   └── email-02/
│       └── email-02-header-analysis.png
└── reports/
    └── final-report.md


**Safety
Raw email files were analyzed without opening links.
Shortened URLs were kept defanged.
No potentially unsafe URL destinations were accessed.
No attachments were opened.
Classifications were based on available email evidence.
