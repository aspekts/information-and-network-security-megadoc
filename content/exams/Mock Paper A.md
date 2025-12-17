---
title: Mock Paper A
date: 2025-12-17
tags:
  - exam
  - practice
  - mock
---

# 📝 Mock Examination A

> [!info] Instructions
> * **Time:** 2 Hours
> * **Questions:** Answer ALL FOUR questions.
> * **Marks:** All questions carry equal marks.

---

## Question 1: Foundations & Risk
**(a)** A web-server hosting a critical e-commerce database has an estimated value of £500,000. A specific SQL Injection vulnerability has an Exposure Factor (EF) of 100% (total data loss). The Annualized Rate of Occurrence (ARO) is estimated to be 0.1 (once every 10 years).
1.  Calculate the **Single Loss Expectancy (SLE)**.
2.  Calculate the **Annualized Loss Expectancy (ALE)**.
3.  If a Web Application Firewall (WAF) costs £20,000 per year to license and maintain, is it cost-effective to implement? [6 marks]

**(b)** Which of the following statements about **Salted Hashes** are true? (Tick all that apply) [4 marks]
- [ ] Salting prevents Rainbow Table attacks.
- [ ] Salting encrypts the password using a public key.
- [ ] Salting makes the password hash collision-resistant.
- [ ] Salting ensures that two users with the same password have different hashes.

**(c)** Explain **Kerckhoffs's Principle**. Why is "Security through Obscurity" considered a bad practice in modern network design? [5 marks]

---

## Question 2: Cryptography
**(a)** You are establishing a Diffie-Hellman key exchange with a partner.
* **Public Parameters:** Prime $p = 23$, Generator $g = 5$.
* **Alice's Private Key:** $a = 6$.
* **Bob's Private Key:** $b = 15$.
1.  Calculate the public value Alice sends to Bob ($A$).
2.  Calculate the Shared Secret ($s$). Show your working. [8 marks]

**(b)** The ciphertext `01011` was encrypted using a **One-Time Pad (OTP)** with the key `11001`.
1.  Recover the plaintext.
2.  Explain why the One-Time Pad is considered to have "Perfect Secrecy" but is impractical for internet traffic. [7 marks]

---

## Question 3: Web Vulnerabilities
**(a)** Consider the following PHP code snippet:
```php
$user = $_GET['username'];
$query = "SELECT * FROM accounts WHERE name = '" . $user . "'";
$db->execute($query);
```
1. Identify the vulnerability.
    
2. Provide a specific input string that an attacker could use to log in without a password (authentication bypass).
    
3. Rewrite the code to fix the vulnerability using a **Prepared Statement**. [9 marks]
    

**(b)** Explain the mechanism of a **Reflected XSS** attack. How does it differ from **Stored XSS** in terms of where the malicious script is saved? [6 marks]

## Question 4: Protocols & Network Defense

**(a)** During an **SSL/TLS Handshake**, the client and server must agree on a "Cipher Suite".

1. Break down the following cipher suite string into its 4 components: `TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256`
    
    - Key Exchange: ?
        
    - Authentication: ?
        
    - Encryption (Cipher): ?
        
    - Integrity (MAC): ?
        
2. Why is **ECDHE** preferred over standard **RSA** for the key exchange? (Hint: Forward Secrecy). [8 marks]
    

**(b)** You are configuring a firewall for a corporate network.

1. What is the difference between a **Packet Filtering Firewall** and a **Stateful Inspection Firewall**?
    
2. Write a rule set (Source, Dest, Port, Action) to allow public web traffic into a Web Server (IP: 10.0.0.5) but block all other access to it. [7 marks]