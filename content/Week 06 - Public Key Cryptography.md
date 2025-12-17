---
title: Week 06 - Public Key Cryptography
date: 2025-12-14
tags:
  - cryptography
  - asymmetric
  - math
  - key-exchange
aliases:
  - RSA
  - Diffie-Hellman
  - Trapdoor Functions
summary: Asymmetric encryption concepts relying on mathematical hard problems like Integer Factorization.
---

## Key Terms
| Term                                                   | Definition                                                                                                                                                                                                                                                                               | Exam Context/Example                                                                                                                                                                                                     |
| :----------------------------------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Public Key Cryptography** (Asymmetric encryption)    | A cryptographic system where each person's key is separated into a **public key (for encryption)**, available to everyone, and a **secret key (for decryption)**, which is kept private by the owner. This allows for secure communication and key exchange without pre-sharing secrets. | Used for secure access to websites or online shopping where pre-exchanging keys is infeasible.                                                                                                                           |
| **Symmetric Key Encryption**                           | A cryptographic system where **one key is used for both encryption and decryption**. Parties must agree on a common secret key beforehand.                                                                                                                                               | Used to guarantee confidentiality and integrity after a secure channel (e.g., established by public-key methods) is set up. Symmetric-key encryption is **more efficient** than public-key encryption for long messages. |
| **Public Key ($pk$)**                                  | The key in an asymmetric system that is **distributed publicly** and is **used to encrypt messages** intended for the owner.                                                                                                                                                             | In RSA, the public key is $(N, e)$. In ElGamal, $pk := g^b$.                                                                                                                                                             |
| **Private Key** (Secret Key, $sk$)                     | The key in an asymmetric system that **must be kept secret** and is **used to decrypt ciphertexts**.                                                                                                                                                                                     | In RSA, the private key is $(N, d)$. In ElGamal, $sk := b$.                                                                                                                                                              |
| **One-way Functions**                                  | Functions that are **easy to compute, but hard to invert**. Computation is efficient, but finding the pre-image is practically infeasible.                                                                                                                                               | Examples include pre-image resistant hash functions, multiplication of two large prime numbers (factoring), and Discrete Exponentiation.                                                                                 |
| **Trapdoor Functions**                                 | **One-way functions that possess trapdoor information**. The inverse is easy to compute only if specific secret information (the trapdoor) is known.                                                                                                                                     | The RSA function $x \mapsto x^e$ is a trapdoor function, where the trapdoor information is the decryption exponent $d$ (derived from the prime factors $p$ and $q$).                                                     |
| **Discrete Exponentiation**                            | The operation $Exp: Z_{p-1} \to Z_p^*, x \mapsto g^x$. It is a function that is **efficiently computable**.                                                                                                                                                                              | Calculating $g^x \mod N$ can be done efficiently using the Square and Multiply algorithm in $O(\log k)$ steps (where $k$ is the exponent).                                                                               |
| **Discrete Logarithm Function**                        | The **inverse function of discrete exponentiation** ($Log: Z_p^* \to Z_{p-1}$). It is **(believed to be) hard** to compute efficiently for sufficiently large primes.                                                                                                                    | Inverting the equation $2^x \mod 11 = 5$ to find $x$ is an example of computing a discrete logarithm. The hardness of this operation is the basis for ElGamal encryption.                                                |
| **Diffie-Hellman Key Exchange**                        | A **public-key method for key agreement** (exchange) that allows two parties (Alice and Bob) to **establish a fresh, shared secret key**. They compute $k_A = (g^b)^a$ and $k_B = (g^a)^b$, resulting in an equal key, $g^{ab}$.                                                         | The key exchange is analogous to mixing colors, where mixing is easy but separating the mixed color is hard. Eve knows $G, g, g^a, g^b$ but must compute $g^{ab}$.                                                       |
| **RSA Cryptosystem**                                   | A widely used public-key cryptosystem (Rivest, Shamir, Adleman) based on the **difficulty of factoring large composite numbers**. It provides encryption and digital signatures.                                                                                                         | Key generation involves choosing large primes $p$ and $q$, computing $N=pq$ (the modulus), and calculating related exponents $e$ and $d$.                                                                                |
| **RSA Modulus ($N$)**                                  | Calculated as **$N = pq$, where $p$ and $q$ are large random primes** of approximately equal size.                                                                                                                                                                                       | The security of RSA depends on the difficulty of finding the factors $p$ and $q$ from the public modulus $N$.                                                                                                            |
| **Textbook RSA**                                       | The basic definition of the RSA scheme, where encryption is $c = m^e \mod N$ and decryption is $m = c^d \mod N$.                                                                                                                                                                         | Textbook RSA is **deterministic** (encrypting the same message twice yields the same ciphertext) and is **not CPA-secure**.                                                                                              |
| **CPA-secure** (Chosen-plaintext attack secure)        | An encryption scheme is CPA-secure if an adversary **cannot do better than random guessing** to win the chosen-plaintext attack game.                                                                                                                                                    | **No deterministic encryption scheme is CPA-secure**. Encryption must be randomized, typically by using encoding schemes like OAEP.                                                                                      |
| **Hybrid Encryption**                                  | A method to encrypt long messages by **combining public-key encryption with symmetric-key encryption**.                                                                                                                                                                                  | The public-key scheme (e.g., RSA) is used to **encrypt the symmetric key ($k$)**, and the symmetric-key scheme (e.g., AES) is used to **encrypt the message ($m$)** using $k$.                                           |
| **Optimal Asymmetric Encryption Padding (OAEP)**       | A **more secure encoding** scheme used in RSA encryption. OAEP randomizes the plaintext before encryption.                                                                                                                                                                               | Using OAEP prevents attacks like Bleichenbacher’s 1-Million-Chosen-Ciphertext Attack and prevents the low encryption exponent attack.                                                                                    |
| **Digital Signature**                                  | The digital counterpart of a handwritten signature. The signature must depend on the message and a secret known only to the signer, and it must be **verifiable by an unbiased third party** using the signer's public key.                                                              | In basic RSA signing, Alice computes the signature $\sigma = m^d \mod N$ using her secret key $d$, and Bob verifies it by checking if $\sigma^e = m \mod N$.                                                             |
| **Hash-then-decrypt paradigm**                         | A method for digital signatures where a **collision resistant hash function ($h$) is first applied to the message** ($m$), and then the hash value $h(m)$ is signed instead of the original message.                                                                                     | Alice’s RSA signature is $\sigma = h(m)^d \mod N$. Bob verifies if $\sigma^e = h(m) \mod N$. This prevents existential forgery attacks associated with basic RSA signatures.                                             |
| **Prime Residue Class Group Modulo $n$ ($Z_n^*$)**     | The set of residue classes ${[a] \mid 1 \le a \le n-1 \text{ and } \gcd(a, n) = 1}$, consisting of elements in $Z_n$ that have **multiplicative inverses** (units).                                                                                                                      | The order of $Z_n^*$ is given by the Euler phi function $\varphi(n)$.                                                                                                                                                    |
| **Euler Phi Function** ($\varphi(n)$)                  | Also called the Euler Totient Function, it is the **number of integers in the interval $[1, n-1]$ which are prime to $n$**.                                                                                                                                                              | Used in RSA key generation to find $d$ such that $ed \equiv 1 \mod \varphi(n)$, where $\varphi(N)=(p-1)(q-1)$.                                                                                                           |
| **Modular Exponentiation**                             | The efficient computation of $a^n$ (usually modulo a number $N$).                                                                                                                                                                                                                        | This calculation is performed using the **square-and-multiply method**. If the calculation is done modulo a prime $p$, the exponent can be reduced modulo $p-1$ (by Fermat's Theorem).                                   |
| **Elliptic Curve Discrete Logarithm Problem**          | The problem of finding $k \in Z_n$ such that **$P = kQ$**, given points $P$ and $Q$ on an elliptic curve.                                                                                                                                                                                | This is the hard problem upon which Elliptic Curve Cryptography (ECC) security is based. $kQ$ is easy to compute using the Double and Add algorithm if $k$ is known.                                                     |
| **Elliptic Curve Digital Signature Algorithm (ECDSA)** | The **elliptic curve analogue of the Digital Signature Algorithm (DSA)**. It uses the properties of points on an elliptic curve defined over a finite field.                                                                                                                             | Key generation involves choosing a secret key $d_A$ and publishing $P_A = d_A Q$, where $Q$ is the base point of prime order $n$.                                                                                        |
# Public vs Private Keys
## Trapdoor Functions
The concept of a **Trapdoor Function** is foundational to public-key cryptography, acting as a one-way mathematical lock that can only be easily opened if special information is known.

### Concept of a Trapdoor One-Way Function

A trapdoor one-way function is a special type of **one-way function**:

- **One-Way Function:** This is a function that is **easy to compute in one direction**, but is **hard to invert** (finding the pre-image is practically infeasible). Examples of candidates for one-way functions include the multiplication of two large prime numbers and Discrete Exponentiation.
- **Trapdoor Property:** A trapdoor function is a one-way function that possesses **trapdoor information**. If this specific secret information (the trapdoor) is known, the inverse of the function becomes **easy to compute**.

The RSA function, $RSAn,e : x \mapsto x^e$, is an example of a trapdoor function.

### How Trapdoor Functions Enable Asymmetric Encryption

The trapdoor one-way function allows public-key cryptography to separate the encryption and decryption processes:

1. **Public Key (The Function):** The function itself, $E_{pk}$, is the public key. This function is **computable by an efficient algorithm** and is publicly announced. When Alice wants to send a message ($m$) to Bob, she uses Bob's public key ($pk$) to compute the ciphertext ($c$) using the encryption function: $c = E_{pk}(m)$.
2. **Private Key (The Trapdoor):** The secret information ($sk$) that allows the function to be easily inverted is called the **trapdoor information**. This secret key is known only to the owner (Bob).
3. **Decryption:** Bob uses his secret key ($sk$) to efficiently compute the pre-image ($m$) from the ciphertext ($c$). Since Bob is the only one who knows the secret key, he is the only one who can decrypt the message.

In essence, the public key allows anyone to securely "lock" a message using the easy-to-compute direction of the trapdoor function, while the private key acts as the hidden **trapdoor** that enables the decryption (reversal) to be done efficiently.

### Computational Infeasibility of Reversal

It is "computationally infeasible" for an adversary (without the private key) to reverse the process because inverting the one-way function requires solving a **fundamentally hard problem**.

In the context of the RSA cryptosystem, the trapdoor function $x \mapsto x^e$ is based on the difficulty of **factoring large composite numbers**.

- **The Hard Problem (Factorization):** RSA key generation involves multiplying two large prime numbers, $p$ and $q$, to get a composite modulus $N = pq$. While multiplication is "easy" (efficiently computable by a computer), factoring $N$ to find $p$ and $q$ is "hard" due to the exponential time required as the size of the numbers increases.
- **The Private Key's Role:** The factors $p$ and $q$ are used to calculate the private decryption exponent $d$. Knowing $d$ (the trapdoor information) makes the inverse operation (decryption) easy.
- **Infeasibility without the Key:** An adversary (Eve) knows $N$ and the public exponent $e$, along with the ciphertext $c = m^e \mod N$. To find the message $m$, Eve would either have to compute the $e$-th root of $c$ modulo $N$ or successfully factor $N$ to find $p$ and $q$. It is widely believed that no efficient algorithm exists for these operations when $p$ and $q$ are sufficiently large. The time needed for a computer to factor these huge numbers can increase to hundreds or thousands of years, thus making the process "computationally infeasible".

## RSA Encryption Rule Set

#### **1. To send a secret message ($m$) to Alice, which key do I use?**

You must use **Alice's Public Key ($pk_{Alice}$)** to encrypt the message.

- **Rule:** The encryption function takes the plaintext message ($m$) and Alice’s public key, $pk=(N, e)$, to produce the ciphertext ($c$) using modular exponentiation: $c = m^e \mod N$.
- **Context:** Alice's public key is distributed publicly and available to everyone. This allows anyone, including you, to encrypt a message intended only for Alice.

#### **2. To decrypt that message, which key does Alice use?**

Alice must use **Alice's Private Key (Secret Key, $sk_{Alice}$)** to decrypt the message.

- **Rule:** The decryption function takes the ciphertext ($c$) and Alice’s private key, $sk=(N, d)$, to recover the plaintext message ($m$) using modular exponentiation: $m = c^d \mod N$.
- **Context:** Alice's private key ($d$) must be kept secret and is only known to her (the owner). This ensures that only Alice can recover the original message.

#### **3. Crucial: Can I decrypt the message with the same key I used to encrypt it? Explain why not.**

**No, you cannot** decrypt the message using the same public key used for encryption.

**Explanation (Asymmetric System and One-Way Functions):**

1. **Asymmetric Nature:** RSA is an **asymmetric encryption** scheme, meaning that the key used for encryption (the public key, $pk$) is intentionally **different** from the key used for decryption (the private key, $sk$). The keys are linked, but distinct.
2. **Trapdoor Function:** The RSA encryption process is based on a **trapdoor one-way function**.
    - **One-Way (Encryption):** Encrypting the message ($m \to m^e \mod N$) is the **easy** direction of the function, and anyone with the public key can perform it efficiently.
    - **Trapdoor (Decryption):** Reversing this process (finding $m$ from $c$, or computing the $e$-th root modulo $N$) is designed to be **computationally infeasible** without the specific secret information, or **trapdoor**.
3. **Key Requirement:** The private key ($d$) acts as the trapdoor information. This key is mathematically constructed based on the factorization of the modulus $N$ ($p$ and $q$), which is kept secret. Without access to the private key $d$, attempting to reverse the encryption using only the public information ($N$ and $e$) requires solving a fundamentally hard problem (either factoring $N$ or computing the $e$-th root modulo $N$), a process that takes a computer an exponentially large amount of time, rendering it **computationally infeasible**.

# The Algorithms: RSA & Diffie-Hellman

The security of the key public-key cryptosystems, RSA and Diffie-Hellman (and its derivative, ElGamal), rests upon different mathematical problems that are currently considered **computationally infeasible** to solve efficiently.

## Comparison of Hard Problems

| Cryptosystem                        | Mathematical Hard Problem               | Description of the Hard Problem                                                                                                                                                                                                        |
| :---------------------------------- | :-------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **RSA Cryptosystem**                | **Integer Factorization Problem** (IFP) | The security of RSA depends on the **difficulty of factoring large composite numbers** ($N$) into their two large prime factors ($p$ and $q$).                                                                                         |
| **Diffie-Hellman (DH) and ElGamal** | **Discrete Logarithm Problem** (DLP)    | The security of DH key exchange and ElGamal encryption relies on the difficulty of **extracting discrete logarithms** (DLP). Given $y = g^x$, finding the exponent $x$ (the discrete logarithm) is hard.                               |
| **ElGamal Variation**               | **Diffie–Hellman Problem** (DHP)        | The security of ElGamal encryption specifically depends on the **Diffie–Hellman problem**: the difficulty of computing $g^{ab}$ from $g^a$ and $g^b$ alone. An efficient algorithm to compute discrete logarithms would solve the DHP. |

---

### Why These Problems are Considered 'Hard'

Both the Integer Factorization Problem (IFP) and the Discrete Logarithm Problem (DLP) are considered "hard" because the known algorithms required to solve them take an **exponential amount of time** relative to the size of the input numbers on classical computers. This makes their computation **practically infeasible** when the numbers (keys) are sufficiently large.

#### 1. Hardness of Integer Factorization (Securing RSA)

Multiplication (the forward process: $p \cdot q = N$) is **easy** and can be performed efficiently, often in less than a second even for very large numbers. Conversely, determining the prime factors ($p$ and $q$) of a very large composite number ($N$) requires complex algorithms and trial and error.

- As the size of the number to be factored grows, the time needed for the calculation **increases rapidly**.
- Factoring extremely large numbers (such as those used for RSA moduli, which are over 300 digits long) would require a computer to run for hundreds or thousands of years, making it a "hard" problem.

The fact that the RSA function ($x \mapsto x^e$) is hard to invert without knowing the secret factors ($p$ and $q$) makes it a **trapdoor function**, providing the basis for RSA's security.

#### 2. Hardness of Discrete Logarithms (Securing Diffie-Hellman/ElGamal)

Discrete Exponentiation (the forward process: $x \mapsto g^x$) is **easy** and can be performed efficiently using algorithms like the Square and Multiply method. However, computing the inverse function, the discrete logarithm, is believed to be hard.

- Inverting the modular exponentiation requires testing all elements until the equation is satisfied. This results in an algorithm with **exponential running time** because the modulus $N$ is exponential in the binary length of $N$.
- While better algorithms exist for specific cases (like the baby-step giant-step algorithm mentioned in a lab context), no algorithm is known that runs efficiently for all moduli on classical computers.
- The computational effort required to solve the DLP is analogous to trying to reverse a mixed color to find the exact original colors used to create it.
## Diffie-Helman Key Exchange
The Diffie-Hellman Key Exchange is a public-key method for **key agreement** that allows two parties, Alice and Bob, to establish a fresh, shared secret key over an insecure, public channel, even though they have never met. The process relies on mathematical operations that are easy to perform in one direction (Discrete Exponentiation) but computationally infeasible to reverse (Discrete Logarithm Problem).

### Analogy: Mixing Colours as a One-Way Function

The underlying trick of Diffie-Hellman is often explained using a paint-mixing analogy, which models the behavior of a one-way function:

1. **Public Agreement (Public Channel):** Alice and Bob first agree publicly on a **fixed, public color** (analogous to the generator $g$). Anyone, including Eve, knows this starting color.
2. **Private Secret Selection:** Alice and Bob both randomly select their own **secret private colors** (analogous to secret exponents $a$ and $b$) and keep them hidden.
3. **Mixing and Sharing (Public Channel):** Alice mixes her secret private color with the public color to create her **mixture**. Bob does the same to create his mixture. They send their respective mixtures to the other party over the public channel.
4. **Shared Secret Key:**
    - Alice takes **Bob's mixture** and adds her **own secret private color** to it.
    - Bob takes **Alice's mixture** and adds his **own secret private color** to it.
5. **Result:** Both Alice and Bob arrive at the **exact same final color**, which is their **shared secret**.

**Why Eve Cannot Determine the Secret:** Eve, who is always listening, can see the public color and both mixtures that were exchanged. However, the trick works because it is **easy to mix two colors** to make a third, but **hard to reverse** a mixed color to find the exact original private colors used. Eve needs one of the private colors to create the final secret color, making it infeasible for her to obtain the secret key.

### Diffie-Hellman Key Exchange Mathematical Steps

The mathematical steps replicate the colour analogy using **Discrete Exponentiation**:

**Setup (Public Information):**

- Alice and Bob agree on a **group $G$** and a **generator $g$** of that group, which are fixed and public. (In modular arithmetic, this often involves a large prime $p$ and a generator $g$ of the group $Z_p^*$.)

**Steps to Establish the Shared Key $k$:**

|Step|Alice's Action (Secret $a$)|Bob's Action (Secret $b$)|Public Information (Eve knows)|
|:--|:--|:--|:--|
|**1. Choose Secrets**|Randomly chooses a secret exponent $a$.|Randomly chooses a secret exponent $b$.|$G, g$|
|**2. Compute & Exchange**|Computes $g^a$ (her public component) and **sends $g^a$ to Bob**.|Computes $g^b$ (his public component) and **sends $g^b$ to Alice**.|$G, g, g^a, g^b$|
|**3. Final Computation**|Computes the shared secret key $k_A = (g^b)^a$.|Computes the shared secret key $k_B = (g^a)^b$.|$G, g, g^a, g^b$|

**Result:**

- Since the laws of exponents dictate that $(g^b)^a$ equals $g^{ba}$, which is the same as $g^{ab}$ or $(g^a)^b$, Alice's calculated key ($k_A$) and Bob's calculated key ($k_B$) are **equal** ($g^{ab}$), giving them a shared secret key.

**Why Eve Cannot Determine the Secret:**

- Eve knows $G$, $g$, $g^a$, and $g^b$, but must compute $g^{ab}$.
- Calculating the exponentiation ($g^x$) is **easy** using algorithms like Square and Multiply.
- However, solving for the secret exponent $a$ from $g^a$ or $b$ from $g^b$ requires computing the **discrete logarithm function** (the inverse of discrete exponentiation), which is **believed to be hard** for classical computers when the numbers are sufficiently large. This computational difficulty of finding the shared secret $g^{ab}$ from the publicly known components is known as the **Diffie–Hellman Problem**.

# Practical Application: Hybrid Encryption

The concept of **Hybrid Encryption** is a highly efficient and widely adopted solution that combines the strengths of both public-key (asymmetric) and symmetric-key cryptography to ensure secure communication of large volumes of data.

### Explanation of Hybrid Encryption

Hybrid encryption is a method used to encrypt long messages by **combining public-key encryption with symmetric-key encryption**.

In a hybrid scheme, the public-key method (like RSA or ElGamal) is used to establish a fresh, temporary secret key, while the symmetric-key method (like AES) is used to encrypt the bulk of the data.

### Why Public-Key Cryptography is Slower

Public-key cryptography (Asymmetric encryption) is generally **much slower and less efficient** than symmetric-key encryption.

- **Asymmetric Encryption:** Schemes like RSA rely on complex, computationally intensive mathematical problems, such as **modular exponentiation** ($m^e \mod N$). While specialized algorithms exist (like the Square-and-Multiply method) to make the computation of $a^n$ efficient, the overall process is inherently complex.
- **Symmetric Encryption:** Symmetric methods use a single key for both encryption and decryption and are designed to be highly optimized and executed very efficiently.

The **advantage** of employing a hybrid approach is that **symmetric-key encryption is much more efficient than public-key encryption** for encrypting the actual message data.

### Standard Hybrid Encryption Workflow (RSA + AES)

The standard hybrid encryption workflow involves two distinct encryption phases:

1. **Public-Key Encryption (RSA) for Key Exchange (Confidentiality of the Key):**
    
    - The sender (Alice) **generates a random, temporary symmetric key ($k$)**, often called a "Session Key" (e.g., a 256-bit AES key).
    - Alice uses the recipient's **Public Key ($pk$)** (e.g., Bob's RSA key) to **encrypt this small key ($k$)**. This results in the first ciphertext component, $c_1 = Enc_{pk}(k)$.
    - The public-key scheme is used here specifically to securely distribute the symmetric key, which is difficult to do otherwise over an insecure channel.
2. **Symmetric-Key Encryption (AES) for Message Encryption (Confidentiality of the Data):**
    
    - Alice uses the newly generated symmetric key ($k$) to **encrypt the actual large message ($m$)** (e.g., a large file or conversation) using the efficient symmetric algorithm (e.g., AES-256). This results in the second ciphertext component, $c_2 = Enc'_{k}(m)$.
    - The entire ciphertext sent to the recipient consists of both components: ($c_1, c_2$), or $RSA_{pk}(k), AES_k(m)$.
3. **Decryption Workflow:**
    
    - The recipient (Bob) first uses his **Private Key ($sk$)** to decrypt the small public-key ciphertext ($c_1$) and recover the symmetric session key ($k$).
    - Once he has $k$, Bob uses this key to decrypt the large symmetric-key ciphertext ($c_2$) and recover the original message ($m$).

### Necessity for Performance

This two-step approach is **necessary for performance** because it maximizes security while minimizing the use of computationally expensive operations:

- **Public-key schemes** (like RSA) are used only for the **short operation of key distribution**. This step is computationally expensive but applied only once to a tiny piece of data (the session key).
- **Symmetric-key schemes** (like AES) are used for the **large operation of data encryption**. Since symmetric encryption is significantly faster, it can handle bulk data (long messages or large files) with far greater efficiency than an asymmetric scheme could.

Thus, hybrid encryption leverages the **public-key scheme's ability to establish a secret securely** without pre-sharing information, and the **symmetric-key scheme's efficiency in encrypting large amounts of data**.

---

_Analogy:_ Think of public-key encryption (RSA) as a massive, heavy armored truck (slow but secure) used only to deliver a single, specialized, lightweight key (the session key). Once that key is delivered, it is used to open the front door of a warehouse where lightning-fast conveyor belts (symmetric encryption/AES) handle the actual huge volume of cargo (the message data).

[!danger] Exam Critical: Textbook RSA vs. Padding

- **Textbook RSA:** The raw math $C = M^e \pmod n$. It is **Insecure** (Not IND-CPA secure).
    
    - _Why?_ It is deterministic. If an attacker knows the possible messages (e.g., "Yes" or "No"), they can encrypt both with the public key and see which ciphertext matches the intercepted one 2.
        
- **OAEP (Optimal Asymmetric Encryption Padding):** The standard fix. It adds randomness (padding) to the message _before_ encryption.
    
    - _Result:_ Encrypting "Yes" twice produces two completely different ciphertexts.

---
# Exam Style Questions
### Short Answer Questions

|Question|Answer|Citation|
|:--|:--|:--|
|**1. Hard Problems in Public Key Cryptography**|What are the two distinct, fundamental mathematical problems that form the security basis for most modern public-key cryptosystems (e.g., RSA and ElGamal)?|The two hard problems are the **difficulty of factoring large numbers** (which secures RSA),, and the **difficulty of extracting discrete logarithms** (which secures ElGamal/Diffie-Hellman),,.|
|**2. CPA Security and Textbook RSA**|Why is "Textbook RSA" considered insecure against a Chosen-Plaintext Attack (CPA)? What characteristic of the encryption scheme makes it vulnerable?|Textbook RSA is considered insecure because it is **deterministic**,,. If the same message ($m$) is encrypted twice, the two ciphertexts are identical,. This allows an adversary (Eve) to choose probable messages, encrypt them herself using the public key ($pk$), and compare the result to the challenge ciphertext to guess the message,.|
|**3. Function of the RSA Trapdoor**|In the context of trapdoor functions, what specific piece of information acts as the "trapdoor" in the RSA cryptosystem, and what function does it enable?|The trapdoor information is the **decryption exponent ($d$)**,. It enables the **efficient computation of the inverse function** (decryption),,.|
|**4. Diffie-Hellman Key Exchange Goal**|What is the purpose of the Diffie-Hellman Key Exchange, and what four specific values must an adversary (Eve) know to attempt to compute the shared secret key ($g^{ab}$)?|The purpose is a **public-key method for key agreement** that allows two parties to **establish a fresh, shared secret key**,. Eve knows the group ($G$), the generator ($g$), and the two publicly exchanged values ($g^a$ and $g^b$),.|
|**5. Elliptic Curve Encryption Basis**|Elliptic Curve Cryptography (ECC) is analogous to systems based on Discrete Logarithms. What operation is computationally easy in ECC, and what is the corresponding "hard problem" that secures it?|The operation that is **easy** to compute is **scalar multiplication** (given a number $x$ and a point $P$, computing $x \cdot P$),. The corresponding hard problem is the **Elliptic Curve Discrete Logarithm Problem (ECDLP)**, which means given $P$ and $Q$ ($Q=xP$), it is hard to find the number $x$,,.|

---

### Scenario-Based Long-Form Questions

**1. RSA Key Security and Factorization**

Alice sets up the RSA cryptosystem. She generates two large primes, $p$ and $q$, and computes the RSA modulus $N=pq$.

1. Explain why the multiplication step ($p \cdot q = N$) is considered "easy" while reversing it (factoring $N$) is "hard," and why this contrast is essential for RSA security.
2. The decryption exponent $d$ is derived such that $ed \equiv 1 \mod \varphi(n)$. If an adversary (Eve) manages to discover the value of the Euler Totient Function, $\varphi(N)$, explain how this compromises the entire security of Alice’s private key ($d$), even without directly factoring $N$.

**Answer:**

1. **Easy Multiplication vs. Hard Factorization:**
    
    - The multiplication step ($p \cdot q = N$) is considered **"easy"** because efficient algorithms exist to compute it, requiring relatively little time even for large numbers,.
    - Reversing this process (factoring $N$) is **"hard"** because the time required for known factorization algorithms increases rapidly as the number size grows. For huge numbers, it may require hundreds or thousands of years to complete the calculation.
    - This contrast is essential because it forms the basis of the **one-way function** used in RSA,. The public key allows anyone to perform the easy, forward calculation (encryption), while the secret factors ($p$ and $q$) provide the trapdoor needed for the owner to perform the hard, inverse calculation (decryption),.
2. **Compromise via $\varphi(N)$:**
    
    - If Eve knows the modulus $N$ and the public exponent $e$, she only needs $\varphi(N) = (p-1)(q-1)$ to calculate the secret decryption exponent $d$,.
    - The exponent $d$ is defined as the multiplicative inverse of $e$ modulo $\varphi(N)$, meaning $ed \equiv 1 \mod \varphi(n)$,.
    - Since the extended Euclidean algorithm efficiently computes $d$ from $e$ and $\varphi(N)$,, knowing $\varphi(N)$ bypasses the need to solve the factoring problem entirely.
    - Once Eve has $d$, she possesses the secret key ($sk$) and the trapdoor information,, allowing her to decrypt any ciphertext intended for Alice,. Furthermore, knowing $\varphi(N)$ and $N$ allows an adversary to efficiently compute the prime factors $p$ and $q$ as well.

**2. Hybrid Encryption and Performance Necessity**

A company needs to transmit large, long documents securely over the internet. They decide to use a **Hybrid Encryption** scheme combining RSA and AES.

1. Describe the standard workflow required to encrypt the document and allow the recipient (Bob) to decrypt it, specifying where the RSA keys and the AES key are used.
2. Justify why this combined approach is necessary, focusing on the comparative efficiency and complexity of the two key types.

**Answer:**

1. **Hybrid Encryption Workflow (RSA + AES):**
    
    - **Generation and Encryption of Session Key:** The sender (Alice) **generates a random, temporary symmetric key ($k$)** (a Session Key),. Alice uses **Bob's Public Key ($pk_{Bob}$)** (the RSA key) to encrypt this small session key, resulting in $c_1 = Enc_{pk}(k)$,.
    - **Encryption of Message:** Alice then uses the efficient **symmetric algorithm (AES)** and the session key ($k$) to encrypt the actual large message ($m$), resulting in $c_2 = Enc'_{k}(m)$,.
    - **Decryption:** Bob receives the combined ciphertext ($c_1, c_2$). He uses his **Private Key ($sk_{Bob}$)** (the RSA key) to decrypt $c_1$ and recover the Session Key ($k$). Then, he uses the recovered Session Key ($k$) to decrypt $c_2$ (the large file) using AES, thereby recovering the original message ($m$).
2. **Necessity and Efficiency Justification:**
    
    - This hybrid approach is necessary because symmetric-key encryption is **much more efficient** than public-key encryption.
    - **Public-key schemes (RSA)** are computationally expensive because they rely on **complex mathematical operations** (like modular exponentiation) derived from fundamentally hard problems (factoring). If the entire large message were encrypted using RSA, the process would be very slow.
    - **Symmetric-key schemes (AES)** are designed to be fast and efficient for bulk data handling,.
    - Therefore, the hybrid model uses the public key (RSA) only for the **short operation of securely distributing the session key** over the public channel. The symmetric key (AES), which is fast, is then used to handle the **time-consuming task of encrypting the large amount of data**, maximizing both security and performance.