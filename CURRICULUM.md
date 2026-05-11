# Mathematics of Cryptography: Master Curriculum Guide

This document is the definitive roadmap for the curriculum. It tracks the actual progression of the 76 modules currently implemented in the library.

## Volume 1: Foundations, Finite Fields, and AES
*Focused on reversible transformations, bit-level logic, and the architecture of the world's most trusted block cipher.*

### I. Mathematical Foundations
1.  **Module 01:** Binary, Hexadecimal, and Bases
2.  **Module 02:** Bitwise Operations as Algebra
3.  **Module 03:** Functions as Machines
4.  **Module 04:** Modular Arithmetic
5.  **Module 05:** Multiplicative Inverses Modulo n
6.  **Module 06:** Euclidean Algorithm
7.  **Module 07:** Extended Euclidean Algorithm

### II. Galois Fields & Polynomials
8.  **Module 08:** Bytes as Polynomials
9.  **Module 09:** Polynomial Addition over GF(2)
10. **Module 10:** Polynomial Multiplication over GF(2)
11. **Module 11:** Polynomial Reduction & Irreducible Polynomials
12. **Module 12:** Multiplication in GF(2^8)
13. **Module 13:** Multiplicative Inverses in GF(2^8)

### III. AES Internal Components
14. **Module 14:** S-Box: Inverse plus Affine Transformation
15. **Module 15:** Inverse S-Box and Reversibility
16. **Module 16:** Linear Transformations & Matrices over GF(2)
17. **Module 17:** Diffusion, Branch Number, and Avalanche
18. **Module 18:** MixColumns as Matrix Multiplication
19. **Module 19:** Inverse MixColumns & Decryption Layers
20. **Module 20:** ShiftRows, Bit Permutations, and Mixing
21. **Module 21:** Full Round Structure Synthesis

### IV. AES Encryption & Key Schedule
22. **Module 22:** AES Encryption Flow
23. **Module 23:** AES Decryption Flow
24. **Module 24:** Key Expansion I: Words and RotWord
25. **Module 25:** Key Expansion II: Full Key Schedule

### V. Block Cipher Modes
26. **Module 26:** ECB Mode & Pattern Leaks
27. **Module 27:** CBC Mode, IVs, and Chaining
28. **Module 28:** CTR Mode & Stream Conversion
29. **Module 29:** Padding & Message Length
30. **Module 30:** Authentication (AEAD)

### VI. AES-GCM (Standard Implementation)
31. **Module 31:** GCM: High-Level Overview
32. **Module 32:** GHASH Inputs & Auth Tags
33. **Module 33:** GHASH Multiplication in GF(2^128)
34. **Module 34:** Toy GHASH (Small Field)
35. **Module 35:** Full 128-bit GHASH Patterns
36. **Module 36:** Nonces, IVs, & Misuse Resistance

---

## Volume 2: Hash Functions, MACs, and Integrity Structures
*Focused on one-way functions, data fingerprints, and advanced authenticated encryption designs.*

### VII. Advanced GCM and AEAD Design
37. **Module 37:** AES-GCM-SIV & Synthetic IV Modes
38. **Module 38:** POLYVAL (GHASH's Little-Endian Cousin)
39. **Module 39:** Synthetic IV Construction Step-by-Step
40. **Module 40:** AEAD Design Tradeoffs & Engineering Reality

### VIII. Hash Functions, MACs, & Key Derivation
41. **Module 41:** What is a Cryptographic Hash Function?
42. **Module 42:** Collision & Preimage Resistance
43. **Module 43:** The Birthday Paradox & Hash Length
44. **Module 44:** Toy Hash Functions: Building & Breaking
45. **Module 45:** Compression Functions & Block Hashing
46. **Module 46:** Merkle-Damgård Construction
47. **Module 47:** Padding, Length Encoding & Extension Attacks
48. **Module 48:** HMAC: Safe Keyed Hashing
49. **Module 49:** MACs, Tags & Authentication Games
50. **Module 50:** Authenticated Encryption (Encrypt-then-MAC)
51. **Module 51:** AEAD Case Study: AES-GCM & GHASH Math
52. **Module 52:** Nonce Misuse, Replay, & Context
53. **Module 53:** Key Derivation Functions (KDFs)
54. **Module 54:** Password Hashing & PBKDF2
55. **Module 55:** Randomness, Entropy, & RNGs

---

## Volume 3: Public-Key Cryptography & PKI
*Focused on number theory, asymmetric mathematics, and the trust architecture of the internet.*

### IX. Asymmetric Foundations (RSA & DH)
56. **Module 56:** One-Way Functions, Trapdoors, and Key Exchange
57. **Module 57:** Diffie-Hellman Mathematics: Modular Exponentiation
58. **Module 58:** RSA Mathematics: Primes, Totients, and Inverses
59. **Module 59:** RSA Worked Examples: Encryption & Signatures

### X. Elliptic Curve Cryptography
60. **Module 60:** ECC Points, Addition, and Scalar Multiplication
61. **Module 61:** Elliptic Curve Diffie-Hellman (ECDH) & Signatures

### XI. Public Key Infrastructure (PKI)
62. **Module 62:** Certificates, PKI, and Trust Chains

---

## Volume 4: Protocols & Real-World Engineering
*Focused on how primitives are composed into secure communication systems.*

### XII. Protocol Architecture
63. **Module 63:** TLS Handshake Mathematics
64. **Module 64:** Hash-Based Authentication & HKDF
65. **Module 65:** Randomness: Nonces, Salts, and IVs
66. **Module 66:** AEAD Composition: GCM, ChaCha20-Poly1305

---

## Volume 5: Foundations of Security Analysis
*Focused on formal goals, attack models, and the limits of modern cryptography.*

### XIII. Security Models & Proofs
67. **Module 67:** Formal Security Goals (IND-CPA, IND-CCA)
68. **Module 68:** Attack Models & Reduction Sketches
69. **Module 69:** Complexity, Parameters, and Bits of Security

### XIV. Implementation & Physical Security
70. **Module 70:** Side Channels: Timing Leaks & Constant-Time
71. **Module 71:** Fault Attacks: Glitching & Verification

### XV. Protocol Composition
72. **Module 72:** Secure Primitives, Insecure Systems
73. **Module 73:** Case Studies: TLS, Signal, SSH, Wireguard

---

## Volume 6: Post-Quantum Foundations
*Focused on the mathematical frontier of quantum-resistant structures.*

### XVI. Lattice-Based Cryptography
76. **Module 76:** Lattice Intuition: Vectors, Grids, and Noise
