---
title: Mock Paper B
date: 2025-12-17
tags:
  - exam
  - practice
  - mock
---

# 📝 Mock Examination B

---

## Question 1: Authentication
**(a)** Compare **Hashing** vs. **Encryption**.
1.  Which one is reversible?
2.  Which one is used for storing passwords?
3.  Which one is used for ensuring data confidentiality during transit? [5 marks]

**(b)** Explain the **"Downgrade Dance"** in the context of the **POODLE** attack on SSL v3.0. How does an attacker force a modern browser to use an insecure protocol? [5 marks]

**(c)** In a **Phishing** attack, list three common "Indicators of Compromise" (red flags) that a user might spot in a malicious email. [5 marks]

---

## Question 2: Public Key Infrastructure (PKI)
**(a)** Alice wants to digitally sign a document to prove it came from her.
1.  Which key does she use to **sign** the hash?
2.  Which key does Bob use to **verify** the signature?
3.  If Bob successfully verifies the signature, what two security properties have been achieved? (e.g., Confidentiality, Integrity, Non-repudiation). [6 marks]

**(b)** A Root Certificate Authority (CA) is compromised.
1.  What is the impact on the "Chain of Trust" for all certificates signed by this CA?
2.  What mechanism (acronym: CRL or OCSP) allows browsers to reject these now-invalid certificates? [4 marks]

**(c)** **RSA Calculation:**
Given $p=3$ and $q=5$.
1.  Calculate the modulus $n$.
2.  Calculate Euler's Totient $\phi(n)$.
3.  If we choose public exponent $e=3$, find the private exponent $d$ such that $d \times e \equiv 1 \pmod{\phi(n)}$. [10 marks]

---

## Question 3: Network Security
**(a)** Analyze the diagram below (Text Description):
* **Zone A:** Contains the Database Server and Employee Workstations.
* **Zone B:** Contains the Public Web Server and Email Relay.
* **Zone C:** The Internet.
1.  Which Zone represents the **DMZ**?
2.  Where should the Firewalls be placed? (Between which zones?)
3.  If the Web Server in Zone B is compromised, what prevents the attacker from immediately accessing the Database in Zone A? [8 marks]

**(b)** Compare **IDS** (Intrusion Detection System) and **IPS** (Intrusion Prevention System).
* Which one is "Passive" and which is "Active"?
* Which one introduces a risk of blocking legitimate traffic (False Positives) that causes a denial of service? [7 marks]

---

## Question 4: Attacks & Defense
**(a)** A user is logged into their banking website. They open a new tab and visit a malicious site which contains a hidden form that submits a "Transfer Money" request to the bank.
1.  Name this attack.
2.  Explain why the bank accepts the request (Hint: Cookies).
3.  What specific token can the bank implement to prevent this? [8 marks]

**(b)** Block Cipher Modes:
1.  Why is **ECB (Electronic Codebook)** mode considered insecure for encrypting images or large files?
2.  What is the purpose of the **IV (Initialization Vector)** in CBC mode? [7 marks]