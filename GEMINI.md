# Mathematics of Cryptography - Project Overview

This directory contains a comprehensive set of educational resources focused on the mathematical foundations of cryptography, specifically centered around the Advanced Encryption Standard (AES) and Galois Fields.

## Directory Overview

The project is structured as a series of 36 tutorials, each accompanied by a workbook. The materials are provided as high-quality, self-contained HTML files that utilize MathJax for mathematical notation and custom CSS for a polished, readable aesthetic.

### Key Content Areas:
1.  **Foundations (Tutorials 1-7):** Number bases (binary, hex), bitwise operations, modular arithmetic, and the Euclidean algorithms.
2.  **Galois Fields (Tutorials 8-13):** Polynomial arithmetic over GF(2), irreducible polynomials, and multiplication/inverses in GF(2^8).
3.  **AES Components (Tutorials 14-21):** S-Box construction, linear transformations, diffusion, MixColumns, and round structure.
4.  **AES Flow (Tutorials 22-25):** Full encryption/decryption walkthroughs and the Key Schedule.
5.  **Block Cipher Modes (Tutorials 26-30):** ECB, CBC, CTR, padding, and AEAD.
6.  **AES-GCM (Tutorials 31-36):** GHASH, multiplication in GF(2^128), and nonce/IV misuse resistance.

## Key Files

-   **`Mathematics Of Cryptography Tutorial Roadmap.pdf`**: Provides a high-level overview and sequencing of the curriculum.
-   **`tutorial_##_..._html.html`**: The primary lesson content for each topic.
-   **`tutorial_##_..._workbook_html.html`**: Interactive or practice-oriented workbooks corresponding to each tutorial.
-   **`Galois Field Multiplication Gentle Tutorial (5).pdf`**: A supplementary deep-dive into Galois Field multiplication.

## Usage

These files are intended to be viewed in a web browser. Each tutorial is self-contained. 

-   **Learning Path:** Follow the numerical order from `tutorial_01` to `tutorial_36`.
-   **Mathematical Notation:** Ensure an internet connection is available when opening HTML files to load the MathJax library from the CDN for proper rendering of equations.
-   **Future Interactions:** When asking about specific cryptographic concepts, reference the relevant tutorial number to help the AI agent provide context-specific answers.
