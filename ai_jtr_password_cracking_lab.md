# Optional Module Lab: AI-Assisted JTR Password Cracking (HexStrike MCP + Claude Desktop)

## Objective
Use Claude Desktop connected to the HexStrike AI MCP server (`hexstrike-ai` on `http://localhost:8888`) to verify John the Ripper, inspect file hashes, and crack the password of `/home/collins/Desktop/hash3.networkwalks_flag1.pdf` using the `rockyou.txt` wordlist.

## Environment & Tooling
- **OS:** Kali Linux VM (Oracle VirtualBox)
- **AI Orchestration:** Claude Desktop with `hexstrike-ai` MCP integration
- **Tools:** John the Ripper (`1.9.0-jumbo-1+bleeding-5184bc0`), `pdf2john`, `qpdf`, `/usr/share/wordlists/rockyou.txt`

## Execution Summary
1. **Tool Verification:** Checked John the Ripper availability and build details through HexStrike MCP (`Execute command` / `hexstrike-ai`).
2. **Hash Calculation:** Generated file checksums for `/home/collins/Desktop/hash3.networkwalks_flag1.pdf` (MD5, SHA-1, SHA-256).
3. **Password Cracking:** Extracted the PDF hash via `pdf2john` and ran `john` against `/usr/share/wordlists/rockyou.txt`, recovering the password `password1` and verifying with `john --show --format=PDF` (`1 password hash cracked, 0 left`).
