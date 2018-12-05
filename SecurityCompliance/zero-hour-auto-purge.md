---
title: "Zero-hour auto purge - protection against spam and malware"
ms.author: krowley
author: kccross
manager: laurawi
ms.date: 10/23/2018
ms.audience: Admin
ms.topic: article
ms.service: o365-administration
localization_priority: Normal
search.appverid:
- MOE150
- MED150
- MBS150
- MET150
ms.assetid: 96deb75f-64e8-4c10-b570-84c99c674e15
description: "Zero-hour auto purge (ZAP) is an email protection feature that detects messages with spam or malware that have already been delivered to your users' inboxes, and then renders the malicious content harmless. How ZAP does this depends on the type of malicious content detected."
---

# Zero-hour auto purge - protection against spam and malware

## Overview

Zero-hour auto purge (ZAP) is an email protection feature that detects messages with spam or malware that have already been delivered to your users' inboxes, and then renders the malicious content harmless. How ZAP does this depends on the type of malicious content detected.
  
ZAP is available with the default Exchange Online Protection that is included with any Office 365 subscription that contains Exchange Online mailboxes.

ZAP is turned on by default, but the folowing conditions must be met:
  
- **Spam action** is set to **Move message to Junk Email folder**. <br/>You can also create a new spam filter policy that applies only to a set of users if you don't want all mailboxes to be screened by ZAP.

- Users have kept their default junk mail settings, and have not turned off junk email protection. (See [Change the level of protection in the Junk Email Filter](https://support.office.com/article/change-the-level-of-protection-in-the-junk-email-filter-e89c12d8-9d61-4320-8c57-d982c8d52f6b) for details about user options in Outlook.) 
  
## How does ZAP work?

Office 365 updates anti-spam engine and malware signatures in real-time on a daily basis. However, your users might still get malicious messages delivered to their inboxes for a variety of reasons, including if content is weaponized after being delivered to users. ZAP addresses this by continually monitoring updates to the Office 365 spam and malware signatures. ZAP can find and remove previously delivered messages that are already in users' inboxes. 
- For mail that is identified as spam, ZAP moves unread messages to users' Junk mail folder. 
- For newly detected malware, ZAP removes attachments from email messages, regardless of whether the email has been read. 
  
The ZAP action is seamless for the mailbox user; they are not notified if an email message is moved.
  
Allow lists, [mail flow rules](https://go.microsoft.com/fwlink/p/?LinkId=722755), and end user rules or additional filters take precedence over ZAP.
  
## To review or set up a spam filter policy
  
1. Go to [https://protection.office.com](https://protection.office.com) and sign in using your work or school account for Office 365.
2. Under **Threat management**, choose **Anti-spam**.
3. Review the standard settings. 
4. If you want to customize your settings, select the **Custom** tab, and turn on **Custom settings**. Edit your settings and if you want, choose **+ Create a policy** to add a new policy. 
    
## To see if ZAP moved your message

If you want to see if ZAP moved your message, you can use either the [Threat Protection Status report](view-email-security-reports.md#threat-protection-status-report-new) (or [Threat Explorer](use-explorer-in-security-and-compliance.md)).
    
## To disable ZAP
  
If you want to disable phish and spam ZAP for your Office 365 tenant, or a set of users, use the **ZapEnabled** parameter of [Set-HostedContentFilterPolicy](https://go.microsoft.com/fwlink/p/?LinkId=722758), an EOP cmdlet.
    
In the following example, ZAP is disabled for a content filter policy named "Test".
    
```
  Set-HostedContentFilterPolicy -Identity Test -ZapEnabled $false
```
If you want to disable malware ZAP for your Office 365 tenant, or a set of users, use the **ZapEnabled** parameter of [Set-MalwareFilterPolicy](https://docs.microsoft.com/en-us/powershell/module/exchange/antispam-antimalware/set-malwarefilterpolicy?view=exchange-ps).

In the following example, ZAP is disabled for a malware filter policy named "Test".

```
  Set-MalwareFilterPolicy -Identity Test -ZapEnabled $false
```

## FAQ

### What happens if a legitimate message is moved to the junk mail folder?
  
You should follow the normal reporting process for false-positives. The only reason the message would be moved from the inbox to the junk mail folder would be because the service has determined that the message was spam or malicious.
  
### What if I use the Office 365 quarantine instead of the junk mail folder?
  
ZAP doesn't move messages into quarantine from the Inbox at this time.
  
### What If I have a custom mail flow rule (Block/ Allow Rule)?
  
Rules created by admins (mail flow rules) or Block and Allow rules take precedence. Such messages are excluded from the feature criteria.
  
## Related Topics

[Office 365 Email Anti-Spam Protection](anti-spam-protection.md)
  
[Block email spam with the Office 365 spam filter to prevent false negative issues](block-email-spam-to-prevent-false-negatives.md)
  

