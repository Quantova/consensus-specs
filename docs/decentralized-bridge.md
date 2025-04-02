# Decentralized bridge Relay with Zero-Knowledge Proofs

## Overview
This repository contains the implementation of a cross-chain bridge that uses zero-knowledge proofs to verify Grandpa finality proofs, enabling secure communication between Quantova and Binance Smart Chain (BSC) networks.

## Architecture Overview
### Components
1. **BSC Host Relay**
   - Connects to both Quantova and BSC networks.
   - Monitors finalized blocks on Quantova.
   - Manages the relay process and proof generation.
   
2. **Grandpa Light Client**
   - Implements the Grandpa consensus verification logic.
   - Verifies finality proofs between block ranges.
   - Maintains the consensus state.

3. **Zero-Knowledge Proof System**
   - Uses RISC0 for generating zero-knowledge proofs.
   - Guest program verifies:
     - Finality proofs from Grandpa consensus.
     - Outward transfer proofs.
     - State transitions.

4. **BSC Contract Integration**
   - Submits verified proofs to BSC network.
   - Updates the light client state.
   - Processes verified transfers.

## Workflow
### Block Monitoring
- Subscribe to finalized blocks on Quantova.
- Track the latest finalized block.

### Proof Collection
- Fetch finality proofs from the last accepted block.
- Collect storage proofs for pending transfers.
- Prepare prover input with consensus state.

### Zero-Knowledge Proof Generation
- Initialize Grandpa light client with the current state.
- Verify finality proofs and transfers.
- Generate proof using RISC0.

### Proof Verification
- Verify the generated proof.
- Extract verified transfers and state updates.

### BSC Submission
- Submit proof and verified transfers to BSC.
- Update light client state.

## Technical Details
### Zero-Knowledge Proof Components
- **Guest Program**: Implements verification logic in RISC-V.
- **Prover**: Generates proofs using RISC0.
- **Verifier**: Validates proofs on-chain.

### State Management
- Maintains last processed nonce.
- Tracks pending transfers.
- Updates light client state.

## Security Considerations
- Zero-knowledge proofs ensure trustless verification of the bridge.
- Verifiable on-chain without expensive full Grandpa finality verification.

## BSC Bridge Pallet
This Substrate pallet implements a light client-based bridge mechanism for Binance Smart Chain (BSC). It verifies BSC headers and processes inward/outward transfers between BSC and the Substrate-based Quantova chain.

### Overview
- **BSC Light Client**: Maintains a light client state for BSC, tracking validator sets and verifying BSC headers.
- **Inward Transfers**: Events from BSC are verified using state proofs and processed on the Substrate chain.
- **Outward Transfers**: Users can register outward transfers to BSC, which are tracked and executed by off-chain relayers.


## Future Development
- Expansion to support multiple bridge integrations, including Ethereum (ETH), Solana (SOL), and Tron (TRX).
- Enhancements for optimized proof generation and submission.
- Further decentralization of the relayer network.
- Advanced security audits and economic modeling for bridge incentives.

## Contributing
We welcome contributions to improve the bridge relay. Please see our Contributing Guidelines.

## Additional Resources
- [Alloy Documentation](https://docs.alloy.rs/)
- [Subxt Documentation](https://docs.rs/subxt/)
- [Binance Smart Chain Documentation](https://docs.binance.org/)

