# Lab Title
The Report

## Scenario Overview

A 2022 threat intelligence report was reviewed to identify dominant attack trends and extract actionable improvements for a developing SOC. The focus was on exploited vulnerabilities, prevalent attacker techniques, and defensive gaps.

## Objective

- Identify major campaigns and exploited vulnerabilities.
- Determine high-impact MITRE techniques affecting organizations.
- Translate intelligence findings into practical SOC improvements.

## Data Sources

- 2022 Threat Detection Report
- MITRE ATT&CK framework

## Key Intelligence Extracted

- Supply chain attack: Log4j
- Most prevalent MITRE technique: T1059
- Exchange vulnerabilities: ProxyLogon, ProxyShell
- Zero-day vulnerability: PrintNightmare (CVE-2021-34527)
- SEO abuse groups: Gootkit, Yellow Cockatoo
- Parent process for malicious JS execution: wscript.exe
- Conti affiliate precursors: Qbot, Bazar, IcedID
- Outdated software targeted by miners: JBoss, WebLogic
- Ransomware group using DDoS extortion: Fancy Lazarus
- RDP protection measure: MFA

## Analysis

The report shows that attackers continue to exploit unpatched enterprise software and rely heavily on scripting-based execution (T1059). Exchange vulnerabilities and zero-day exploits contributed to widespread compromise. SEO poisoning remains an effective initial access method. Ransomware operations increasingly leverage affiliate access models and additional extortion tactics. Outdated infrastructure significantly increases exposure to coin mining and ransomware activity.

## Findings

- Execution through scripting remains a dominant attack method.
- Unpatched Exchange and enterprise software create high-risk exposure.
- SEO poisoning and affiliate-based ransomware access models are active threats.
- RDP without MFA significantly increases ransomware risk.

## Risk Impact

Severity: High

Organizations lacking strong patch management, scripting visibility, and MFA enforcement are at elevated risk of ransomware, privilege escalation, and widespread compromise.

## Recommendations

- Prioritize patching of externally exposed and outdated systems.
- Strengthen detection coverage for scripting activity (T1059).
- Monitor suspicious use of wscript.exe.
- Enforce MFA on all RDP access.
- Regularly review threat intelligence to adjust detection priorities.
