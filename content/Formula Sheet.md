---
title: 🧮 Exam Formula Sheet
date: 2025-05-24
tags:
  - math
  - logic
  - quick-reference
---

# 📐 Formula & Logic Cheat Sheet

> [!warning] Exam Rule
> Always show your working. If you forget the exact number, write down the formula you are trying to use to get partial marks.

---

## 1. Risk Management (Week 1)

This cheat sheet details the mathematical formulas and strict logical processes for risk assessment and management found in the sources.

| Formula/Steps                                                                                                             | Variable Definitions                                                                                                                         | Worked Example                                                                                                                                                                            |
| :------------------------------------------------------------------------------------------------------------------------ | :------------------------------------------------------------------------------------------------------------------------------------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Risk Associated with Vulnerabilities (Working Definition)**                                                             |                                                                                                                                              |                                                                                                                                                                                           |
| $$\text{risk} = (\text{impact to asset from exploit of vulnerability}) \text{ x } (\text{probability of occurrence})$$    | **Risk:** The possibility to suffer harm or loss.                                                                                            | If the impact (I) of data exposure is rated 5 (High) and the probability (P) of the exploit occurring is rated 3 (Medium): $$\text{Risk} = I \times P$$ $$\text{Risk} = 5 \times 3 = 15$$ |
| **Annualized Loss Expectancy (ALE) Calculation**                                                                          |                                                                                                                                              |                                                                                                                                                                                           |
| $$\text{ALE} = \text{Expected loss} \text{ x } (\text{Number of incidents expected in an average year})$$                 | **ALE:** Annualized Loss Expectancy (the total expected loss over one year).                                                                 | **Scenario:** Calculate ALE for Teller Cash theft.                                                                                                                                        |
|                                                                                                                           | **Expected loss:** The financial amount lost per incident (e.g., $3,240 for Teller Cash).                                                    | **Expected loss:** $3,240                                                                                                                                                                 |
|                                                                                                                           | **Number of incidents expected (Incidence):** The estimated frequency of the event occurring in an average year (e.g., 200 for Teller Cash). | **Incidence:** 200                                                                                                                                                                        |
|                                                                                                                           |                                                                                                                                              | $\text{ALE} = $3,240 \times 200 = $648,000$                                                                                                                                               |
| **Risk Assessment (Strict Logical Process)**                                                                              |                                                                                                                                              |                                                                                                                                                                                           |
| 1. Identify **assets**, **threat agents**, and **threats** to assets,.                                                    | **Asset:** What is being protected (e.g., data, physical items, people),.                                                                    | **1. Identify:** Asset is the sensitive customer database. Threat Agent is an external attacker. Threat is a system breach/data exposure.                                                 |
| 2. Identify **vulnerabilities** that can be exploited,.                                                                   | **Threat Agent:** Who is the attacker (e.g., organized criminals, nation states),.                                                           | **2. Identify:** Vulnerability is the lack of redundancy for the database back-end, which creates a single point of failure,.                                                             |
| 3. **Measure** probability of occurrence and impact (potential loss) of exploits,.                                        | **Vulnerability:** A weakness that can be used to harm us.                                                                                   | **3. Measure:** Probability of failure is moderate. Impact (loss of ability to process payments) is high.                                                                                 |
| **Risk Mitigation (Strict Logical Process)**                                                                              |                                                                                                                                              |                                                                                                                                                                                           |
| 1. Prioritise the risks.                                                                                                  | **Risk:** The possibility of suffering harm or loss.                                                                                         | **1. Prioritise:** The risk of data loss due to database failure is critical (High Priority).                                                                                             |
| 2. Identify countermeasures.                                                                                              | **Countermeasures:** Means (controls) to detect, deter, or deny attacks,.                                                                    | **2. Identify:** Implement physical controls (backup power generators) and logical controls (redundancy for the database),.                                                               |
| 3. Evaluate the countermeasures: How well they reduce risk; how expensive they are; what new risks/trade-offs they bring. | **Trade-offs:** New risks or diminished productivity resulting from implementation,.                                                         | **3. Evaluate:** Redundancy significantly reduces downtime risk but incurs high implementation and maintenance expense.                                                                   |
| 4. Implement countermeasures (and stay within a given budget).                                                            | **Budget:** Financial constraint for implementing security measures.                                                                         | **4. Implement:** Deploy the redundant database back-end and operational procedures to maintain it.                                                                                       |
| **Incident Response (Strict Logical Process)**                                                                            |                                                                                                                                              |                                                                                                                                                                                           |
| The process consists of six phases:                                                                                       | **Preparation:** Activities performed in advance of an incident (e.g., documentation, training).                                             | **Preparation:** Develop an incident response plan for malware infection.                                                                                                                 |
| 1. Preparation.                                                                                                           | **Detection and analysis:** Identifying an issue and determining if it constitutes an incident.                                              | **Detection:** IDS/AV alerts on a malware infection.                                                                                                                                      |
| 2. Detection and analysis.                                                                                                | **Containment:** Taking steps to prevent further damage (e.g., disconnecting a server),.                                                     | **Containment:** Disconnect the infected server from the network.                                                                                                                         |
| 3. Containment.                                                                                                           | **Eradication:** Removing the effects of the issue from the environment (e.g., removing malware).                                            | **Eradication:** Remove the malware and scan other hosts for infection,.                                                                                                                  |
| 4. Eradication.                                                                                                           | **Recovery:** Restoring devices or data to a working state, better than before the incident began.                                           | **Recovery:** Restore the server and data from clean backup media.                                                                                                                        |
| 5. Recovery.                                                                                                              | **Post incident activity:** Determining what happened, why, and how to prevent recurrence (postmortem).                                      | **Post Incident:** Update administrative controls/policies to address the vulnerability used in the attack.                                                                               |

---

## 2. Symmetric Cryptography (Week 3)

|Formula/Steps|Variable Definitions|Worked Example|
|:--|:--|:--|
|**Formal Encryption Scheme Correctness Condition**|||
|$Dec(k, Enc(k, m)) = m$|$Enc$: Encryption algorithm. $Dec$: Decryption algorithm. $k$: A specific key in the key set $K$. $m$: Plaintext message in the set $M$.|None provided in the source for this formal definition.|
|**Shift Cipher (Caesar Cipher)**|||
|$C = P + K \pmod{26}$|$C$: Ciphertext letter (0-25). $P$: Plaintext letter (0-25). $K$: Key (fixed shift amount).|Plaintext $P$ (15) added to key $K=U$ (20) gives 35. $35 \pmod{26} = 9$, which corresponds to ciphertext $J$.|
|**One-Time Pad (OTP) Encryption/Decryption**|||
|Encryption: $Enc_k(m) = k \oplus m$,. Decryption: $Dec_k(c) = k \oplus c$,. Correctness: $Dec_k(Enc_k(m)) = k \oplus (k \oplus m) = m$.|$k$: Truly random key stream. $m$: Plaintext string. $c$: Ciphertext string. $\oplus$: Bitwise XOR operator,.|Plaintext $m$ (binary: $1001000 \ldots$) XORed ($\oplus$) with random key $k$ (binary: $1101011 \ldots$) yields ciphertext $c$ (binary: $0100011 \ldots$).|
|**OTP Key Reuse Vulnerability (Attack)**|||
|$Enc_k(m_0) \oplus Enc_k(m_1) = m_0 \oplus m_1$|$m_0, m_1$: Two distinct plaintexts encrypted with the same key $k$. $Enc_k$: Ciphertext result.|If a key stream is used twice, XORing the two ciphertexts reveals the difference between the plaintexts ($m_0 \oplus m_1$),.|
|**Shannon's Theorem (Key Space Minimum)**|||
|$|K|\geq|
|**Counter (CTR) Mode Keystream Generation**|||
|Keystream blocks $K_i$ are generated by $K_i = E_k(IV + i)$ or $K_i = {IV + i}_K$,. Encryption: $C_i = M_i \oplus K_i$.|$E_k$: Block cipher encryption function under key $k$. $IV$: Initialization Vector (starting counter value). $i$: The counter increment ($1, 2, 3, \ldots$). $M_i, C_i$: Plaintext and ciphertext blocks.|The keystream is generated by encrypting $IV+1, IV+2, IV+3, \ldots$ and then XORing this entire pseudorandom stream with the plaintext blocks.|
|**Cipher-Block Chaining (CBC) Mode**|||
|Encryption: $c_i \leftarrow E_k(m_i \oplus c_{i-1})$. Decryption: $m_i \leftarrow E^{-1}_k(c_i) \oplus c_{i-1}$.|$E_k$: Encryption function under key $k$. $E^{-1}_k$: Decryption function. $m_i$: Current plaintext block. $c_i$: Current ciphertext block. $c_{i-1}$: Previous ciphertext block ($c_0$ is the IV). $\oplus$: XOR operator.|None provided. CBC encryption starts by XORing the first plaintext block ($m_1$) with a random $c_0$ (IV) before encryption.|
|**Merkle-Damgård Iteration (Hash Construction)**|||
|Iteration: $v_i := f(v_{i-1}|m_i)$. Final Hash: $h(m) := v_{k+1}$.|$f$: Compression function ($n+r$ bits $\rightarrow n$ bits). $v_i$: Intermediate hash value ($n$-bits). $v_0$: Initial $n$-bit hash value. $m_i$: Message block ($r$-bits). $k$: Total number of message blocks after padding. $|
|**Birthday Attack Calculation (Hash)**|||
|Expected Collisions $\approx 2^{n/2}$ computations,.|$n$: Length of the hash output in bits (e.g., 128 for MD5 or 160 for SHA-1). $2^{n/2}$: The square root of the total hash space $2^n$.|For a 128-bit hash function (like MD5), finding a collision requires about $2^{64}$ hash computations. For SHA-1 (160 bits), the brute-force maximum effort is $2^{80}$.|
|**Message Authentication Code (HMAC)**|||
|$\text{HMAC}(k,m) = h((k \oplus \text{opad})|h((k \oplus \text{ipad})|m))$,.|
|**DES Feistel Round Function (Inversion)**|||
|Forward (Input $X, Y$, Key $k_i$): Output $W = Y$, $V = X \oplus f(k_i, Y)$. Reverse (Input $W, V$, Key $k_i$): Output $Y = W$, $X = V \oplus f(k_i, W)$.|$X, Y$: Left and right halves of input block. $W, V$: Left and right halves of output block. $f$: Round function. $k_i$: Round key. $\oplus$: XOR operator.|Decryption of the Feistel function requires applying the same round function $f$ in reverse order using the ciphertext half $W$ to recover the plaintext half $X$,.|
|**RSA Asymmetric Cryptography**|||
|Encryption: $C \equiv M^e \pmod{N}$. Decryption: $M \equiv C^d \pmod{N}$. Signature: $\text{Sig}_d(M) \equiv M^d \pmod{N}$.|$M$: Message. $C$: Ciphertext. $N$: Public modulus ($N=pq$). $e$: Public exponent (Encryption key). $d$: Private exponent (Decryption key).|The core mathematical operation relies on finding $d$ such that $de \equiv 1 \pmod{\phi(N)}$, where $\phi(N) = (p-1)(q-1)$.|
|**Discrete Logarithm Problem**|||
|$y = g^x \pmod{p}$|$p$: Large prime number. $g$: Primitive root (generator). $x$: Discrete logarithm (secret exponent). $y$: Public result.|When working modulo 7, using generator $g=5$, $5^3 \equiv 6 \pmod{7}$. The discrete logarithm of 6 is 3.|
|**Diffie-Hellman Shared Secret Generation**|||
|Shared Secret: $K_{AB} = g^{x_A x_B} \pmod{p}$.|$g, p$: Publicly known generator and prime. $x_A, x_B$: Alice's and Bob's secret exponents. $y_A = g^{x_A}$ and $y_B = g^{x_B}$ are the public keys.|Alice computes $y_B^{x_A}$ and Bob computes $y_A^{x_B}$, both resulting in the shared secret $g^{x_A x_B}$.|
|**Shannon's Discrete Entropy Formula**|||
|$H = -K \sum p_i \log p_i$.|$H$: Entropy (measure of choice/uncertainty). $p_i$: Probability of the $i$-th event. $K$: Positive constant (determines unit of measure).|For two possibilities with probabilities $p$ and $q=1-p$, the entropy is $H = -(p \log p + q \log q)$.|
|**Shannon's Noiseless Channel Capacity**|||
|$C = \lim_{T \to \infty} \frac{\log N(T)}{T}$.|$C$: Channel capacity (bits per second). $N(T)$: Number of allowed signals of duration $T$.|For symbols $S_1, \ldots, S_n$ with durations $t_1, \ldots, t_n$, the capacity $C = \log X_0$, where $X_0$ is the largest real solution of the characteristic equation: $X^{-t_1} + X^{-t_2} + \ldots + X^{-t_n} = 1$.|

---

## 3. Asymmetric Cryptography (Week 6)

### I. RSA Cryptosystem

|Category|The Formula/Steps|Variable Definitions|Worked Example: Key Generation & Operations|
|:--|:--|:--|:--|
|**Key Generation: Modulus**|$N = p \cdot q$|**$N$**: RSA modulus,. **$p, q$**: Large, random, distinct primes,,.|**Setup**: 1. Choose large distinct primes $p$ and $q$, compute $N = p \cdot q$. 2. Compute $\phi(N) = (p-1)(q-1)$. 3. Choose $e$ such that $\gcd(e, \phi(N)) = 1$. 4. Compute $d$ such that $ed \equiv 1 \pmod{\phi(N)}$ using the Extended Euclidean Algorithm.|
|**Key Generation: Exponents**|1. $\phi(N) = (p-1)(q-1)$,,,. 2. Choose encryption exponent $e$ such that $\gcd(e, \phi(N)) = 1$,,. 3. Compute decryption exponent $d$ such that $e d \equiv 1 \pmod{\phi(N)}$,,.|**$\phi(N)$**: Euler phi function/Euler totient function, the number of integers prime to $N$. **$e$**: Encryption exponent (Public key component),. **$d$**: Decryption exponent (Private/Secret key component),.|**Factoring $N$ (If $\phi(N)$ is known)**: $p+q = N - \phi(N) + 1$ and $p-q = \sqrt{(p+q)^2 - 4N}$.|
|**Encryption (Textbook RSA)**|$c = m^e \bmod N$,,,.|**$m$**: Plaintext message (must be $m \in Z_N$),. **$c$**: Ciphertext,. **$pk$**: Public key, $(N, e)$.|_The provided sources do not include a complete small-number textbook RSA example showing key generation, encryption, and decryption._|
|**Decryption (Textbook RSA)**|$m = c^d \bmod N$,,,.|**$sk$**: Secret key, $(N, d)$.|**Correctness (Logical Process)**: The inverse property ensures $m^{ed} \equiv m \pmod N$,.|
|**Common-Modulus Attack**|Find $r, s$ such that $r e_1 + s e_2 = 1$. Message recovery: $m = c_1^r \cdot (c_2^{-1})^{-s} \pmod n$.|**$e_1, e_2$**: Encryption exponents of two users sharing the same modulus $N$. **$c_1, c_2$**: Ciphertexts of the same message $m$ encrypted with $e_1, e_2$.|_Steps rely on the Extended Euclidean Algorithm to find $r$ and $s$._|
|**Low-Encryption-Exponent Attack**|Use CRT to compute $m^e \bmod{n_1 n_2 n_3}$ (where $e=3$). If $m^e < n_1 n_2 n_3$, compute $m$ by ordinary $e$-th root (e.g., cube root in Z).|**$n_i$**: Modulus of recipient $i$. **$e$**: Small encryption exponent (e.g., 3).|_This logical process works if the same message $m$ is sent to multiple recipients with relatively prime moduli._|
|**Modular Exponentiation**|Compute $g^k \bmod N$ efficiently using the **Square and Multiply** method,. The complexity is $O(\log k)$ or $O(n)$ if $k$ is an $n$-bit number.|**$g$**: Base. **$k$**: Exponent. **$N$**: Modulus.|**Example step**: $a^{14} = ((a^2 a)^2 a)^2$.|

---

### II. Diffie-Hellman & ElGamal Cryptosystems

|Category|The Formula/Steps|Variable Definitions|Worked Example (Modulo 17)|
|:--|:--|:--|:--|
|**Diffie-Hellman (DH) Key Exchange**|Shared Secret Key: $k_A = (g^b)^a = g^{ba}$ (Alice's computation),. $k_B = (g^a)^b = g^{ab}$ (Bob's computation),.|**$G$**: A group (e.g., multiplication modulo a large prime). **$g$**: A generator of $G$. **$a, b$**: Randomly chosen, secret exponents (Alice's and Bob's private keys, respectively),. **$g^a, g^b$**: Public exchange values.|**Setup**: $G$ is multiplication $\bmod 17$, $g=3$. Alice chooses $a=4$. Bob chooses $b=6$. **Exchange**: Alice sends $g^a = 3^4 \bmod 17 = 13$. Bob sends $g^b = 3^6 \bmod 17 = 15$,. **Shared Key**: $k_A = (15)^4 \bmod 17 = 16$. $k_B = (13)^6 \bmod 17 = 16$. Equal key: $16$.|
|**ElGamal Encryption (Classic)**|Ciphertext $c = (c_1, c_2)$ where: $c_1 = g^a$ and $c_2 = g^{ba} \cdot m$,.|**$G$**: Group. **$g$**: Generator. **$b$**: Bob's private key (secret exponent). **$pk$**: Bob's public key, $g^b$. **$a$**: Alice's randomly chosen secret exponent. **$m$**: Plaintext message. **$g^{ba}$**: Shared secret key derived from DH.|**Setup**: $G$ is multiplication $\bmod 17$, $g=3$. Bob private key $b=6$, Public key $pk=15$. Alice chooses $a=4$. Message $m=5$,. **Encryption**: Compute $g^{ba} = (g^b)^a = 15^4 \bmod 17 = 16$. $c_1 = g^a = 13$. $c_2 = 16 \cdot 5 \bmod 17 = 12$. Ciphertext $c = (13, 12)$.|
|**ElGamal Decryption (Classic)**|Compute shared secret key: $g^{ba} = (c_1)^b = (g^a)^b$,. Recover plaintext: $m = c_2 / g^{ba}$ (division/multiplication by inverse). If working modulo prime $p$, $m = c_1^{p-1-x} c_2 \pmod p$.|**$c_1$**: First component of ciphertext ($g^a$). **$c_2$**: Second component of ciphertext ($g^{ba} \cdot m$). **$b$**: Bob's private key.|**Decryption**: Bob computes $g^{ba} = (13)^6 \bmod 17 = 16$. To find $m$, he divides $c_2=12$ by $16 \pmod{17}$. The resulting plaintext is $m=5$.|
|**ElGamal Signature: Signing**|1. Choose random $k$ such that $\gcd(k, p-1)=1$. 2. $r = g^k \pmod p$. 3. $s = k^{-1}(m - rx) \pmod{(p-1)}$. Signature is $(r, s)$.|**$x$**: Secret key exponent. **$p$**: Prime modulus. **$k$**: Random integer (Ephermeral key).|_A worked example is requested but not provided in the source material for the ElGamal Signature scheme._|
|**ElGamal Signature: Verification**|1. Compute $v = g^m$. 2. Compute $w = y^r r^s$. 3. Accept if $v = w$.|**$y$**: Public key ($g^x$). **$m$**: Message (or hash of message). **$r, s$**: Signature components.|**Proof of Correctness**: $w = y^r r^s = (g^x)^r (g^k)^s = g^{xr} g^{ks} = g^{xr + k(k^{-1}(m-rx))} = g^{xr + m - rx} = g^m = v$ (Exponents are modulo $p-1$).|

---

### III. Digital Signature Algorithm (DSA) & ECDSA

|Category|The Formula/Steps|Variable Definitions|Worked Example: Calculation Steps|
|:--|:--|:--|:--|
|**DSA Signing**|1. Choose random $k$, $1 \le k \le q-1$. 2. $r = (g^k \bmod p) \bmod q$. 3. $s = k^{-1}(m + rx) \bmod q$. Signature is $(r, s)$.|**$p$**: Large prime modulus. **$q$**: Prime divisor of $p-1$ (order of subgroup $G_q$). **$g$**: Element of order $q$ in $Z_p^*$. **$x$**: Secret exponent (key). **$m$**: Message (or hash of message). **$k$**: Random integer.|_A worked example is requested but not provided in the source material for the DSA signing steps._|
|**DSA Verification**|1. Compute $t = s^{-1} \bmod q$. 2. Compute $v = ((g^m y^r)^t \bmod p) \bmod q$. 3. Accept if $v = r$.|**$y$**: Public key ($g^x$). **$r, s$**: Signature components. **$t$**: Multiplicative inverse of $s$ mod $q$.|**Proof of Correctness**: $v = (g^{(m+rx)t} \bmod p) \bmod q$. Since $s = k^{-1}(m+rx) \bmod q$, then $(m+rx)t \equiv k \pmod q$. Thus $g^{(m+rx)t} \equiv g^k \pmod p$ (since $g^q \equiv 1 \bmod p$). Therefore $v = (g^k \bmod p) \bmod q = r$.|
|**ECDSA Signing**|1. Choose random $k$, $1 \le k \le n-1$. 2. Compute $kQ = (x_{kQ}, y_{kQ})$. $r = x_{kQ} \bmod n$. 3. $s = k^{-1}(m + r d_A) \bmod n$. Signature is $(r, s)$.|**$Q$**: Base point on elliptic curve $E(F_q)$ of prime order $n$,. **$d_A$**: Alice's secret key (number). **$m$**: Message element in $Z_n$. **$k$**: Random integer.|_A worked example is requested but not provided in the source material for the ECDSA signing steps._|
|**ECDSA Verification**|1. Compute $v = s^{-1} \bmod n$. 2. Compute $w_1 = m v \bmod n$ and $w_2 = r v \bmod n$. 3. Compute verification point $R = w_1 Q + w_2 P_A$. 4. Accept if $r = x_R \bmod n$ (where $R=(x_R, y_R)$).|**$P_A$**: Alice's public key point ($d_A Q$). **$r, s$**: Signature components. **$n$**: Order of base point $Q$. **$x_R$**: X-coordinate of point $R$.|**Proof of Correctness**: $R = w_1 Q + w_2 P_A$. Substituting definitions gives $R = k Q$. Thus $x_R = x_{kQ}$ and $r = x_R \bmod n$.|
|**ECC Scalar Multiplication**|Compute $x \cdot P$. Method is **Double and Add**.|**$x$**: Scalar (number). **$P$**: Point on the curve.|**Double and Add Recursion**: If $x$ is even: Compute $Q = (x/2) P$. Result is $Q+Q$. If $x$ is odd: Compute $Q = (x-1) P$. Result is $P + Q$.|

---

### IV. Other Relevant Processes & Functions

|Category|The Formula/Steps|Variable Definitions|Notes|
|:--|:--|:--|:--|
|**Euclidean Algorithm (GCD)**|**Input**: $\gcd(a, b)$. 1. while $b \ne 0$ do: $r \leftarrow a \bmod b$. $a \leftarrow b$. $b \leftarrow r$. 2. return $\text{abs}(a)$.|**$a, b$**: Integers. **$r$**: Remainder.|Computes the greatest common divisor. $\gcd(a, b) = \gcd(b, a \bmod b)$.|
|**PKCS#1 V1.5 Encoding**|$x = 00|02|r|
|**OAEP Encryption**|1. Choose random $r$. 2. $x = (m \oplus G(r))|(r \oplus h(m \oplus G(r)))$. 3. $c = f(x)$.|**$m$**: Message ($|
|**OAEP Decryption**|Given $c$. 1. Compute $f^{-1}(c) = a|b$ ($|a|
|**Paillier Encryption (Homomorphic)**|$c = g^m \omega^n$.|**$n$**: RSA modulus ($pq$). **$\omega$**: Random element in $Z_n^_$. **$m$**: Message in $Z_n$. **$g$**: Element of order $n$ in $Z_{n^2}^_$.|**Homomorphic property**: $E_{pk}(m + m', \omega \cdot \omega') = E_{pk}(m, \omega) \cdot E_{pk}(m', \omega')$.|
|**Paillier Decryption**|$L(x) = (x-1)/n$. $m = [L(c^\lambda \bmod n^2)] [L(g^\lambda \bmod n^2)]^{-1}$.|**$\lambda$**: Secret key $\text{lcm}(p-1, q-1)$.|Requires knowledge of the secret key $\lambda$ and prime factors $p, q$ to compute $\lambda$.|
|**Euler Phi Function ($\phi(n)$)**|If $n = \prod_{i=1}^k p_i^{e_i}$ (prime factorization), then $\phi(n) = n \prod_{i=1}^k (1 - 1/p_i)$.|**$n$**: Integer. **$p_i$**: Distinct prime factors.|If $n=pq$ (two primes), $\phi(n) = (p-1)(q-1)$.|

---

### Analogy: Trapdoor Functions

The core mathematical concepts used in public-key cryptography—modular exponentiation (RSA) and discrete exponentiation (DH/ElGamal)—are based on **one-way functions**. These functions are like digital locks: they are easy to compute in one direction, but extremely hard to reverse,.

- **Diffie-Hellman/ElGamal** uses discrete exponentiation, which is a one-way function without a readily available shortcut: $g^x$ is easy to compute, but finding $x$ (the Discrete Logarithm) is hard. This is like mixing paint (easy to mix, hard to unmix).
- **RSA** uses modular exponentiation, which is a **trapdoor one-way function**: $m^e \bmod N$ is easy to compute, but reversing it ($c^d \bmod N$) is hard unless you have the secret key $d$, which acts as the trapdoor,. The knowledge of the prime factors $p$ and $q$ of $N$ (the second one-way function, factoring) creates this trapdoor. This is analogous to a public lock: anyone can close it, but only the person with the private key can open it.

---

## 4. Logical Processes (Non-Math)

### **Digital Signature Verification (Week 7)**
$$\text{Valid if: } \text{Decrypt}_{Pub}(Signature) == \text{Hash}(Message)$$

### **TCP Handshake (Week 2)**
1.  **SYN:** Client $\to$ Server (Seq = $x$)
2.  **SYN-ACK:** Server $\to$ Client (Seq = $y$, Ack = $x+1$)
3.  **ACK:** Client $\to$ Server (Seq = $x+1$, Ack = $y+1$)