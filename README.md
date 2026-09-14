# ILEAPP Stored XSS


```
# Exploit Title: iLEAPP Stored XSS in SMS/iMessage Chat HTML Report
# Date: 2026-09-14
# Exploit Author: Chokri Hammedi
# Software: https://github.com/abrignoni/iLEAPP
# Vendor: https://github.com/abrignoni
# Version: v2026.4.0
# Tested on: Linux
# Vulnerability Type: Stored Cross-Site Scripting
# CWE: CWE-79



## Description

iLEAPP is vulnerable to stored Cross-Site Scripting in the generated SMS/iMessage chat HTML report.

When iLEAPP parses an iPhone backup containing an SMS or iMessage with HTML/JavaScript content, the message body is rendered into the generated chat report without proper output encoding.
As a result, attacker-controlled JavaScript executes when the examiner opens the generated HTML report in a browser.

This issue affects the SMS/iMessage chat rendering path, where evidence-derived message content is passed into the chat report and rendered as HTML instead of inert text.


## Proof of Concept

Send or store the following SMS/iMessage payload on an iPhone:

<img src=x onerror=alert('iLEAPP_SMS_XSS_POC_2026_09_14')>

Then create an iPhone backup containing the message and process it with iLEAPP.



1. Send the payload as an SMS/iMessage to the test iPhone.
2. Create an iPhone backup.
3. Open iLEAPP GUI or CLI.
4. Select the iPhone backup as input.
5. Run the SMS/iMessage artifact.
6. Open the generated HTML report.
7. Navigate to the SMS/iMessage chat report.



## Observed Result

The JavaScript payload executes when the generated SMS/iMessage chat report is opened.


## Impact

An attacker who can place a crafted SMS/iMessage on a device later processed by iLEAPP can execute JavaScript in the forensic examiner’s browser when the report is viewed.

Potential impact includes:

- Report content manipulation
- Evidence hiding or visual tampering
- Reading data available in the report DOM
- Triggering browser requests to external infrastructure
- Social engineering against the examiner through trusted forensic output


## Root Cause

Untrusted evidence-derived SMS/iMessage content is inserted into the generated HTML chat report without proper escaping or safe DOM insertion.

Message content should be treated as text, not HTML.
```
<img width="1188" height="935" alt="image" src="https://github.com/user-attachments/assets/7b464d8d-f9bb-4bd6-8260-4eae2140a96f" />
