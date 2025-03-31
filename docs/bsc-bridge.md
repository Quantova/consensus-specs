# Centralized Bridge Relayer

The Centralized Bridge Relayer is a stateless service that enables cross-chain communication between **Quantova** and **Binance Smart Chain (BSC)**. This bridge facilitates seamless asset transfers and cross-chain messaging between the two networks.

## Overview

The relayer listens for events on both chains and relays relevant transactions across networks, making it possible to:
- Transfer tokens from BSC to Quantova
- Transfer tokens from Quantova to BSC
- Exchange cross-chain messages and data

## Features

- **Bidirectional Asset Transfers**: Move tokens seamlessly between Quantova and BSC
- **Event-Driven Architecture**: Automatically processes events from both chains
- **BSC Connection**: Uses [Alloy](https://docs.rs/alloy) providers to connect to BSC via WebSockets
- **Quantova Connection**: Uses [Subxt](https://docs.rs/subxt) to connect to Quantova and submit extrinsics
- **Efficient Event Relay**:
  - **BSC → Quantova**: Subscribes to contract events on BSC and relays them to Quantova
  - **Quantova → BSC**: Listens for pallet events on Quantova and triggers transactions on BSC

## Prerequisites

1. **WebSocket endpoints**
   - A running BSC node that supports WebSocket (e.g., BSC testnet node)
   - A running Quantova node at an accessible WebSocket URL (e.g., `ws://localhost:9944`)

2. **ABI file**
   - A contract ABI JSON file named `centralized_bridge_relay_bsc_abi.json` in the working directory

3. **Seed Phrase**
   - A valid ECDSA seed phrase (BIP-39 mnemonic) used to sign transactions on both networks

## Installation

```bash
# Clone the repository
git clone https://github.com/Quantova/centralized-bridge-relayer.git
cd centralized-bridge-relayer

# Build the relayer
cargo build --release
```

## Usage

Run the binary with the required CLI arguments:

```bash
./target/release/centralized-bridge-relayer \
  --bsc-endpoint "ws://bsc-testnet.example.org:8546" \
  --bsc-contract-address "0x1234567890abcdef1234567890abcdef12345678" \
  --quantova-endpoint "ws://127.0.0.1:9944" \
  --seed-phrase "your test mnemonic phrase goes here"
```

### Command Line Options

```
Usage: centralized-bridge-relayer [OPTIONS] --bsc-endpoint <BSC_ENDPOINT> --bsc-contract-address <BSC_CONTRACT_ADDRESS> --quantova-endpoint <QUANTOVA_ENDPOINT> --seed-phrase <SEED_PHRASE>

Options:
  -b, --bsc-endpoint <BSC_ENDPOINT>      
          Binance Smart Chain RPC endpoint

  -c, --bsc-contract-address <BSC_CONTRACT_ADDRESS>      
          Binance Smart Chain Contract address

  -g, --quantova-endpoint <QUANTOVA_ENDPOINT>      
          Quantova RPC endpoint

  -s, --seed-phrase <SEED_PHRASE>      
          Relayer ECDSA seed phrase to initialize private key

  -i, --in-memory-events <IN_MEMORY_EVENTS>      
          In memory events to store in buffer [default: 1000]

  -h, --help      
          Print help (see a summary with '-h')
  -V, --version   
          Print version
```

## How It Works

1. **Initialization**
   - Connects to BSC using the Alloy library
   - Connects to Quantova using the Subxt library
   - Derives signing keys from the provided seed phrase

2. **Event Listening**
   - Spawns two async tasks to monitor both chains simultaneously
   - BSC listener watches for specific contract event logs
   - Quantova listener watches for `OutwardRemittanceRegistered` events

3. **Cross-Chain Relay**
   - When a BSC event is detected, creates and submits an extrinsic to Quantova
   - When a Quantova event is detected, triggers a contract call on BSC

## Metadata Extraction

To generate the required `metadata.scale` file from Quantova for use with the bridge:

1. Install the SubXT CLI:
   ```bash
   cargo install subxt-cli
   ```

2. Generate the metadata file:
   ```bash
   subxt metadata \
       --url ws://localhost:9944 \
       --format scale \
       > metadata.scale
   ```

## Development and Testing

To run the test suite:

```bash
cargo test
```

The tests assume a local Quantova node running on `ws://localhost:9944`.

## Project Structure

```
.
├── Cargo.toml
├── Cargo.lock
├── README.md
├── main.rs                  // Main entry point, sets up event listeners
├── cli.rs                   // CLI argument parser using Clap
├── subxt_config.rs          // Subxt configuration for Quantova's runtime types
├── tests.rs                 // Integration tests
└── centralized_bridge_relay_bsc_abi.json  // ABI file for the BSC contract
```

## Contributing

We welcome contributions to improve the bridge relayer. Please see our [Contributing Guidelines](../CONTRIBUTING.md).

## Additional Resources

- [Alloy Documentation](https://docs.rs/alloy)
- [Subxt Documentation](https://docs.rs/subxt)
- [Binance Smart Chain Documentation](https://docs.bnbchain.org/docs/bnb-chain-overview)
