# Protected Password Cracking Lab: John the Ripper, Johnny & Networkwalks

## Objective
Demonstrate offline password recovery on protected PDF files by extracting cryptographic hashes and executing dictionary attacks across three distinct environments: CLI (`John the Ripper`), GUI (`Johnny`), and browser-based utilities (`Networkwalks`).

## Core Cryptographic Principles
- **Encryption vs. Hashing:** Encryption is reversible with a valid key; hashing is a one-way mathematical function producing a fixed-length digest.
- **Dictionary Attack Mechanics:** Password crackers hash candidate words from a wordlist (such as `rockyou.txt`) and compare the resulting digests against the target hash until a match is found.

## Methodologies Executed
1. **John the Ripper (JTR CLI):**
   - Extracted the PDF hash using `pdf2john.pl locked.pdf > hash.txt`.
   - Executed dictionary cracking via `john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt`.
   - Verified recovered credentials with `john --show hash.txt`.
2. **Johnny (JTR GUI):**
   - Configured the `john` binary path in Johnny's settings.
   - Loaded the cleaned `$pdf$...` hash file and ran a graphical dictionary attack with real-time progress tracking.
3. **Networkwalks Browser Utilities:**
   - Extracted the file hash via the **Networkwalks Hash Calculator** and recovered the plaintext password using the **Networkwalks Password Cracker**.

## Defensive Countermeasures
- Enforce high-entropy passwords (14+ characters mixing uppercase, lowercase, digits, and symbols).
- Avoid dictionary words, predictable patterns, or personal identifiers.
- Implement modern slow key-derivation functions and Multi-Factor Authentication (MFA).
