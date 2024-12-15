# defi-empire
ERC20 and Vault Contracts

## Overview
This repository contains two core smart contracts:
1. **ERC20 Contract**: Implements a standard ERC20 token.
2. **Vault Contract**: Manages token deposits and withdrawals securely.

These contracts can be deployed on any Ethereum-compatible blockchain to create and manage a token and its associated vault functionalities.

---

## Features

### **ERC20 Contract**
- **Standard Token Functionality**:
  - Transfer tokens between accounts.
  - Approve and transfer tokens on behalf of another account.
  - Query token balances and allowances.
- **Customizable Parameters**:
  - Token name, symbol, initial supply, and decimal places.
- **Minting/Burning** (Optional):
  - If enabled, tokens can be minted or burned by the contract owner.

### **Vault Contract**
- **Deposit ERC20 Tokens**:
  - Allows users to deposit the ERC20 token into the vault.
- **Withdraw ERC20 Tokens**:
  - Users can withdraw their tokens from the vault.
- **Balance Tracking**:
  - Tracks deposits and allows secure withdrawals.
- **Admin Privileges** (Optional):
  - The admin can define additional rules or limits for deposits and withdrawals.

---

## Prerequisites

- **Node.js** (v14 or higher)
- **Hardhat** (for local development and testing)
- **Metamask** (or any other Web3 wallet)
- **Dependencies**:
  ```bash
  npm install --save-dev @openzeppelin/contracts ethers hardhat
  ```

---

## Deployment

### Step 1: Clone the Repository
```bash
git clone <repository-url>
cd <repository-folder>
```

### Step 2: Configure Environment

Create a `.env` file to store your private key and RPC URL:
```env
PRIVATE_KEY=<your-wallet-private-key>
RPC_URL=<your-ethereum-node-url>
```

### Step 3: Compile the Contracts
```bash
npx hardhat compile
```

### Step 4: Deploy the Contracts
Run the deployment script:
```bash
npx hardhat run scripts/deploy.js --network <network-name>
```
Replace `<network-name>` with the desired network (e.g., `localhost`, `goerli`, `mainnet`).

---

## Usage

### Interacting with the ERC20 Contract

#### Mint Tokens (if enabled):
```solidity
function mint(address to, uint256 amount) external;
```
- **Parameters**:
  - `to`: Address to receive the minted tokens.
  - `amount`: Number of tokens to mint.

#### Transfer Tokens:
```solidity
function transfer(address to, uint256 amount) external returns (bool);
```

#### Approve Allowance:
```solidity
function approve(address spender, uint256 amount) external returns (bool);
```

#### Transfer on Behalf:
```solidity
function transferFrom(address from, address to, uint256 amount) external returns (bool);
```

### Interacting with the Vault Contract

#### Deposit Tokens:
```solidity
function deposit(uint256 amount) external;
```
- **Preconditions**:
  - The user must first approve the Vault contract to spend the tokens.

#### Withdraw Tokens:
```solidity
function withdraw(uint256 amount) external;
```

#### Check Balance:
```solidity
function getBalance(address user) external view returns (uint256);
```

## Security Considerations

1. **Reentrancy**:
   - The Vault contract uses checks-effects-interactions to prevent reentrancy attacks.
2. **Access Control**:
   - Ensure only authorized accounts can mint or burn tokens (if enabled).
3. **Token Approvals**:
   - Be cautious with large approvals to avoid token theft.

---

## License
This project is licensed under the MIT License. See the `LICENSE` file for details.



## Acknowledgments
- [OpenZeppelin Contracts](https://github.com/OpenZeppelin/openzeppelin-contracts) for providing secure and tested smart contract libraries.
