### **Key Cryptographic Hash Functions & Integrity Formulas Summary**
*(Complete mathematical reference – every formula and quantitative result that appears or is derived in MOOC 4)*

#### 1. Cryptographic Hash Function – Core Properties & Security Levels

| Property                  | Definition                                                                 | Brute-force complexity (2025)                  |
|---------------------------|---------------------------------------------------------------------------|------------------------------------------------|
| Preimage resistance       | Given h, find m such that H(m) = h                                        | ≈ 2ⁿ operations                                |
| 2nd preimage resistance   | Given m₁, find m₂ ≠ m₁ with H(m₂) = H(m₁)                                 | ≈ 2ⁿ operations                                |
| Strong collision resistance| Find any m₁ ≠ m₂ such that H(m₁) = H(m₂)                                 | ≈ 2ⁿ/² (Birthday paradox)                      |

**Current secure output lengths (2025 standards)**
| Desired security | Minimum hash output size (n) | Examples                     |
|------------------|------------------------------|------------------------------|
| 128-bit          | 256 bits                     | SHA-256, SHA3-256            |
| 192-bit          | 384 bits                     | SHA-384, SHA3-384            |
| 256-bit          | 512 bits                     | SHA-512, SHA3-512            |
| Collision-only   | ≥ 256 bits mandatory         | SHA-1 (160 bits) = broken    |
| Legacy (broken)  | 128–160 bits                 | MD5, SHA-1                   |

**Birthday attack effort**  
Probability ≥ 50% of collision after ≈ 2ⁿ/² hash computations  
→ 128-bit hash → 2⁶⁴ ≈ 1.8 × 10¹⁹ attempts (feasible with massive resources)  
→ 256-bit hash → 2¹²⁸ attempts (completely infeasible)

#### 2. General Hash Function Structure (Merkle-Damgård)

H(M) = CVₙ where:  
CV₀ = IV (fixed public initial value)  
CVᵢ = f(CVᵢ₋₁, Mᵢ)      (compression function f)  
Last block Mₙ includes length padding (MD-strengthening)

#### 3. Hash Chain (used in S/Key, Lamport OTP)

Notation: H⁽ᵏ⁾(x) = H(H(...H(x)...))  – k times  
User stores H⁽¹⁰⁰⁾(x) on server  
Login n: send H⁽¹⁰⁰⁻ⁿ⁾(x)  
Server verifies: H(received value) = previously stored value  
Then stores received value for next login

#### 4. Merkle Tree (Hash Tree)

Leaf nodes:      hᵢ = H(dataᵢ)  
Internal node:   h_parent = H(h_left ‖ h_right)  
Root = Merkle root  
Verification of one block needs only log₂(N) sibling hashes

#### 5. Message Authentication Code (MAC) – Security

MAC(K, M) = T (tag)  
Security goal: attacker cannot forge a valid (M′, T′) without K

| Attack type               | Effort required                                 |
|---------------------------|-------------------------------------------------|
| Key recovery              | ≈ 2ᵏ (k = key length)                          |
| Existential forgery       | min(2ᵏ, 2ⁿ)                                     |
| Recommended (2025)        | k ≥ 128 bits and n ≥ 128 bits (preferably 256) |

#### 6. Standard MAC Constructions

| MAC          | Underlying primitive | Output size | Formula (simplified)                              | Status (2025) |
|--------------|----------------------|-------------|---------------------------------------------------|---------------|
| HMAC         | Any hash H           | = n         | HMAC(K,m) = H((K⊕opad) ‖ H((K⊕ipad) ‖ m))          | Secure        |
| CMAC (NIST)  | Block cipher (AES)   | ≤ block     | AES-based one-key TDEA or AES with key derivation | Secure        |
| DAA (old)    | DES-CBC              | 16–64 bits  | Last block of DES-CBC encryption                  | Broken        |

#### 7. Digital Signature – Generic Construction

**Signing** (Alice)  
s = Sign_{SK_A}(H(m)) = [H(m)]^{d_A} mod n          (RSA example)  
or using DSA/ECDSA scheme  
Send: (m, s)

**Verification** (anyone with PK_A)  
Verify: H(m) == Decrypt_{PK_A}(s)  
or verify signature equation

**Standard real-world schemes (2025)**
| Scheme   | Security (bits) | Signature size | Recommended |
|----------|-----------------|----------------|-------------|
| RSA-PSS  | 128–256         | ≈ modulus      | Yes         |
| ECDSA    | 128–256         | 2×curve size   | Yes         |
| Ed25519  | ≈128            | 64 bytes       | Widely used |
| Dilithium (post-quantum) | 128–256 | 2–5 KB         | Future-proof|

#### 8. Bitcoin Mining (Proof-of-Work) – Exact Formula

Block is valid if:  
**SHA256(SHA256(header ‖ nonce)) < target**  
where target = 2²⁵⁶ / difficulty  
→ Current difficulty (2025) requires ≈ 2⁹⁵–2⁹⁶ hash attempts per block on average

#### Quick Reference Table (2025)

| Primitive        | Minimum safe size today | Broken examples          |
|------------------|--------------------------|--------------------------|
| Hash output      | 256 bits                 | MD5 (128), SHA-1 (160)   |
| MAC key & tag    | 128 bits (256 preferred) | DES-MAC, 64-bit MACs     |
| RSA signature    | 3072–4096 bits           | 1024-bit and below       |
| ECC/EdDSA        | 256 bits                 | –                        |

These are **all** the formulas, quantitative security levels, and mathematical constructions explicitly presented or derived throughout **MOOC 4: Cryptographic Hash and Integrity Protection**. Keep this summary as your definitive cheat-sheet for exams and real-world design decisions.

</DOCUMENT>
