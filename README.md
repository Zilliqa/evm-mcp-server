# EVM MCP Server

![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)
![EVM Networks](https://img.shields.io/badge/Networks-30+-green)
![TypeScript](https://img.shields.io/badge/TypeScript-5.0+-3178C6)
![Viem](https://img.shields.io/badge/Viem-1.0+-green)

A comprehensive Model Context Protocol (MCP) server that provides blockchain services across multiple EVM-compatible networks. This server enables AI agents to interact with Zilliqa, Ethereum, Optimism, Arbitrum, Base, Polygon, and many other EVM chains with a unified interface.

## 📋 Contents

- [Overview](#overview)
- [Features](#features)
- [Supported Networks](#supported-networks)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Server Configuration](#server-configuration)
- [Usage](#usage)
- [Usage Examples](#usage-examples)
- [API Reference](#api-reference)
  - [Tools](#tools)
  - [Resources](#resources)
- [Security Considerations](#security-considerations)
- [Project Structure](#project-structure)
- [Development](#development)
- [License](#license)

## 🔭 Overview

The MCP EVM Server leverages the Model Context Protocol to provide blockchain services to AI agents. It supports a wide range of services including:

- Reading blockchain state (balances, transactions, blocks, etc.)
- Interacting with smart contracts
- Transferring tokens (native, ERC20, ERC721, ERC1155)
- Querying token metadata and balances
- Chain-specific services across 30+ EVM networks

All services are exposed through a consistent interface of MCP tools and resources, making it easy for AI agents to discover and use blockchain functionality.

## ✨ Features

### Blockchain Data Access

- **Multi-chain support** for 30+ EVM-compatible networks
- **Chain information** including blockNumber, chainId, and RPCs
- **Block data** access by number, hash, or latest
- **Transaction details** and receipts with decoded logs
- **Address balances** for native tokens and all token standards
- **ENS resolution** for human-readable Ethereum addresses (use 'vitalik.eth' instead of '0xd8dA6BF26964aF9D7eEd9e03E53415D37aA96045')

### Token services

- **ERC20 Tokens**
  - Get token metadata (name, symbol, decimals, supply)
  - Check token balances
  - Transfer tokens between addresses
  - Approve spending allowances

- **NFTs (ERC721)**
  - Get collection and token metadata
  - Verify token ownership
  - Transfer NFTs between addresses
  - Retrieve token URIs and count holdings

- **Multi-token standard (ERC1155)**
  - Get token balances and metadata
  - Transfer tokens with quantity
  - Access token URIs

### Smart Contract Interactions

- **Read contract state** through view/pure functions
- **Write services** with private key signing
- **Contract verification** to distinguish from EOAs
- **Event logs** retrieval and filtering

### Comprehensive Transaction Support

- **Native token transfers** across all supported networks
- **Gas estimation** for transaction planning
- **Transaction status** and receipt information
- **Error handling** with descriptive messages

## 🌐 Supported Networks

### Mainnets
- Zilliqa (Default network)
- Ethereum (ETH)
- Optimism (OP)
- Arbitrum (ARB)
- Arbitrum Nova
- Base
- Polygon (MATIC)
- Polygon zkEVM
- Avalanche (AVAX)
- Binance Smart Chain (BSC)
- zkSync Era
- Linea
- Celo
- Gnosis (xDai)
- Fantom (FTM)
- Filecoin (FIL)
- Moonbeam
- Moonriver
- Cronos
- Scroll
- Mantle
- Manta
- Blast
- Fraxtal
- Mode
- Metis
- Kroma
- Zora
- Aurora
- Canto
- Flow
- Lumia

### Testnets
- Sepolia
- Optimism Sepolia
- Arbitrum Sepolia
- Base Sepolia
- Polygon Amoy
- Avalanche Fuji
- BSC Testnet
- zkSync Sepolia
- Linea Sepolia
- Scroll Sepolia
- Mantle Sepolia
- Manta Sepolia
- Blast Sepolia
- Fraxtal Testnet
- Mode Testnet
- Metis Sepolia
- Kroma Sepolia
- Zora Sepolia
- Celo Alfajores
- Goerli
- Holesky
- Flow Testnet
- Filecoin Calibration
- Lumia Testnet

## 🛠️ Prerequisites

- [Bun](https://bun.sh/) 1.0.0 or higher
- Node.js 18.0.0 or higher (if not using Bun)

## 📦 Installation

```bash
# Clone the repository
git clone https://github.com/Zilliqa/evm-mcp-server.git
cd evm-mcp-server

# Install dependencies with Bun
bun install

# Or with npm
npm install
```

## ⚙️ Server Configuration

The server uses the following default configuration:

- **Default Chain ID**: 32769 (Zilliqa Mainnet)
- **Server Port**: 3000
- **Server Host**: 0.0.0.0 (accessible from any network interface)

These values are hard-coded in the application. If you need to modify them, you can edit the following files:

- For chain configuration: `src/core/chains.ts`
- For server configuration: `src/server/http-server.ts`

## 🚀 Usage

### Running the Server Locally

Start the server using stdio mode (for embedding in CLI tools):

```bash
# Start the stdio server
bun start

# Development mode with auto-reload
bun dev
```

Or start the HTTP server with SSE for web applications:

```bash
# Start the HTTP server
bun start:http

# Development mode with auto-reload
bun dev:http
```

### Connecting to the Server

Connect to this MCP server using any MCP-compatible client. For testing and debugging, you can use the [MCP Inspector](https://github.com/modelcontextprotocol/inspector).

### Connecting from Cursor

To connect to the MCP server from Cursor:

1. Open Cursor and go to Settings (gear icon in the bottom left)
2. Click on "Features" in the left sidebar
3. Scroll down to "MCP Servers" section
4. Click "Add new MCP server"
5. Enter the following details:
   - Server name: `evm-mcp-server`
   - Type: `command`
   - Command: `bun run src/index.ts` (use the full env-mcp-server path)

6. Click "Save"

Once connected, you can use the MCP server's capabilities directly within Cursor. The server will appear in the MCP Servers list and can be enabled/disabled as needed.

### Using mcp.json with Cursor

For a more portable configuration that you can share with your team or use across projects, you can create an `.cursor/mcp.json` file in your project's root directory (use the full env-mcp-server path):

```json
{
  "mcpServers": {
    "evm-mcp-server": {
      "command": "bun",
      "args": [
        "run", 
        "src/index.ts", 
      ]
    },
    "evm-mcp-http": {
      "command": "bun",
      "args": [
        "run", 
        "src/server/http-server.ts", 
      ]
    }
  }
}
```

Place this file in your project's `.cursor` directory (create it if it doesn't exist), and Cursor will automatically detect and use these MCP server configurations when working in that project. This approach makes it easy to:

1. Share MCP configurations with your team
2. Version control your MCP setup
3. Use different server configurations for different projects

### Example: HTTP Mode with HTTP Streamable

If you're developing a web application and want to connect to the HTTP server with HTTP Streamable, you can use this configuration:

```json
{
  "mcpServers": {
    "evm-mcp-server": {
      "httpUrl": "http://localhost:3000/mcp"
    }
  }
}
```

This connects directly to the HTTP server's SSE endpoint, which is useful for:
- Web applications that need to connect to the MCP server from the browser
- Environments where running local commands isn't ideal
- Sharing a single MCP server instance among multiple users or applications

To use this configuration:
1. Create a `.cursor` directory in your project root if it doesn't exist
2. Save the above JSON as `mcp.json` in the `.cursor` directory
3. Restart Cursor or open your project
4. Cursor will detect the configuration and offer to enable the server(s)

## Deployment

### Kubernetes

The Kubernetes manifests for deploying this server are located in the `cd/` directory. Environment-specific configurations can be found in `cd/overlays/`.

### Production Environment

A production version of this server is automatically deployed via GitHub Actions pipelines. The deployment is triggered on the creation of a new release and it is accessible at the following URL:

- **URL**: https://evm.mcp.zilliqa.com/mcp

### Configuring the LLM settings

Add this configuration in the LLM local settings to test the MCP server. This is an example for Gemini:

```json
"mcpServers": {
  "evm-mcp-server": {
    "httpUrl": "https://evm.mcp.zilliqa.com/mcp"
  }
}
```

## Usage Examples

### Latest Block

Fetch the latest block from a specified network using the `get_latest_block` tool. This returns full block metadata including hashes, gas data, and consensus certificate fields (where applicable). If a network is not specified if will point to Zilliqa mainnet.

#### Prompt

```
Get the latest block timestamp.
```

#### Direct Tool Invocation (JSON)

```json
{
  "tool": "get_latest_block",
  "arguments": {
    "network": "zilliqa"
  }
}
```

#### Expected Response (Example)

```json
{
  "number": "10411684",
  "view": "0x9ff9c5",
  "hash": "0x233df5d7e60b9947e4b25be0691a690787c89fac76dd55f23f5078c6dcbd4dfc",
  "parentHash": "0xfbbc175435f5d82e6f7a18d261889c01379845904cac20aabca91923921f6f7a",
  "nonce": "0x0000000000000000",
  "sha3Uncles": "0x1dcc4de8dec75d7aab85b567b6ccd41ad312451b948a7413f0a142fd40d49347",
  "transactionsRoot": "0x56e81f171bcc55a6ff8345e692c0f86e5b48e01b996cadc001622fb5e363b421",
  "stateRoot": "0x2808d2a9d0910ef38aa5f87cda28e4d30f8e67047c51d9f40e56d9703fecc66f",
  "receiptsRoot": "0x56e81f171bcc55a6ff8345e692c0f86e5b48e01b996cadc001622fb5e363b421",
  "miner": "0x63ce81c023bb9f8a6ffa08fcf48ba885c21fcfbc",
  "difficulty": "0",
  "totalDifficulty": "0",
  "extraData": "0x",
  "gasLimit": "84000000",
  "gasUsed": "0",
  "timestamp": "1759152508",
  "mixHash": "0x0000000000000000000000000000000000000000000000000000000000000000",
  "logsBloom": "0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
  "baseFeePerGas": "0",
  "size": "440",
  "transactions": [],
  "uncles": [],
  "quorumCertificate": {
    "signature": "0xb532b66d680036b0364db472264f0a0c6874f5df844c60a81194053a949d2d71bb213f5ca3f21991e08844e2fae0183a0a3365294cff221857eddd194f899ea56feaba0f23eb2b181f760b9254a72cb3544f2de4fa204a9501548ef55dce03cb",
    "cosigned": "0xf77ffb0000000000000000000000000000000000000000000000000000000000",
    "view": "0x9ff9c4",
    "block_hash": "0xfbbc175435f5d82e6f7a18d261889c01379845904cac20aabca91923921f6f7a"
  }
}
```

#### Validation via Zilliqa Stats Dashboard

You can manually verify the block number, hash, and timestamp against the public stats dashboard https://stats.zq2-mainnet.zilliqa.com/.

### Zilliqa Testnet Faucet

Request test tokens (ZIL) on the Zilliqa testnet using the `request_zilliqa_faucet` MCP tool. This is useful for quickly funding an address before testing contract interactions, transfers, or balance queries.

#### Prompt

```
Request test tokens using the testnet-zilliqa faucet to the 0xc8d812e26216be9784EeEbeeaBff76c9Fb36272f address.
```

#### Direct Tool Invocation (JSON)

```json
{
  "tool": "request_zilliqa_faucet",
  "arguments": {
    "address": "0xc8d812e26216be9784EeEbeeaBff76c9Fb36272f"
  }
}
```

#### Expected Successful Response

```
**Faucet Request Successful** ✅

**Network:** testnet
**Address:** `0xc8d812e26216be9784EeEbeeaBff76c9Fb36272f`
**Amount:** 100 ZIL
**Status:** Request submitted successfully
**Transaction ID:** `0x283d62ed94456bd8aee16fa1f89a0538178e78f8219881b5e0e8c7a0531c525f`
**Explorer:** https://otterscan.testnet.zilliqa.com/tx/0x283d62ed94456bd8aee16fa1f89a0538178e78f8219881b5e0e8c7a0531c525f

**Note:** It may take a few moments for the tokens to appear in your account.
```

If the faucet rate limits you, you will receive a failure message with guidance to retry later.

#### Verify the Funded Balance

You can confirm receipt of funds by querying the balance:

Prompts:
```
Get the balance of 0xc8d812e26216be9784EeEbeeaBff76c9Fb36272f address for the testnet-zilliqa network.
```
```
Get the last request tokens transaction on address 0xc8d812e26216be9784EeEbeeaBff76c9Fb36272f for the testnet-zilliqa network.
```

### Zilliqa Address Conversion

Convert a Zilliqa address between hex (`0x...`) and bech32 (`zil1...`) formats using the `convert-zilliqa-address` tool. This only applies to Zilliqa networks.

#### Prompt

```
What is the Zilliqa address of 0x625dAB280fC96fFc8b28f5a5e9e0f19a93c6D0D8?
```

#### Direct Tool Invocation (JSON)

```json
{
  "tool": "convert-zilliqa-address",
  "arguments": {
    "address": "0x625dAB280fC96fFc8b28f5a5e9e0f19a93c6D0D8",
    "network": "zilliqa"
  }
}
```

#### Expected Response

```json
{
  "network": "zilliqa",
  "chainId": 32769,
  "input": "0x625dAB280fC96fFc8b28f5a5e9e0f19a93c6D0D8",
  "output": "zil1vfw6k2q0e9hlezeg7kj7nc83n2fud5xcch9k57",
  "direction": "hex-to-bech32"
}
```

#### Reverse Conversion Prompt

```
What is the address of zil1vfw6k2q0e9hlezeg7kj7nc83n2fud5xcch9k57?
```

#### Notes

- The tool auto-detects the conversion direction if the `direction` parameter is omitted.
- Only valid for Zilliqa networks (mainnet: `zilliqa`, testnet: `testnet-zilliqa`).
- Useful before interacting with tooling that expects a specific format.

## 📚 API Reference

### Tools

The server provides the following MCP tools for agents. **All tools that accept address parameters support both Ethereum addresses and ENS names.**

#### Token services

| Tool Name | Description | Key Parameters |
|-----------|-------------|----------------|
| `get-token-info` | Get ERC20 token metadata | `tokenAddress` (address/ENS), `network` |
| `get-token-balance` | Check ERC20 token balance | `tokenAddress` (address/ENS), `ownerAddress` (address/ENS), `network` |
| `transfer-token` | Transfer ERC20 tokens | `privateKey`, `tokenAddress` (address/ENS), `toAddress` (address/ENS), `amount`, `network` |
| `approve-token-spending` | Approve token allowances | `privateKey`, `tokenAddress` (address/ENS), `spenderAddress` (address/ENS), `amount`, `network` |
| `get-nft-info` | Get NFT metadata | `tokenAddress` (address/ENS), `tokenId`, `network` |
| `check-nft-ownership` | Verify NFT ownership | `tokenAddress` (address/ENS), `tokenId`, `ownerAddress` (address/ENS), `network` |
| `transfer-nft` | Transfer an NFT | `privateKey`, `tokenAddress` (address/ENS), `tokenId`, `toAddress` (address/ENS), `network` |
| `get-nft-balance` | Count NFTs owned | `tokenAddress` (address/ENS), `ownerAddress` (address/ENS), `network` |
| `get-erc1155-token-uri` | Get ERC1155 metadata | `tokenAddress` (address/ENS), `tokenId`, `network` |
| `get-erc1155-balance` | Check ERC1155 balance | `tokenAddress` (address/ENS), `tokenId`, `ownerAddress` (address/ENS), `network` |
| `transfer-erc1155` | Transfer ERC1155 tokens | `privateKey`, `tokenAddress` (address/ENS), `tokenId`, `amount`, `toAddress` (address/ENS), `network` |

#### Blockchain services

| Tool Name | Description | Key Parameters |
|-----------|-------------|----------------|
| `get-chain-info` | Get network information | `network` |
| `get-balance` | Get native token balance | `address` (address/ENS), `network` |
| `transfer-eth` | Send native tokens | `privateKey`, `to` (address/ENS), `amount`, `network` |
| `get-transaction` | Get transaction details | `txHash`, `network` |
| `read-contract` | Read smart contract state | `contractAddress` (address/ENS), `abi`, `functionName`, `args`, `network` |
| `write-contract` | Write to smart contract | `contractAddress` (address/ENS), `abi`, `functionName`, `args`, `privateKey`, `network` |
| `is-contract` | Check if address is a contract | `address` (address/ENS), `network` |
| `resolve-ens` | Resolve ENS name to address | `ensName`, `network` |

#### Zilliqa services

| Tool Name | Description | Key Parameters |
|-----------|-------------|----------------|
| `convert-zilliqa-address` | Convert a Zilliqa address between bech32 (zil1...) and hex (0x...) formats. | `address`, `direction`, `network` |
| `request-zilliqa-faucet` | Request test tokens from Zilliqa testnet faucet for development and testing purposes | `address` |

### Resources

The server exposes blockchain data through the following MCP resource URIs. All resource URIs that accept addresses also support ENS names, which are automatically resolved to addresses.

#### Blockchain Resources

| Resource URI Pattern | Description |
|-----------|-------------|
| `evm://{network}/chain` | Chain information for a specific network |
| `evm://chain` | Ethereum mainnet chain information |
| `evm://{network}/block/{blockNumber}` | Block data by number |
| `evm://{network}/block/latest` | Latest block data |
| `evm://{network}/address/{address}/balance` | Native token balance |
| `evm://{network}/tx/{txHash}` | Transaction details |
| `evm://{network}/tx/{txHash}/receipt` | Transaction receipt with logs |

#### Token Resources

| Resource URI Pattern | Description |
|-----------|-------------|
| `evm://{network}/token/{tokenAddress}` | ERC20 token information |
| `evm://{network}/token/{tokenAddress}/balanceOf/{address}` | ERC20 token balance |
| `evm://{network}/nft/{tokenAddress}/{tokenId}` | NFT (ERC721) token information |
| `evm://{network}/nft/{tokenAddress}/{tokenId}/isOwnedBy/{address}` | NFT ownership verification |
| `evm://{network}/erc1155/{tokenAddress}/{tokenId}/uri` | ERC1155 token URI |
| `evm://{network}/erc1155/{tokenAddress}/{tokenId}/balanceOf/{address}` | ERC1155 token balance |

## 🔒 Security Considerations

- **Private keys** are used only for transaction signing and are never stored by the server
- Consider implementing additional authentication mechanisms for production use
- Use HTTPS for the HTTP server in production environments
- Implement rate limiting to prevent abuse
- For high-value services, consider adding confirmation steps

## 📁 Project Structure

```
evm-mcp-server/
├── src/
│   ├── index.ts                # Main stdio server entry point
│   ├── server/                 # Server-related files
│   │   ├── http-server.ts      # HTTP server with SSE
│   │   └── server.ts           # General server setup
│   ├── core/
│   │   ├── chains.ts           # Chain definitions and utilities
│   │   ├── resources.ts        # MCP resources implementation
│   │   ├── tools.ts            # MCP tools implementation
│   │   ├── prompts.ts          # MCP prompts implementation
│   │   └── services/           # Core blockchain services
│   │       ├── index.ts        # Operation exports
│   │       ├── balance.ts      # Balance services
│   │       ├── transfer.ts     # Token transfer services
│   │       ├── utils.ts        # Utility functions
│   │       ├── tokens.ts       # Token metadata services
│   │       ├── contracts.ts    # Contract interactions
│   │       ├── transactions.ts # Transaction services
│   │       └── blocks.ts       # Block services
│   │       └── clients.ts      # RPC client utilities
├── package.json
├── tsconfig.json
└── README.md
```

## 🛠️ Development

To modify or extend the server:

1. Add new services in the appropriate file under `src/core/services/`
2. Register new tools in `src/core/tools.ts`
3. Register new resources in `src/core/resources.ts`
4. Add new network support in `src/core/chains.ts`
5. To change server configuration, edit the hardcoded values in `src/server/http-server.ts`

## 📄 License

This project is licensed under the terms of the [MIT License](./LICENSE).
