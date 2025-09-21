 Network-Reconnaissance-With-Nmap
A hands-on demonstration of network reconnaissance, service enumeration, and vulnerability scanning using Nmap, following a structured methodology.

 Network Reconnaissance & Vulnerability Assessment with Nmap

A practical project demonstrating a structured approach to network security assessment using Nmap. This project documents the process of discovering hosts, enumerating services, and identifying potential vulnerabilities on a target system.

 📖 Project Overview

This assessment was performed against a local host in a controlled lab environment. The goal was to emulate the initial stages of a penetration test: **Reconnaissance** and **Enumeration**.

 🎯 Objectives

*   **Host Discovery:** Identify live hosts on the network.
*   **Port Scanning:** Discover open ports and services.
*   **Service Enumeration:** Determine the version of software running on open ports.
*   **Vulnerability Scanning:** Use Nmap's scripting engine to check for known vulnerabilities.
*   **Reporting:** Document findings in a clear and structured manner.

 ⚙️ Tools Used

*   **Nmap** (v7.98) - The core scanning tool
*   **Windows PowerShell** - Command-line environment
*   **A custom PowerShell script** (`gnmap_to_csv.ps1`) - For parsing results

 🚀 Methodology & Commands Executed

The assessment followed a phased approach:

1.  **Setup & Verification**
    *   `nmap --version`
    *   `mkdir C:\nmap_scans` - Created a directory for organized output.

2.  **External Test Scan** (scanme.nmap.org)
    *   `nmap -sV scanme.nmap.org -oA C:\nmap_scans\scanme_demo`

3.  **Host Discovery** on local network
    *   `nmap -sn 192.168.31.237 -oA C:\nmap_scans\01-hosts`

4.  **Full TCP Port Scan**
    *   `nmap -sS -Pn -p- -T4 -oA C:\nmap_scans\02-full-tcp 192.168.31.237`

5.  **Service and Version Detection**
    *   `nmap -sV -sC -oA C:\nmap_scans\03-svc-versions 192.168.31.237`

6.  **Vulnerability Scanning**
    *   `nmap -sV --script vuln -oA C:\nmap_scans\05-vuln 192.168.31.237`

7.  **Reporting & Analysis**
    *   `Get-ChildItem -Path C:\nmap_scans -Force` - Listed all output files.
    *   Custom script executed: `.\gnmap_to_csv.ps1` - Generated a summary report.

 📊 Key Findings & Analysis

A summary of the most interesting results from the scans.

**Open Ports & Services Identified:**
| Port | State | Service | Version |
| :--- | :--- | :--- | :--- |
| 135/tcp | open | msrpc | Microsoft Windows RPC |
| 139/tcp | open | netbios-ssn | Microsoft Windows netbios-ssn |
| 445/tcp | open | microsoft-ds | (Could not confirm version) |
| 3306/tcp | open | mysql | MySQL (Unauthorized) |
| 7070/tcp | open | ssl/realserver | AnyDesk Client |

**Vulnerability Scan Results:**
*   The `vuln` script scan did not identify any critical vulnerabilities for the primary services (e.g., SMB).
*   **Note:** The MySQL server returned an "unauthorized" status, which is a common finding but should be investigated further in a real assessment.
