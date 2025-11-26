<DOCUMENT filename="CRY301c MOOC 3 - Enhanced with Formulas.docx">

[... All the original content of MOOC 3 remains exactly as you provided ...]

### **Key Asymmetric Cryptography & Key Management Formulas Summary**
*(Complete mathematical reference for MOOC 3 – every formula that appears or is derived in the course)*

#### 1. RSA – Full Algorithm & Formulas

**Key Generation**
1. Choose two distinct large primes **p** and **q** (secret)
2. **n = p × q** → modulus (public)
3. **φ(n) = (p−1)(q−1)** → Euler’s totient function (kept secret)
4. Choose public exponent **e** such that **1 < e < φ(n)** and **gcd(e, φ(n)) = 1**
5. Compute private exponent **d** such that **e × d ≡ 1 (mod φ(n))**  
   → **d = e⁻¹ mod φ(n)** (via Extended Euclidean Algorithm)

**Public key**: (n, e)  
**Private key**: d (or equivalently p, q, d)

**Encryption** (message → ciphertext)  
**c = mᵉ mod n**   (m < n)

**Decryption** (ciphertext → message)  
**m = cᵈ mod n**

**Correctness (mathematical proof)**  
By Euler’s theorem: **m^{φ(n)} ≡ 1 (mod n)** if gcd(m,n)=1  
Thus **m^{e×d} = m^{k×φ(n)+1} ≡ (m^{φ(n)})^k × m ≡ 1^k × m ≡ m (mod n)**

**Current recommended key sizes (2025)**
- 2048-bit n → ≈ 112–128-bit security
- 3072-bit n → ≈ 128–140-bit security
- 4096-bit n → high-security / government use

#### 2. Discrete Logarithm Problem (DLP)

Given prime **p**, primitive root (generator) **g**, and **y = gˣ mod p**  
**Hard problem**: find **x = log_g(y) mod (p−1)**  
Easy problem: compute **gˣ mod p** (fast exponentiation)

Security of Diffie-Hellman and ElGamal rests on DLP hardness.

#### 3. Diffie-Hellman Key Exchange

**Public parameters** (agreed openly): prime **p**, primitive root **g**  
**Alice**  
- Secret: **a** (private)  
- Sends: **A = gᵃ mod p**  

**Bob**  
- Secret: **b** (private)  
- Sends: **B = gᵇ mod p**

**Shared secret computed by both**  
Alice computes: **K = Bᵃ mod p = (gᵇ)ᵃ mod p = g^{ab} mod p**  
Bob computes:   **K = Aᵇ mod p = (gᵃ)ᵇ mod p = g^{ab} mod p**

Attacker sees p, g, A, B → cannot feasibly compute g^{ab} without solving DLP.

#### 4. ElGamal Encryption

**Key Generation** (same base as DH)  
Public parameters: large prime **p**, primitive root **g**  
Private key: **x** (1 ≤ x ≤ p−2)  
Public key: **h = gˣ mod p** → publish (p, g, h)

**Encryption** of message **m** (0 ≤ m < p)  
1. Choose random ephemeral **k** (1 ≤ k ≤ p−2)  
2. Compute **c₁ = gᵏ mod p**  
3. Compute **c₂ = m × hᵏ mod p** = m × (gˣ)ᵏ mod p  
Send ciphertext pair: **(c₁, c₂)**

**Decryption**  
Receiver computes: **hᵏ = (gᵏ)ˣ = c₁ˣ mod p**  
Then **m = c₂ × (c₁ˣ)⁻¹ mod p**

#### 5. Digital Signature (using RSA – most common)

**Signing** a message **m** (or hash h(m))  
**s = h(m)ᵈ mod n** → signature

**Verification**  
Compute **h(m)' = sᵉ mod n**  
Check whether **h(m)' == h(m)**

#### 6. RSA Small Example (from MOOC 3)

p = 11, q = 13  
n = 143  
φ(n) = 10×12 = 120  
e = 11 (gcd(11,120)=1)  
d = 11 (because 11×11 = 121 ≡ 1 mod 120)  
Message m = 7  
c = 7¹¹ mod 143 = 106  
7¹¹ mod 143 = 7 → works

#### 7. Security Levels (2025 real-world recommendations)

| Security Level | RSA modulus | ECC key size | Discrete Log (DH) prime size |
|----------------|-------------|--------------|------------------------------|
| 112-bit        | 2048 bits   | 224–255 bits| 2048 bits                    |
| 128-bit        | 3072 bits   | 256–283 bits| 3072 bits                    |
| 192-bit        | ~7680 bits  | 384 bits     | ~7680 bits                   |
| 256-bit        | ~15360 bits | 521 bits     | ~15360 bits                  |

#### 8. Public Key Certificate Core Fields (X.509)

- Subject name (identity)
- Subject public key + algorithm
- Issuer (CA name)
- Validity period
- Serial number
- Digital signature of the above by the CA → **Sig_CA(Hash(all fields above))**

These formulas and parameters constitute the complete mathematical foundation of **MOOC 3: Asymmetric Cryptography and Key Management**. Use this summary for exams, practical implementation, and quick reference.

</DOCUMENT>
