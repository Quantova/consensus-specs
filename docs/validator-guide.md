# Validator Guide

This guide provides comprehensive information about becoming a validator on the Quantova network.

## Becoming a Validator

Validators play a crucial role in the Quantova network by participating in block production and finalization through our Pure Proof of Stake (PPoS) consensus mechanism.

### Requirements

- Meet the [hardware requirements](./node-setup.md#hardware-requirements)
- Stake a minimum amount of QTOV tokens
- Maintain high uptime and network connectivity
- Follow network upgrades and participate in governance

### Validator Selection Process

Validators are selected based on their stake weight in a probabilistic manner, ensuring fair distribution of block production opportunities. The network implements automatic validator rotation after each era to prevent centralization.

## Staking & Governance

- No **KYC requirements**, allowing permissionless participation
- Validators must adhere to on-chain governance rules to avoid penalties
- Staking positions can be adjusted during designated periods

## Incentives: Rewards & Slashing

- Validators earn **staking rewards & transaction fees**
- Nominators receive a share of staking rewards based on delegated stake
- **Slashing** penalties apply for:
  - Downtime/inactivity
  - Double signing (signing conflicting blocks)
  - Malicious behavior

## Setting Up a Validator Node

Follow the instructions in the [Node Setup Guide](./node-setup.md) to set up your local validator node.

### Additional Validator Setup Steps

1. **Generate Session Keys**:
   ```sh
   curl -H "Content-Type: application/json" -d '{"id":1, "jsonrpc":"2.0", "method": "author_rotateKeys", "params":[]}' http://localhost:9945
   ```

2. **Bond Tokens and Set Session Keys**:
   Use the Quantova Explorer or CLI to:
   - Bond your QTOV tokens
   - Set your session keys
   - Declare your intention to validate

3. **Monitor Your Validator**:
   Set up monitoring to ensure your validator remains online and performs as expected.

## Best Practices

- **Security**: Run your validator on a secure, dedicated server with proper firewall configurations
- **Redundancy**: Consider setting up a backup validator to maintain uptime
- **Updates**: Stay informed about network upgrades and update your node promptly
- **Monitoring**: Implement comprehensive monitoring and alerting
- **Community**: Participate in the validator community to stay informed

## FAQ

### How does slashing work?

Slashing is a penalty mechanism that confiscates a portion of a validator's stake for rule violations. The severity of slashing depends on the type and frequency of the violation, ranging from minor penalties to complete removal from the validator set.