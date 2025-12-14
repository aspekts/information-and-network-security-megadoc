---
title: Security Exam Dashboard
date: 2025-05-24
tags:
  - exam
  - dashboard
  - security
---

# 🛡️ Information & Network Security

> [!important] Exam Strategy
> **Goal:** Quick retrieval. Use **Cmd+K** (or Ctrl+K) to search for keywords immediately.
> **Key Resources:** [[Master Definitions Table]] | [[Formula Sheet]] | [[Acronym Buster]]

---

## 📅 Weekly Modules

### **Foundations**
* [[Week 01 - Risk Management]]
    * *Topics:* CIA Triad, OWASP Risk Rating, Risk Treatment (Accept, Transfer, Mitigate).
* [[Week 02 - Sockets & Networking]]
    * *Topics:* TCP Handshake, Secure vs. Standard Sockets, Client-Server code logic.

### **Cryptography (The Core)**
* [[Week 03 - Symmetric Cryptography]]
    * *Topics:* Stream vs. Block, Perfect Secrecy, OTP, Hash vs. MAC, Modes of Operation (ECB/CBC).
* [[Week 06 - Public Key Cryptography]]
    * *Topics:* RSA, Diffie-Hellman, Trapdoor Functions, Hybrid Encryption.
* [[Week 07 - PKI & Digital Signatures]]
    * *Topics:* Certificate Authorities, Chain of Trust, Non-repudiation.

### **System & Web Security**
* [[Week 04 - Authentication & Human Factors]]
    * *Topics:* Passwords, Phishing, Salting/Hashing.
* [[Week 05 - Web Vulnerabilities]]
    * *Topics:* SQL Injection (SQLi), XSS, CSRF, Input Validation.

### **Network Defense & Protocols**
* [[Week 08 - Security Protocols]]
    * *Topics:* SSL/TLS Handshake, POODLE Attack, Kerberos.
* [[Week 09 - Network Defense]]
    * *Topics:* Firewalls (Packet filtering), IDS vs. IPS, DMZ Architecture.

---

## 🧠 Quick Reference Tables

| Concept | vs. | Concept | Key Difference |
| :--- | :---: | :--- | :--- |
| **Stream Cipher** | vs | **Block Cipher** | Bit-by-bit (Fast) vs. Chunk-by-chunk (Storage). |
| **Hash** | vs | **MAC** | Integrity only vs. Integrity + Sender Auth. |
| **Symmetric** | vs | **Asymmetric** | Shared Key (Speed) vs. Public/Private Pair (Key Exchange). |
| **IDS** | vs | **IPS** | Passive Alerting vs. Active Blocking. |

> [!tip] Common Ports
> * **HTTP:** 80
> * **HTTPS:** 443
> * **SSH:** 22
> * **DNS:** 53

---

## 🗺️ Topic Map
* #cryptography
* #network-security
* #web-security
* #risk-management