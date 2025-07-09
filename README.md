# Q3-25-Anchor-Vault

A simple Solana vault program built with the Anchor framework.
This project demonstrates how to create, deposit to, withdraw from, and close a vault account on Solana, with full TypeScript tests.
Table of Contents
Overview
How It Works
Program Structure
Accounts
Instructions
Getting Started
Prerequisites
Build & Test
Project Structure
How to Use
License
Overview
This project is a minimal Solana smart contract (program) for a "vault" system, where each user can:
Initialize their own vault (a PDA account)
Deposit SOL into their vault
Withdraw SOL from their vault
Close their vault and reclaim all funds
All logic is written in Rust using Anchor, and tested with TypeScript using the Anchor test framework.
How It Works
Program Structure
Rust program: Located in programs/anchor-vault/src/lib.rs
TypeScript tests: Located in tests/anchor-vault.ts
The program uses Program Derived Addresses (PDAs) to create unique vault accounts for each user, ensuring only the owner can interact with their vault.
Accounts

1. vault_state (PDA)
   Stores bump seeds for address derivation.
   Created with seeds: ["state", user_pubkey]
2. vault (PDA)
   Holds the actual SOL.
   Created with seeds: ["vault", vault_state_pubkey]
3. signer
   The user interacting with the vault.
4. system_program
   The built-in Solana program for account creation and SOL transfers.
   Instructions
5. Initialize
   Creates a new vault_state and vault PDA for the user.
   Transfers enough SOL to make the vault rent-exempt.
6. Deposit
   Transfers SOL from the user to their vault.
7. Withdraw
   Transfers SOL from the vault back to the user.
   Uses PDA seeds to sign for the vault.
8. Close
   Transfers all remaining SOL from the vault to the user.
   Closes the vault_state account, returning rent to the user.
   Getting Started
   Prerequisites
   Rust
   Solana CLI
   Node.js
   Yarn
   Anchor CLI
   Build & Test
   Apply to README.md
   test
   Project Structure
   Apply to README.md
   )
   How to Use
9. Initialize a Vault
   The user calls initialize, which creates their unique vault accounts.
10. Deposit SOL
    The user calls deposit(amount) to move SOL into their vault.
11. Withdraw SOL
    The user calls withdraw(amount) to move SOL from their vault back to their wallet.
12. Close Vault
    The user calls close to empty the vault and reclaim rent.
    All these actions are tested in tests/anchor-vault.ts using the Anchor TypeScript client.
    License
    MIT
    Example: Test Flow
    The test file (tests/anchor-vault.ts) demonstrates the full lifecycle:
    Initialize: Creates a vault for the test wallet.
    Deposit: Deposits 0.01 SOL.
    Withdraw: Withdraws 0.005 SOL.
    Close: Closes the vault and returns all funds.
    This project is a great starting point for learning Anchor and Solana PDAs!
    Feel free to fork, modify, and experiment.
