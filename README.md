# 🥢 Enhanced Tutorial: Simulating a Substrate-based Blockchain Network with Chopsticks

## 📝 Introduction

Chopsticks is a powerful tool that allows you to create a parallel reality of your Substrate network. It's useful for testing, development, and experimentation with blockchain networks.

## 📋 Prerequisites

Before we start, ensure you have the following:

1. **🦀 Rust**: Install Rust (version >= 1.64) and set up your environment.
   - 🔧 Install Rust: [Rust Installation Guide](https://www.rust-lang.org/tools/install)
   - 🎯 Add the wasm32-unknown-unknown target:
     ```bash
     rustup target add wasm32-unknown-unknown
     ```

2. **💻 Node.js and npm**: Install Node.js and npm (useful for some Substrate development tasks).

3. **🧰 Development Environment**: Set up your preferred IDE (e.g., Visual Studio Code) with Rust and Substrate extensions.

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
