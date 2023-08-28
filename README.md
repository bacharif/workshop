# StarkNet First Project Guide

## Introduction

StarkNet is a decentralized, permissionless zk-rollup that allows you to build scalable and secure applications. This guide aims to walk you through the process of setting up your first StarkNet project using the `scarb` command-line tool.

The command-line suite `scarb` is a powerful utility for StarkNet development. It allows you to scaffold, build, and deploy smart contracts on the StarkNet network.

## Prerequisites

- A Unix-like operating system (Linux, macOS)
- Curl installed for downloading `scarb`, `starkli`
- Rust and Cargo for installing `katana`

### Installing Scarb CLI

\`\`\`bash
curl --proto '=https' --tlsv1.2 -sSf https://docs.swmansion.com/scarb/install.sh | sh
\`\`\`

### Installing Katana

\`\`\`bash
mkdir ~/.dojo && cd ~/.dojo
git clone https://github.com/dojoengine/dojo
cd dojo
cargo install --path ./crates/katana --locked --force
\`\`\`

### Installing Starkli

\`\`\`bash
curl https://get.starkli.sh | sh
\`\`\`

## Steps

### Step 1: Create a New Project

To create a new StarkNet project, use the `scarb new` command followed by your project's name:

\`\`\`bash
scarb new <project_name>
\`\`\`

### Step 2: Navigate to Project Directory

Navigate into the project directory:

\`\`\`bash
cd <project_name>
\`\`\`

### Step 3: Create the Signer

Create a new signer using Starkli:

\`\`\`bash
starkli signer keystore from-key ./keystore.json
\`\`\`

### Step 4: Set Up Account Descriptors

Complete the following JSON file to set up your account descriptors:

\`\`\`json
{
  "version": 1,
  "variant": {
    "type": "open_zeppelin",
    "version": 1,
    "public_key": "<SMART_WALLET_PUBLIC_KEY>"
  },
  "deployment": {
    "status": "deployed",
    "class_hash": "<SMART_WALLET_CLASS_HASH>",
    "address": "<SMART_WALLET_ADDRESS>"
  }
}
\`\`\`

To get `<SMART_WALLET_PUBLIC_KEY>`:

\`\`\`bash
starkli signer keystore inspect ~/.starkli-wallets/deployer/account0_keystore.json
\`\`\`

To get `<SMART_WALLET_CLASS_HASH>`:

\`\`\`bash
starkli class-hash-at <SMART_WALLET_ADDRESS> --rpc http://0.0.0.0:5050
\`\`\`

Note: Make sure you run the following command in another terminal before fetching the class hash:

\`\`\`bash
katana --accounts 3 --seed 0 --gas-price 250
\`\`\`

### Step 5: Explore the Project

Inside the project directory, you'll find several files and folders that make up the basic structure of a StarkNet project. You can now proceed to write your smart contracts, test them, and deploy them to the StarkNet network.

### Step 6: Declare the Smart Contract

Declare your smart contract using Starkli:

\`\`\`bash
starkli declare target/dev/workshop_SimpleStorage.sierra.json --compiler-version 2.1.0 --rpc http://0.0.0.0:5050 --account ~/.starkli-wallets/deployer/account0_account.json --keystore ~/.starkli-wallets/deployer/account0_keystore.json
\`\`\`

### Step 7: Deploy the Smart Contract

Deploy your smart contract using Starkli:

\`\`\`bash
starkli deploy 0x056486e36366049e8475e58e309668d0d829f8e7a1303737f1e6804844adfd09 42 --rpc http://0.0.0.0:5050 --account ~/.starkli-wallets/deployer/account0_account.json --keystore ~/.starkli-wallets/deployer/account0_keystore.json
\`\`\`

### Step 8: Call the Smart Contract

Call your smart contract using Starkli:

\`\`\`bash
starkli call 0x07ba115d69cb54cd1ab4559cfd2386ff7fa44303896507f6c610d005dd52a10e get --rpc http://0.0.0.0:5050
\`\`\`

### Step 9: Invoke a Function in the Smart Contract

Invoke a function in your smart contract using Starkli:

\`\`\`bash
starkli invoke 0x07ba115d69cb54cd1ab4559cfd2386ff7fa44303896507f6c610d005dd52a10e set 5 --rpc http://0.0.0.0:5050 --account ~/.starkli-wallets/deployer/account0_account.json --keystore ~/.starkli-wallets/deployer/account0_keystore.json
\`\`\`

## Summary

Here's a quick summary of the commands you'll run to start your first StarkNet project:

\`\`\`bash
# Install Scarb CLI
curl --proto '=https' --tlsv1.2 -sSf https://docs.swmansion.com/scarb/install.sh | sh

# Install Katana
mkdir ~/.dojo && cd ~/.dojo
git clone https://github.com/dojoengine/dojo
cd dojo
cargo install --path ./crates/katana --locked --force

# Install Starkli
curl https://get.starkli.sh | sh

# Create a new StarkNet project
scarb new <project_name>

# Navigate to the project directory
cd <project_name>

# Create the Signer
starkli signer keystore from-key ./keystore.json

# Declare the Smart Contract
starkli declare target/dev/workshop_SimpleStorage.sierra.json --compiler-version 2.1.0 --rpc http://0.0.0.0:5050 --account ~/.starkli-wallets/deployer/account0_account.json --keystore ~/.starkli-wallets/deployer/account0_keystore.json

# Deploy the Smart Contract
starkli deploy 0x056486e36366049e8475e58e309668d0d829f8e7a1303737f1e6804844adfd09 42 --rpc http://0.0.0.0:5050 --account ~/.starkli-wallets/deployer/account0_account.json --keystore ~/.starkli-wallets/deployer/account0_keystore.json
\`\`\`

# Call the Smart Contract
starkli call 0x07ba115d69cb54cd1ab4559cfd2386ff7fa44303896507f6c610d005dd52a10e get --rpc http://0.0.0.0:5050

# Invoke a Function in the Smart Contract
starkli invoke 0x07ba115d69cb54cd1ab4559cfd2386ff7fa44303896507f6c610d005dd52a10e set 5 --rpc http://0.0.0.0:5050 --account ~/.starkli-wallets/deployer/account0_account.json --keystore ~/.starkli-wallets/deployer/account0_keystore.json
\`\`\`

Happy coding! 🚀
# workshop
