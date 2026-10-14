# Strip Contracts

A Solidity-based smart contract ecosystem for the Strip protocol, built with Hardhat and designed for treasury management, staking, emissions, and bond-based capital formation on Avalanche.

## Overview

Strip is a treasury-driven token economy that coordinates emissions, staking incentives, and bond issuance around a governance-controlled treasury. This repository contains the core protocol contracts and deployment scripts that power the on-chain ecosystem.

The project includes:

- Governance-aligned treasury and reserve management
- Token minting and vesting logic for the Strip ecosystem
- Staking and reward distribution infrastructure
- Bond markets for protocol funding and treasury growth
- Supporting utilities such as bonding calculators, wrappers, and liquidity helpers

## System Architecture

### Core token layer

- StripERC20: the core Strip token implementation
- sStripERC20: staked/receipt token for staking and vesting flows
- wSStrip: wrapped staked token utility

### Treasury and policy

- Treasury: central protocol treasury that holds reserves and manages policy-driven allocations
- DAO / governance integration: multi-signature governance and treasury control patterns for upgrades and policy changes

### Staking and incentives

- Staking: lock STRIP and distribute protocol rewards over epochs
- StakingDistributor: handles reward emission scheduling and distribution
- StakingWarmup and StakingHelper: user-facing staking support and warmup flows

### Bonding and capital markets

- BondDepository / EthBondDepository: bond market contracts allowing treasury capital raises in exchange for discounted STRIP emissions
- StandardBondingCalculator: pricing and valuation utilities for bond calculations
- ZapIn: utility contracts for liquidity/integration workflows

## Repository Structure

```text
contracts/
  BondDepository.sol
  EthBondDepository.sol
  StripERC20.sol
  SStripERC20.sol
  Staking.sol
  StakingDistributor.sol
  StakingHelper.sol
  StakingWarmup.sol
  StandardBondingCalculator.sol
  Treasury.sol
  wSStrip.sol
  ZapIn.sol
  mocks/

scripts/
  deploy/
  deployAll.js
  deploy_lp.js
  deploy.js
  main_deploy.js
  mocks/

hardhat.config.js
package.json
```

## Tech Stack

- Solidity: 0.4.16, 0.5.x, 0.6.x, 0.7.x, 0.8.x via multi-compiler Hardhat config
- Hardhat: local compilation, deployment, and testing
- Ethers.js + Hardhat plugin stack
- OpenZeppelin libraries and test helpers

## Prerequisites

Before working with the contracts, install the required tooling:

- Node.js 16+ recommended
- npm or yarn
- A funded wallet/private key for deployment networks
- Access to an Avalanche RPC endpoint for testnet or mainnet deployments

## Installation

```bash
npm install
```

## Configuration

Create a `.env` file in the project root with the required deployment key:

```bash
PRIVATEKEY=your_private_key_here
```

The Hardhat configuration includes:

- `fuji` for Avalanche Fuji testnet
- `mainnet` for Avalanche mainnet

## Useful Commands

```bash
# Compile contracts
npx hardhat compile

# Run the test suite
npm test

# Clean artifacts
npm run clean

# Full ecosystem deployment script
npm run start

# Fuji deployment
npm run start:fuji

# Mainnet deployment
npm run start:mainnet

# Solidity linting
npm run lint:sol
```

## Deployment Flow

This repository includes deployment scripts under `scripts/deploy/` for a staged deployment model. The flow is generally structured as:

1. Deploy the Strip token
2. Deploy the staking and sSTRIP components
3. Deploy the treasury and reserve logic
4. Configure the distributor and staking rewards
5. Deploy bond contracts and initialize terms
6. Configure vault approvals and treasury allocations
7. Verify addresses and initialize protocol-wide parameters

For a full local or test environment bootstrapping flow, use the project-wide deploy script in `scripts/deployAll.js`.

## Notes on the Deployment Scripts

The scripts are intentionally flexible and are designed for protocol setup and testnet demonstration rather than a fully generic application template. Some scripts assume pre-existing token addresses or a specific deployment sequence, so it is recommended to review the relevant script before running it in a production environment.

## Security Considerations

This repository contains protocol-grade smart contracts and deployment logic, but it should be treated as a serious production system. Before deploying to mainnet:

- Audit all contracts and deployment scripts
- Validate all constructor parameters and policy addresses
- Review treasury permissions and role assignments
- Test on a fork or testnet before production use
- Treat private keys and deployment addresses as highly sensitive

## License

This project is licensed under the MIT License. See the LICENSE file in the repository root for details.

## Maintainer Notes

This repository is structured for protocol experimentation, staging, and deployment orchestration. It is best suited to teams working on a treasury-driven DeFi product and for developers who want a real-world example of staking, treasury policy, and bonding mechanics in Solidity.

---

For deeper protocol understanding, review the contracts in `contracts/` alongside the deployment scripts in `scripts/deploy/` and verify the intended sequence before executing a live deployment.
