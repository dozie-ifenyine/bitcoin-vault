# Bitcoin Vault Protocol

[![License: ISC](https://img.shields.io/badge/License-ISC-blue.svg)](https://opensource.org/licenses/ISC)
[![Clarity](https://img.shields.io/badge/Clarity-3.0-orange.svg)](https://book.clarity-lang.org/)
[![Stacks](https://img.shields.io/badge/Stacks-Blockchain-purple.svg)](https://www.stacks.co/)

> Next-generation collateralized lending ecosystem leveraging STX tokens with intelligent risk assessment, automated position management, and community-driven liquidation mechanisms for sustainable DeFi growth.

## 🌟 Overview

Bitcoin Vault transforms traditional lending by creating a decentralized financial infrastructure where STX holders can unlock liquidity without selling their assets. The protocol employs sophisticated algorithms for real-time risk assessment, dynamic collateral requirements, and seamless liquidation processes. Designed for both retail users and institutional participants, Bitcoin Vault offers transparent, efficient, and secure lending solutions while maintaining the decentralized ethos of Bitcoin.

## 🏗️ System Architecture

### High-Level Architecture

```text
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   User Layer    │    │  Admin Layer    │    │ Liquidator API  │
│                 │    │                 │    │                 │
│ • Deposit       │    │ • Set Ratios    │    │ • Monitor       │
│ • Borrow        │    │ • Set Fees      │    │ • Liquidate     │
│ • Repay         │    │ • Set Thresholds│    │ • Profit        │
│ • Withdraw      │    │                 │    │                 │
└─────────┬───────┘    └─────────┬───────┘    └─────────┬───────┘
          │                      │                      │
          └──────────────────────┼──────────────────────┘
                                 │
                    ┌─────────────▼─────────────┐
                    │   Bitcoin Vault Core     │
                    │                           │
                    │ • Risk Management        │
                    │ • Position Tracking      │
                    │ • Collateral Engine      │
                    │ • Liquidation Engine     │
                    └─────────────┬─────────────┘
                                  │
                      ┌───────────▼───────────┐
                      │    STX Token Layer    │
                      │                       │
                      │ • STX Transfers       │
                      │ • Balance Management  │
                      │ • Collateral Storage  │
                      └───────────────────────┘
```

### Contract Architecture

The Bitcoin Vault Protocol is built as a single smart contract with modular functionality:

#### Core Components

1. **Risk Management Engine**
   - Dynamic collateral ratio calculations
   - Real-time health monitoring
   - Automated liquidation triggers

2. **Position Management System**
   - User portfolio tracking
   - Collateral and debt accounting
   - Interest calculation algorithms

3. **Liquidation Engine**
   - Community-driven liquidations
   - Automated position closure
   - Liquidator incentive mechanisms

4. **Administrative Framework**
   - Protocol parameter management
   - Fee structure configuration
   - Risk threshold adjustments

## 📊 Data Flow

### 1. Deposit Flow

```text
User → STX Transfer → Contract Storage → Position Update → Collateral Available
```

### 2. Borrow Flow

```text
User Request → Collateral Check → Risk Assessment → STX Transfer → Debt Recording
```

### 3. Repay Flow

```text
User Payment → STX Transfer → Debt Reduction → Position Update → Collateral Release
```

### 4. Liquidation Flow

```text
Health Monitor → Threshold Breach → Liquidator Action → Asset Transfer → Position Closure
```

## 🚀 Features

### Core Functionality

- **Collateralized Lending**: Deposit STX tokens as collateral to borrow against
- **Dynamic Risk Management**: Real-time collateral ratio monitoring and adjustment
- **Automated Liquidations**: Community-driven liquidation system for undercollateralized positions
- **Flexible Withdrawals**: Withdraw excess collateral while maintaining minimum ratios

### Key Benefits

- **Capital Efficiency**: Unlock liquidity without selling assets
- **Transparent Risk**: Clear collateral requirements and liquidation thresholds
- **Decentralized Governance**: Community-managed protocol parameters
- **Low Fees**: Minimal protocol fees for sustainable operation

## 📋 Protocol Parameters

| Parameter | Default Value | Range | Description |
|-----------|---------------|-------|-------------|
| Minimum Collateral Ratio | 150% | 110% - 500% | Minimum required collateralization |
| Liquidation Threshold | 130% | 110% - MCR | Health ratio triggering liquidation |
| Protocol Fee | 1% | 0% - 10% | Fee on borrowed amounts |

## 🔧 Smart Contract Interface

### Public Functions

#### Core Operations

- `deposit()` - Deposit STX as collateral
- `borrow(amount: uint)` - Borrow STX against collateral
- `repay(amount: uint)` - Repay borrowed STX
- `withdraw(amount: uint)` - Withdraw excess collateral
- `liquidate(user: principal)` - Liquidate undercollateralized position

#### Administrative Functions

- `set-minimum-collateral-ratio(new-ratio: uint)` - Update minimum collateral requirements
- `set-liquidation-threshold(new-threshold: uint)` - Update liquidation trigger point
- `set-protocol-fee(new-fee: uint)` - Update protocol fee structure

### Read-Only Functions

- `get-user-position(user: principal)` - Get user's position details
- `get-protocol-stats()` - Get comprehensive protocol statistics

## 🛡️ Security Features

### Risk Management

- **Minimum Collateral Ratios**: Enforced 150% default collateralization
- **Liquidation Thresholds**: Automated position closure at 130% health ratio
- **Parameter Bounds**: Strict limits on all configurable parameters

### Access Control

- **Owner-Only Administration**: Critical functions restricted to contract owner
- **Self-Liquidation Prevention**: Users cannot liquidate their own positions
- **Input Validation**: Comprehensive parameter and amount validation

### Error Handling

- Comprehensive error codes for all failure scenarios
- Atomic transaction guarantees
- Overflow protection on all calculations

## 🚦 Getting Started

### Prerequisites

- [Clarinet](https://github.com/hirosystems/clarinet) v2.0+
- [Node.js](https://nodejs.org/) v18+
- [Stacks CLI](https://docs.stacks.co/docs/stacks-cli)

### Installation

```bash
# Clone the repository
git clone https://github.com/dozie-ifenyine/bitcoin-vault.git
cd bitcoin-vault

# Install dependencies
npm install

# Check contract syntax
clarinet check

# Run tests
npm test
```

### Deployment

```bash
# Deploy to testnet
clarinet deploy --testnet

# Deploy to mainnet
clarinet deploy --mainnet
```

## 🧪 Testing

### Unit Tests

```bash
# Run all tests
npm test

# Run tests with coverage
npm run test:report

# Watch mode for development
npm run test:watch
```

### Test Coverage

- ✅ Core functionality (deposit, borrow, repay, withdraw)
- ✅ Liquidation scenarios
- ✅ Administrative functions
- ✅ Error conditions and edge cases
- ✅ Risk management calculations

## 📈 Usage Examples

### Basic Lending Flow

```javascript
// 1. Deposit collateral
await contractCall('deposit', []);

// 2. Borrow against collateral (maintaining 150% ratio)
const borrowAmount = 1000000; // 1 STX in microSTX
await contractCall('borrow', [borrowAmount]);

// 3. Repay loan
await contractCall('repay', [borrowAmount]);

// 4. Withdraw collateral
const withdrawAmount = 500000; // 0.5 STX
await contractCall('withdraw', [withdrawAmount]);
```

### Liquidation Example

```javascript
// Monitor position health
const userPosition = await contractCall('get-user-position', [userAddress]);
const ratio = (userPosition.totalCollateral * 100) / userPosition.totalBorrowed;

// Liquidate if below threshold
if (ratio < 130) {
  await contractCall('liquidate', [userAddress]);
}
```

## 🔍 Monitoring & Analytics

### Key Metrics

- **Total Value Locked (TVL)**: `total-deposits`
- **Total Borrowed**: `total-borrows`
- **Protocol Utilization**: `total-borrows / total-deposits`
- **Average Collateral Ratio**: Across all positions

### Health Monitoring

- Position-level health ratios
- Protocol-wide risk assessment
- Liquidation opportunity tracking

## 🤝 Contributing

We welcome contributions to the Bitcoin Vault Protocol! Please see our [Contributing Guidelines](CONTRIBUTING.md) for details.

### Development Workflow

1. Fork the repository
2. Create a feature branch
3. Write tests for new functionality
4. Ensure all tests pass
5. Submit a pull request

## 📜 License

This project is licensed under the ISC License - see the [LICENSE](LICENSE) file for details.

## 🔗 Links

- **Documentation**: [docs.bitcoinvault.fi](https://docs.bitcoinvault.fi)
- **Discord**: [Join our community](https://discord.gg/bitcoinvault)
- **Twitter**: [@BitcoinVaultFi](https://twitter.com/BitcoinVaultFi)
- **Website**: [bitcoinvault.fi](https://bitcoinvault.fi)

## ⚠️ Disclaimer

This software is experimental and may contain bugs. Use at your own risk. Always conduct thorough testing before deploying to mainnet. The developers are not responsible for any financial losses incurred through the use of this protocol.

---

Built with ❤️ on Stacks Blockchain

## 🏗️ System Architecture

### High-Level Architecture

```text
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   User Layer    │    │  Admin Layer    │    │ Liquidator API  │
│                 │    │                 │    │                 │
│ • Deposit       │    │ • Set Ratios    │    │ • Monitor       │
│ • Borrow        │    │ • Set Fees      │    │ • Liquidate     │
│ • Repay         │    │ • Set Thresholds│    │ • Profit        │
│ • Withdraw      │    │                 │    │                 │
└─────────┬───────┘    └─────────┬───────┘    └─────────┬───────┘
          │                      │                      │
          └──────────────────────┼──────────────────────┘
                                 │
                    ┌─────────────▼─────────────┐
                    │   Bitcoin Vault Core     │
                    │                           │
                    │ • Risk Management        │
                    │ • Position Tracking      │
                    │ • Collateral Engine      │
                    │ • Liquidation Engine     │
                    └─────────────┬─────────────┘
                                  │
                      ┌───────────▼───────────┐
                      │    STX Token Layer    │
                      │                       │
                      │ • STX Transfers       │
                      │ • Balance Management  │
                      │ • Collateral Storage  │
                      └───────────────────────┘
```

### Contract Architecture

The Bitcoin Vault Protocol is built as a single smart contract with modular functionality:

#### Core Components

1. **Risk Management Engine**
   - Dynamic collateral ratio calculations
   - Real-time health monitoring
   - Automated liquidation triggers

2. **Position Management System**
   - User portfolio tracking
   - Collateral and debt accounting
   - Interest calculation algorithms

3. **Liquidation Engine**
   - Community-driven liquidations
   - Automated position closure
   - Liquidator incentive mechanisms

4. **Administrative Framework**
   - Protocol parameter management
   - Fee structure configuration
   - Risk threshold adjustments

## 📊 Data Flow

### 1. Deposit Flow

```text
User → STX Transfer → Contract Storage → Position Update → Collateral Available
```

### 2. Borrow Flow

```text
User Request → Collateral Check → Risk Assessment → STX Transfer → Debt Recording
```

### 3. Repay Flow

```text
User Payment → STX Transfer → Debt Reduction → Position Update → Collateral Release
```

### 4. Liquidation Flow

```text
Health Monitor → Threshold Breach → Liquidator Action → Asset Transfer → Position Closure
```

## 🚀 Features

### Core Functionality

- **Collateralized Lending**: Deposit STX tokens as collateral to borrow against
- **Dynamic Risk Management**: Real-time collateral ratio monitoring and adjustment
- **Automated Liquidations**: Community-driven liquidation system for undercollateralized positions
- **Flexible Withdrawals**: Withdraw excess collateral while maintaining minimum ratios

### Key Benefits

- **Capital Efficiency**: Unlock liquidity without selling assets
- **Transparent Risk**: Clear collateral requirements and liquidation thresholds
- **Decentralized Governance**: Community-managed protocol parameters
- **Low Fees**: Minimal protocol fees for sustainable operation

## 📋 Protocol Parameters

| Parameter | Default Value | Range | Description |
|-----------|---------------|-------|-------------|
| Minimum Collateral Ratio | 150% | 110% - 500% | Minimum required collateralization |
| Liquidation Threshold | 130% | 110% - MCR | Health ratio triggering liquidation |
| Protocol Fee | 1% | 0% - 10% | Fee on borrowed amounts |

## 🔧 Smart Contract Interface

### Public Functions

#### Core Operations

- `deposit()` - Deposit STX as collateral
- `borrow(amount: uint)` - Borrow STX against collateral
- `repay(amount: uint)` - Repay borrowed STX
- `withdraw(amount: uint)` - Withdraw excess collateral
- `liquidate(user: principal)` - Liquidate undercollateralized position

#### Administrative Functions

- `set-minimum-collateral-ratio(new-ratio: uint)` - Update minimum collateral requirements
- `set-liquidation-threshold(new-threshold: uint)` - Update liquidation trigger point
- `set-protocol-fee(new-fee: uint)` - Update protocol fee structure

### Read-Only Functions

- `get-user-position(user: principal)` - Get user's position details
- `get-protocol-stats()` - Get comprehensive protocol statistics

## 🛡️ Security Features

### Risk Management

- **Minimum Collateral Ratios**: Enforced 150% default collateralization
- **Liquidation Thresholds**: Automated position closure at 130% health ratio
- **Parameter Bounds**: Strict limits on all configurable parameters

### Access Control

- **Owner-Only Administration**: Critical functions restricted to contract owner
- **Self-Liquidation Prevention**: Users cannot liquidate their own positions
- **Input Validation**: Comprehensive parameter and amount validation

### Error Handling

- Comprehensive error codes for all failure scenarios
- Atomic transaction guarantees
- Overflow protection on all calculations

## 🚦 Getting Started

### Prerequisites

- [Clarinet](https://github.com/hirosystems/clarinet) v2.0+
- [Node.js](https://nodejs.org/) v18+
- [Stacks CLI](https://docs.stacks.co/docs/stacks-cli)

### Installation

```bash
# Clone the repository
git clone https://github.com/dozie-ifenyine/bitcoin-vault.git
cd bitcoin-vault

# Install dependencies
npm install

# Check contract syntax
clarinet check

# Run tests
npm test
```

### Deployment

```bash
# Deploy to testnet
clarinet deploy --testnet

# Deploy to mainnet
clarinet deploy --mainnet
```

## 🧪 Testing

### Unit Tests

```bash
# Run all tests
npm test

# Run tests with coverage
npm run test:report

# Watch mode for development
npm run test:watch
```

### Test Coverage

- ✅ Core functionality (deposit, borrow, repay, withdraw)
- ✅ Liquidation scenarios
- ✅ Administrative functions
- ✅ Error conditions and edge cases
- ✅ Risk management calculations

## 📈 Usage Examples

### Basic Lending Flow

```javascript
// 1. Deposit collateral
await contractCall('deposit', []);

// 2. Borrow against collateral (maintaining 150% ratio)
const borrowAmount = 1000000; // 1 STX in microSTX
await contractCall('borrow', [borrowAmount]);

// 3. Repay loan
await contractCall('repay', [borrowAmount]);

// 4. Withdraw collateral
const withdrawAmount = 500000; // 0.5 STX
await contractCall('withdraw', [withdrawAmount]);
```

### Liquidation Example

```javascript
// Monitor position health
const userPosition = await contractCall('get-user-position', [userAddress]);
const ratio = (userPosition.totalCollateral * 100) / userPosition.totalBorrowed;

// Liquidate if below threshold
if (ratio < 130) {
  await contractCall('liquidate', [userAddress]);
}
```

## 🔍 Monitoring & Analytics

### Key Metrics

- **Total Value Locked (TVL)**: `total-deposits`
- **Total Borrowed**: `total-borrows`
- **Protocol Utilization**: `total-borrows / total-deposits`
- **Average Collateral Ratio**: Across all positions

### Health Monitoring

- Position-level health ratios
- Protocol-wide risk assessment
- Liquidation opportunity tracking

## 🤝 Contributing

We welcome contributions to the Bitcoin Vault Protocol! Please see our [Contributing Guidelines](CONTRIBUTING.md) for details.

### Development Workflow

1. Fork the repository
2. Create a feature branch
3. Write tests for new functionality
4. Ensure all tests pass
5. Submit a pull request

## 📜 License

This project is licensed under the ISC License - see the [LICENSE](LICENSE) file for details.
