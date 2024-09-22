# 🥢 Open Hack Chopstick

## 📝 Introduction

Chopsticks is a powerful tool that allows you to create a parallel reality of your Substrate network. It's useful for testing, development, and experimentation with blockchain networks.

## 📝 Prerequisites

Before we start, ensure you have the following:

1. **🦀 Rust**: Install Rust and set up your environment.
   - 🔧 Install Rust: [Rust Installation Guide](https://www.rust-lang.org/tools/install)
   - 🎯 Add the wasm32-unknown-unknown target:
     ```bash
     rustup target add wasm32-unknown-unknown
     ```

2. **💻 Visual Studio Code (VS Code)**: Set up VS Code for Rust and Substrate development.
   - 📥 Download and install VS Code from the [official website](https://code.visualstudio.com/).
   - 🧩 Install the following extensions in VS Code:
     - **🦀 Rust Extension**:
       - 🔍 Go to the Extensions view (`Ctrl+Shift+X`).
       - 🔎 Search for "Rust" and install the [Rust extension by rust-lang](https://marketplace.visualstudio.com/items?itemName=rust-lang.rust).
     - **🧬 Substrate Extension**:
       - 🔍 In the Extensions view, search for "Substrate" and install the [Substrate extension](https://marketplace.visualstudio.com/items?itemName=paritytech.vscode-substrate).
     - **🔬 Rust Analyzer Extension (Recommended)**:
       - 🚀 This extension provides enhanced Rust language support, including code completion and inline error checking.
       - 🔎 Search for "Rust Analyzer" in the Extensions view and install the [Rust Analyzer extension](https://marketplace.visualstudio.com/items?itemName=matklad.rust-analyzer).

### 📦 Setup on Different Operating Systems

### 🪟 Windows

1. **🦀 Install Rust**:
   - **🔄 Option 1: Native Windows Installation**
     - 📥 Download and install Rust using the installer provided at the [official Rust website](https://www.rust-lang.org/tools/install).
     - 🖥️ Open Command Prompt (cmd) or PowerShell and run:
       ```bash
       rustup target add wasm32-unknown-unknown
       ```
   - **🐧 Option 2: Using WSL2 (Recommended)**
     - 🔧 Install WSL2 if you haven't already by following the [WSL installation guide](https://docs.microsoft.com/en-us/windows/wsl/install).
     - 📦 Install a Linux distribution from the Microsoft Store (e.g., Ubuntu).
     - 🖥️ Open your WSL2 terminal (e.g., Ubuntu) and install Rust:
       ```bash
       curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
       ```
     - 🎯 After installation, add the wasm32 target:
       ```bash
       rustup target add wasm32-unknown-unknown
       ```

2. **🥢 Install Chopsticks**:
   - **🔄 Option 1: Native Windows Installation**
     - 🖥️ Open Command Prompt or PowerShell and run:
       ```bash
       cargo install chopsticks --git https://github.com/AcalaNetwork/chopsticks.git
       ```
   - **🐧 Option 2: Using WSL2**
     - 🖥️ In your WSL2 terminal, run:
       ```bash
       cargo install chopsticks --git https://github.com/AcalaNetwork/chopsticks.git
       ```

3. **📦 Install Node.js and NPM** (optional, but useful for some Substrate development tasks):
   - **🔄 Option 1: Native Windows Installation**
     - 📥 Download the Windows installer from the [Node.js website](https://nodejs.org/) and run it.
     - ✅ Confirm installation by running in Command Prompt:
       ```bash
       node -v
       npm -v
       ```
   - **🐧 Option 2: Using WSL2**
     - 🖥️ In your WSL2 terminal, install Node.js using the package manager:
       ```bash
       sudo apt update
       sudo apt install nodejs npm
       ```
     - ✅ Confirm installation by running:
       ```bash
       node -v
       npm -v
       ```

## 🚀 Quick Start

To quickly fork an existing network (e.g., Acala mainnet), run:

```bash
npx @acala-network/chopsticks@latest --endpoint=wss://acala-rpc-2.aca-api.network/ws
```

## 📁 Using Configuration Files

For more complex setups, it's recommended to use a configuration file. Create a file named `chopsticks.yml` in your project root:

```yaml
endpoint: "ws://127.0.0.1:9944"
mock-signature-host: true
db: ./db.sqlite

import-storage:
  System:
    Account:
      - - "5GrwvaEF5zXb26Fz9rcQpDWS57CtERHpNehXCPcNoHGKutQY"
        - data:
            free: "1000000000000000000000"
  Balances:
    TotalIssuance: "1000000000000000000000"

runtime:
  wasm_file: ./runtime/target/release/wbuild/node-runtime/node_runtime.wasm
```

To run Chopsticks with a config file:

```bash
npx @acala-network/chopsticks@latest -c acala
```

## 🏃‍♂️ Advanced Usage

### 🔄 Replay Blocks

To replay the latest block:

```bash
npx @acala-network/chopsticks@latest run-block --endpoint=wss://acala-rpc-2.aca-api.network/ws
```

Options:
- `-b|--block`: Replay a specific block hash
- `--output-path=<file_path>`: Print out JSON file
- `--html`: Generate storage diff preview
- `--open`: Automatically open the HTML file

### 🧪 Dry Run

Dry run an extrinsic:

```bash
npx @acala-network/chopsticks@latest dry-run --config=configs/mandala.yml --html --open --extrinsic=0x...
```

Dry run a call (with mocked signature):

```bash
npx @acala-network/chopsticks@latest dry-run --config=configs/mandala.yml --html --open --extrinsic=0x... --address=5GrwvaEF5zXb26Fz9rcQpDWS57CtERHpNehXCPcNoHGKutQY
```

### 🌐 XCM Multichain Setup

To set up an XCM multichain environment:

```bash
npx @acala-network/chopsticks@latest xcm -r kusama -p karura -p statemine
```

### 🔌 Plugins and RPC Methods

Chopsticks supports plugins and custom RPC methods. To load custom RPC methods:

```bash
npx @acala-network/chopsticks@latest --unsafe-rpc-methods=rpc-methods-scripts.js
```

⚠️ **Warning**: Only load trusted scripts as this feature is unsafe.

### 📦 Prefetching Storages

For testing big migrations, you can prefetch and cache storages. Add a `prefetch-storages` section to your config file:

```yaml
prefetch-storages:
  - '0x123456'
  - Balances
  - Tokens.Accounts
  - System: Account
  - Tokens:
      Accounts: [5GrwvaEF5zXb26Fz9rcQpDWS57CtERHpNehXCPcNoHGKutQY]
```

Alternatively, use the `fetch-storages` subcommand:

```bash
npx @acala-network/chopsticks@latest fetch-storages 0x123456 Balances Tokens.Accounts --endpoint=wss://acala-rpc-0.aca-api.network --block=<blockhash> --db=acala.sqlite
```

## 🎭 Try-Runtime CLI

Chopsticks also includes a Try-Runtime CLI for advanced testing and migration scenarios. Refer to the [Try-Runtime documentation](packages/chopsticks/src/plugins/try-runtime/README.md) for more information.

## 🌐 Web Testing

Chopsticks can run in a browser environment, allowing you to turn a mainnet into a devnet directly in your browser. Check out the example at [acalanetwork.github.io/chopsticks](https://acalanetwork.github.io/chopsticks/).

## 🔗 Additional Resources

- [Chopsticks Wiki](https://github.com/AcalaNetwork/chopsticks/wiki)
- [EVM+ Tracing Documentation](packages/chopsticks/src/plugins/trace-transaction/README.md)

By following this enhanced tutorial, you'll be able to leverage the full power of Chopsticks for simulating, testing, and experimenting with Substrate-based blockchain networks.
