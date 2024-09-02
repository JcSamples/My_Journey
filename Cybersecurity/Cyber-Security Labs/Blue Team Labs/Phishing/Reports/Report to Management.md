In this example, a malicious email was reported to the security team by the payroll department. The email claimed to be from the UK government and instructed the recipient to review the attached tax announcement. After analyzing the attachment, it was found to be [Emotet malware](https://www.malwarebytes.com/emotet/), which infected two machines before being contained by the incident response team. The email body also included a URL that connects to a domain and downloads the same file attached to the email. The investigation analyst retrieved the following IOCs:

- **Sender:** HMRC-0fficial@govpayments.net
- **Server Sending IP:** 129.33.19.188 _(Example value)_
- **Reverse DNS:** mail-govpayments.net _(Example value)_
- **Subject:** HMRC 2020 Tax Announcement IMPORTANT
- **URL:** hxxp://hmrc.adverticementgov.com/1jfa/download.php? _(Example value)_
- **Attachment Name:** HMRC-Tax-Announcement-Readme.pdf.exe
- **File MD5 Hash:** 0a52730597fb4ffa01fc117d9e71e3a9 _(Example value)_

The sender address comes from the domain @govpayments.net, which is not a legitimate site used by the UK government or HMRC. `**[2]**` While we can block the sending domain because it is impersonating a legitimate government-owned domain, we have only received emails from one sending mailbox, and blocking the domain at this time may be excessive. `**[3]**` Blocking the sender “HMRC-0fficial@govpayments.net” would prevent more malicious emails from being sent by this sender. `**[4]**` There would be no negative impact on the business by blocking this malicious sending address.

- `**[5]**` Sender address block (email gateway) “HMRC-0fficial@govpayments.net” on March 1 at 3:37 PM by Chris C.

`**[6]**` The URL used in the email is used to download the same Emotet payload as the attachment. `**[7]**` After investigating the domain, it was found to be created purely for malicious purposes, and there is no business justification for employees to visit it. We can block the entire domain to prevent users from visiting the malicious link, or any others hosted on the site.

- `**[8]**` Domain Block (Web Proxy) “hmrc.adverticementgov.com” on March 1 at 3:41 PM by Chris C.