# Lab Title
Follina

## Scenario Overview

A newly disclosed remote code execution vulnerability, CVE-2022-30190 (Follina), was reported to be actively exploited. A suspicious Word document was identified for analysis to determine whether it leveraged this vulnerability and to assess potential impact.

## Objective

- Identify and profile the malicious document sample.
- Determine how the Follina vulnerability is triggered.
- Analyze execution behavior and detection opportunities.
- Map observed behavior to MITRE ATT&CK and the associated CVE.

## Data Sources

- Malicious Microsoft Word document (sample.doc)
- Extracted XML relationship file
- Remote HTML content referenced by the document
- Public threat intelligence (VirusTotal, MITRE ATT&CK)

## Investigation Process

The document hash was calculated to uniquely identify the sample. The file was identified as a Microsoft Word 2007+ (OOXML) document despite using a .doc extension. The archive structure was extracted and inspected, focusing on relationship files to identify external references.

The file word/_rels/document.xml.rels contained an external OLE relationship pointing to a remote HTML resource. That URL was confirmed through VirusTotal behavior analysis as being retrieved during execution.

## Evidence

- SHA1: 06727ffda60359236a8029e0b3e8a0fd11c23313
- Extracted URL: https://www.xmlformats.com/office/word/2022/wordprocessingDrawing/RDF842l.html
- XML file containing URL: word/_rels/document.xml.rels
- Exploit trigger threshold: 4096 bytes
- Process targeted for termination: msdt.exe
- MITRE Technique: T1559
- CVE: CVE-2022-30190

## Analysis

The document leverages an external relationship to retrieve remote HTML content. When opened, Microsoft Word processes this external content, which invokes the ms-msdt protocol handler.

The ms-msdt protocol launches msdt.exe (Microsoft Support Diagnostic Tool). The vulnerability (CVE-2022-30190) allows attacker-controlled parameters to be passed through this mechanism, leading to arbitrary code execution without requiring macros.

Observed behavior indicates the sample attempts to terminate msdt.exe if an instance is already running, likely to ensure a clean execution path for the malicious invocation. The abnormal parent-child relationship between WINWORD.EXE and msdt.exe is inconsistent with legitimate document behavior and provides a strong detection opportunity.

## Findings

The analyzed sample exploits CVE-2022-30190 (Follina) to achieve remote code execution. It retrieves external HTML content via a relationship file and abuses the ms-msdt protocol to invoke msdt.exe. The behavior aligns with MITRE ATT&CK technique T1559 (Inter-Process Communication).

## Risk Impact

Severity: High

Successful exploitation allows remote code execution upon document interaction. In a real-world environment, this could provide initial access to an attacker and enable further compromise depending on the delivered payload.

## Recommendations

- Apply security updates addressing CVE-2022-30190.
- Disable or restrict the ms-msdt protocol handler if not required.
- Monitor for Office applications spawning msdt.exe (Event ID 4688).
- Block or monitor connections to the extracted URL/domain.
- Hunt for the provided SHA1 across endpoints.