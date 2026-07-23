# Final_Year_Project-SecureDeepScan
Web Based website which check websites vulnerability and perform testing.

# SecureDeepScan (DeepScan)

**Web Vulnerability Scanning and Testing Platform**

SecureDeepScan is a free, open-source Dynamic Application Security Testing (DAST) tool that lets users scan a website for common OWASP Top 10 vulnerabilities — such as SQL Injection, Cross-Site Scripting (XSS), broken authentication, and security misconfigurations — through a simple, one-click web interface. It's built to make basic security testing accessible to students, small businesses, and junior developers who can't afford commercial tools like Burp Suite Pro or Acunetix.

## Overview

Most existing vulnerability scanners fall into two extremes: expensive enterprise platforms (high cost, complex setup) or raw open-source tools (powerful, but require technical configuration to interpret results). SecureDeepScan sits in between — it wraps the industry-standard **OWASP ZAP** scanning engine behind a lightweight dashboard and translates raw scan data into a plain-English, categorized report, so non-security users can understand and fix issues without expert help.

## Key Features

- **Simple URL Submission** — Enter a target website URL and scan depth to start a scan; no login or account required.
- **Automated Web Crawling** — Uses Beautiful Soup 4 to map the site structure and discover all accessible pages, links, and input fields (forms, search bars, login fields).
- **Vulnerability Detection Engine** — Integrates the OWASP ZAP API to actively scan for OWASP Top 10 threats (SQLi, XSS, CSRF, missing security headers, etc.).
- **Real-Time Progress Tracking** — Shows scan status as it progresses instead of leaving the user waiting on a blank screen.
- **Categorized Reporting** — Generates a PDF report (via Jinja2 + ReportLab) that groups findings by severity (High / Medium / Low) with plain-English remediation steps.
- **Scan History** — Stores past scans and reports so users can review previous results.

## Tech Stack

| Layer | Technology |
|---|---|
| Backend Framework | Django (MVC/MVT architecture) |
| Language | Python |
| Security Engine | OWASP ZAP API |
| Web Crawling | Beautiful Soup 4 |
| Database | MySQL |
| Frontend | HTML, CSS |
| Reporting | Jinja2, ReportLab (PDF generation) |
| Notifications | SMTP |

## System Architecture

The system follows an **MVC architecture**:

- **Model** — Handles database operations (User, WebsiteScan, ScanReport, ThreatDetection entities).
- **View** — Dashboard, Website Scan, and Scan Report views.
- **Controller** — Business logic split across a **Website Scan Controller** (`submitURL`, `startScan`, `generateReport`, `detectVulnerabilities`) and a **Notification Controller** (`sendAlert`, `sendReportNotification`).

### Database Schema (core entities)

- **WebsiteScan** — `scan_id`, `website_url`, `scan_date`
- **ScanReport** — `report_id`, `scan_date`, `risk_level`, `result_summary`, `scan_id` (FK)
- **ThreatDetection** — `threat_id`, `threat_name`, `threat_type`, `severity`, `report_id` (FK)
- **SystemLog** — `log_id`, `activity`, `log_time`, `status`, `user_id`

Relationships are enforced with Primary Key / Foreign Key constraints, `NOT NULL`, `UNIQUE`, and `CHECK` constraints for data integrity.

## How It Works

1. User submits a target website URL and scan depth.
2. Beautiful Soup 4 crawls the site to map pages, links, and input fields.
3. OWASP ZAP actively scans the discovered surface for known vulnerabilities.
4. Scan progress is shown in real time.
5. Results are compiled and rendered into a categorized PDF report with severity levels and remediation guidance.

## Scope

**In scope:** web application-layer DAST scanning, automated crawling, OWASP Top 10 vulnerability detection, plain-English PDF reporting.

**Out of scope:** static source code analysis, post-exploitation/active attack attempts, and network or server infrastructure testing.

## User Roles

| User | Technical Level | Interaction |
|---|---|---|
| Small Business Owner | Low | One click to scan, plain-text report |
| Junior Web Developer | Medium | Scan + inspect specific vulnerable endpoints to fix code |
| Security Expert | High | Automate repetitive scans, validate findings |

## Project Status

Final Year Project — actively in development.

## Author

**Hannan Fiaz**
Department of Information Technology, Faculty of Computing
The Islamia University of Bahawalpur

- GitHub: [github.com/AbdulHannan15](https://github.com/AbdulHannan15/)
- Project Repo: [Final_Year_Project-DeepScan](https://github.com/AbdulHannan15/Final_Year_Project-DeepScan)
