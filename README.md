# TokenVM - Metacrafters HyperSDK Project

TokenVM is a showcase application built using HyperSDK, designed to demonstrate token minting and trading functionalities. The platform empowers users to create, mint, trade, and manage custom tokens, coupled with an embedded on-chain exchange for seamless trading. With TokenVM, you can:

- Create and mint assets with customizable metadata.
- Burn assets or update metadata when required.
- Trade tokens using an efficient on-chain order book.

TokenVM includes a robust CLI tool and serves RPC requests through an in-memory order book for trading operations. It’s an excellent starting point for exploring the intersection of exchanges and blockchain technology.

## Status
TokenVM is currently in its **ALPHA** stage and is not ready for production use. The framework is under active development, and significant changes may occur as modules are optimized and audited.

---

## Key Features

### 1. Arbitrary Token Minting
TokenVM allows easy creation, minting, and transferring of user-generated tokens. Asset creators have "admin control," enabling them to:
- Mint additional tokens.
- Update metadata (e.g., during a reveal).
- Transfer or revoke ownership.

The storage engine is optimized for efficient asset management, using just 72 bytes of state per balance entry. This format supports parallel execution of transfers that don’t involve overlapping accounts, maximizing scalability.

---

### 2. On-Chain Token Trading
TokenVM facilitates fully on-chain token trading. Users can:
- Create offers specifying the rate and token they are willing to accept.
- Fill offers partially or fully if they meet trading criteria.

**Efficient Order Management**
Orders are stored using 152 bytes of state per order, enabling:
- Parallel execution of fills.
- Scalability within trading pairs, unlike pool-based mechanisms like AMMs.

An in-memory order book keeps track of on-chain orders for easy client interaction.

---

### 3. In-Memory Order Book
TokenVM’s in-memory order book efficiently manages trading pairs by organizing orders using a max-heap structure. This design ensures:
- Fast access to the best rates.
- Real-time synchronization with on-chain transactions.

---

### 4. Sandwich Resistance
TokenVM’s architecture prevents transaction manipulation by block producers, ensuring:
- Consistent pricing for trades.
- Protection against malicious front-running attacks.

---

### 5. Partial Fills and Refunds
Fills can be partial, and any unused pledged assets are refunded, preventing loss due to concurrent order interactions.

---

### 6. Expiring Fills
Transactions can include expiration times, ensuring that orders do not persist indefinitely without user intervention.

---

### 7. Avalanche Warp Support
TokenVM leverages Avalanche Warp Messaging (AWM) for seamless asset transfers between Subnets without requiring external bridges or relayers. Features include:
- Secure cross-Subnet transfers.
- Unique AssetIDs for imported assets.
- Export restrictions to prevent contagion in case of failures.

Users can tip relayers and swap assets during import to cover transaction fees.

---

## Getting Started

### Prerequisites
Ensure you have the necessary tools and dependencies installed to build and run TokenVM.

### Launching TokenVM Subnet
Run the following command to set up your own TokenVM Subnet:
```bash
./scripts/run.sh
```
This allocates all network funds to a default address (`demo.pk`). For single Subnet testing, use:
```bash
MODE="run-single" ./scripts/run.sh
```

### Building the CLI Tool
Compile the CLI using:
```bash
./scripts/build.sh
```
The compiled CLI will be available at `./build/token-cli`.

### Configuring the CLI
Import the default key and chain information using:
```bash
./build/token-cli key import demo.pk
./build/token-cli chain import-anr
```

---

## Token Operations

### 1. Create an Asset
Create your own token with the command:
```bash
./build/token-cli action create-asset
```
Follow the prompts to configure the asset.

### 2. Mint Tokens
Mint tokens for the created asset:
```bash
./build/token-cli action mint-asset
```
Specify the recipient address and amount during the process.

### 3. Check Balances
Verify your token balance:
```bash
./build/token-cli key balance
```

---

## Demos
Experience TokenVM with hands-on demos. Launch your TokenVM Subnet and explore:
- Asset creation and minting.
- On-chain trading with partial fills and refunds.

---
