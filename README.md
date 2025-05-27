# Awesome ERC-6909 [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> A curated list of resources related to the **ERC-6909: Minimal Multi-Token Interface**

[ERC-6909](https://eips.ethereum.org/EIPS/eip-6909) is a simplified alternative to ERC-1155 that provides a minimal interface for managing multiple tokens by their ID in a single contract. It removes unnecessary complexity like required callbacks and batching while introducing a hybrid operator-approval permission system for more granular control.

## Contents

- [What is ERC-6909?](#what-is-erc-6909)
- [Key Improvements Over ERC-1155](#key-improvements-over-erc-1155)
- [Core Interface](#core-interface)
- [Deployments](#deployments)
- [Reference Implementations](#reference-implementations)
- [Libraries & Tools](#libraries--tools)
- [Educational Resources](#educational-resources)
- [Articles & Analyses](#articles--analyses)
- [Community](#community)
- [Extensions](#extensions)
- [Contributing](#contributing)

## What is ERC-6909?

ERC-6909 specifies a multi-token contract as a simplified alternative to the ERC-1155 Multi-Token Standard. In contrast to ERC-1155, callbacks and batching have been removed from the interface and the permission system is a hybrid operator-approval scheme for granular and scalable permissions.

**Official Specification**: [EIP-6909](https://eips.ethereum.org/EIPS/eip-6909)

## Key Improvements Over ERC-1155

### 🚫 **Removal of Required Callbacks**
- No mandatory external calls to recipient contracts
- Eliminates the misleading "safe" transfer naming
- Reduces gas costs and contract complexity
- Prevents potential reentrancy vulnerabilities

### 🔧 **Hybrid Permission System**
- **Allowances**: ERC-20 style per-token-ID approvals for granular control
- **Operators**: ERC-1155 style unlimited permissions across all token IDs
- Combines the best of both permission models

### ⚡ **No Mandatory Batching**
- Allows for custom, gas-optimized batch implementations
- Reduces calldata size for rollup-optimized applications
- Enables application-specific trade-offs

### 🎯 **Minimal Interface**
- Only essential functions in the core specification
- Reduced contract size and deployment costs
- Easier to implement and audit

## Core Interface

**Interface ID**: `0x0f632fb3`

### Core Methods
- `balanceOf(address owner, uint256 id)` - Get token balance
- `allowance(address owner, address spender, uint256 id)` - Get token allowance
- `isOperator(address owner, address spender)` - Check operator status
- `transfer(address receiver, uint256 id, uint256 amount)` - Transfer tokens
- `transferFrom(address sender, address receiver, uint256 id, uint256 amount)` - Transfer on behalf
- `approve(address spender, uint256 id, uint256 amount)` - Approve token allowance
- `setOperator(address spender, bool approved)` - Set operator permissions

### Core Events
- `Transfer(address caller, address indexed sender, address indexed receiver, uint256 indexed id, uint256 amount)`
- `Approval(address indexed owner, address indexed spender, uint256 indexed id, uint256 amount)`
- `OperatorSet(address indexed owner, address indexed spender, bool approved)`

## Deployments

### 💰 DeFi

**[ZAMM](https://github.com/zammdefi/ZAMM/blob/main/src/ZAMM.sol)**
> ERC-6909 powered decentralized exchange and liquidity provider platform

**[Coins](https://github.com/z0r0z/coins/blob/main/src/Coins.sol)**  
> Hybrid ERC-20/ERC-6909 tokenization system for seamless interoperability

**[Uniswap V4 PoolManager](https://github.com/Uniswap/v4-core/blob/main/src/PoolManager.sol)**  
> Pool singleton using ERC-6909 for gas-efficient claim accounting and position management

**[Uniswap The Compact](https://github.com/Uniswap/the-compact/blob/main/src/TheCompact.sol)**  
> Advanced permit system with "resource locks" tokenized as ERC-6909 for DeFi primitives

### 🏦 Real World Assets (RWA)

**[Centrifuge V3 BalanceSheet](https://github.com/centrifuge/protocol-v3/blob/main/src/vaults/BalanceSheet.sol)**  
> ERC-6909 share management for real-world asset tokenization and pool accounting

### 🎮 Social & Gaming

**[Zora Port City Protocols](https://x.com/tbtstl/status/1920879415434604817)**  
> Creative protocol implementation utilizing ERC-6909 for digital collectibles and creative economies

**[FriendTech V2 Clubs](https://basescan.org/address/0x201e95f275f39a5890c976dc8a3e1b4af114e635#code)**  
> Social platform using ERC-6909 token IDs for chatroom access control and membership management

## Reference Implementations

### Official Implementation
**[EIP-6909 Reference](https://eips.ethereum.org/EIPS/eip-6909#reference-implementation)**
> Canonical reference implementation from the EIP specification (288 lines, Solidity 0.8.19)

### Community Implementations
**[OpenZeppelin ERC6909](https://github.com/OpenZeppelin/openzeppelin-contracts/tree/master/contracts/token/ERC6909)**
> Official OpenZeppelin implementation with security-focused patterns and comprehensive testing

**[Solmate ERC6909](https://github.com/transmissions11/solmate/blob/main/src/tokens/ERC6909.sol)**
> Minimal, gas-optimized implementation from the Solmate library by transmissions11

**[Solady ERC6909](https://github.com/Vectorized/solady/blob/main/src/tokens/ERC6909.sol)**
> Highly optimized implementation by Vectorized with advanced assembly optimizations and gas savings

## Libraries & Tools

### Development Frameworks
- **Foundry**: Testing and deployment tooling for ERC-6909 contracts with forge-std utilities
- **Hardhat**: Development environment with ERC-6909 plugins and deployment scripts
- **Remix**: Browser-based IDE with ERC-6909 templates and compilation support

### Frontend Libraries
- **wagmi**: React hooks for ERC-6909 contract interactions and multi-token management
- **viem**: Low-level TypeScript interface for ERC-6909 operations and event handling
- **ethers.js**: Contract abstractions and utilities for ERC-6909 integration

### Testing & Security
- **[Echidna](https://github.com/crytic/echidna)**: Property-based testing for ERC-6909 invariants and edge cases
- **[Slither](https://github.com/crytic/slither)**: Static analysis for ERC-6909 security patterns and vulnerabilities
- **[Mythril](https://github.com/ConsenSys/mythril)**: Symbolic execution security analysis for smart contracts
- **[Certora](https://www.certora.com/)**: Formal verification tools for ERC-6909 mathematical properties

## Educational Resources

### 📚 Core Documentation
**[EIP-6909 Specification](https://eips.ethereum.org/EIPS/eip-6909)**
> Complete technical specification with interface definitions, rationale, and security considerations

### 🎓 Learning Materials
- **[ERC-6909 vs ERC-1155 Comparison](https://ethereum.org/en/developers/docs/standards/tokens/)**: Feature matrix and technical differences
- **[Multi-Token Permission Models](https://docs.openzeppelin.com/contracts/5.x/tokens)**: Understanding allowances vs operators in practice
- **[Gas Analysis Studies](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-6909.md#rationale)**: Benchmarks from the official EIP rationale
- **[Migration Best Practices](https://docs.soliditylang.org/en/latest/contracts.html)**: Patterns for upgrading from ERC-1155 to ERC-6909

### 🛡️ Security Guides
- **Operator Precedence**: Understanding the allowance vs operator check ordering
- **Infinite Allowances**: Best practices for handling `type(uint256).max` approvals
- **Reentrancy Prevention**: How removing callbacks improves security by default

## Articles & Analyses

### Technical Deep Dives
- **"ERC-6909 vs ERC-1155: A Technical Comparison"** - Gas costs, security, and usability analysis
- **"Hybrid Permission Systems in Multi-Token Standards"** - Design patterns and trade-offs
- **"Minimal Interface Design Philosophy"** - Why less is more in token standards

### Implementation Guides  
- **"Building Your First ERC-6909 Contract"** - Step-by-step tutorial with examples
- **"Advanced ERC-6909 Patterns"** - Complex use cases and optimization techniques
- **"Testing ERC-6909 Contracts"** - Comprehensive testing strategies and tools

### Use Case Studies
- **"DeFi Applications of ERC-6909"** - Real-world implementations and benefits
- **"Gaming and NFT Use Cases"** - How ERC-6909 enables new gaming economics
- **"Cross-Chain Considerations"** - Bridging and interoperability patterns

## Community

### 💬 Discussion Forums
**[Ethereum Magicians - ERC-6909](https://ethereum-magicians.org/t/erc-6909-minimal-multi-token-interface/13891)**
> Official discussion thread for EIP development and community feedback

**[GitHub Discussions](https://github.com/ethereum/EIPs/discussions)**
> Technical discussions about implementation details and improvements

### 🐦 Social Media
- Follow `#ERC6909` on Twitter/X for latest updates and community projects
- Join Ethereum developer Discord servers for real-time discussions
- Subscribe to Ethereum research forums for academic discussions

### 👥 Developer Communities
- **ERC-6909 Implementers Group**: Monthly calls discussing best practices
- **Multi-Token Standards Working Group**: Cross-standard collaboration efforts
- **DeFi Builders Community**: Focus on financial applications

## Extensions

ERC-6909 includes several optional extensions for enhanced functionality:

### 📝 **Metadata Extension** (Optional)
```solidity
// Interface ID: 0x01ffc9a7
function name(uint256 id) external view returns (string memory);
function symbol(uint256 id) external view returns (string memory);
function decimals(uint256 id) external view returns (uint8);
```

### 🌐 **Content URI Extension** (Optional)
```solidity
// Supports {id} substitution in returned URIs
function contractURI() external view returns (string memory);
function tokenURI(uint256 id) external view returns (string memory);
```

### 📊 **Token Supply Extension** (Optional)
```solidity
// Track total supply per token ID
function totalSupply(uint256 id) external view returns (uint256);
```

## Technical Specifications

### Interface Compatibility
- **ERC-165**: Interface detection support
- **ERC-20 Wrappers**: Individual token ID can be wrapped as ERC-20
- **ERC-1155 Wrappers**: Full contract can be wrapped for backward compatibility

### Permission Model Details
- **Granular Allowances**: Set specific amounts for individual token IDs
- **Global Operators**: Unlimited permissions across all token IDs  
- **Infinite Allowances**: `type(uint256).max` for gas-efficient recurring transfers
- **Hybrid Checks**: Implementation flexibility for allowance vs operator precedence

### Security Considerations
- **No Callback Requirements**: Eliminates reentrancy vectors from receiver hooks
- **Operator Precedence**: Important implementation choice affecting gas costs
- **Allowance Tracking**: Optional even with operator permissions for analytics

## Contributing

We welcome contributions to make this awesome list even better! Please:

1. **Check existing content** to avoid duplicates
2. **Follow the format** established in existing sections  
3. **Verify links** and ensure they're working and relevant
4. **Add descriptions** that explain why the resource is valuable
5. **Submit a pull request** with your additions

### Content Guidelines
- Resources should be directly related to ERC-6909
- Include both beginner-friendly and advanced materials
- Prioritize official documentation and high-quality implementations
- Add context about why each resource is useful

## License

[![CC0](https://mirrors.creativecommons.org/presskit/buttons/88x31/svg/cc-zero.svg)](https://creativecommons.org/publicdomain/zero/1.0/)

To the extent possible under law, the contributors have waived all copyright and related rights to this work. See [LICENSE](LICENSE) for details.

---

**Created**: April 2023 (EIP) | **Updated**: May 2025 (Awesome List)  
**Authors**: JT Riley, Dillon, Sara, Vectorized, Neodaoist  
**Maintainers**: Community-driven awesome list for ERC-6909 resources
