### **Key Cryptography & Information Theory Formulas Summary**
*(Added for quick reference – contains every specific formula appearing or derived in MOOC 1)*

#### 1. Information Entropy (Shannon Entropy)

**a. Uniform distribution (all outcomes equally likely)**  
When there are **N** equally probable outcomes:  
**H = log₂(N)** bits  
- Example: fair coin → N=2 → H = log₂(2) = **1 bit**  
- Example: 4 weather states in Gotham (S, R, W, C) → N=4 → H = log₂(4) = **2 bits**  
- For **m** independent identical events: **H_total = m × log₂(N)**

**b. General (non-uniform) distribution**  
**H = − Σ (pᵢ × log₂(pᵢ))**  where pᵢ is the probability of outcome i  
(Shannon’s 1948 formula)  
- Colorado Springs example:  
  P(S)=0.5, P(C)=0.25, P(R)=0.125, P(W)=0.125  
  H = −[0.5 log₂0.5 + 0.25 log₂0.25 + 0.125 log₂0.125 + 0.125 log₂0.125] = **1.75 bits**

**c. Maximum entropy**  
Entropy is maximized when the distribution is uniform:  
**H_max = log₂(N)**

#### 2. Brute-Force (Key Search) Complexity

- Number of possible keys for a key of length **n** bits (uniformly random):  
  **|K| = 2ⁿ**
- Worst-case trials in brute-force attack: **2ⁿ**
- Average-case trials (if attacker stops when found): **2ⁿ⁻¹**
- Example calculations from the course:  
  - 56-bit key → ~2⁵⁶ ≈ 7.2 × 10¹⁷ keys  
  - At 10⁷ decryptions/sec → ~114 years on average  
  - 128-bit key → 2¹²⁸ ≈ 3.4 × 10³⁸ keys → 5.4 × 10¹⁷ years

#### 3. Perfect Secrecy (Shannon’s Condition)

A cryptosystem has **perfect secrecy** if and only if:  
- The key is at least as long as the plaintext  
- The key is truly random  
- The key is used only once (One-Time Pad requirement)  

Formally:  
**H(M | C) = H(M)**  
(Entropy of the message given the ciphertext equals entropy of the message alone → ciphertext reveals no information about plaintext)

#### 4. Key Entropy and Security Relationship

Effective key entropy from attacker’s perspective:  
**H(K)** = expected bits of uncertainty in the key  
Higher H(K) → stronger resistance against brute-force and most other attacks.

#### 5. Computational Security (Practical Security)

Security level is often expressed as resisting an attacker with **2^k** operations:  
- 2⁸⁰ operations ≈ 80-bit security (formerly considered safe)  
- 2¹²⁸ operations ≈ 128-bit security (current standard for symmetric ciphers, e.g., AES-128)  
- 2²⁵⁶ operations ≈ 256-bit security (AES-256, post-quantum readiness)

#### Quick Reference Table (from the MOOC examples)

| Key length (bits) | Possible keys | Approx. brute-force time (10⁷ dec/sec) | Security comment            |
|-------------------|---------------|----------------------------------------|-----------------------------|
| 2                 | 4             | microseconds                           | Toy example                 |
| 56 (old DES)      | 7.2 × 10¹⁷    | ~114 years                             | Broken (1990s–2000s)        |
| 128 (AES-128)     | 3.4 × 10³⁸    | 5.4 × 10¹⁷ years                       | Secure today                |
| 256 (AES-256)     | 1.1 × 10⁷⁷    | astronomical                           | Future-proof                |

These are all the specific mathematical formulas and quantitative relationships explicitly presented or derived in **MOOC 1: Cryptography and Information Theory**. They serve as the core mathematical toolkit for the rest of the course.
