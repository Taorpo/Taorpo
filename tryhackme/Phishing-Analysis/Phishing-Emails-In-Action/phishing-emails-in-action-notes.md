# Phishing Emails in Action — Notes

## Overview

Phishing emails are designed to trick recipients into revealing sensitive information or executing malicious actions. Attackers often rely on urgency, deception, and technical tricks to appear legitimate.

---

## Common Phishing Techniques

### 1. Sense of Urgency

* Phishing emails often create **panic or urgency** (e.g., *“Account will be locked”*).
* This pressures users into acting quickly without verifying authenticity.
* Goal: **Harvest credentials or personal data**.

---

### 2. Poor Grammar & Typos

* Many phishing emails contain:

  * Misspellings
  * Awkward sentence structure
  * Inconsistent formatting
* These are common red flags, though some modern phishing emails are well-written.

---

### 3. BCC (Blind Carbon Copy) Abuse

* **BCC** allows a sender to email many recipients without revealing their addresses.
* Often used in phishing campaigns to:

  * Hide mass distribution
  * Appear more personal or targeted

---

### 4. Suspicious Attachments

* Be cautious with unexpected attachments.
* Common malicious file types:

  * `.exe`
  * `.zip`
  * `.docm`
  * `.dot`

#### `.DOT` Files

* A **`.dot` file** is a Microsoft Word template file.
* Can contain **malicious macros**.
* Attackers may use **double file extensions** to hide the real type:

  * Example: `Invoice.pdf.dot`

---

## Malicious Links & URLs

### Warning Signs

* Do **not click links** if you don’t know where they lead.
* Watch out for:

  1. **Spoofed email addresses**
  2. **URL shortening services** (hide the real destination)
  3. **HTML links impersonating trusted brands**

---

### Spoofed & Shortened URLs

* Shortened URLs may redirect to malicious websites.
* Attackers use them to bypass filters and hide intent.
* Always hover over links or inspect them carefully.

---

### Inspecting Email Source Code

* Viewing the **email headers/source** can reveal:

  * The true sender
  * The actual link destination
  * Signs of spoofing or manipulation
* Helps determine the **sender’s intent**.

---

## Pixel Tracking

### What is Pixel Tracking?

* A technique used to monitor email recipients.
* Involves embedding a **tiny, invisible image** in the email.

### How It Works

* When the email is opened:

  * The image loads from a remote server
  * The sender can collect:

    * Email open time
    * Recipient’s IP address
    * Device or email client used

### Why It’s Dangerous

* Confirms that an email address is active.
* Enables further targeted phishing or spam campaigns.

---

## Key Takeaways

* Always verify senders before interacting.
* Avoid clicking unknown links or downloading attachments.
* Inspect URLs and file extensions carefully.
* Phishing relies on **human error**—slow down and analyze.

