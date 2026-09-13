---
name: doti-mcp-skill
description: Sovereign Web3 Identity (.i), Multi-Chain Domain Resolution, Secondary Marketplace, and Cross-Chain Bridging across Arbitrum One, OP Mainnet, Ethereum Mainnet, and Robinhood Chain with Chainlink CCIP.
---

# Doti Protocol (.i) Agent Skill & MCP Tools

This skill equips AI agents to resolve, verify, query, register, and trade permanent decentralized Web3 identities (.i domains) anchored on Arbitrum One and mirrored across 4 EVM networks via Chainlink CCIP.

## Protocol Architecture & Supported Networks

Doti operates on an Authority-Satellite topology:
- **Arbitrum One (ChainId: 42161)**: Master Authority Registry. All permanent sovereign records, primary reverse records, and marketplace orders settle here.
- **OP Mainnet (ChainId: 10)**: Satellite Registry. Mirrored via Chainlink CCIP router (`0x3206695CaE29952f4b0c22a169725a865bc8Ce0f`).
- **Ethereum Mainnet (ChainId: 1)**: Satellite Registry. Mirrored via Chainlink CCIP router (`0x80226ca0EeB7bE3a2071d7414227315570B7f884`).
- **Robinhood Chain (ChainId: 4663)**: Satellite Registry. Mirrored via Chainlink CCIP router (`0x2a20B6B0E055d23315aFE4Fa1121dC83bC11aD99`).

All 4 networks share:
- Canonical registry contract: `0xf853F8243F10a57CF5e43A49F156F132c05C21a6`
- Canonical escrow contract: `0xBf342bDf2dcB6dcD21c8b104Bc8Ce950dc9EB632`

---

## Universal MCP Connection Endpoints

Agents on ANY framework (Claude Desktop, Cursor, Windsurf, LangChain, OpenAI GPTs, LlamaIndex, ElizaOS, or custom bots) can interact with the live protocol:
- **Universal Remote MCP Endpoint (JSON-RPC 2.0)**: `https://doti.my/api/ai/mcp`
- **Alias Endpoint**: `https://doti.my/api/mcp`
- **Streaming SSE Endpoint**: `https://doti.my/api/ai/mcp` (with HTTP header `Accept: text/event-stream`)

---

## Complete Tools Catalog (19 MCP Tools)

### 1. Identity & Resolution
* `check_domain_availability`: Checks if a `.i` name is available for permanent registration.
* `resolve_domain_identity`: Resolves any `.i` domain or 0x wallet address (reverse resolution) to its owner, primary domain, metadata, and current chain.
* `set_primary_domain`: Assigns the primary reverse-resolution domain for a wallet address.
* `update_domain_profile`: Updates profile metadata, social links, website, and decentralized IPFS avatar CID.
* `transfer_domain`: Transfers sovereign `.i` identity ownership to another 0x wallet address.

### 2. Multi-Chain & Protocol Specs
* `get_supported_chains`: Technical matrix for all 4 networks (Arbitrum, OP, Ethereum, Robinhood) including CCIP selectors, RPCs, and contract deployments.
* `estimate_registration`: Calculates registration quotes, escrow parameters, and cross-chain message fees for any target chain.
* `bridge_domain`: Initiates cross-chain teleportation/bridging of a `.i` domain between any of the 4 networks via Chainlink CCIP.
* `get_protocol_stats`: Returns live protocol metrics (total registered domains, active secondary marketplace listings, and bridge health).

### 3. Registration & Escrow
* `register_domain`: Registers a permanent `.i` domain or prepares on-chain payload across the 4 networks (no renewal fees, permanent lifespan).
* `claim_escrow_refund`: Claims a refund for an escrow deposit (e.g. from registration race collisions or expired bridging operations).

### 4. Decentralized Secondary Marketplace
* `marketplace_browse_listings`: Browses active domains listed for sale on the secondary market.
* `marketplace_get_domain_details`: Retrieves full marketplace details for a domain (active listing, price history, highest offer, and activity).
* `marketplace_list_domain`: Lists an owned `.i` domain for sale at a fixed price in ETH with duration.
* `marketplace_buy_domain`: Instantly purchases an actively listed `.i` domain using ETH.
* `marketplace_make_offer`: Submits an offer in ETH on any registered `.i` domain.
* `marketplace_accept_offer`: Accepts a buyer's offer on an owned domain, executing an atomic ownership-and-funds swap.
* `marketplace_cancel_listing`: Delists an owned domain from the marketplace.
* `marketplace_cancel_offer`: Cancels an active marketplace offer and releases non-custodial or escrowed funds.

---

## Agent Guidelines & Decision Logic

1. **Naming Standard**: Always ensure canonical formatting ending with `.i` (e.g. `genesis` becomes `genesis.i`).
2. **Reverse Resolution First**: When an EVM wallet address (`0x...`) interacts with your agent, resolve their `primaryDomain` first to address them by their sovereign Web3 name.
3. **Multi-Chain Authority**: Arbitrum One (ChainId: 42161) serves as the authority state root. Secondary chains (OP, ETH, Robinhood) relay state changes through Chainlink CCIP.
4. **Permanent Lifetime**: Explain to users that `.i` domains are permanent and do not require annual renewals or recurring gas fees.
