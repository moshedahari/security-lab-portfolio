# Lab Title
Log Analysis - Privilege Escalation

## Scenario Overview

Sensitive data restricted to the root account was accessed and leaked from a Linux server hosting a PHP-based website. Upload filtering was reportedly enforced to prevent malicious PHP execution. Bash history was provided to determine how the attacker obtained root-level access.

## Objective

- Identify how the attacker gained interactive access.
- Determine how privilege escalation to root occurred.
- Extract tools, techniques, and misconfigurations exploited.

## Data Sources

- Provided bash history
- Server directory paths and permissions
- GTFOBins reference material

## Investigation Process

The bash history was reviewed sequentially to reconstruct attacker actions. Commands were grouped into phases including system enumeration, privilege escalation attempts, and cleanup. Particular attention was given to web directory activity, SUID binary discovery, and execution of privileged shells.

## Evidence

- Additional local user present: daniel
- Web uploads directory accessed: /var/www/html/uploads
- File removed: /var/www/html/uploads/x.phtml
- Enumeration script downloaded:
  - linux-exploit-suggester.sh
- Packet capture tool attempted:
  - tcpdump
- SUID binary discovery:
  - find / -type f -user root -perm -4000 2>/dev/null
- Privilege escalation execution:
  - ./usr/bin/python -c 'import os; os.execl("/bin/sh", "sh", "-p")'

## Analysis

At the start of the recorded history, the attacker was already operating interactively on the system, navigating web directories and executing commands such as `id` and `whoami`, indicating an established foothold prior to the visible session.

After confirming access, the attacker conducted local system enumeration. This included reviewing user directories, checking running processes, examining configuration files, and downloading `linux-exploit-suggester.sh` to assist in identifying privilege escalation vectors. The attacker also manually searched for SUID binaries.

A misconfigured SUID `python` binary was identified and exploited using a known GTFOBins technique to spawn a privileged shell (`sh -p`). This resulted in full root-level access. Following escalation, the attacker removed `x.phtml`, likely to reduce visible forensic artifacts.

The deletion of `/var/www/html/uploads/x.phtml`, combined with the known `.phtml` file extension bypass described in the scenario, strongly suggests that a web shell existed in the uploads directory. The exact moment of upload is not visible in the bash history, as file uploads would occur via HTTP rather than the shell.

## Findings

- The attacker had an interactive foothold before the recorded bash history begins.
- The attacker performed structured local enumeration, including downloading a privilege escalation helper script.
- Root access was achieved by abusing a misconfigured SUID `python` binary.
- The web shell was removed after escalation, indicating cleanup activity.

## Risk Impact

Severity: High

The attacker achieved full root-level control of a server hosting sensitive data. Weak file upload controls and improper SUID permissions allowed complete system compromise.

## Recommendations

- Remove unnecessary SUID permissions, particularly from interpreter binaries such as `python`.
- Enforce strict server-side file validation, including MIME-type verification and execution restrictions.
- Disable script execution within upload directories.
- Monitor for SUID enumeration activity and unusual interpreter-based shell spawning.
- Implement centralized logging and file integrity monitoring for web directories.
