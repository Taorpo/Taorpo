# Phishing Analysis – TryHackMe Room

## Overview

Phishing is a form of social engineering where attackers use deceptive emails, calls, or messages to trick people into revealing sensitive information or performing harmful actions. Social engineering is the broader technique of manipulating people to divulge information or take actions that compromise security through communication and psychological pressure.

Phishing campaigns commonly aim to steal credentials, financial data, or to deliver malware by abusing trust, urgency, fear, or curiosity. This room focused on understanding how email works, how phishing emails travel, and how to manually analyze suspicious messages.

***

## Email Address Basics

An email address has three main parts:

- User mailbox (username), which identifies the individual account on the mail server.
- The `@` symbol, which separates the user from the domain.
- Domain, which indicates the mail server handling that account, such as `example.com`.

Example format used in the room: `billy@johndoe.com`.

Understanding the structure helps spot spoofed domains, typosquatting, and other subtle changes that appear legitimate at first glance.

***

## Email Delivery Protocols

Email delivery relies on three core protocols that have different roles.

- **SMTP (Simple Mail Transfer Protocol)** – Used for sending email from a client to a mail server and between mail servers; it handles outgoing messages only.
- **POP3 (Post Office Protocol v3)** – Downloads emails from the server to a single device, often removing them from the server after retrieval, which is good for offline access but poor for multi‑device sync.
- **IMAP (Internet Message Access Protocol)** – Keeps emails on the server and synchronizes changes across multiple clients, making it better when accessing the same mailbox from several devices.

In a typical flow, the sender’s mail client uses SMTP to push the email to their mail server, SMTP relays it to the recipient’s mail server, and then the recipient reads it using IMAP or POP3 from their email client.

***

## POP3 vs IMAP (Room Notes)

From the room notes:

- POP3 usually downloads messages and (by default) deletes them from the server, so emails live primarily on the device that pulled them.
- IMAP keeps messages on the server and syncs state across devices, allowing the same mailbox to be accessed consistently from multiple locations.

This distinction matters when investigating phishing because where messages are stored (server vs device) affects how logs, copies, and artifacts can be collected.

***

## Types of Phishing

The room covered several phishing categories, all under the **social** engineering umbrella.

- Spam / junk phishing – High‑volume generic emails sent to many recipients, often poorly targeted.
- Phishing – General deceptive emails seeking credentials or sensitive information.
- Spear phishing – Highly targeted messages crafted for a specific individual or role, often using personal or organizational details.
- Whaling – Phishing targeting high‑value executives or decision‑makers such as CEOs or CFOs.
- Smishing – Phishing through SMS text messages.
- Vishing – Phishing conducted via voice calls, often pretending to be support, banks, or internal staff.

All of these attacks rely on manipulation, urgency, and trust to bypass technical controls by exploiting people instead.

***

## Business Email Compromise (BEC)

Business Email Compromise is a phishing and social engineering attack where an adversary compromises or impersonates a trusted business email account to perform fraudulent actions. The attacker may gain control of an internal employee’s account or spoof a trusted address, then request wire transfers, change payment details, or ask for sensitive data.

BEC often targets finance, HR, or executives, and uses realistic‑looking conversations or invoices to convince internal staff to approve unauthorized or fraudulent transactions.
***

## How Email Travels (High‑Level)

The room emphasized visualizing the path of an email from sender to recipient:

- The sender composes an email in a client (e.g., Outlook, webmail) and sends it using SMTP to their outgoing mail server.
- That server uses DNS to locate the recipient’s mail server and relays the message via SMTP.
- The recipient’s mail server stores the message until the recipient connects using IMAP or POP3, at which point the email is retrieved and displayed in the client.

Understanding this flow helps pinpoint which servers and logs to inspect when tracking phishing attempts or delivery issues.

***

## Manually Analyzing Suspicious Emails

The room walked through a manual process for analyzing potentially malicious emails, focusing on content and technical indicators.
1. **Header inspection**
- Review “From”, “Reply‑To”, and “Return‑Path” fields to see if the actual sending domain matches the displayed sender.
- Check Received headers for unusual hops, unknown servers, or unexpected sending IPs.

2. **Subject and content review**
- Look for urgency, threats, unexpected attachments, or requests for credentials or money.
- Identify spelling mistakes, odd phrasing, or mismatched branding that may indicate a fake message.

3. **Link and URL analysis**
- Hover over links to see the real destination and compare it to the displayed text and legitimate domain.
- Defang malicious URLs (e.g., `hxxp[:]//example[.]com`) and analyze them in tools like CyberChef or other URL analyzers.

4. **Attachment and encoding checks**
- Treat unexpected attachments as suspicious, especially document files with macros or scripts.
- Use base64 decoding or similar techniques to inspect encoded payloads, ensuring correct syntax and spacing when decoding.

5. **Context verification**
- Confirm requests through out‑of‑band channels (phone, internal chat) when money, credentials, or sensitive data are involved.

These steps slow the attacker’s advantage and help identify subtle indicators of compromise before interacting with any payloads.

***

## Internal Message Format (Email Headers)

The room highlighted that raw emails contain structured header fields that reveal routing and authentication details.

- Key header fields: `From`, `To`, `Subject`, `Date`, `Reply-To`, `Message-ID`, `Received`, and sometimes authentication results like SPF, DKIM, and DMARC.
- Reading the full header allows analysts to see which servers handled the message, whether domains and IPs align with legitimate infrastructure, and whether basic authentication checks passed or failed.

Learning to read headers is essential for distinguishing spoofed messages from legitimate mail and for reconstructing how an attack reached the inbox.

***

## Social Engineering Elements to Watch

When reviewing phishing emails, the non‑technical cues are as important as the protocols.

- Authority: The email appears to be from a boss, executive, or trusted organization demanding quick action.
- Urgency and fear: Threats of account closure, legal issues, or missed opportunities if the recipient does not act immediately.
- Curiosity and reward: Unexpected refunds, prizes, or job offers that seem slightly too good to be true.

Recognizing these patterns helps users resist manipulation even when the technical aspects look convincing.

***

## What I Learned (Room Reflection)

From this TryHackMe room, key takeaways included:

- Understanding what makes up an email address and how small domain changes can signal phishing.
- Learning how email travels from sender to recipient over SMTP, POP3, and IMAP, and why that matters for log analysis.
- Gaining practice viewing and interpreting source code of email headers and bodies to identify spoofing and routing anomalies.
- Recognizing common phishing and BEC techniques, including spear phishing, whaling, smishing, and vishing, and how they exploit human trust.
- Using tools like CyberChef and base64 decoding to safely inspect URLs, payloads, and encoded content.

These concepts build a foundation for more advanced email security work such as incident response, threat hunting, and writing detection rules.

***

## Personal Notes from the Lab

- Need more efficient command‑line directory navigation; double‑check directory structure before running tools.
- When decoding base64 content, use the correct syntax (for example, `base64 -d < file>` on Linux) and ensure spacing is correct so the command interprets input properly.
- Continue practicing manual email analysis in real or simulated inboxes to reinforce pattern recognition and comfort with raw headers.
