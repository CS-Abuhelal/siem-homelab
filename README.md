# SIEM Home Lab

My home SOC: Wazuh running in VirtualBox, monitoring a Windows 11 machine — my own.

I built this to practice the workflows a SOC analyst actually does day to day: enrolling agents, chasing down vulnerability alerts, mapping events to MITRE ATT&CK, and running compliance scans. Watching your own machine through a SIEM turns out to be a fast way to learn — every finding is personal.

![Wazuh endpoint dashboard overview](screenshots/dashboard-overview.png)

## Setup

- **SIEM:** Wazuh v4.14.5, single-node, deployed from the official OVA
- **Hypervisor:** Oracle VirtualBox
- **Monitored endpoint:** Windows 11 machine enrolled as a Wazuh agent
- **Modules enabled:** Threat Hunting, File Integrity Monitoring, Security Configuration Assessment, MITRE ATT&CK mapping, Vulnerability Detection

## What it found

- **CVE-2025-55130 (Critical, CVSS 9.1)** sitting in the Node.js install on my own machine, plus 17 High / 15 Medium / 2 Low findings across the software inventory. Nothing teaches patch management like your own laptop failing a scan.
- **489 events mapped to MITRE ATT&CK T1562.001** (Defense Evasion — Disable or Modify Tools). Traced them to a benign scheduled software-protection service — a lesson in why baselining matters before you panic.
- **25% CIS benchmark compliance** — 351 of 482 checks failed against the CIS Windows 11 Enterprise Benchmark v3.0.0. That's what a default, out-of-the-box install looks like against an enterprise baseline.

## Full report

The complete write-up — lab setup, findings with dashboard evidence, risk summary, and remediation steps — is in [writeup.md](writeup.md).
