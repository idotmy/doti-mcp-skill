# Doti Protocol (.i) — Universal MCP Server & Agent Skill

[![Model Context Protocol](https://img.shields.io/badge/MCP-Standard%20v2024--11--05-blue.svg)](https://modelcontextprotocol.io)
[![Universal Compatibility](https://img.shields.io/badge/Compatibility-Claude%20%7C%20Cursor%20%7C%20Windsurf%20%7C%20LangChain%20%7C%20OpenAI-success.svg)](#client-setup-instructions)
[![Arbitrum One](https://img.shields.io/badge/Authority%20Chain-Arbitrum%20One%20(42161)-sky.svg)](https://arbiscan.io)
[![Chainlink CCIP](https://img.shields.io/badge/Bridging-Chainlink%20CCIP%20v1.5-375BD2.svg)](https://chain.link/ccip)
[![Chains](https://img.shields.io/badge/Supported%20Chains-4%20EVM%20Networks-green.svg)](#supported-networks)

Sovereign Web3 Identity (.i) and Multi-Chain Domain Name Service across **Arbitrum One**, **OP Mainnet**, **Ethereum Mainnet**, and **Robinhood Chain** with **Chainlink CCIP**.

This repository implements the open **Model Context Protocol (MCP)** specification. It works with **ANY** AI platform, IDE, agent framework, or client supporting MCP or JSON-RPC 2.0.

---

## 🌐 Live MCP Endpoints

Connect any MCP client or AI agent directly to the cloud server:

* **Production MCP Endpoint:**
  ```
  https://doti.my/api/ai/mcp
  ```
* **Alias Endpoint:**
  ```
  https://doti.my/api/mcp
  ```
* **Protocol Transport:** HTTP JSON-RPC 2.0 & Server-Sent Events (SSE)

---

## ⛓️ Supported Networks

| Network | Chain ID | Role | CCIP Selector | Canonical Contract | Escrow Contract |
|---|---|---|---|---|---|
| **Arbitrum One** | `42161` | Authority Anchor | `4949039107694359620` | `0xf853F8243F10a57CF5e43A49F156F132c05C21a6` | `0xBf342bDf2dcB6dcD21c8b104Bc8Ce950dc9EB632` |
| **OP Mainnet** | `10` | Satellite (Mirrored) | `3734403246176062136` | `0xf853F8243F10a57CF5e43A49F156F132c05C21a6` | `0xBf342bDf2dcB6dcD21c8b104Bc8Ce950dc9EB632` |
| **Ethereum Mainnet** | `1` | Satellite (Mirrored) | `5009297550715157269` | `0xf853F8243F10a57CF5e43A49F156F132c05C21a6` | `0xBf342bDf2dcB6dcD21c8b104Bc8Ce950dc9EB632` |
| **Robinhood Chain** | `4663` | Satellite (Mirrored) | `6180753054346818345` | `0xf853F8243F10a57CF5e43A49F156F132c05C21a6` | `0xBf342bDf2dcB6dcD21c8b104Bc8Ce950dc9EB632` |

---

## 🚀 Universal Client Setup

### 1. Claude Desktop
Add to your `claude_desktop_config.json`:
```json
{
  "mcpServers": {
    "doti": {
      "type": "http",
      "url": "https://doti.my/api/ai/mcp"
    }
  }
}
```

### 2. Cursor IDE & Windsurf
Add to your `.cursor/mcp.json` or project MCP settings:
```json
{
  "mcpServers": {
    "doti": {
      "type": "http",
      "url": "https://doti.my/api/ai/mcp"
    }
  }
}
```

### 3. Python & LangChain / LangGraph
```python
import httpx

payload = {
    "jsonrpc": "2.0",
    "id": 1,
    "method": "tools/call",
    "params": {
        "name": "check_domain_availability",
        "arguments": {"domainName": "agent.i"}
    }
}
response = httpx.post("https://doti.my/api/ai/mcp", json=payload)
print(response.json()["result"]["content"][0]["text"])
```

### 4. Direct cURL / REST API
```bash
curl -X POST https://doti.my/api/ai/mcp \
  -H "Content-Type: application/json" \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/call","params":{"name":"resolve_domain_identity","arguments":{"identifier":"genesis.i"}}}'
```

### 5. Optional Community Registries
This server conforms to standard remote MCP specifications and can be registered on any directory (Glama, Smithery, OpenMCP, or Pulse) using the remote URL `https://doti.my/api/ai/mcp`.

---

## 🛠️ Complete Tools Catalog (19 MCP Tools)

| Category | Tool Name | Description |
|---|---|---|
| **Identity** | `check_domain_availability` | Check if a `.i` name is available for permanent registration. |
| **Identity** | `resolve_domain_identity` | Forward & reverse lookup for any `.i` domain or 0x address. |
| **Identity** | `set_primary_domain` | Set default reverse domain for a wallet address. |
| **Identity** | `update_domain_profile` | Update profile metadata, social links, and IPFS avatar CID. |
| **Identity** | `transfer_domain` | Transfer sovereign ownership to another 0x address. |
| **Multi-Chain** | `get_supported_chains` | Retrieve configuration for Arbitrum, OP, Ethereum, Robinhood. |
| **Multi-Chain** | `estimate_registration` | Calculate registration quote and CCIP message fees. |
| **Multi-Chain** | `bridge_domain` | Teleport domain across the 4 networks using Chainlink CCIP. |
| **Multi-Chain** | `get_protocol_stats` | Live on-chain metrics, registered domains, and volume. |
| **Registration**| `register_domain` | Mint or prepare payload for permanent .i registration. |
| **Registration**| `claim_escrow_refund` | Claim refund from escrow (collisions or expired bridge). |
| **Marketplace** | `marketplace_browse_listings` | Browse active domains listed on the secondary market. |
| **Marketplace** | `marketplace_get_domain_details`| View listing details, floor, bids, and sale history. |
| **Marketplace** | `marketplace_list_domain` | List an owned domain for sale at a fixed price in ETH. |
| **Marketplace** | `marketplace_buy_domain` | Instantly buy a listed domain using ETH. |
| **Marketplace** | `marketplace_make_offer` | Submit an ETH offer on any registered domain. |
| **Marketplace** | `marketplace_accept_offer` | Accept a buyer's offer with atomic swap settlement. |
| **Marketplace** | `marketplace_cancel_listing` | Delist an owned domain from the marketplace. |
| **Marketplace** | `marketplace_cancel_offer` | Cancel an active offer and release non-custodial lock. |
