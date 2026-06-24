# Email Security &amp; Phishing Analysis in Microsoft Defender

## Objective:
The Email Security & Phishing Analysis in Microsoft Defender project documents my participation in the Day 16 Mini Project of the 30-Day MyDFIR Microsoft Challenge. The objective was to configure email security controls within Microsoft Defender for Office 365, validate their effectiveness against phishing threats, and perform an end-to-end phishing investigation. Through this project, I strengthened my skills in email security, threat analysis, OSINT, incident response, and Microsoft Defender technologies by simulating a real-world phishing attack scenario

## Project Overview:
This project focuses on implementing Safe Links and Safe Attachments policies in Microsoft Defender for Office 365, validating email protection controls, investigating a phishing email, analyzing email headers, performing OSINT on indicators of compromise (IOCs), and documenting incident response actions.

### Tools Used:
- Microsoft Defender for Office 365
- Microsoft Defender XDR
- Microsoft 365 Explorer
- Safe Links
- Safe Attachments
- Notepad++
- VirusTotal
- AbuseIPDB
- Proton Mail

### Skill Developed:
- Email security administration
- Phishing investigation
- Email header analysis
- IOC identification and analysis
- Threat intelligence validation
- Incident response
- Microsoft Defender for Office 365

### Key Deliverables:
- Safe Links policy configuration
- Safe Attachments policy configuration
- Email security policy testing
- Email header analysis
- IOC enrichment using OSINT
- Phishing investigation report
- Incident response documentation
- Security recommendations and remediation actions

## Steps Performed:
- Set Up a SAFE LINK policy:
  - In Microsoft Defender, navigate to Email & collaboration -> Policies & rules -> Threat policies -> Safe Links
<img width="750" height="418" alt="image" src="https://github.com/user-attachments/assets/2a670009-bdec-413e-be91-9c92eca7122d" />






- Deployed the Microsoft Sentinel Training Lab solution.
<img width="707" height="386" alt="image" src="https://github.com/user-attachments/assets/7a0cae76-8002-49e1-8dd1-79677f96b14d" />

- Connected Microsoft Defender XDR to Microsoft Sentinel.
<img width="703" height="392" alt="image" src="https://github.com/user-attachments/assets/e3ca776d-1fb0-43de-a66d-60213ac72d34" />
<img width="703" height="361" alt="image" src="https://github.com/user-attachments/assets/1fe6353e-235d-407e-85b8-0f84a551088f" />

- Developed KQL queries to: 
   - Identify malicious sender domains
   - Analyze Azure activity logs
   - Investigate error events
<img width="683" height="411" alt="image" src="https://github.com/user-attachments/assets/6b1b4b28-866e-49b2-a63d-1495c551a891" />
<img width="691" height="264" alt="image" src="https://github.com/user-attachments/assets/96517f56-2665-4ca4-8607-930a36b54324" />
<img width="691" height="240" alt="image" src="https://github.com/user-attachments/assets/9e4bc1bc-a288-48d8-a219-7b11f668fe3d" />


- Created a custom Sentinel Workbook containing: 
   - Activity Volume
   - Top 5 Failed User Logins 
   - Malicious Sender Domains
   - Successful Activities
<img width="752" height="335" alt="image" src="https://github.com/user-attachments/assets/c27e33db-3878-4e83-8ef5-f4dbf229e7cf" />
<img width="752" height="215" alt="image" src="https://github.com/user-attachments/assets/8be7fdfa-674a-49cf-9243-3e4438782f4b" />
<img width="750" height="259" alt="image" src="https://github.com/user-attachments/assets/2aa9a5e9-e694-4a6f-99c0-8737cf53db0e" />
<img width="749" height="270" alt="image" src="https://github.com/user-attachments/assets/6e9be7fc-8329-45be-a95d-13b9dafd8166" />

- Created a detection rule to identify accounts with excessive failed logons using Event ID 4625:
<img width="752" height="419" alt="image" src="https://github.com/user-attachments/assets/f9123fa4-66f1-4b79-b928-5c72c3a839c0" />
<img width="752" height="419" alt="image" src="https://github.com/user-attachments/assets/262fc0a0-8e10-46bd-8c31-30a0b5bc15b6" />
<img width="752" height="419" alt="image" src="https://github.com/user-attachments/assets/f93c95cf-9e47-4cb0-a594-d530540b03fc" />

- Investigated a phishing email that was marked as phishing but still allowed into the environment.
<img width="738" height="384" alt="image" src="https://github.com/user-attachments/assets/031e615b-4443-4c2c-bc6e-3e62d9a13b4a" />

- Created bookmarks and converted findings into a security incident for further analysis.
<img width="749" height="413" alt="image" src="https://github.com/user-attachments/assets/44746922-2fa1-4d4f-9bb0-4982e590cd41" />
<img width="750" height="408" alt="image" src="https://github.com/user-attachments/assets/65103eb7-8425-4c45-85ea-32c971982e3c" />
<img width="749" height="414" alt="image" src="https://github.com/user-attachments/assets/b3e3b924-5344-4078-9c11-06d6079ab9f5" />


#### Key Findings:
- A phishing email successfully bypassed email controls despite:
   - SPF failure 
   - DMARC failure 
   - Missing DKIM validation 
   - High threat confidence score 
- The sender domain used typosquatting techniques to impersonate Microsoft SharePoint. 
- The sender IP had a malicious reputation according to threat intelligence sources.

#### What I Learned:
- How Microsoft Sentinel integrates with Microsoft Defender XDR.
- How to build effective KQL queries for threat hunting.
- How workbooks improve visibility into security data.
- How detection rules automate security monitoring.
- How phishing campaigns can bypass security controls when policies are not properly configured.
- How bookmarks and incidents support SOC investigations.

#### What I Would Do Differently in a Production SOC:
- Enable stricter email filtering and anti-spoofing policies.
- Configure automatic quarantine actions for high-confidence phishing emails.
- Implement domain similarity protection.
- Automate threat intelligence enrichment using Sentinel playbooks.
- Create automated incident response workflows for phishing detections.

## Investigation Report:

#### Phishing Email Investigation:
A phishing email impersonating SharePoint was delivered to an executive mailbox despite multiple authentication failures and a phishing verdict.

#### Query Used:
- MailGuard365_Threats_CL     
  | where ThreatVerdict contains "phish" and Direction == "Inbound"
  | where Action contains "Allow" and SPFResult == "Fail" and DKIMResult == "None" and DMARCResult == "Fail"
  | sort by ThreatConfidence

<img width="758" height="420" alt="image" src="https://github.com/user-attachments/assets/a788bad8-b715-4eff-b256-0f427dfbb744" />


#### Indicators Identified:
- IP: 185.220.101.55
- Domain: sh4repoint-pkwork[.]xyz
- Recipient: ceo@pkwork.onmicrosoft.com
- Subject: SharePoint: Board meeting documents shared with you
- Attachment: Q4-Board-Meeting-Agenda.docx
- Verdict: Phishing (Confidence: 93)
- Email Authentication: SPF Fail | DKIM None | DMARC Fail
- Delivery Status: Allowed

#### Investigation:
A phishing email was received on 2026‑06‑11 07:17:42 UTC from sharepoint-notify@h4repoint-pkwork[.]xyz, originating from the malicious IP 185.220.101.55 (100% abuse on AbuseIPDB). The message included a typosquatted URL (hxxp[://]sh4repoint-pkwork[.]xyz/download/board-agenda) and a Word attachment (Q4-Board-Meeting-Agenda.docx). Email authentication checks failed (SPF/DMARC failed, DKIM none), yet the email was still delivered despite a phishing threat score of 93. An investigation is ongoing to determine whether the link or attachment was accessed and to assess any potential data exposure.

<img width="501" height="428" alt="image" src="https://github.com/user-attachments/assets/b2b77daa-7009-497a-8ff9-1a268660d5fc" />
<img width="1239" height="647" alt="image" src="https://github.com/user-attachments/assets/92f4a39a-9506-452d-a243-0b2f7fe7a7b9" />

#### Incident Analysis:
- WHO: Malicious sender IP 185.220.101.55 (100% abuse on AbuseIPDB).
- WHAT: Phishing email from sharepoint-notify@sh4repoint-pkwork[.]xyz containing a typosquatted URL and the attachment Q4‑Board‑Meeting‑Agenda.docx.
- WHEN: Sent on 2026‑06‑11 07:17:42 UTC and delivered despite failing email security checks.
- WHERE: Targeted ceo@pkwork.onmicrosoft.com with subject “SharePoint: Board meeting documents shared with you.”  
- WHY: Likely aimed at credential theft or delivering malware to compromise the CEO’s system.
- HOW: Email passed through because the security gateway was likely not configured to block or quarantine such threats.

#### Recommendations:
- Use Threat Intelligence to verify sender IPs/domains; in this case, 185.220.101.55 was confirmed malicious.
- Delete the identified phishing email and configure email security controls to automatically delete or quarantine similar phishing emails in the future.
- Enable domain similarity protection to detect spoofed or look‑alike domains.
- Search the organization for any other emails from 185.220.101.55 or sh4repoint-pkwork.xyz.
- Conduct targeted phishing awareness training focused on identifying Microsoft 365 and SharePoint impersonation emails, recognizing typosquatted domains, verifying unexpected file-sharing requests, avoiding suspicious links and attachments, promptly reporting phishing attempts, and understanding the risks of credential theft, malware, and business email compromise (BEC).

## Project Summary:
By completing this project, I can now:
- Deploy and configure Microsoft Sentinel.
- Connect Microsoft Defender XDR data sources.
- Create custom KQL queries for threat hunting.
- Build Sentinel workbooks and dashboards.
- Create detection rules for security monitoring.
- Investigate phishing incidents using log data and threat intelligence.
- Use bookmarks and incidents to support SOC workflows.

## Most Impactful Learning Experience:
The phishing investigation provided the most realistic SOC experience by combining threat hunting, log analysis, threat intelligence validation, incident creation, and remediation recommendations into a single workflow.
