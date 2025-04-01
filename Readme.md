# Quantova Blockchain


## Overview

Quantova is a high-performance Layer 1 blockchain built on the Substrate framework, utilizing a **Pure Proof of Stake (PPoS)** consensus model. Designed for scalability, security, and decentralization, Quantova ensures fast transaction finality and seamless integration with existing blockchain ecosystems.


<img src="/images/layer_flow.jpg" alt="overview" width="300">

### Key Features

- **EVM Compatibility** – Supports Ethereum-style signatures, allowing developers to use tools like MetaMask, Remix, Hardhat, and Web3.js
- **Fast Finality** – Utilizes GRANDPA consensus for deterministic finality, ensuring finalized blocks cannot be reverted
- **High Throughput** – Blocks are produced every **3 seconds** for efficient transaction processing
- **Decentralized Validator Set** – PPoS ensures fair selection, automatic rotation, and economic security mechanisms
- **Robust Security** – Implements strict slashing conditions for malicious validators and enforces censorship resistance
- **Cross-Chain Bridge** – Centralized relayer for seamless asset transfers between Quantova and Binance Smart Chain (BSC)

## Network Information

| Parameter              | Value                            |
|------------------------|----------------------------------|
| **Network Name**       | Quantova Network                 |
| **RPC URL**            | https://rpc.quantova.org         |
| **Chain ID**           | 42                           |
| **Symbol**             | QTOV                             |
| **Block Explorer URL** | [QuantovaScan.io](https://quantovasc.io) |
| **Website**            | [Quantova.org](https://quantova.org) |

## Documentation

- [Consensus Mechanism](./docs/consensus.md) - Details about Quantova's Pure Proof of Stake implementation
- [Node Setup Guide](./docs/node-setup.md) - Instructions for running validator and full nodes
- [Validator Guide](./docs/validator-guide.md) - Requirements and steps to become a validator
- [Security Model](./docs/security-model.md) - Security assumptions and attack resistance
- [BSC Bridge](./docs/bsc-bridge.md) - Documentation for the Centralized Bridge Relayer between Quantova and BSC

## Additional Resources

- [Quantova Explorer](https://qtovascan.io/)
- [Quantova GitHub](https://github.com/Quantova)
- [Quantova Documentation](https://docs.quantova.org/)
- [Consensus Specifications (PDF)](https://github.com/Quantova/consensus-specs/blob/main/docs/Consensus-Mechanism-Report.pdf)

## Quick Start

To start running a Quantova node, refer to our [Node Setup Guide](./docs/node-setup.md).

## License

Quantova is licensed under [Apache 2.0](./LICENSE).
