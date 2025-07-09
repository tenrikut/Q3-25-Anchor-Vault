# Q3-25-Anchor-Vault

A simple Solana vault program built with the [Anchor framework](https://book.anchor-lang.com/).

This project demonstrates how to create, deposit to, withdraw from, and close a vault account on Solana, with full TypeScript tests.

---

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [How It Works](#how-it-works)
  - [Program Structure](#program-structure)
  - [Accounts](#accounts)
  - [Instructions](#instructions)
- [Getting Started](#getting-started)
  - [Prerequisites](#prerequisites)
  - [Build & Test](#build--test)
- [Project Structure](#project-structure)
- [Usage](#usage)
- [License](#license)

---

## Overview

This project is a minimal Solana smart contract (program) for a "vault" system, where each user can:

- **Initialize** their own vault (a PDA account)
- **Deposit** SOL into their vault
- **Withdraw** SOL from their vault
- **Close** their vault and reclaim all funds

All logic is written in Rust using Anchor, and tested with TypeScript using the Anchor test framework.

---

## Features

- Each user gets a unique vault (like a private bank account)
- Deposit and withdraw SOL at any time
- Only the owner can access their vault
- Vaults are Program Derived Addresses (PDAs) for security
- Full test suite in TypeScript

---

## How It Works

### Program Structure

- **Rust program**: Located in `programs/anchor-vault/src/lib.rs`
- **TypeScript tests**: Located in `tests/anchor-vault.ts`

The program uses **Program Derived Addresses (PDAs)** to create unique vault accounts for each user, ensuring only the owner can interact with their vault.

### Accounts

#### 1. `vault_state` (PDA)

- Stores bump seeds for address derivation.
- Created with seeds: `['state', user_pubkey]`

#### 2. `vault` (PDA)

- Holds the actual SOL.
- Created with seeds: `['vault', vault_state_pubkey]`

#### 3. `signer`

- The user interacting with the vault.

#### 4. `system_program`

- The built-in Solana program for account creation and SOL transfers.

### Instructions

#### 1. **Initialize**

- Creates a new `vault_state` and `vault` PDA for the user.
- Transfers enough SOL to make the vault rent-exempt.

#### 2. **Deposit**

- Transfers SOL from the user to their vault.

#### 3. **Withdraw**

- Transfers SOL from the vault back to the user.
- Uses PDA seeds to sign for the vault.

#### 4. **Close**

- Transfers all remaining SOL from the vault to the user.
- Closes the `vault_state` account, returning rent to the user.

---

## Getting Started

### Prerequisites

- [Rust](https://www.rust-lang.org/tools/install)
- [Solana CLI](https://docs.solana.com/cli/install-solana-cli-tools)
- [Node.js](https://nodejs.org/)
- [Yarn](https://classic.yarnpkg.com/en/docs/install/)
- [Anchor CLI](https://book.anchor-lang.com/getting_started/installation.html)

### Build & Test

```sh
# Install dependencies
yarn install

# Build the program
anchor build

# Run tests (this will start a local validator, deploy, and test)
anchor test
```

---

## Project Structure

```
anchor-vault/
├── Anchor.toml                # Anchor config
├── Cargo.toml                 # Rust workspace config
├── programs/
│   └── anchor-vault/
│       ├── Cargo.toml
│       └── src/
│           └── lib.rs         # Main program logic
├── tests/
│   └── anchor-vault.ts        # TypeScript tests
├── migrations/
│   └── deploy.ts
├── package.json
├── tsconfig.json
└── target/                    # Build output (auto-generated)
```

---

## Usage

### 1. **Initialize a Vault**

- The user calls `initialize`, which creates their unique vault accounts.

### 2. **Deposit SOL**

- The user calls `deposit(amount)` to move SOL into their vault.

### 3. **Withdraw SOL**

- The user calls `withdraw(amount)` to move SOL from their vault back to their wallet.

### 4. **Close Vault**

- The user calls `close` to empty the vault and reclaim rent.

All these actions are tested in `tests/anchor-vault.ts` using the Anchor TypeScript client.

---

## License

MIT

---

**This project is a great starting point for learning Anchor and Solana PDAs!**
Feel free to fork, modify, and experiment.
