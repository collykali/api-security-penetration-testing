# HexStrike AI MCP Server & Claude Desktop Integration Lab

## Objective
Integrate the HexStrike AI Model Context Protocol (MCP) server (`v6.0.0`) with Claude Desktop on Kali Linux to enable AI-assisted cybersecurity reconnaissance and tool orchestration.

## Environment & Configuration
- **OS:** Kali Linux (Oracle VirtualBox)
- **Local MCP Server:** `hexstrike_server.py` running on `http://127.0.0.1:8888` inside Python virtual environment (`~/hexstrike-ai/hexstrike-env`)
- **Client Bridge:** `~/.config/Claude/claude_desktop_config.json` configured to execute `hexstrike_mcp.py` via stdio
- **Launch Flags:** `claude-desktop-unofficial --no-sandbox --disable-gpu`

## Verification Summary
- Connected `hexstrike-ai` under Claude Desktop Connectors.
- Executed live `Server health` MCP tool call with human-in-the-loop approval.
- Verified 16 installed security binaries including `nmap`, `wafw00f`, `theharvester`, `httpx`, `burpsuite`, `zaproxy`, `wireshark`, and `postman`.
