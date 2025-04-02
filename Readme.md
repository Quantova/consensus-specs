# Quantova Blockchain

## Overview

Quantova is a high-performance Layer 1 blockchain built on the Substrate framework, utilizing a **Pure Proof of Stake (PPoS)** consensus model. Designed for scalability, security, and decentralization, Quantova ensures fast transaction finality and seamless integration with existing blockchain ecosystems.

To future-proof security against quantum computing threats, Quantova integrates **post-quantum cryptographic mechanisms**, making it one of the first Substrate-based blockchains to adopt quantum-resistant encryption methods. The network leverages **lattice-based cryptography**, including **Kyber** for key exchange and **Dilithium** for digital signatures, ensuring long-term resilience against quantum attacks. Additionally, Quantova employs the **SHA-3 hashing algorithm**, a NIST-standardized cryptographic hash function, to provide enhanced security for transaction integrity and data authentication.

<img src="/images/layer_flow.jpg" alt="overview" width="300">

### Key Features

- **EVM Compatibility** – Supports Ethereum-style signatures, allowing developers to use tools like MetaMask, Remix, Hardhat, and Web3.js
- **Fast Finality** – Utilizes GRANDPA consensus for deterministic finality, ensuring finalized blocks cannot be reverted
- **High Throughput** – Blocks are produced every 3 seconds for efficient transaction processing
- **Decentralized Validator Set** – PPoS ensures fair selection, automatic rotation, and economic security mechanisms
- **Robust Security** – Implements strict slashing conditions for malicious validators and enforces censorship resistance
- **Cross-Chain Bridge** – Decentralized relayer that uses zero-knowledge proofs to verify GRANDPA finality proofs, enabling secure communication between Quantova and Binance Smart Chain (BSC) networks.
- **Governance & Address Blacklisting** – A voting system powered by QTOV token holders allows for the blacklisting of malicious addresses. Token holders can vote to blacklist addresses engaging in illicit activities, based on predefined parameters currently under discussion.
- **No Forced Upgrades** – Quantova does not include the `sudo` pallet, meaning there are no privileged keys that allow forced upgrades to the Substrate framework. This ensures the chain remains immutable and truly decentralized.
- **Post-Quantum Cryptographic Security** – Implements lattice-based cryptographic algorithms such as **Kyber** (for key exchange) and **Dilithium** (for digital signatures) to ensure resistance against quantum computing attacks. This enhances the longevity and security of transactions and data integrity on the network.
- **SHA-3 Hashing Algorithm** – Uses **SHA-3** for cryptographic hashing, ensuring enhanced security against collision attacks and improving the integrity of stored blockchain data.
- **Hybrid Encryption Model** – Combines traditional elliptic curve cryptography (ECC) with post-quantum algorithms to provide backward compatibility while transitioning towards quantum-resistant security.
- **Secure Key Management** – Uses quantum-safe cryptographic primitives to enhance wallet security and prevent unauthorized access even in the presence of quantum adversaries.

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
- [BSC Bridge](./docs/decentralized-bridge.md) - Documentation for the Decentralized Bridge Relayer between Quantova and BSC

## Additional Resources

- [Quantova Explorer](https://qtovascan.io/)
- [Quantova GitHub](https://github.com/Quantova)
- [Quantova Documentation](https://docs.quantova.org/)
- [Consensus Specifications (PDF)](https://github.com/Quantova/consensus-specs/blob/main/docs/Consensus-Mechanism-Report.pdf)

## Quick Start

To start running a Quantova node, refer to our [Node Setup Guide](./docs/node-setup.md).

## License

Quantova is licensed under [Apache 2.0](./LICENSE).
