---
title: Week 03 - Introduction to Cryptography and Symmetric Ciphers
date: 2025-12-14
tags:
  - cryptography
  - symmetric
  - math
  - integrity
aliases:
  - Block Ciphers
  - Stream Ciphers
  - Hash Functions
  - MAC
summary: Encryption where keys are shared. Covers AES, RC4, Perfect Secrecy, and Modes of Operation (ECB/CBC).
---
## Key Terms

| Term                                        | Definition                                                                                                                                                                                                                     | Exam Context/Example                                                                                                                                                                                       |
| :------------------------------------------ | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Cryptography**                            | The science of keeping information secure, particularly referring to confidentiality and integrity (through hashing).                                                                                                          | Provides tools that underlie most modern security protocols and is the key enabling technology for protecting distributed systems.                                                                         |
| **Cryptology**                              | The overarching field of study that covers cryptography (designing ciphers) and cryptanalysis (breaking them).                                                                                                                 | Often shortened to just crypto.                                                                                                                                                                            |
| **Kerckhoffs' Principle**                   | The cryptographic system must remain secure even if the adversary knows all the details about the algorithms and their implementation; security must be based entirely on the secret keys.                                     | Represents the opposite approach to "security through obscurity".                                                                                                                                          |
| **Plaintext / Cleartext**                   | Unencrypted data or the original message to be transmitted.                                                                                                                                                                    | In modern cryptography, often represented as a string of bits.                                                                                                                                             |
| **Ciphertext**                              | The encrypted form of the plaintext message.                                                                                                                                                                                   | Is transmitted over an insecure channel.                                                                                                                                                                   |
| **Encryption Scheme (Cipher)**              | A pair of algorithms, Enc (encryption) and Dec (decryption), that transform plaintext ($M$) into ciphertext ($C$) using a key ($K$) and satisfy the correctness condition $Dec(k, Enc(k, m)) = m$.                             | Historical examples include the Shift Cipher used by Julius Caesar.                                                                                                                                        |
| **Key**                                     | Secret information, roughly analogous to a password, used by cryptographic algorithms to encrypt or decrypt a message.                                                                                                         | The range of all possible values for the key is called the **keyspace**.                                                                                                                                   |
| **Symmetric Cryptography**                  | Utilises a single key for both encryption and decryption, hence also known as **private key** or **shared-key** cryptography.                                                                                                  | Examples include DES and AES. A basic problem is how to securely exchange the shared secret key.                                                                                                           |
| **Asymmetric Cryptography**                 | Utilises two mathematically related keys: a public key (for encryption) and a private key (for decryption), hence also known as **public-key** cryptography.                                                                   | Examples include the RSA algorithm. It solves the problem of key exchange as the public key is shared openly.                                                                                              |
| **Block Cipher**                            | A symmetric-key encryption scheme that processes plaintext blocks of a fixed length (e.g., $n$ bits) and outputs ciphertext blocks of the same fixed length.                                                                   | DES uses a 64-bit block length; AES uses 128 bits. Often modeled as a **Pseudorandom Permutation (PRP)**.                                                                                                  |
| **Stream Cipher**                           | Encrypts a stream of plaintext characters/bits character by character/bit by bit using a **key stream** (a sequence of key elements).                                                                                          | The most famous example is **Vernam's One-Time Pad**. Used where data is in a continuous stream.                                                                                                           |
| **One-Time Pad (OTP)**                      | A stream cipher using bitwise XOR where the key stream is truly random and must be as long as the message and never reused.                                                                                                    | Provides **perfect secrecy** (unconditional security) against adversaries with unlimited resources, proven by Claude Shannon's theorem. Impractical due to key length requirements.                        |
| **Pseudorandom Permutation (PRP)**          | An abstract concept for a keyed function (like a block cipher) that is efficient to evaluate and invert (one-to-one) and is computationally indistinguishable from a truly random permutation.                                 | Block ciphers like AES and 3DES are PRPs.                                                                                                                                                                  |
| **Pseudorandom Function (PRF)**             | An abstract concept for a keyed function that is computationally indistinguishable from a truly random function; it is not necessarily invertible or one-to-one.                                                               | Used to make stream ciphers practical by stretching a short key (**seed**) into a long key stream using a **PRNG**.                                                                                        |
| **Electronic Codebook (ECB) Mode**          | A block cipher mode where each block of plaintext is encrypted independently with the key.                                                                                                                                     | Highly insecure because identical plaintext blocks encrypt to identical ciphertext blocks, revealing patterns and allowing cut-and-splice attacks.                                                         |
| **Cipher-Block Chaining (CBC) Mode**        | A block cipher mode where the previous ciphertext block is XORed ($\oplus$) with the current plaintext block before encryption.                                                                                                | Requires a unique **Initialization Vector (IV)** for the first block to ensure distinct ciphertexts, even if the plaintext is the same. Encryption is sequential, although decryption can be parallelized. |
| **Counter (CTR) Mode**                      | A block cipher mode that operates in parallel by encrypting a counter (or $IV + i$) to generate a keystream, which is then XORed with the plaintext blocks.                                                                    | Advantage is high parallelizability for fast data links, as each block encryption is independent.                                                                                                          |
| **Hash Function**                           | A function that maps an arbitrary length input string (**message**) to a fixed-length output bit string (**message digest** or **hash**).                                                                                      | Used widely in cryptography for checking file integrity, digital signatures, and password databases (keyless cryptography).                                                                                |
| **One-wayness (OW) / Pre-image Resistance** | The property that given a hash value $y$, it is computationally infeasible to find the original input message $x$ such that $h(x) = y$.                                                                                        | Essential for password storage, ensuring that the stored hash cannot be trivially inverted to reveal the password.                                                                                         |
| **Second Pre-image Resistance (TCR)**       | The property that given a specific message $x$, it is infeasible to find a distinct message $x' \neq x$ such that $h(x') = h(x)$.                                                                                              | Required for file integrity checks/modification detection; an adversary needs to modify a file $F$ to $F'$ without changing the hash $h(F)$. **Collision resistance** is a stronger property.              |
| **Collision Resistance (CR)**               | The property that it is computationally infeasible to find _any_ pair of distinct messages $m$ and $m'$ such that $h(m) = h(m')$.                                                                                              | A hash function must be CR if used with digital signatures, otherwise an attacker could substitute a signed message $M$ with a different message $M'$ having the same hash.                                |
| **Birthday Attack**                         | A brute-force attack against collision resistance that exploits the birthday paradox, requiring approximately $2^{n/2}$ hash computations (where $n$ is the hash output length) to find a collision.                           | Requires hash outputs to be long enough (e.g., >160 bits) to make $2^{n/2}$ computations impractical for an attacker.                                                                                      |
| **Digital Signature**                       | Allows one party (the signer) to sign a message using their **private key** so that any party can verify the message's authenticity and integrity using the signer's **public key**.                                           | Provides **non-repudiation** (the sender cannot deny sending the message). Typically signs the cryptographic hash value of the message, rather than the message itself.                                    |
| **Message Authentication Code (MAC)**       | A symmetric key technique using a shared secret key ($k$) to augment a message $m$ with a code ($MAC(k, m)$) to guarantee data **integrity** and message **authentication**.                                                   | Implemented either by using a block cipher in a specific mode (like CBC-MAC, using only the last ciphertext block) or from hash functions (like **HMAC**).                                                 |
| **HMAC**                                    | A standard method to convert a cryptographic hash function $H$ into a MAC by applying $H$ twice using variants of the secret key $k$ (e.g., $h(k \oplus A, h(k \oplus B, M))$).                                                | Used to avoid the **length extension problem** inherent in simple keyed hash constructions. Widely used in practice (e.g., TLS protocol).                                                                  |
| **Diffusion**                               | A design principle for block ciphers and hash functions aimed at spreading the influence of the plaintext/input widely, such that changing one input bit affects, on average, half the output bits (the **avalanche effect**). | A necessary property alongside **confusion** for building strong ciphers.                                                                                                                                  |
| **Feistel Cipher**                          | An iterated block cipher structure where the input block is split into two halves, and in each round, one half is transformed and combined (usually XORed) with the other half.                                                | The structure ensures that decryption is easy by reversing the round functions, even if the round functions themselves are not invertible.                                                                 |
| **Chosen-Plaintext Attack (CPA)**           | An attack model where the adversary is able to choose plaintexts and obtain the corresponding ciphertexts under the target key.                                                                                                | Often possible in real systems (e.g., IFF systems). Used to define the rigorous security concept **IND-CPA security**.                                                                                     |
| **Entropy ($H$) (Information Theory)**      | A logarithmic measure of information, choice, or uncertainty for a set of probabilities, typically calculated as $H = -\sum p_i \log p_i$.                                                                                     | Used to define the theoretical limits of compression and coding efficiency for a source of information.                                                                                                    |
## Stream Ciphers vs Block Ciphers
|Characteristic|Stream Ciphers|Block Ciphers|
|:--|:--|:--|
|**Input Processing**|Encrypts the plaintext message one bit at a time, or character by character in a continuous stream. Stream ciphers are modeled as pseudorandom generators (PRGs).|Encrypts data in fixed-length, predetermined chunks, known as blocks. Block ciphers are modeled as pseudorandom permutations (PRPs).|
|**Error Propagation**|Errors typically affect only the bit or block containing the corruption. For example, in Output Feedback (OFB) mode, a transmission bit error in block $c_i$ affects only the decryption of that specific block. In Counter (CTR) mode, an error in ciphertext block $c_i$ affects only $c_i$.|Are more sensitive to errors, as an error can render unusable a larger segment of data. For example, in Cipher-Block Chaining (CBC) mode, an error in ciphertext block $c_i$ affects the decryption of both $c_i$ and $c_{i+1}$.|
|**Performance**|Generally faster than block ciphers. Are often preferred for situations where data is in a continuous stream, such as moving over a network. Can operate almost at gigabit rates.|Often slower than stream ciphers. Can be highly efficient if used in modes that allow parallelisation, such as Counter (CTR) mode, where each block encryption is independent. They are typically better when the message size is fixed or known in advance, such as when encrypting a file.|
|**Examples**|Vernam's One-Time Pad, RC4, ORYX, SEAL.|Data Encryption Standard (DES), Triple DES (3DES), Advanced Encryption Standard (AES) (also known as Rijndael), Serpent, Blowfish, Twofish, CAST5, RC6, IDEA.|

**Comparison and Contrast Summary:**

The primary distinction is in **how data is processed**: block ciphers handle data in fixed-size blocks, while stream ciphers handle data continuously, often bit-by-bit. This processing method affects their security properties and implementation feasibility:

1. **Speed and Use Case:** Stream ciphers are typically much faster and are preferred for continuous, real-time data flow. Block ciphers are commonly used for bulk encryption of data where the message size is known, like files.
2. **Error Handling:** Stream ciphers generally offer better localization of errors, meaning a single corrupted bit during transmission often only affects that corresponding bit upon decryption (depending on the mode). Block ciphers are inherently more sensitive to errors, as a single error can propagate to damage multiple data segments unless carefully managed by modes like CTR.
3. **Key Concept:** Stream ciphers are derived from pseudorandom number generators (PRNGs) used to create a key stream, often based on shortening the impractical key length required for the perfectly secret One-Time Pad. Block ciphers are modeled as pseudorandom permutations (PRPs).


## Distinction Between Cryptographic Hash Functions and MACs

The distinction between a **Cryptographic Hash Function** and a **Message Authentication Code (MAC)** lies primarily in their inputs, outputs, and the specific security goals they achieve.

Both cryptographic hash functions and MACs are used to guarantee the integrity of data. However, MACs are fundamentally keyed operations, while hash functions are not, leading to different security assurances.

A **Cryptographic Hash Function** (or Message Digest) takes an arbitrarily long input message and maps it to a fixed-length output string (the hash or message digest). The key properties required of a good cryptographic hash function include one-wayness (pre-image resistance), second pre-image resistance, and collision resistance. A hash value is essentially a compact, practically unique fingerprint of the message.

A **Message Authentication Code (MAC)** is also a fixed-length code generated from a message. However, a MAC is a symmetric key technique that uses a shared secret key ($k$) to produce the code, augmenting the message $m$ with $MAC(k, m)$.

|Characteristic|Cryptographic Hash Function (H)|Message Authentication Code (MAC)|
|:--|:--|:--|
|**Key Usage**|Does **not** require a secret key. Operations are public.|Requires a **secret key** ($k$) shared between the sender and receiver.|
|**Security Goal**|Provides data **Integrity** only (Modification Detection).|Provides both data **Integrity** and **Data Origin Authentication**.|

**Security Goal Explanation**

- **Cryptographic Hash Function (Integrity Only):** Since there is no secret key involved, anyone can compute the hash of a message. If an adversary modifies a file $F$ to $F'$, they must ensure that $h(F') = h(F)$ to avoid detection; this is only prevented if the hash function is second pre-image resistant. However, an attacker could potentially modify both the message _and_ the hash value if the hash is not secured in a tamper-proof location, as the adversary knows the algorithm used to calculate the hash. Because the process is public, a hash alone cannot prove who created the message.
- **Message Authentication Code (Integrity + Data Origin Authentication):** Because the MAC requires a shared secret key $k$ to compute the $\text{MAC}(k, m)$, only a party possessing that secret key can generate a valid MAC. When the receiver verifies the message by checking if the calculated MAC matches the received tag, a match confirms that the message has not been modified (Integrity) and that it came from the expected party who shares the key (Authentication).

### Scenario Application

|Scenario|Tool to Use|Rationale|
|:--|:--|:--|
|**Ensure a file hasn't been corrupted by a hard drive error.**|**Cryptographic Hash Function (H)**|You want to check the file's integrity against a securely stored, previous hash value (or "fingerprint"). A simple hard drive error is an accidental corruption, not an intentional attack, so you only need **Integrity** assurance, which the hash provides.|
|**Ensure a hacker didn't modify a message in transit.**|**Message Authentication Code (MAC)**|You need assurance that the message was not modified (**Integrity**) _and_ that it came from the trusted, expected sender (**Data Origin Authentication**). Since only the sender and receiver possess the secret key, a MAC prevents a hacker from injecting or modifying the message without being detected.|

A MAC combines the integrity check of a hash function with the security of a secret key, acting like a tamper-evident seal that only authorized users can apply. The integrity provided by a hash function alone is more like checking a package's weight against a known standard—it confirms the content hasn't changed, but not who packed it or if someone could sneakily swap the weight tag.

| **Method**           | **Order**                                     | **Security Status**                                                                         |
| -------------------- | --------------------------------------------- | ------------------------------------------------------------------------------------------- |
| **Encrypt-then-MAC** | Encrypt plaintext, then MAC the _ciphertext_. | **Safest** (Standard practice). Verifies integrity _before_ decrypting, preventing attacks. |
| **MAC-then-Encrypt** | MAC plaintext, then Encrypt both.             | **Risky** (Used in SSL, prone to padding oracle attacks like POODLE).                       |
| **Encrypt-and-MAC**  | Encrypt plaintext, MAC plaintext separately.  | **Weak** (The MAC might leak info about the plaintext).                                     |
## Constructing MACs
> 
> 1. **Cryptographic Hash Functions:** Used to build **HMAC** (e.g., HMAC-SHA256).
>     
> 2. **Block Ciphers:** Used to build **CBC-MAC** (encrypting a message in CBC mode and keeping only the final block as the "Tag").
>     
> 3. **Pseudorandom Permutations (PRPs):** Since Block Ciphers are PRPs, PRPs are theoretically capable of constructing MACs.
>     

> - _Note:_ Shift ciphers or simple Stream ciphers (XOR) cannot create secure MACs because they are linear and malleable.
>
## Difference between Perfect Secrecy and Computational Security

The concepts of Perfect Secrecy and Computational Security define the two primary ways to approach the security of an encryption scheme, based on the assumed power of the adversary.

The fundamental difference lies in the resources available to the adversary:

|Feature|Perfect Secrecy (Information-Theoretic Security)|Computational Security|
|:--|:--|:--|
|**Adversary Power**|**Unlimited computational resources** (or "infinite computational resources"). The adversary is not computationally bounded.|**Limited computational resources**; the adversary is computationally bounded, typically modelled as having polynomial-time computing power on a probabilistic Turing Machine.|
|**Security Guarantee**|The adversary learns **no additional information** about the plaintext after observing the ciphertext, even if they have unlimited time and power.|The scheme can be broken if the adversary has sufficiently large computing power, but it is infeasible for a realistic (polynomial-time) adversary to compromise confidentiality.|
|**Independence**|The plaintext ($m$) and the ciphertext ($Enc_k(m)$) are mathematically independent.|The plaintext and ciphertext are independent **"from the point of view of a computationally limited adversary"**.|
|**Basis of Proof**|Based on **Information Theory** and Shannon's theory, defining measures of information like Entropy.|Based on Complexity Theory, assuming algorithms with non-polynomial running time are inefficient.|

Perfect secrecy represents an ideal, unconditional security, whereas computational security is a more realistic assurance for modern cryptography, acknowledging that adversaries are bound by the physics of computation.

### Why the One-Time Pad Offers Perfect Secrecy but is Impractical

The **One-Time Pad (OTP)** is the most famous example of a cipher that provides perfect secrecy because it is mathematically proven to be secure even against adversaries with unlimited computational resources. This proof was established by Claude Shannon. When a secret key ($k$) is chosen uniformly at random, the resulting ciphertext $c = k \oplus m$ has a uniform distribution that is independent of the plaintext $m$; therefore, observing $c$ provides no information about $m$.

However, the OTP is **completely impractical** for general use due to three critical drawbacks:

1. **Key Length:** The key ($k$) must be chosen uniformly at random and **must be as long as the message** ($|K| \geq |M|$ is necessary for any perfectly secret encryption scheme, proven by Shannon's theorem).
2. **Key Randomness:** It is extremely difficult to generate truly random strings of the required length.
3. **Key Reuse:** The key **cannot be reused**. If a key stream is used twice to encrypt two messages ($m$ and $m'$), an adversary can simply XOR the two ciphertexts ($c \oplus c'$) to reveal the difference between the plaintexts ($m \oplus m'$), which destroys the security.

### How Pseudo-Random Generators Bridge the Gap

Since the fundamental drawback of the OTP—the requirement that the key be as long as the message—is unavoidable for perfect secrecy (due to Shannon's theorem), modern cryptography relies on **Computational Security** and the use of **Pseudo-Random Generators (PRGs)**.

PRGs are used to "shorten" the key needed for the OTP, making the scheme practical while accepting a compromise on the absolute level of security.

1. **Stretching the Key:** A PRG is a mechanism that takes a short, truly random input (**seed**, $s$, which acts as the secret key $k$) and algorithmically stretches it into a much longer, pseudo-random output ($G(s)$), known as the **key stream**.
2. **Creating a Practical Stream Cipher:** This long key stream is then used like a one-time pad, XORed ($\oplus$) bitwise with the plaintext message $m$ to generate the ciphertext $c$ ($c = m \oplus G(s)$).
3. **Achieving Computational Security:** Because $G(s)$ is generated deterministically from a short seed, the resulting scheme is no longer perfectly secret. However, a cryptographic PRG is designed so that its output is **computationally indistinguishable from a truly random string**. This ensures that a computationally bounded adversary cannot distinguish the resulting stream cipher from a true OTP, thus providing **computational secrecy**.

In essence, PRGs sacrifice the theoretical guarantee of perfect secrecy (which is impossible to achieve practically anyway) for the strong, practical guarantee of computational security, allowing block ciphers and modern stream ciphers to function securely using short, manageable keys.


There are three primary **Modes of Operation** for block ciphers: Electronic Codebook (ECB), Cipher-Block Chaining (CBC), and Counter (CTR) mode. These modes extend block ciphers, which have a fixed block size (e.g., 64 bits for DES, 128 bits for AES), to process messages of arbitrary length.

### 1. Electronic Codebook (ECB) Mode

ECB mode is the most straightforward method, where each block of the plaintext message is encrypted independently using the block cipher function ($E_k$) and the shared secret key ($k$).

- **Operation:** The message ($m$) is divided into blocks ($m_1, m_2, \ldots, m_l$), and each block is encrypted to produce the corresponding ciphertext block ($c_i = E_k(m_i)$).
- **Security and Weakness:** This mode is highly insecure and **should not be used** for most applications, especially messages longer than one block. ECB is **not CPA-secure** (secure against Chosen-Plaintext Attack). Because the encryption of each block is deterministic and independent, **identical plaintext blocks result in identical ciphertext blocks**. This repetition reveals patterns in the data, which an attacker can exploit to deduce information about the plaintext.
- **Decryption and Error Handling:** Decryption uses the inverse function ($E^{-1}_k$) on each block independently. A transmission bit error in a single ciphertext block affects the decryption only of that specific block.
- **Real-World Risk:** In ECB mode, messages with authentication requirements, such as bank payment messages, are vulnerable to **cut and splice attacks** along the block boundaries.

### 2. Cipher-Block Chaining (CBC) Mode

CBC mode introduces a chaining mechanism to ensure that the encryption of any block depends on all preceding blocks, thus obscuring patterns found in the plaintext.

- **Operation:** Before encryption, the current plaintext block ($m_i$) is **bitwise XORed ($\oplus$) with the previous ciphertext block** ($c_{i-1}$). The result is then encrypted using the key: $c_i = E_k(m_i \oplus c_{i-1})$.
- **Initial Value (IV):** Since the first plaintext block ($m_1$) does not have a previous ciphertext block, an unpredictable block known as the **Initialization Vector (IV)** ($c_0$) is used instead. This IV must be **selected at random** for every message to prevent identical plaintexts from encrypting to identical ciphertexts, which is crucial for achieving security.
- **Decryption:** Decryption uses the inverse block function ($E^{-1}_k(c_i)$) and then XORs the result with the previous ciphertext block ($c_{i-1}$) to recover the plaintext: $m_i = E^{-1}_k(c_i) \oplus c_{i-1}$.
- **Performance and Parallelisation:** CBC encryption is **sequential** (cannot be easily parallelized) because the encryption of block $m_i$ requires the output of block $c_{i-1}$. However, **decryption can be parallelized**.
- **Error Propagation:** A transmission bit error in block $c_i$ affects the decryption of both **block $c_i$ and the subsequent block $c_{i+1}$**. CBC is **self-synchronizing** in that if one or more blocks are lost, the system can recover after a short time.

### 3. Counter (CTR) Mode

CTR mode transforms a block cipher into a stream cipher, offering the significant advantage of parallel processing.

- **Operation:** A **counter value** is encrypted for each plaintext block to generate a **pseudorandom key stream** block. The key stream block is then **XORed ($\oplus$) with the plaintext block** to produce the ciphertext. The counter is an initial value (IV) that increments for each block (e.g., $IV+1, IV+2, \ldots$).
- **Key Stream Generation:** The key stream ($G(k, IV)$) is generated by encrypting the unique counter for each block: $G(k, IV) := F_k(IV + 1) \parallel F_k(IV + 2) \parallel \ldots$.
- **Decryption and Parallelisation:** Decryption works by generating the identical key stream and XORing it with the ciphertext. The major benefit of CTR mode is that encryption and decryption of each block are **independent**, making it highly **parallelizable**. This allows for faster processing on systems with multiple processors or high-speed data links.
- **Error Propagation:** A transmission bit error in ciphertext block $c_i$ affects **only the decryption of that specific block**.
- **Uniqueness Requirement:** It is critical that the IV (or the combination of IV and the incremented counter $IV + i$) **never repeats** for a given key, which is why the block length must be large enough to avoid repetition.

It is important to note that CBC and CTR, while addressing confidentiality concerns, **do not provide protection against active attacks like message tampering** by themselves, and must be used in conjunction with a message integrity mechanism like a Message Authentication Code (MAC).

#### Properties of Counter (CTR) Mode

CTR mode transforms a block cipher into a stream cipher by generating a unique key stream that is XORed with the plaintext blocks.

|Property|Description|Citation|
|:--|:--|:--|
|**Keystream Generation**|A random Initialization Vector (IV) is taken as a starting point and is then incremented ($IV+1, IV+2, \ldots$) for each block. The block cipher encrypts this counter value to generate a pseudorandom keystream block $K_i = F_k(IV+i)$.||
|**Error Propagation**|A transmission bit error in a ciphertext block $c_i$ affects **only** the decryption of that specific block $c_i$.||
|**Parallelization**|Both **encryption and decryption can be parallelized** (done in parallel) because the keystream for each block can be generated independently of all others. This offers a performance benefit over modes like CBC.||
|**Random Access**|Yes, CTR mode allows **random access** to any block in the ciphertext. This is possible because the generation of the keystream for block $i$ (based on $IV+i$) does not depend on the encryption of block $i-1$.||
|**Integrity**|Like all symmetric encryption modes, CTR mode by itself is **not secure against an active attacker** who can tamper with the traffic. It only provides confidentiality (eavesdropping security) and must be used with a message integrity mechanism.||

### The MAC Security Game

A Message Authentication Code (MAC) scheme is formally defined by a pair of algorithms, $(\text{tag}, \text{vrfy})$. The tagging algorithm, $\text{tag}$, takes a key $K$ and a message $M$ to produce a tag $T$, and the verification algorithm, $\text{vrfy}$, checks if the tag is valid for the message and key.

The **MAC Security Game** (or informal security definition) is used to determine if an adversary can successfully break a MAC scheme.

**The Game's Setup:**

1. The adversary interacts with an **oracle** (a black box) that holds the secret key $k$.
2. The adversary is allowed to select multiple messages ($m_1, m_2, \ldots, m_w$) and submit them to the oracle.
3. For each message submitted, the oracle returns the corresponding valid MAC tag ($t_1, t_2, \ldots, t_w$) computed using the secret key $k$.

**How an Attacker Wins:**

The adversary **breaks the MAC scheme** if, at the end of the game, they output a new message-tag pair $(m', t')$ such that:

1. The tag $t'$ is a **valid tag** for the message $m'$ when verified by the receiver: $\text{vrfy}_k(m', t') = \text{true}$.
2. The message $m'$ is a **new message** that was **not** among the messages $m_1, \ldots, m_w$ previously queried by the adversary.

Winning the game essentially means the adversary successfully forges a valid authentication tag for a message they did not previously observe or control. MACs do not, however, inherently protect against "replay attacks" since the verification function ($\text{vrfy}$) has no memory or state to detect if a valid message/tag pair $(m, t)$ is being retransmitted.
## Four Standard Cryptographic Attack Models

The four standard cryptographic attack models, classified by the assumed resources available to the adversary (Eve), are as follows:

|Attack Model|Definition|Attacker's Additional Access/Information (Aside from Ciphertext)|
|:--|:--|:--|
|**Ciphertext-Only Attack (COA)**|An attack where the adversary obtains only the ciphertexts that result from the encryption scheme. An encryption method that cannot resist a COA is considered completely insecure.|**None**. The adversary must deduce the plaintext or key from the intercepted ciphertext alone.|
|**Known-Plaintext Attack (KPA)**|An attack where the adversary has the ability to obtain pairs of plaintexts and their corresponding ciphertexts. This information is used to try and decrypt a new ciphertext for which the plaintext is unknown.|**Plaintext-ciphertext pairs**. The plaintexts are drawn from some distribution that the adversary does not control. This scenario is often available to an attacker, as messages may be sent in standard formats known to the adversary.|
|**Chosen-Plaintext Attack (CPA)**|An attack where the adversary has the ability to choose plaintexts and obtain the corresponding ciphertexts under the target key. This model assumes the adversary obtains all desired plaintext-ciphertext pairs first, then performs the analysis without further interaction, meaning they only need access to the encrypting device once.|**Ciphertexts for plaintexts of their choosing**. The attacker can choose the input messages to be encrypted to help in deducing the key.|
|**Chosen-Ciphertext Attack (CCA)**|An attack where the adversary is able to choose ciphertexts and obtain the corresponding plaintexts. The adversary has access to the decryption device.|**Plaintexts for ciphertexts of their choosing**. The adversary may query a decryption oracle.|

**Additional Context:**

In both the **Chosen-Plaintext Attack (CPA)** and its stronger variant, the **Adaptively-chosen-plaintext attack** (where the attacker can switch between gathering pairs and performing analysis repeatedly), the adversary's objective is typically to recover the key or deduce the answer to a query they haven't already made (a forgery attack).

The strength of a cryptographic scheme is often defined against these attack models. For example, a scheme that can resist a CPA is defined as having **indistinguishable encryptions under a chosen-plaintext attack (IND-CPA)**, meaning a computationally bounded adversary cannot perform better than random guessing.


## Confusion vs Diffusion

Shannon's concepts of **Confusion** and **Diffusion** are two fundamental design principles for strong cryptographic algorithms, particularly block ciphers, intended to obscure the relationship between the plaintext, the ciphertext, and the key.

### Confusion and Diffusion

- **Confusion:** This principle aims to make the relationship between the secret key and the ciphertext as complex and indirect as possible. Confusion is achieved by adding unknown key values to the data, which makes it harder for an attacker to deduce the value of a plaintext symbol from the ciphertext.
- **Diffusion:** This principle ensures that the influence of the plaintext spreads widely throughout the ciphertext. Specifically, diffusion means spreading the plaintext information through the ciphertext. Ideally, changing one input bit should, on average, cause **half of the output bits to change**—an effect known as the **avalanche effect**. Diffusion is necessary, along with confusion, to build strong ciphers.

### Role of S-boxes and P-boxes (Permutations) in Ciphers

Ciphers that combine substitution and permutation circuits repeatedly, often called **SP-networks**, utilize S-boxes and P-boxes to achieve these goals.

**1. Confusion (Substitution Box / S-box):**

- **Function:** Substitution boxes, or S-boxes, provide the necessary **non-linearity** and complexity for **confusion**. A substitution circuit replaces plaintext symbols with ciphertext symbols based on a lookup table or a non-linear function.
- **Mechanism:** An S-box typically accepts a block of input bits (e.g., four bits wide) and provides a corresponding output block, often visualized as a lookup table containing a permutation of numbers.
- **Example (Rijndael/AES):** In the Rijndael algorithm (AES), the **SubBytes** step, which is the only non-linear transformation, substitutes the bytes of the state matrix using a function called the S-box. This step is crucial for ensuring non-linearity. The strength of the S-box in ciphers like DES depends on its specific design.

**2. Diffusion (Permutation / P-box):**

- **Function:** A permutation circuit, or P-box, shuffles or rearranges bits (transposition) within the block to achieve **diffusion**.
- **Mechanism:** Diffusion spreads the influence of an input bit change across many output bits over multiple rounds. Instead of having simple permutation of wires, it is often more efficient to use a **linear transformation** in which each input bit in one round is the result of the exclusive-or ($\oplus$) of several output bits in the previous round. For example, the design of the Serpent algorithm uses a linear transformation that ensures that a change in an input bit propagates rapidly through the cipher—the avalanche effect.
- **Example (Rijndael/AES):** In AES, the linear transformation (MixColumns and ShiftRows steps) is designed to ensure that a change in the input can potentially affect all of the output after just two rounds, demonstrating effective diffusion. The **MixColumns** step achieves diffusion by mixing the four bytes in a column using matrix multiplication.

By iterating rounds of substitution (confusion) and permutation (diffusion), strong modern block ciphers are built. If a cipher has poor diffusion, changing a single letter of the plaintext may only cause a single letter of the ciphertext to change, which makes it vulnerable to cryptanalysis.


# Exam Style Questions

### Short Answer Exam Questions

| Question                                                                                                                                  | Answer                                                                                                                                                                                                                                                                                                                                                                                           |
| :---------------------------------------------------------------------------------------------------------------------------------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **1.** Define **Cryptography** and **Cryptanalysis**, and explain how they relate to the broader field of **Cryptology**.                 | **Cryptography** is the science of keeping information secure, particularly referring to confidentiality and integrity (through hashing). **Cryptanalysis** is the science of breaking through the encryption used to create the ciphertext or studying attacks against cryptographic schemes. **Cryptology** is the overarching field of study that covers both cryptography and cryptanalysis. |
| **2.** State **Kerckhoffs' Principle** and describe the security concept it opposes.                                                      | Kerckhoffs' Principle states that the cryptographic system must remain secure even if the adversary knows all the details about the algorithms and their implementation; security must be based entirely on the secret keys. This principle represents the opposite approach to "**security through obscurity**".                                                                                |
| **3.** Explain the **One-Wayness (or Pre-image Resistance)** property of cryptographic hash functions and give a practical application.   | **One-wayness** means that, given a hash value $y$, it is computationally infeasible to find the original input message $x$ such that $h(x) = y$. A primary application is **password storage**, where the hash of a user's password is saved instead of the cleartext password itself; this prevents the password from being discovered even if the stored hash value is exposed.               |
| **4.** Distinguish between a **Chosen-Plaintext Attack (CPA)** and a **Known-Plaintext Attack (KPA)** in terms of the adversary's access. | In a **Known-Plaintext Attack (KPA)**, the adversary obtains pairs of plaintexts and their corresponding ciphertexts, but the plaintexts are randomly chosen by the source. In a **Chosen-Plaintext Attack (CPA)**, the adversary has the stronger ability to actively **choose the plaintexts** they want encrypted and obtain the corresponding ciphertexts.                                   |
| **5.** Why is **Electronic Codebook (ECB) Mode** considered insecure for encrypting messages longer than one block?                       | ECB mode is highly insecure because **identical plaintext blocks result in identical ciphertext blocks**. This property reveals patterns in the plaintext, making the scheme predictable and vulnerable to cut-and-splice attacks, thus failing to provide CPA-security.                                                                                                                         |

---
## Exam Style Questions
### Scenario-Based Long-Form Questions

#### 1. Auction Bidding Commitment and Hash Function Properties

Alice wishes to participate in a sealed-bid auction using a cryptographic commitment scheme based on a hash function, $h$. She first computes a commitment $C(x) = h(x)$, where $x$ is her bid, and submits $C(x)$ publicly. Later, when bidding closes, she reveals $x$ to prove her original bid.

**Required Analysis:**

1. Identify the three essential properties the hash function $h$ must satisfy to ensure the security and integrity of the bidding process.
2. For each property, explain how its absence would allow a malicious bidder (Eve) or Alice herself to break the auction process (i.e., violate commitment secrecy or integrity).

**Answer and Citation:**

1. The three essential properties the hash function $h$ must satisfy for this commitment scheme are **One-Wayness (OW)**, **Collision Resistance (CR)**, and **Non-Malleability (NM)**.
    
2. **Analysis of Required Properties:**
    
    - **One-Wayness (OW) / Pre-image Resistance:**
        
        - **Purpose:** Ensures the secrecy of the bid. $C(x)$ should not reveal $x$.
        - **Break Scenario:** If the property is absent, an adversary (like another bidder, Eve) could observe Alice's public commitment $C(x)$, invert the hash function to find $x$ (Alice's bid), and then adjust her own bid accordingly to win.
    - **Collision Resistance (CR):**
        
        - **Purpose:** Ensures that Alice cannot open her commitment in multiple ways.
        - **Break Scenario:** If Alice could efficiently find two distinct bids, $x$ (e.g., $100$) and $x'$ (e.g., $1$ billion), such that $h(x) = h(x')$, she could wait until all other bids were revealed. Depending on whether $100$ or $1$ billion would be more beneficial to her (e.g., depending on whether she won or lost), she could then dishonestly claim that her commitment was for the advantageous bid, thereby breaking the system.
    - **Non-Malleability (NM):**
        
        - **Purpose:** Prevents an attacker from modifying or relating their own commitment to Alice's commitment in a predictable way.
        - **Break Scenario:** If the function were malleable, an attacker (Eve) who sees Alice's commitment $C(x)$ might be able to computationally produce a commitment $C(x')$ corresponding to a related bid $x'$ (e.g., $x' = x + 1$) without knowing $x$ itself. If Eve could successfully submit $C(x')$ (a slightly higher bid), she could use Alice's original commitment to guarantee she wins by a slight margin.

#### 2. Confidentiality and Integrity for Networked Data

A software developer is designing a secure protocol using the AES block cipher (128-bit block size). The application requires the encryption of very long, continuous data streams transmitted over an insecure network, and also requires strong assurance that the message has not been altered by an active network attacker.

**Required Analysis:**

1. Which **mode of operation** (ECB, CBC, or CTR) is most suitable for encrypting this continuous stream data, and what primary operational advantage does it offer in high-speed applications?
2. Explain why this chosen mode of operation, or indeed **any** symmetric encryption mode, is insufficient by itself against an active attacker.
3. What specific cryptographic mechanism must be used _in conjunction with_ the encryption to guarantee data integrity and origin authentication against an active attacker, and how does this mechanism achieve this assurance?

**Answer and Citation:**

1. **Chosen Mode of Operation:**
    
    - **Counter (CTR) Mode** is the most suitable mode for continuous data streams and high-speed applications.
    - **Advantage:** CTR mode converts the block cipher into a stream cipher by generating a keystream independently for each block. This allows the encryption and decryption processes to be **highly parallelized** (or processed independently), enabling faster processing on systems with multiple cores or high-speed data links.
2. **Insufficiency of Encryption Alone:**
    
    - Encryption modes like CTR or CBC are designed primarily to provide **confidentiality** (or eavesdropping security).
    - They are insufficient against an **active attacker** because they do not protect message **integrity** or **authenticity**. An active attacker can tamper with the encrypted traffic in the network, alter the ciphertext, or inject new messages without being detected by the decryption process alone. For example, in stream ciphers, an attacker can flip bits in the ciphertext, causing predictable changes in the decrypted plaintext, which destroys integrity.
3. **Required Integrity Mechanism:**
    
    - The mechanism required is a **Message Authentication Code (MAC)**. MACs are the standard symmetric key technique used to guarantee data **integrity** and message **authentication**.
    - **How MACs Provide Assurance:** A MAC uses a **shared secret key** ($k$) to calculate a tag ($\text{tag}_k(m)$) for the message. Only parties possessing this secret key can generate a valid tag. The receiver re-computes the MAC using the same secret key and compares it to the received tag. If the MACs match, the receiver is assured that the message has not been modified (Integrity) and that it originated from a party holding the shared secret key (Data Origin Authentication). A common implementation derived from hash functions is **HMAC**. | |