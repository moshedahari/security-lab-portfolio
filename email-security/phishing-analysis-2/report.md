# Lab Title

Phishing Analysis 2

## Scenario Overview

A suspected phishing email was reported for analysis. The objective was to triage the message, extract indicators, and assess whether it formed part of a credential-harvesting campaign.

## Objective

- Extract key email metadata and sender information.
- Identify impersonation tactics.
- Analyze embedded URLs and page behavior.
- Collect actionable indicators for detection and blocking.

## Data Sources

- Raw phishing email (.eml)
- Email headers and body content
- URL2PNG screenshot service
- Text editor review of message source

## Investigation Process

The email headers were reviewed to identify sender, recipient, subject line, and timestamp. The body content was inspected for embedded links and impersonation attempts. The main call-to-action URL was extracted and analyzed. The message source was reviewed in a text editor to determine encoding methods. External resources referenced within the email were examined to identify additional infrastructure indicators.

## Evidence

- Sending email: amazon@zyevantoby.cn
- Recipient email: saintington73@outlook.com
- Subject line: Your Account has been locked
- Impersonated company: Amazon
- Date and time sent: 14 Jul 2021 01:40:32 +0900
- Main call-to-action URL: https://emea01.safelinks.protection.outlook.com/?url=https://amaozn.zzyuchengzhika.cn/?mailtoken=saintington73@outlook.com&data=04|01||70072381ba6e49d1d12d08d94632811e|84df9e7fe9f640afb435aaaaaaaaaaaa|1|0|637618004988892053|Unknown|TWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0=|1000&sdata=oPvTW08ASiViZTLfMECsvwDvguT6ODYKPQZNK3203m0=&reserved=0
- Landing page heading: This web page could not be loaded.
- Encoding scheme used in body: base64
- Logo retrieval URL: https://images.squarespace-cdn.com/content/52e2b6d3e4b06446e8bf13ed/1500584238342-OX2L298XVSKF8AO6I3SV/amazon-logo?format=750w&amp;content-type=image%2Fpng
- Facebook profile referenced: amir.boyka.7

## Analysis

The sender domain does not match Amazon and originates from a suspicious foreign domain. The subject line uses urgency to prompt immediate action. The embedded SafeLinks URL ultimately redirects to a lookalike domain attempting to mimic Amazon. The email body was base64 encoded, which is common in HTML email formatting. The decoded content revealed embedded phishing links.

## Findings

The email is a phishing attempt impersonating Amazon to induce credential submission. It uses domain spoofing, encoded content, and redirection techniques to bypass basic filtering controls.

## Risk Impact

Severity: Medium

If the recipient interacted with the link, account credentials could have been exposed. The impersonation of a trusted brand increases likelihood of user interaction.

## Recommendations

- Block identified malicious domains and URLs at email and web gateways.
- Monitor for similar spoofed domains targeting users.
- Implement detection for brand impersonation combined with external login URLs in email content.
- Provide user awareness training focused on brand impersonation.
