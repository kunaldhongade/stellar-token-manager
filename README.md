# Stellar Token Builder using Soroban

## Overview

This project demonstrates a **simple token creation system** built on the **Soroban smart contract platform** for the Stellar blockchain. The contract allows you to deploy tokens with specified metadata, manage balances, set allowances, and perform transfers. This modular contract leverages Soroban SDK to interact with accounts and maintain token data efficiently.

---

## Features

- **Token Initialization**: Create tokens with custom metadata like name, symbol, and decimal places.
- **Minting**: Admin can mint new tokens to specified accounts.
- **Transfer Mechanism**: Token holders can transfer tokens between accounts.
- **Allowance Management**: Set allowances for other accounts to spend tokens on behalf of the owner.
- **Balance Management**: Track account balances securely.
- **Admin Functions**: Admin control for minting and transferring tokens.

---

## Contract Modules

- **admin.rs**: Handles administrator roles for managing token operations.
- **allowance.rs**: Manages allowances between accounts for token spending.
- **balance.rs**: Provides utilities for reading and updating account balances.
- **contract.rs**: Main entry point with functions like initialization, transfer, and minting.
- **metadata.rs**: Stores and retrieves metadata such as token name, symbol, and decimals.
- **storage_types.rs**: Defines custom data structures used throughout the contract.
- **test.rs**: Contains unit tests for validating the contract’s behavior.

---

## Setup and Deployment

### Prerequisites

- **Rust** and **Cargo** installed.
- **Soroban CLI** installed: [Installation Guide](https://soroban.stellar.org/docs/getting-started/setup).
- **Stellar Wallet or Test Account** for deploying contracts on the testnet.

---

### Build the Contract

1. Navigate to the contract folder:
   ```bash
   cd contracts/lumifi_token_laucher
   ```

2. Build the contract using Soroban CLI:
   ```bash
   soroban contract build
   ```

3. Deploy the contract:
   ```bash
   soroban contract deploy --wasm target/wasm32-unknown-unknown/release/lumifi_token_laucher.wasm --network testnet
   ```

4. Note the **contract ID** from the deployment output, as it will be used for further interactions.

---

## Usage Guide

### 1. **Initialize Token**
Initialize a token with metadata such as name, symbol, and decimal points.

```bash
soroban contract invoke --id <CONTRACT_ID> --fn create_token --arg <ADMIN_ADDRESS> --arg 18 --arg "MyToken" --arg "MTK"
```

### 2. **Mint Tokens**
The admin can mint tokens for a specific account.

```bash
soroban contract invoke --id <CONTRACT_ID> --fn mint --arg <ACCOUNT_ADDRESS> --arg 1000
```

### 3. **Transfer Tokens**
A user can transfer tokens to another account.

```bash
soroban contract invoke --id <CONTRACT_ID> --fn transfer --arg <FROM_ADDRESS> --arg <TO_ADDRESS> --arg 50
```

### 4. **Set Allowance**
Set allowance for another account to spend on behalf of the owner.

```bash
soroban contract invoke --id <CONTRACT_ID> --fn approve --arg <OWNER_ADDRESS> --arg <SPENDER_ADDRESS> --arg 100
```

### 5. **Check Balance**
View the balance of a specific account.

```bash
soroban contract invoke --id <CONTRACT_ID> --fn balance --arg <ACCOUNT_ADDRESS>
```

---

## Example Workflow

1. **Create a Token:**
   Admin initializes a token named "MyToken" with the symbol "MTK".
2. **Mint Tokens:**
   Admin mints 1,000 tokens to User A.
3. **Transfer Tokens:**
   User A transfers 50 tokens to User B.
4. **Set Allowance:**
   User A approves User B to spend 100 tokens on their behalf.
5. **Check Balances:**
   Check the balances of User A and User B to confirm transactions.

---

## Testing

Use the included `test.rs` file to validate the contract’s behavior.

```bash
cargo test
```

---

## Troubleshooting

If you encounter issues during the build or deployment, ensure:

- Rust and Soroban CLI are correctly installed.
- The Stellar testnet is accessible.
- You have the correct contract ID and function names.

---

## License

This project is licensed under the MIT License.

---

## Conclusion

This project offers a simple but powerful token management system using Soroban on Stellar. It serves as a foundation for building more complex decentralized applications, such as liquidity pools, swaps, or DeFi solutions.
