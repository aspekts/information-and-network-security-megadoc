---
title: Mock Paper C
date: 2025-05-24
tags:
  - exam
  - practice
  - risk
  - crypto
  - sql
---

# 📝 Mock Examination C

> [!info] Instructions
> * **Time:** 2 Hours
> * **Questions:** Answer ALL questions.
> * **Self-Correction:** Click the "Reveal Answer" dropdowns to check your marking scheme.

---

## Question 1: Risk Management (Week 1)

**(a) Multiple Choice**
Which statement accurately describes the relationship between an Asset, a Threat, and a Vulnerability? [3 marks]
* A. An Asset is any control used to reduce risk, a Threat is the cost of implementing that control, and a Vulnerability is the resulting risk reduction.
* B. A Threat is the specific security mechanism used to protect data, and a Vulnerability is the system specification that defines acceptable behavior.
* C. A Threat is the potential cause of an unwanted event that may harm assets, and a Vulnerability is a characteristic of a system that can be exploited by that threat.
* D. An Asset is the possibility of suffering harm or loss, and Risk is what we must know to assess a system's security.

<details>
<summary>🔻 Click to reveal answer</summary>

**Correct Answer: C**

**Reasoning:**
* **Threat:** Potential cause of an unwanted event.
* **Vulnerability:** A weakness or characteristic that can be exploited.
* **Risk:** Occurs only when a Threat coincides with a Vulnerability.
</details>

**(b) ALE Calculation**
Calculate the **Annualized Loss Expectancy (ALE)** for the loss type "Teller cash" given the following data:
* **Expected Loss (per incident):** $3,240
* **Incidence (ARO):** 200 incidents per year.

Show the formula used and the final value. [5 marks]

<details>
<summary>🔻 Click to reveal answer</summary>

**Formula:**
$$\text{ALE} = \text{SLE} \times \text{ARO}$$
*(Single Loss Expectancy × Annualized Rate of Occurrence)*

**Calculation:**
$$\text{ALE} = 3,240 \times 200$$

**Final Answer:**
**$648,000**
</details>

**(c) Scenario Analysis**
A software company hosts its primary repository on an unsecured legacy server (high vulnerability). The threat of corporate espionage is high. A breach would be catastrophic. Replacing the server is expensive.
**Decision:** Should they Accept, Avoid, Mitigate, or Transfer? Justify your answer. [6 marks]

<details>
<summary>🔻 Click to reveal answer</summary>

**Strategy: Mitigate**

**Justification:**
1.  **Why not Accept?** The impact is catastrophic; accepting effectively means willing to go out of business.
2.  **Why not Transfer?** Insurance covers money, but cannot replace lost proprietary source code or reputation.
3.  **Why Mitigate?** Even though the cost is high, the cost of the loss is greater. Implementing controls (firewalls, encryption) or upgrading the OS directly reduces the *vulnerability*, which is the only variable the company can control.
</details>

---

## Question 2: Cryptography (Weeks 3 & 6)

**(a) Modular Arithmetic**
Calculate $7^{13} \pmod{11}$. Show your working using Fermat's Little Theorem or the square-and-multiply method. [8 marks]

<details>
<summary>🔻 Click to reveal answer</summary>

**Step 1: Simplify Exponent (Fermat's Little Theorem)**
* Since $p=11$ is prime, $a^{p-1} \equiv 1 \pmod p$.
* $7^{10} \equiv 1 \pmod{11}$.
* Therefore, $7^{13} = 7^{10} \times 7^3 \equiv 1 \times 7^3 \pmod{11}$.

**Step 2: Calculate Remainder**
* We need $7^3 \pmod{11}$.
* $7^2 = 49$.
* $49 \pmod{11} = 5$ (since $4 \times 11 = 44$).
* $7^3 \equiv 5 \times 7 = 35$.
* $35 \pmod{11} = 2$ (since $3 \times 11 = 33$).

**Final Answer: 2**
</details>

**(b) RSA Key Generation**
Given primes $p=3$ and $q=11$, and public exponent $e=3$:
1.  Calculate the Modulus ($N$).
2.  Calculate Euler's Totient $\phi(N)$.
3.  Calculate the Private Key ($d$). [8 marks]

<details>
<summary>🔻 Click to reveal answer</summary>

**1. Modulus (N)**
$$N = p \times q = 3 \times 11 = 33$$

**2. Totient $\phi(N)$**
$$\phi(N) = (p-1)(q-1) = 2 \times 10 = 20$$

**3. Private Key (d)**
We need $d$ such that $d \times e \equiv 1 \pmod{20}$.
* Equation: $3d = 1 + 20k$
* If $k=1$, $3d = 21$.
* $d = 7$.

**Check:** $7 \times 3 = 21$, which is $1 \pmod{20}$.
**Answer: d=7**
</details>

---

## Question 3: Web Security (Week 5)

**(a) Vulnerability Identification**
Review the code:
```php
$query = "SELECT userid FROM users WHERE username = '$username' AND password = '$password'";
```
1. Identify the vulnerability.
    
2. Explain the effect of the input: `' OR '1'='1`. [6 marks]
    

<details> <summary>🔻 Click to reveal answer</summary>

**1. Vulnerability:** **SQL Injection (SQLi)**. The code concatenates user input directly into the query string.

**2. Exploitation:**

- The `'` closes the password field.
    
- `OR '1'='1'` adds a condition that is **always true**.
    
- The query becomes `SELECT ... WHERE ... password = '' OR '1'='1'`.
    
- **Result:** The database returns all rows (bypassing authentication) because the logic evaluates to TRUE.
    

</details>

**(b) Remediation** Rewrite the PHP code above to fix the vulnerability using the industry standard defense. [6 marks]

<details> <summary>🔻 Click to reveal answer</summary>

**Defense: Prepared Statements (Parameterized Queries)**

**Corrected Code:**

PHP

```
// 1. Prepare template with placeholders (?)
$stmt = $pdo->prepare("SELECT userid FROM users WHERE username = ? AND password = ?");

// 2. Execute sending data separately
$stmt->execute([$username, $password]);
```

_Note: Input validation is a secondary defense; Prepared Statements are the primary fix._

</details>