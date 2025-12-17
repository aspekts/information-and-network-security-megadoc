---
title: Mock Paper E
date: 2025-05-24
tags:
  - exam
  - official
  - quiz
---

# 🎓 Official Revision Quiz (High Accuracy)

> [!warning] Source Material
> This content is derived directly from the module lead's revision quiz. **High probability of exam appearance.**

## Part 1: Definitions & Concepts

**(Q15) Cybersecurity vs. InfoSec**
What is the difference?
<details><summary>Reveal</summary>
**D:** Cybersecurity focuses on protecting information *systems* (digital), while Information Security covers information in general (digital, physical, paper).
</details>

**(Q26) Hidden Messages**
Hiding a secret message within another message (like an image) is called:
<details><summary>Reveal</summary>
**Steganography** (Distinct from Cryptography, which hides the *meaning*, not the existence).
</details>

**(Q33) Weak Hashing**
How do you make password hashing insecure? (Select all)
<details><summary>Reveal</summary>
* [x] Using a **small salt** (Rainbow tables become feasible).
* [x] Using an **efficient** (fast) hash function (Brute force becomes too easy).
* *Note:* You WANT a "Slow" hash (like bcrypt/Argon2) and a "Large" salt.
</details>

---

## Part 2: Cryptography Implementation

**(Q7) Authenticated Encryption**
What is the strongest approach for ensuring confidentiality and integrity?
<details><summary>Reveal</summary>
**Encrypt-then-MAC** (Encrypt the data first, then generate a MAC of the ciphertext).
</details>

**(Q28) RSA Vulnerability**
Can an adversary efficiently determine which of two messages corresponds to a ciphertext if **Textbook RSA** (no padding) is used?
<details><summary>Reveal</summary>
**Yes.** Because Textbook RSA is **deterministic**. The attacker encrypts both potential messages with the public key and checks which one matches the ciphertext.
*Fix:* Use **OAEP Padding**.
</details>

**(Q14) CTR Mode Properties**
Which of these is **TRUE** about CTR mode?
<details><summary>Reveal</summary>
* [x] Encryption **can** be parallelized.
* [x] Decryption **can** be parallelized.
* [x] Errors in one block **do not** propagate to others (only the specific bit is corrupted).
</details>

---

## Part 3: Network & Protocols

**(Q10) Java Sockets**
Securing a socket with TLS requires creating a **KeyStore** (for own keys) and a **TrustStore** (for trusted CA certs).

**(Q5) Remote Access Security**
Which is the **least** secure method listed?
<details><summary>Reveal</summary>

**C:**  Graphical remote access using a legacy **VNC server** (Often unencrypted passwords).
*Comparison:* SSH and VPN-tunneled RDP provide encryption.

</details>

**(Q22) Stateful Firewall**
What defines a stateful firewall?
<details><summary>Reveal</summary>
**C:** It can track the state of active connections (e.g., "This packet belongs to an established TCP stream").
</details>