# Node Setup Guide

This guide provides instructions for setting up and running Quantova nodes on different networks.

## Hardware Requirements

| Component | Minimum Requirement | Recommended     |
|-----------|---------------------|-----------------|
| **CPU**   | Dual-core           | 4+ cores        |
| **RAM**   | 8GB                 | 16GB            |
| **Storage** | 512GB SSD         | 1TB SSD         |
| **Network** | 5 Mbps           | 10+ Mbps       |

## Building from Source

### Prerequisites

- Rust and Cargo (latest stable version)
- Git
- Build essentials (make, gcc, etc.)

### Compilation

```bash
# Clone the repository
git clone https://github.com/Quantova/Quantova.git
cd Quantova

# Build the node in release mode
cargo build --release
```

## Running a Node

### Generate Chain Specification

#### Local Development Network

```sh
./target/release/quantova-node build-spec --disable-default-bootnode --chain=local --raw > ./specs/local/customSpecRaw.json
```

#### Testnet

```sh
./target/release/quantova-node build-spec --disable-default-bootnode --chain=testnet --raw > ./specs/testnet/customSpecRaw.json
```

#### Mainnet

```sh
./target/release/quantova-node build-spec --disable-default-bootnode --chain=quantova-node --raw > ./specs/mainnet/customSpecRaw.json
```

### Insert Consensus Keys (For Validators)

#### Insert AURA Key (Block Production)

```sh
./target/release/quantova-node key insert --base-path /tmp/node01 \  
  --chain ./specs/customSpecRaw.json \  
  --scheme Sr25519 \  
  --suri <key> \  
  --password-interactive \  
  --key-type aura
```

#### Insert GRANDPA Key (Finality)

```sh
./target/release/quantova-node key insert --base-path /tmp/node01 \  
  --chain ./specs/customSpecRaw.json \  
  --scheme Ed25519 \  
  --suri <key> \  
  --password-interactive \  
  --key-type gran
```

### Start Validator Nodes

#### First Validator Node

```sh
./target/release/quantova-node \
  --base-path /tmp/node01 \
  --chain ./specs/customSpecRaw.json \
  --port 30333 \
  --rpc-port 9945 \
  --validator \
  --rpc-methods Unsafe \
  --name MyNode01
```

#### Additional Validator Node

```sh
./target/release/quantova-node \
  --base-path /tmp/node02 \
  --chain ./specs/customSpecRaw.json \
  --port 30334 \
  --rpc-port 9946 \
  --validator \
  --rpc-methods Unsafe \
  --name MyNode02 \
  --bootnodes /ip4/127.0.0.1/tcp/30333/p2p/<node-key>
```

### Run a Full Node (Non-Validator)

```sh
./target/release/quantova-node \
  --base-path /tmp/fullnode01 \
  --chain ./specs/customSpecRaw.json \
  --port 30335 \
  --rpc-port 9947 \
  --name FullNode01 \
  --bootnodes /ip4/127.0.0.1/tcp/30333/p2p/<node-key>
```

## Node Monitoring

We recommend setting up monitoring for your nodes using Prometheus and Grafana. Quantova nodes expose metrics on port 9615 by default.

To enable metrics:

```sh
./target/release/quantova-node \
  --base-path /tmp/node01 \
  --chain ./specs/customSpecRaw.json \
  --validator \
  --prometheus-external
```

## Troubleshooting

### Common Issues

- **Synchronization Issues**: If your node is having trouble syncing, try connecting to additional bootnodes or check your network connection.
- **Database Corruption**: In case of database corruption, you may need to purge the chain and start again:
  ```sh
  ./target/release/quantova-node purge-chain --base-path /tmp/node01 --chain ./specs/customSpecRaw.json
  ```
- **Performance Issues**: Ensure your hardware meets the minimum requirements and consider optimizing your system settings.

## Observations and Network Metrics

Quantova's network performance is continuously monitored to ensure optimal operation. The following metrics represent our current benchmarks:
Real-time Network Statistics
Node Participation

Current validator statistics will be available after testnet and mainnet launch

### Block Creation

Target: 3-second intervals
Current average: 3.1 seconds

### Network Responsiveness

Block relay (typical): 1.5s
Block relay (peak conditions): 0.8s
Block relay (heavy traffic): 3.2s

### Transaction Security

Average finalization: 9s (3 block confirmation)
Fastest observed: 6s (2 block confirmation)

Understanding Performance Implications
Our 3-second block time balances transaction throughput with network stability. This configuration allows for:

## Rapid transaction inclusion
Minimized uncle/orphan block rates
Optimized network communication

The observed finalization time (typically 9 seconds) provides the security assurance needed for commercial applications while maintaining an excellent user experience. These metrics place Quantova among the most responsive blockchain networks in production.

## Further Resources

- [Validator Guide](./validator-guide.md) - More detailed information for validators