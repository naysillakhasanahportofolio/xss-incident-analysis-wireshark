# Cybersecurity Incident Analysis: Web Cross-Site Scripting (XSS) Using TCPDump & Wireshark

A technical security analysis focusing on detecting, capturing, and analyzing malicious network traffic generated during a Cross-Site Scripting (XSS) exploit. This project demonstrates proficiency in using open-source packet sniffing tools (**TCPDump** and **Wireshark**) to perform incident handling and digital forensics on web application vulnerabilities.

## 🎯 Project Overview
* **Focus Vulnerability:** Stored / Reflected Cross-Site Scripting (XSS)
* **Core Tools Used:** TCPDump (CLI Packet Capture), Wireshark (GUI Packet Analysis)
* **Environment:** Controlled Virtual Lab Network

---

## 🔍 Incident Analysis Workflow & Methodology

### 1. Packet Capturing via TCPDump
* Configured live network monitoring on specific target interfaces to record raw transit data.
* Executed tactical traffic filtering to isolate HTTP web service exchanges, saving raw streams into standardized capture files (`.pcap`) for forensic investigation.

### 2. Deep Packet Inspection via Wireshark
* Imported the generated `.pcap` files into Wireshark for payload structure extraction.
* Applied specialized display filters (e.g., `http.request.method == "POST"` or `http contains "script"`) to isolate anomalies.
* **Key Discovery:** Reconstructed the TCP stream to trace the exact malicious script injected into the web environment, observing how parameter inputs were weaponized by the adversary.
* **Credential Exposure Check:** Analyzed packet strings in plaintext ASCII formats within the data streams to inspect the visibility of sensitive parameters like user inputs and directory paths (`/users.txt`).

---

## 🛠️ Environment & Tools Used
* **Network Analyzers:** Wireshark, TCPDump
* **Host Operating Systems:** Linux Platform, Windows 11
* **Virtualization:** Oracle VirtualBox
* **Target Environment:** Vulnerable Web Server Application

---

## 🛡️ Mitigation & Remediation Strategies
1. **Input Validation & Sanitization:** Enforce strict allow-lists on the server-side for all incoming HTTP request parameters to strip out executable JavaScript contexts (e.g., `<script>` tags).
2. **Context-Aware Output Encoding:** Ensure that any user-supplied data reflected on the browser interface is properly encoded (HTML entities) to prevent arbitrary browser execution.
3. **Secure Protocol Enforcements:** Transition from plaintext HTTP to encrypted HTTPS to render intercepted packets unreadable to unauthenticated network sniffers.
