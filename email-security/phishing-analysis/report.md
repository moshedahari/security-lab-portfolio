# Lab Title
Phishing Analysis

## Scenario Overview

A user reported a suspicious email to the SOC. The email and its attachment were analyzed to determine whether it was a phishing attempt and to extract actionable artifacts.

## Objective

- Identify key email metadata and indicators.
- Analyze the attachment for malicious content.
- Extract infrastructure and hosting details related to the phishing attempt.
- Assess risk and recommend defensive measures.

## Data Sources

- Forwarded phishing email (.eml format)
- Email header metadata
- Attachment file
- Reverse DNS lookup
- WHOIS lookup
- URL2PNG screenshot service

## Investigation Process

The email headers were reviewed to identify the recipient, subject, timestamp, and originating IP address. The IP was analyzed using reverse DNS to determine associated infrastructure. The attachment was opened and inspected to extract embedded URLs. The identified URL was reviewed to determine hosting provider and page content using screenshot and lookup services.

## Evidence

- Primary recipient: kinnar1975@yahoo.co.uk
- Subject: Undeliverable: Website contact form submission
- Date and time sent: 18 March 2021 04:14
- Originating IP: 103.9.171.10
- Reverse DNS host: c5s2-1e-syd.hosting-services.net.au
- Attachment name: Website contact form submission.eml
- Extracted URL: https://35000usdperwwekpodf.blogspot.sg?p=9swghttps://35000usdperwwekpodf.blogspot.co.il?o=0hnd
- Hosting service: Blogspot
- Webpage heading: Blog has been removed

## Analysis

The email uses an “undeliverable contact form submission” theme and includes an attached .eml that contains a link. The extracted URL points to Blogspot-hosted content, which is frequently used for low-friction hosting. The originating IP resolves to a hosting domain, suggesting the email originated from hosted infrastructure rather than an internal corporate mail system. The URL2PNG snapshot indicates the page was removed at the time of review.

## Findings

The analyzed email exhibits characteristics consistent with a phishing attempt. It uses a contact form themed subject line, originates from hosted infrastructure, and contains a Blogspot-hosted URL within an attached .eml file. These indicators suggest the message was crafted to redirect the recipient to externally hosted content for potential malicious purposes.

## Risk Impact

Severity: Medium

If the user had interacted with the phishing link, credentials or sensitive information could have been compromised. The use of common hosting services increases the likelihood of similar future attempts.

## Recommendations

- Block the identified IP and malicious URLs at the email gateway and web proxy.
- Monitor for additional emails with similar subject lines or attachment names.
- Implement URL rewriting and sandbox detonation for attachments.
- Provide user awareness training on phishing recognition.
