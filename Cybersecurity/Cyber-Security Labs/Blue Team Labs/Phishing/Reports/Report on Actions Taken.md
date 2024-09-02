

In this example, the investigation analyst encountered a DHL credential harvesting attempt, which was received by 23 employees. After investigating the email, the analyst recovered the following artifacts:

- **Sender:** contact@dhl.com
- **Server Sending IP:** 209.85.167.42
- **Reverse DNS:** mail-lf1-f42.google.com
- **Subject:** “DHL Delivery Failed RESPONSE NOW — URGENT!!”
- **URL:** hxxps://dhl-faileddelivery.shanepppalkkbc.com _(Example value)_

The sender address was successfully spoofed as contact@dhl.com; however, the sending IP revealed it was actually a Gmail address, and therefore not from DHL. `**[2]**` We cannot block the server’s sending IP since it belongs to Gmail, and doing so would negatively impact the company by blocking legitimate emails. `**[3]**` Blocking the sender “contact@dhl.com” is also not appropriate since legitimate emails from this address would be blocked. `**[4]**` I blocked the subject line in the email gateway since it is highly unlikely that legitimate DHL emails would use it. `**[5]**` This action would have no negative impact on the business and would prevent more emails from this attack from being delivered to employees' inboxes.

- `**[6]**` Subject line block (email gateway) “DHL Delivery Failed RESPONSE NOW — URGENT!!” on December 22 at 12:03 PM by Jane Smith.

`**[7]**` The URL used in the credential harvester is a malicious domain “shanepppalkbc[.]com” that uses a subdomain “dhl-faileddelivery” to appear more legitimate when reading the link. `**[8]**` After investigating the domain, it was found to be created purely for malicious purposes, and there is no business justification for employees to visit it. We can block the entire domain to prevent users from accessing the malicious link, or any others hosted on the site.

- `**[9]**` Domain Block (Web Proxy) “shanepppalkbc[.]com” on December 22 at 12:07 PM by Jane Smith.