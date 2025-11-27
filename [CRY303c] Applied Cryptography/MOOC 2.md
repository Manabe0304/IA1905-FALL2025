### **Key Symmetric Cryptography Formulas Summary**
*(Complete reference of every mathematical formula and quantitative result explicitly mentioned or derived in MOOC 2)*

#### 1. Caesar Cipher
- Alphabet size: **|A| = 26** (English uppercase)
- Encryption: **c = (p + k) mod 26**
- Decryption: **p = (c − k) mod 26**
- Number of distinct keys: **25** (k = 0 is identity, usually excluded)

#### 2. Monoalphabetic Substitution Cipher
- Key space size (all possible letter permutations): **26! ≈ 4.03 × 10²⁶**
- Still vulnerable to frequency analysis (preserves letter frequencies)

#### 3. Vigenère (Polyalphabetic) Cipher
- Key repeated to match plaintext length
- Encryption (letter level): **cᵢ = (pᵢ + kᵢ mod period) mod 26**
- Effective key space: **26^m** where **m** = key length
  - Example: “LEMON” (m=5) → 26⁵ = 11,881,376 keys

#### 4. General Transposition / Permutation Cipher
- For block length **n**, number of possible keys = **n!**
  - n=4 → 24 keys  
  - n=6 → 720 keys  
  - n=8 → 40,320 keys

#### 5. Ideal Block Cipher
- Block size: **n** bits → 2ⁿ possible plaintext blocks
- Required number of distinct keys for perfect (one-to-one) mapping: **(2ⁿ)!**
- Minimum key length to index all possible mappings:  
  **log₂((2ⁿ)!) ≈ n × 2ⁿ bits** (using Stirling’s approximation)  
  → Impractical even for n=64 (~10²¹ bits)

#### 6. Feistel Cipher (General Structure)
- Block size: usually **2 × m** bits (e.g., DES: 64 bits → m=32)
- After **r** rounds:  
  Final Left  = Initial Right  
  Final Right = Initial Left ⊕ F-sequence
- Crucial property: **Decryption uses same structure, only subkeys reversed**

#### 7. Data Encryption Standard (DES)
- Block size: **64 bits**
- Effective key size: **56 bits** (64-bit key input, 8 parity bits dropped)
- Number of rounds: **16**
- Subkey size per round: **48 bits**
- Brute-force complexity: **2⁵⁶ ≈ 7.2 × 10¹⁶ keys**
  - Average trials: **2⁵⁵**
  - 1998: cracked in ~3 days (EFF DES Cracker)
- S-boxes: 8 × (6→4 bit) nonlinear substitution tables

#### 8. Double-DES & Meet-in-the-Middle Attack
- Naive expectation: 112-bit security (2 × 56)
- Actual security via MitM: **≈ 2⁵⁶** operations + 2⁵⁶ storage
- Formula:  
  **C = E_{K2}(E_{K1}(P))**  
  Attack: Precompute **E_{K1}(P)** for all K1, then try decrypting C with all K2 → collision at intermediate value

#### 9. Triple-DES (3DES)
- Standard form (Keying Option 2): **E_{K1} → D_{K2} → E_{K1}** (112-bit effective key)
- Full 3 independent keys: 168-bit key
- Meet-in-the-Middle resistance: **≈ 2¹¹²** operations
- Still used in legacy systems (e.g., EMV banking)

#### 10. Advanced Encryption Standard (AES)
| Variant     | Key Length | Block Size | Rounds |
|-------------|------------|------------|--------|
| AES-128     | 128 bits   | 128 bits   | 10     |
| AES-192     | 192 bits   | 128 bits   | 12     |
| AES-256     | 256 bits   | 128 bits   | 14     |

- State: 4×4 byte matrix (16 bytes = 128 bits)
- Round operations: SubBytes → ShiftRows → MixColumns → AddRoundKey
- Brute-force complexity: **2¹²⁸**, **2¹⁹²**, **2²⁵⁶** respectively (currently unbreakable)

#### 11. Block Cipher Modes of Operation – Core Formulas

| Mode  | Encryption Formula                          | Decryption Formula                          | IV/Nonce Required? | Error Propagation | Parallelizable? |
|-------|---------------------------------------------|---------------------------------------------|---------------------|-------------------|-----------------|
| ECB   | Cᵢ = E_K(Pᵢ)                                | Pᵢ = D_K(Cᵢ)                                | No                  | None              | Yes             |
| CBC   | Cᵢ = E_K(Pᵢ ⊕ C_{i-1})   (C₀ = IV)          | Pᵢ = D_K(Cᵢ) ⊕ C_{i-1}                       | Yes (secret/random) | 1 + next block    | No (enc/dec)    |
| CFB   | Cᵢ = Pᵢ ⊕ E_K(C_{i-1})                        | Pᵢ = Cᵢ ⊕ E_K(C_{i-1})                       | Yes                 | Current + next    | No              |
| OFB   | Oᵢ = E_K(O_{i-1}),  Cᵢ = Pᵢ ⊕ Oᵢ               | Pᵢ = Cᵢ ⊕ Oᵢ (same stream)                  | Yes (nonce)         | Only current      | Yes (precompute)|
| CTR   | Cᵢ = Pᵢ ⊕ E_K(Nonce || Counter + i)           | Pᵢ = Cᵢ ⊕ E_K(Nonce || Counter + i)         | Yes (unique nonce)  | Only current      | Yes (fully)     |

#### Quick Security Level Reference (2025 standards)
| Security Level | Minimum Symmetric Key Size | Example Use Today                   |
|----------------|----------------------------|-------------------------------------|
| 80-bit         | 160 bits (broken)          | Legacy only                         |
| 112-bit        | 2×56-bit (3DES)            | Legacy banking                      |
| 128-bit        | AES-128                    | Standard (TLS, disk encryption)     |
| 256-bit        | AES-256                    | High-security, post-quantum ready   |

These formulas and values represent the complete mathematical foundation of **MOOC 2: Symmetric Cryptography**. Keep this summary handy for exams, exercises, and understanding modern cipher design.
