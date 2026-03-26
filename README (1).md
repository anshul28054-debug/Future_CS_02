# FUTURE_CS_02 — Phishing Email Analysis Report

> **Author:** Anshul  
> **Domain:** Cybersecurity | Threat Intelligence & Email Forensics  
> **Date:** March 26, 2026

---

## 📋 Overview

This project presents a forensic analysis of **10 email samples** — 3 sourced from real-world inbox captures and 7 from curated public phishing datasets. Each sample was evaluated across authentication records, sender identity, content patterns, embedded links, and IP reputation to classify it as **Phishing**, **Suspicious**, or **Safe**.

---

## 🛠️ Tools Utilized

| Tool | Purpose |
|------|---------|
| **Google Admin Toolbox – Message Header Analyzer** | Evaluate SPF, DKIM, and DMARC authentication results; inspect email routing paths and delivery timestamps across all 10 samples |
| **Cisco Talos Intelligence** | IP reputation analysis and network ownership identification for real-world samples (E-01, E-02, E-03) |
| **Gmail "Show Original" Feature** | Extract raw, unprocessed email headers from authenticated inbox messages |
| **Public GitHub Phishing Datasets** | Source for curated phishing samples (E-04 through E-10) |

---

## 🔍 Analysis Methodology

The analysis followed a structured, five-phase approach designed for reproducibility and evidential rigor.

### Phase 1 — Header Extraction & Authentication Analysis
- Raw email headers extracted using Gmail's "Show Original" feature
- Headers parsed via Google Admin Toolbox Message Header Analyzer
- SPF, DKIM, and DMARC results recorded for pass/fail/none status
- Routing hops and delivery timestamps examined for anomalies

### Phase 2 — Sender Domain Verification
- Display names cross-referenced against actual sending addresses (envelope `From`)
- Mismatches between display names and registered domains flagged as spoofing indicators
- Domain registration age and legitimacy considered for borderline cases

### Phase 3 — Content Examination
- Email bodies reviewed for social engineering patterns:
  - **Urgency cues** — e.g., "Account suspended", "Verify immediately"
  - **Reward-based lures** — e.g., "You have won", "Claim your prize"
  - **Brand impersonation** — banks, government agencies, tech platforms
- Personalization level of greetings analyzed as a sophistication indicator

### Phase 4 — Link Inspection
- Embedded URLs extracted via raw HTML source analysis
- No links activated or visited — all inspection was **passive**
- URL structures evaluated for domain spoofing, path obfuscation, and redirect chains

### Phase 5 — IP Reputation Analysis
- Sending IPs submitted to Cisco Talos Intelligence for reputation scoring
- Historical behavior, block-list status, and network ownership reviewed
- Results correlated with authentication failures to strengthen classification confidence

---

## 📊 Classification Framework

Each email was assessed using a **four-indicator scoring model**:

| Indicators Present | Classification | Risk Level |
|--------------------|---------------|------------|
| 2 or more | 🔴 **Phishing** | High |
| 1 | 🟠 **Suspicious** | Medium |
| 0 | 🟢 **Safe** | Low |

**The four assessed indicators:**
1. Authentication failure (SPF / DKIM / DMARC)
2. Sender domain spoofing
3. Social engineering content
4. Malicious or obfuscated links

---

## 📁 Sample Analysis Overview

| Sample | Source | Auth Status | Classification |
|--------|--------|-------------|----------------|
| E-01 | Real-world | SPF Fail | 🔴 Phishing |
| E-02 | Real-world | DKIM Fail | 🔴 Phishing |
| E-03 | Real-world | DMARC None | 🟠 Suspicious |
| E-04 | GitHub Dataset | SPF Fail | 🔴 Phishing |
| E-05 | GitHub Dataset | DKIM Pass | 🟠 Suspicious |
| E-06 | GitHub Dataset | DMARC Fail | 🔴 Phishing |
| E-07 | GitHub Dataset | SPF Pass | 🟢 Safe |
| E-08 | GitHub Dataset | DKIM Fail | 🔴 Phishing |
| E-09 | GitHub Dataset | DMARC Fail | 🔴 Phishing |
| E-10 | GitHub Dataset | SPF Fail | 🔴 Phishing |

---

## 📌 Key Findings

- **7 of 10** samples were classified as Phishing
- **Authentication failures** were the most common indicator (present in 7 samples)
- **Display name spoofing** observed in 6 samples, impersonating financial and tech brands
- **Urgency-driven language** appeared in 80% of phishing-classified samples
- All real-world samples (E-01–E-03) originated from IPs flagged by Cisco Talos as untrusted

---

## ✅ Conclusion

Email-based phishing attacks continue to rely on a consistent and detectable set of indicators: authentication failures, sender identity deception, urgency-based social engineering, and obfuscated hyperlinks. The four-indicator classification model proved effective in distinguishing phishing from legitimate correspondence across both real-world and dataset samples.

---

*Report prepared by **Anshul** | FUTURE_CS_02 Cybersecurity Practicum*
