
<p align="center">
  <img src="screenshots/Phishing_Email_logo.png" alt="Phishing_Email_logo"/>
</p>

<div align="center">

<table width="100%" border="1" cellpadding="6" cellspacing="0">
  <tr>
    <td align="left" ><b>🎯 Target</b></td>
    <td>Phishing_Email</td>
  </tr>
  <tr>
    <td align="left" ><b>👨‍💻 Author</b></td>
    <td><code>sonyahack1</code></td>
  </tr>
  <tr>
    <td align="left" ><b>📅 Date</b></td>
    <td>25.08.2026</td>
  </tr>
  <tr>
    <td align="left" ><b>📊 Difficulty</b></td>
    <td>Very Easy 🟢</td>
  </tr>
  <tr>
    <td align="left" ><b>📁 Category</b></td>
    <td> SOC / phishing </td>
  </tr>
  <tr>
    <td align="left" ><b>🛠️ Tools</b></td>
    <td> virustotal | curl | sha256sum </td>
  </tr>

</table>

</div>

## Sherlock Scenario

Your email address has been leaked and you receive an email from Paypal in German. Try to analyze the suspicious email.

File location: `C:\Users\LetsDefend\Desktop\Files\PhishingChallenge.zip`
Password: `infected`

## Investigation Flow

- [return path](#return-path)
- [domain name](#domain-name)
- [sha256](#sha-256)
- [virus total](#virus-total)

<h2 align="center"> 📝 Report </h2>

Extract the archive containing the malicious email:

<p align="center">
  <img src="screenshots/unpacking_archive.png" alt="unpacking_archive" />
</p>

<p align="center">
  <img src="screenshots/phish_eml.png" alt="phish_eml" />
</p>

The extracted file contains an email written in German and purporting to originate from PayPal:

<p align="center">
  <img src="screenshots/email.png" alt="email" />
</p>

### return path

`Question`: `What is the return path of the email?`

Examine the email's raw source code:

<p align="center">
  <img src="screenshots/source_code.png" alt="source_code" />
</p>

<p align="center">
  <img src="screenshots/return_path.png" alt="return_path" />
</p>

The following `return path` address is identified in the email headers - `bounce@rjttznyzjjzydnillquh.designclub.uk.com`

### domain name

`Question`: `What is the domain name of the url in this mail?`

Extract the URL associated with the button in the email and save it to a text file for further analysis:

<p align="center">
  <img src="screenshots/button_link.png" alt="button_link" />
</p>

<p align="center">
  <img src="screenshots/domain.png" alt="domain" />
</p>

The extracted URL points to the following domain: `storage.googleapis.com`

`Question`: Is the domain mentioned in the previous question suspicious?

`Answer`: Yes, its use in this context is suspicious. Threat actors may abuse cloud-hosting services to distribute malicious content. A PayPal-themed email directing the recipient to an externally hosted object on this domain is inconsistent with the expected PayPal infrastructure and should be investigated further.

### sha256

`Question`: `What is the body SHA-256 of the domain?`

Use the `sha256sum` utility to calculate the `SHA-256` hash of the extracted email body:

<p align="center">
  <img src="screenshots/sha256.png" alt="sha256" />
</p>

`Answer`: `13945ecc33afee74ac7f72e1d5bb73050894356c4bf63d02a1a53e76830567f5`

### virus total

`Question`: `Is this email a phishing email?`

Submit the complete URL extracted from the email button to `VirusTotal` and review the detection results to determine whether it has been associated with malicious activity:

<p align="center">
  <img src="screenshots/virus_total.png" alt="virus_total" />
</p>

`Answer`: `Yes`