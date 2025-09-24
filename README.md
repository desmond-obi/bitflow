# BitFlow Protocol

## Institutional Bitcoin Bridge Infrastructure

[![Clarity Version](https://img.shields.io/badge/clarity-v3-blue)](https://book.clarity-lang.org/)
[![Stacks](https://img.shields.io/badge/built%20on-Stacks-orange)](https://www.stacks.co/)
[![License](https://img.shields.io/badge/license-ISC-green)](LICENSE)

### Overview

BitFlow Protocol is an advanced cross-chain liquidity solution that seamlessly connects Bitcoin's Layer 1 security with Stacks Layer 2 DeFi capabilities. The protocol enables verified Bitcoin deposits to mint 1:1 backed sBTC tokens through a decentralized oracle network with enterprise-grade compliance and security features.

### Key Features

#### 🔐 **Decentralized Oracle Consensus**

Multi-signature validation from verified Bitcoin node operators ensuring transaction authenticity and cross-chain security.

#### ⚡ **Adaptive Security Framework**

Dynamic validation thresholds that scale with transaction volume and market conditions for optimal security-performance balance.

#### 🏛️ **Regulatory Compliance Layer**

Integrated KYC/AML screening with real-time address monitoring and configurable whitelist management for institutional adoption.

#### 🛡️ **Institutional Security Standards**

- Time-locked withdrawals
- Multi-signature custody
- Automated circuit breaker mechanisms
- Emergency pause functionality

#### ⚡ **Lightning Network Integration**

Atomic swap compatibility for instant Bitcoin settlement and enhanced liquidity provision.

#### 📊 **Transparent Reserve Management**

Real-time proof of reserves with immutable audit trails for complete transparency and trust.

## Architecture

### Core Components

```text
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Bitcoin L1    │◄──►│  BitFlow Core   │◄──►│   Stacks L2     │
│                 │    │                 │    │                 │
│ • BTC Deposits  │    │ • Oracle Net    │    │ • sBTC Tokens   │
│ • Tx Validation │    │ • Compliance    │    │ • DeFi Access   │
│ • Settlement    │    │ • Security      │    │ • Liquidity     │
└─────────────────┘    └─────────────────┘    └─────────────────┘
```

### Smart Contract Structure

- **Oracle Registry**: Manages authorized Bitcoin validators
- **Compliance System**: Whitelist and KYC/AML integration
- **Bridge Core**: Processes deposits and mints sBTC tokens
- **Security Layer**: Pause mechanisms and deposit limits
- **Fee Management**: Configurable bridge fees and treasury

## Getting Started

### Prerequisites

- [Clarinet](https://github.com/hirosystems/clarinet) v2.0+
- [Node.js](https://nodejs.org/) v18+
- [Git](https://git-scm.com/)

### Installation

1. **Clone the repository**

   ```bash
   git clone https://github.com/desmond-obi/bitflow.git
   cd bitflow
   ```

2. **Install dependencies**

   ```bash
   npm install
   ```

3. **Check contract validity**

   ```bash
   clarinet check
   ```

### Development

#### Running Tests

```bash
# Run all tests
npm test

# Run tests with coverage and gas cost analysis
npm run test:report

# Watch mode for development
npm run test:watch
```

#### Contract Validation

```bash
# Check contract syntax and type safety
clarinet check

# Format contracts
clarinet fmt

# Console REPL for testing
clarinet console
```

### Configuration

#### Protocol Parameters

| Parameter | Default Value | Description |
|-----------|---------------|-------------|
| Bridge Fee | 0.25% (25 bp) | Fee charged on deposits |
| Max Deposit | 500 BTC | Maximum single deposit limit |
| Oracle Threshold | Multi-sig | Consensus requirement |

#### Environment Settings

The protocol supports multiple deployment environments:

- **Devnet**: Development and testing
- **Testnet**: Public testing environment  
- **Mainnet**: Production deployment

Configuration files are located in the `settings/` directory.

## API Reference

### Public Functions

#### Oracle Management

```clarity
;; Register new oracle validator (Admin only)
(register-oracle (oracle-address principal))

;; Revoke oracle privileges (Admin only)  
(revoke-oracle (oracle-address principal))
```

#### Compliance Management

```clarity
;; Add address to whitelist (Admin only)
(whitelist-address (recipient principal))

;; Remove address from whitelist (Admin only)
(delist-address (recipient principal))
```

#### Core Bridge Operations

```clarity
;; Process Bitcoin deposit and mint sBTC tokens
(process-bitcoin-deposit 
  (bitcoin-tx-hash (string-ascii 64))
  (deposit-amount uint)
  (recipient-address principal))
```

#### Protocol Configuration

```clarity
;; Emergency pause/resume (Admin only)
(pause-protocol)
(resume-protocol)

;; Update bridge fee (Admin only)
(update-bridge-fee (new-fee-bp uint))

;; Adjust deposit limits (Admin only)
(update-deposit-limit (new-limit uint))
```

### Read-Only Functions

```clarity
;; Get total Bitcoin locked
(get-total-locked-bitcoin)

;; Check user sBTC balance
(get-user-balance (user principal))

;; Verify oracle status
(is-authorized-oracle (oracle principal))

;; Check whitelist status
(is-whitelisted-address (address principal))

;; Get protocol configuration
(get-protocol-config)

;; Check transaction processing status
(is-transaction-processed (btc-hash (string-ascii 64)))
```

## Security Features

### Access Control

- **Admin Functions**: Restricted to protocol administrator
- **Oracle Network**: Multi-signature validation requirements
- **Whitelist System**: Compliance-driven recipient validation

### Risk Management

- **Deposit Limits**: Configurable maximum deposit amounts
- **Duplicate Prevention**: Transaction hash tracking
- **Emergency Controls**: Protocol pause mechanism
- **Fee Protection**: Maximum fee caps (5%)

### Audit Trail

All protocol operations are logged on-chain with:

- Transaction hashes
- Timestamp information
- Amount tracking
- Participant addresses

## Error Codes

| Code | Constant | Description |
|------|----------|-------------|
| 100 | ERR-UNAUTHORIZED | Access denied |
| 101 | ERR-INVALID-AMOUNT | Invalid amount specified |
| 102 | ERR-INSUFFICIENT-BALANCE | Insufficient balance |
| 103 | ERR-PROTOCOL-PAUSED | Protocol is paused |
| 104 | ERR-DUPLICATE-TRANSACTION | Transaction already processed |
| 105 | ERR-ORACLE-CONSENSUS-FAILED | Oracle validation failed |
| 106 | ERR-RECIPIENT-NOT-WHITELISTED | Recipient not authorized |
| 107 | ERR-DEPOSIT-LIMIT-EXCEEDED | Deposit exceeds limit |
| 108 | ERR-INVALID-BITCOIN-HASH | Invalid transaction hash |
| 109 | ERR-INVALID-PARAMETERS | Invalid input parameters |

## Contributing

We welcome contributions to BitFlow Protocol! Please see our [Contributing Guidelines](CONTRIBUTING.md) for details.

### Development Process

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Make your changes
4. Add tests for new functionality
5. Ensure all tests pass (`npm test`)
6. Commit your changes (`git commit -m 'Add amazing feature'`)
7. Push to the branch (`git push origin feature/amazing-feature`)
8. Open a Pull Request

### Code Standards

- Follow Clarity best practices
- Maintain comprehensive test coverage
- Document all public functions
- Use clear, descriptive naming
- Include security considerations

## Deployment

### Testnet Deployment

```bash
# Deploy to testnet
clarinet deployments generate --testnet

# Check deployment status
clarinet deployments check --testnet
```

### Mainnet Deployment

```bash
# Generate mainnet deployment plan
clarinet deployments generate --mainnet

# Deploy to mainnet (requires signing)
clarinet deployments apply --mainnet
```

## Roadmap

### Phase 1: Core Infrastructure ✅

- [x] Basic bridge functionality
- [x] Oracle network integration
- [x] Compliance framework
- [x] Security mechanisms

### Phase 2: Advanced Features 🚧

- [ ] Lightning Network integration
- [ ] Multi-signature custody
- [ ] Advanced oracle consensus
- [ ] Governance token integration

### Phase 3: Ecosystem Expansion 📋

- [ ] Cross-chain interoperability
- [ ] Institutional custody solutions
- [ ] Advanced DeFi integrations
- [ ] Mobile wallet support

## License

This project is licensed under the ISC License - see the [LICENSE](LICENSE) file for details.

## Support

- **Documentation**: [docs.bitflow.finance](https://docs.bitflow.finance)
- **Discord**: [BitFlow Community](https://discord.gg/bitflow)
- **Twitter**: [@BitFlowProtocol](https://twitter.com/BitFlowProtocol)
- **Email**: [support@bitflow.finance](mailto:support@bitflow.finance)

## Acknowledgments

- [Stacks Foundation](https://stacks.org/) for the Bitcoin-powered smart contract platform
- [Hiro Systems](https://hiro.so/) for Clarinet development tools
- [Bitcoin Core](https://bitcoincore.org/) for the foundational Bitcoin infrastructure
