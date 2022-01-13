# Phishing

*"Adversaries may send phishing messages to gain access to victim systems. Nearly all forms of phishing are some form of electronically delivered social engineering message. Phishing can be targeted, known as spearphishing. In spearphishing, a specific individual, company, or industry will be targeted by the adversary. More generally, adversaries can conduct non-targeted phishing, such as in mass malware spam campaigns.*

*Adversaries may send victims emails containing malicious attachments or links, typically to execute malicious code on victim systems. Phishing may also be conducted via third-party services, like social media platforms. Phishing may also involve social engineering techniques, such as posing as a trusted source."* - MITRE ATT&CK Framework

## Signs
- Misspellings
- Grammar Errors
- Call to action
- Sense of urgency
- Fear
- Authority
- Danger
- Social appeal
- Unknown sender making requests
- Links that don't match email domains or contain a ton of extra text in the URL
- Reply to emails that don't match the sender (or the domain)
- Too good to be true

## Source
An email's source will inform a lot of the hidden information within the email.
### Headers
Emails contain a list of "headers" that correspond with information about the email, its paths, various authentication checks, and so on. Some of the headers determine how the email is displayed or are otherwise rendered for the end-user, and others are used only by email systems. 