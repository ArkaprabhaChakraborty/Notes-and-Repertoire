---
description: Fundamentals of red teaming concepts, frameworks and methodologies
---

# Introduction

## What is Red Teaming? <a href="#user-content-what-is-red-teaming" id="user-content-what-is-red-teaming"></a>

**Red Teaming** is a highly advanced and adversary-focused cybersecurity assessment designed to simulate real-world attack scenarios. Unlike traditional penetration testing, Red Team operations aim to evaluate the **overall resilience of an organization** not just technical vulnerabilities, but also people, processes, and detection capabilities.

Red Teams emulate the **TTPs (Tactics, Techniques, and Procedures)** of real-world adversaries, such as **Advanced Persistent Threats (APTs)**, using structured methodologies like the **MITRE ATT\&CK framework** and the **Cyber Kill Chain**. These operations are stealthy by nature and often conducted **without the prior knowledge of the defensive team**, in order to create a truly realistic adversarial simulation.

***

## **Core Objectives of a Red Team Operation** <a href="#user-content-core-objectives-of-a-red-team-operation" id="user-content-core-objectives-of-a-red-team-operation"></a>

* **Holistic Evaluation**: Assess how well an organization can detect, respond to, and recover from sophisticated cyberattacks.
* **Realism Over Checklists**: Focus on threat emulation, not simple vulnerability scanning.
* **Cross-Domain Coverage**: Examine the effectiveness of technology, human behavior, and process integrity.

***

## Key Characteristics <a href="#user-content-key-characteristics" id="user-content-key-characteristics"></a>

| Aspect          | Red Team                                                                                                     |
| --------------- | ------------------------------------------------------------------------------------------------------------ |
| **Objective**   | Test the organization's resilience against real-world threats.                                               |
| **Approach**    | Covert adversary simulation with realistic goals and constraints.                                            |
| **Scope**       | Broad and customized: includes infrastructure, applications, personnel, physical security, and supply chain. |
| **Methodology** | TTP-based emulation using frameworks like **MITRE ATT\&CK**, **Cyber Kill Chain**, and custom threat models. |
| **Duration**    | Long-term engagements: from **several weeks to months**.                                                     |
| **Stealth**     | Conducted without notifying Blue Team or IT staff (Black Box).                                               |
| **Outcome**     | Measure incident detection, alert handling, escalation paths, and response effectiveness.                    |
| **Tooling**     | Custom-built malware, **C2 frameworks**, evasive payloads, manual TTP chaining, and Red Team infrastructure. |

***

#### How is Red Teaming Different from Penetration Testing? <a href="#user-content-how-is-red-teaming-different-from-penetration-testing" id="user-content-how-is-red-teaming-different-from-penetration-testing"></a>

While often confused, **Red Teaming** and **Penetration Testing** serve different purposes:

| **Aspect**       | **Red Team**                                                              | **Penetration Test**                                            |
| ---------------- | ------------------------------------------------------------------------- | --------------------------------------------------------------- |
| **Goal**         | Evaluate overall defence posture and threat response                      | Identify and exploit specific vulnerabilities                   |
| **Tactics**      | Emulate real attackers (APTs, insiders, hacktivists, etc.)                | Use known vulnerabilities and exploitation tools                |
| **Visibility**   | Operates covertly, often unknown to defenders                             | Typically conducted with full or partial awareness              |
| **Scope**        | Wide: includes physical access, social engineering, and system compromise | Narrow: focuses on systems, apps, or networks                   |
| **Duration**     | Weeks or months                                                           | Days to a few weeks                                             |
| **Deliverables** | Narrative report on detection, response gaps, and kill chain breakdown    | Technical vulnerability report and remediation steps            |
| **Tooling**      | Custom tools, obfuscated payloads, live C2 infrastructure                 | Scanners and exploitation frameworks (e.g., Nessus, Burp Suite) |

***

## Methodology and Frameworks <a href="#user-content-methodology-and-frameworks" id="user-content-methodology-and-frameworks"></a>

A Red Team operation is **not a simple checklist exercise**. It is scenario-driven and often aligned with threat intelligence. The following frameworks guide most modern Red Team engagements:

### **1. MITRE ATT\&CK**&#x20;

The MITRE ATT\&CK framework is a globally recognized knowledge base that catalogs adversary tactics, techniques, and procedures (TTPs) based on real-world observations. It serves as a foundation for threat modelling and adversary emulation planning. The framework is structured into matrices tailored for various domains, including enterprise, mobile, and cloud environments.

MITRE ATT\&CK Framework – Enterprise Tactics:&#x20;

1. **Reconnaissance:** Gathering information about the target to plan future operations (e.g., DNS info, employee emails).
2. **Resource Development:** Establishing resources, such as infrastructure or tools, to support attack operations.
3. **Initial Access:** Gaining an initial foothold in the target environment (e.g., phishing, exploiting vulnerabilities).
4. **Execution:** Running malicious code or commands on compromised systems to achieve specific objectives.
5. **Persistence:** Maintaining access to compromised systems, even after a reboot or remediation attempts.
6. **Privilege Escalation:** Gaining higher levels of access or privileges within the target environment.
7. **Defense Evasion:** Employing tactics to avoid detection by security controls.
8. **Credential Access:** Stealing credentials or obtaining legitimate credentials for unauthorized access.
9. **Discovery:** Exploring the target environment to collect information regarding the network, systems, and user accounts.
10. **Lateral Movement:** Moving laterally within the network to expand their reach and access additional systems.
11. **Collection:** Gathering data or information from compromised systems (e.g., sensitive files, credentials).
12. **Command and Control (C2):** Creating communication channels between compromised systems and external controlled entities.
13. **Exfiltration:** Stealing or moving data from the target environment to external locations or systems.
14. **Impact:** Disrupting, modifying, or destroying systems or data within the target environment.

The ATT\&CK matrix is structured around **tactics** (the **why**) and **techniques** (the **how**). Each tactic represents a **goal** or **step** in an adversary’s kill chain. A comprehensive library of adversary actions, organized by:&#x20;

1. **Tactics:** These represent the _why_ behind an adversary's actions - their strategic goals during different phases of an attack. For example, a tactic might be "Initial Access" (gaining entry) or "Lateral Movement" (moving through the network after initial entry).
2. **Techniques:** These are the _how_ - the specific methods or actions an adversary uses to achieve a tactic. For instance, under the "Initial Access" tactic, a technique might be "Spearphishing Attachment".
3. **Procedures:** These are even more granular, detailing the specific steps or implementations adversaries use for a particular technique or sub-technique. An example could be using a specific tool or a particular sequence of commands

### **2. Cyber Kill Chain**&#x20;

A model developed by Lockheed Martin that describes the stages of a cyberattack. Developed by Lockheed Martin, the Cyber Kill Chain outlines the stages of a cyberattack, from initial reconnaissance to achieving the attacker's objectives. This model aids in understanding and disrupting adversary operations at various phases.

* Reconnaissance: The attacker gathers information about the target to identify potential vulnerabilities and entry points. This can involve passive techniques like collecting public data (OSINT) or active scanning.
* Weaponization: The attacker creates a weaponized payload, such as malware or an exploit kit, that is tailored to exploit the identified vulnerabilities. This involves designing and customizing malicious tools to achieve the attacker's goals.
* Delivery: The malicious payload is delivered to the target through various means, including phishing emails, compromised websites, or infected attachments.
* Exploitation: The attacker exploits the vulnerability to execute the malicious payload and gain initial access to the target system.
* Installation: The attacker installs malware or backdoors on the compromised system to establish persistent access and maintain a foothold.
* Command and Control (C2): The attacker establishes a communication channel to remotely control the compromised systems, issue commands, and exfiltrate data.
* Actions on Objectives: The attacker carries out their ultimate goal, such as data theft, system disruption, or financial gain.&#x20;

### **3. Unified Kill Chain**

The **Unified Kill Chain (UKC)** was proposed by Paul Pols in 2017 to integrate and extend the **Lockheed Martin Cyber Kill Chain** and the **MITRE ATT\&CK** framework. It provides a **comprehensive and detailed 18-phase model** of adversary behaviour, covering both **external** and **internal** attack vectors across the full lifecycle of a cyberattack.

<table data-header-hidden><thead><tr><th width="132"></th><th width="151"></th><th width="526"></th></tr></thead><tbody><tr><td><strong>Stage</strong></td><td><strong>Phase</strong></td><td><strong>Description</strong></td></tr><tr><td><strong>Initial Foothold</strong></td><td><strong>Target Selection</strong></td><td>The attacker chooses specific organizations, systems, or users to target based on strategic goals.</td></tr><tr><td></td><td><strong>Information Gathering</strong></td><td>Open-source and technical reconnaissance to collect intel about infrastructure, personnel, and technologies.</td></tr><tr><td></td><td><strong>Weakness Identification</strong></td><td>Analysis of gathered data to identify potential vulnerabilities or human weaknesses to exploit.</td></tr><tr><td></td><td><strong>Weaponization</strong></td><td>Creation or customization of payloads (e.g., malware, exploits) tailored to identified weaknesses.</td></tr><tr><td></td><td><strong>Delivery</strong></td><td>Transmitting the payload to the victim through vectors like phishing emails, drive-by downloads, or infected media.</td></tr><tr><td></td><td><strong>Social Engineering</strong></td><td>Manipulating human behavior to enable execution (e.g., convincing users to click links or enable macros).</td></tr><tr><td></td><td><strong>Exploitation</strong></td><td>Triggering the exploit to gain initial code execution or unauthorized access on a target system.</td></tr><tr><td></td><td><strong>Installation</strong></td><td>Installing malicious software or scripts to maintain a presence in the victim’s environment.</td></tr><tr><td><strong>Internal Propagation</strong></td><td><strong>Internal Reconnaissance</strong></td><td>Exploring the internal network to discover assets, services, and potential targets for lateral movement.</td></tr><tr><td></td><td><strong>Privilege Escalation</strong></td><td>Gaining higher-level access or administrative privileges to expand control over the environment.</td></tr><tr><td></td><td><strong>Credential Dumping</strong></td><td>Extracting stored or cached credentials for use in further compromise or impersonation.</td></tr><tr><td></td><td><strong>Lateral Movement</strong></td><td>Moving across systems within the network using stolen credentials, exploits, or trusted tools.</td></tr><tr><td></td><td><strong>Defense Evasion</strong></td><td>Bypassing or disabling security mechanisms like antivirus, EDR, or logging to avoid detection.</td></tr><tr><td></td><td><strong>Persistence</strong></td><td>Ensuring long-term access through methods that survive reboots or user logouts (e.g., startup tasks, new accounts).</td></tr><tr><td><strong>Actions on Objectives</strong></td><td><strong>Data Collection</strong></td><td>Locating and aggregating sensitive or high-value data (e.g., documents, databases, credentials).</td></tr><tr><td></td><td><strong>Command and Control (C2)</strong></td><td>Establishing communication between the compromised systems and attacker-controlled servers.</td></tr><tr><td></td><td><strong>Data Exfiltration</strong></td><td>Transferring the collected data out of the victim’s environment, often covertly.</td></tr><tr><td></td><td><strong>Impact</strong></td><td>Executing the final objective, such as data encryption, destruction, theft, or service disruption.</td></tr></tbody></table>

### **4. TIBER-EU**&#x20;

Threat Intelligence-Based Ethical Red Teaming, used by financial institutions in Europe. TIBER-EU is a European framework designed to enhance the cyber resilience of financial institutions through threat intelligence-led Red Team testing. It emphasizes realistic simulations of cyberattacks to assess and improve detection and response capabilities.

<table data-header-hidden><thead><tr><th width="184"></th><th></th></tr></thead><tbody><tr><td><strong>Phase</strong></td><td><strong>Description</strong></td></tr><tr><td><strong>1. Preparation Phase</strong></td><td><p>Establishes the scope, governance, and planning of the test. Includes legal, logistical, and stakeholder arrangements.<br></p><ul><li>Project Setup: Define the test scope, identify critical functions and systems, and establish alignment with National Competent Authorities (NCAs) and regulators.</li><li>Provider Procurement: Procure external service providers, namely a Threat Intelligence Provider (TIP) and a Red Team (RT), ensuring they meet the required standards.</li><li>Risk Assessment: Conduct a risk assessment to understand potential vulnerabilities and define the scope of the test</li></ul></td></tr><tr><td><strong>2. Testing Phase</strong></td><td><p>Involves threat intelligence gathering and execution of Red Team operations against critical systems, simulating real-world threat actor behaviours.<br></p><ul><li><strong>Threat Intelligence</strong>: Tailored threat intel aligned with the threat landscape and entity profile.</li><li><strong>Red Team Test</strong>: Covert execution of simulated attacks targeting people, processes, and technology.</li><li>Continuous coordination with a White Team (trusted insiders managing the test internally).</li></ul></td></tr><tr><td><strong>3. Closure Phase</strong></td><td><p>Focuses on analysing findings, replaying attacks (Blue Team awareness), and delivering a comprehensive report with lessons learned and remediation plans.<br></p><ul><li><strong>Replay &#x26; Debrief</strong>: Blue Team analyzes the attacks (replay exercise).</li><li><strong>Reporting</strong>: Red and Blue teams produce individual reports; a final TIBER-EU report consolidates findings.</li><li><strong>Remediation</strong>: Plan actions to close identified gaps and improve resilience.</li></ul></td></tr></tbody></table>

### Additional Noteworthy Frameworks <a href="#user-content-additional-noteworthy-frameworks" id="user-content-additional-noteworthy-frameworks"></a>

* **CBEST (UK)**: A framework developed by the Bank of England to assess the cyber resilience of financial institutions through intelligence-led testing.
* **iCAST (Hong Kong)**: Implemented by the Hong Kong Monetary Authority, focusing on threat intelligence-based assessments for financial entities.
* **CORIE (Australia)**: An initiative aimed at enhancing the cyber resilience of Australia's financial sector through coordinated Red Team exercises.
* **ABS Red Teaming (Singapore)**: Guidelines provided by the Association of Banks in Singapore to conduct Red Team assessments within the banking sector.
* **NIST 800-115** (modified use): Defines **Red Teaming** as a covert, goal-driven subset of adversarial assessments that simulates real-world attacks to evaluate an organization's detection and response capabilities. It goes beyond traditional penetration testing by targeting people, processes, and technology.&#x20;

***

## Tooling <a href="#user-content-tooling" id="user-content-tooling"></a>

Red Teamers rely on a blend of **public, private, and custom tools**, including:

* **C2 Frameworks**: Cobalt Strike, Sliver, Havoc, Mythic
* **Offensive Scripting**: PowerShell, C++, Python
* **Evasion Techniques**: Obfuscation, DLL sideloading, AMSI and ETW bypass
* **Infrastructure**: Redirectors, staging servers, and domain fronting
* **Physical/SE**: BadUSBs, cloned badges, phishing payloads, rogue Wi-Fi access points

***

## **Adversary Simulation vs. Adversary Emulation** <a href="#user-content-adversary-simulation-vs-adversary-emulation" id="user-content-adversary-simulation-vs-adversary-emulation"></a>

<table data-header-hidden><thead><tr><th width="157"></th><th></th><th></th></tr></thead><tbody><tr><td>Aspect</td><td><strong>Adversary Simulation</strong></td><td><strong>Adversary Emulation</strong></td></tr><tr><td><strong>Definition</strong></td><td>A broader exercise that simulates the behavior of an attacker without replicating a specific one.</td><td>A precise reproduction of a known threat actor's real-world TTPs.</td></tr><tr><td><strong>Goal</strong></td><td>Test an organization's detection and response capabilities under attack-like conditions.</td><td>Assess how the environment responds to the <strong>exact behaviors</strong> of a known adversary.</td></tr><tr><td><strong>Threat Actor Specificity</strong></td><td>Generalized attacker behavior (e.g., a phishing campaign, lateral movement scenario).</td><td>Tightly aligned to an actual actor (e.g., APT29, FIN7) using intelligence-backed TTPs.</td></tr><tr><td><strong>Use Case</strong></td><td>Red Team operations, security control validation, SOC exercises.</td><td>Threat-informed defense, purple teaming, detection rule tuning.</td></tr><tr><td><strong>Frameworks Used</strong></td><td>MITRE ATT&#x26;CK, Cyber Kill Chain, custom scenarios.</td><td>MITRE ATT&#x26;CK, threat intel reports (Mandiant, CISA, etc.), CTI data.</td></tr><tr><td><strong>Realism Level</strong></td><td>High, but focused on scenario impact over exact fidelity.</td><td>Very high — attempts to <strong>mimic attacker behavior exactly</strong>.</td></tr><tr><td><strong>Customization</strong></td><td>Flexible — adapted to organization’s environment and goals.</td><td>Rigid — based on the known techniques of a specific APT or group.</td></tr><tr><td><strong>Examples</strong></td><td>Simulating ransomware deployment in a finance department.</td><td>Recreating APT28’s spear-phishing + malware dropper chain.</td></tr></tbody></table>

