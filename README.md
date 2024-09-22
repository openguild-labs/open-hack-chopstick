# 🥢 Tutorial: Simulating a Substrate-based Blockchain Network with Chopsticks

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

[Continue with setup instructions for 🍎 macOS and 🐧 Linux...]

## 🚀 Step 1: Prepare Your Substrate Project

🔧 Ensure your Substrate-based project is set up and compiled. You'll need the WebAssembly runtime file and the genesis configuration.

## 📝 Step 2: Create a Chopsticks Configuration File

🗒️ Create a file named `chopsticks.yml` in your project root. This file will define your network configuration:

```yaml
endpoint: "ws://127.0.0.1:9944"
mock-signature-host: true
db: ./db.sqlite

import-storage:
  System:
    Account:
      -
        - - "5GrwvaEF5zXb26Fz9rcQpDWS57CtERHpNehXCPcNoHGKutQY"
        - data:
            free: "1000000000000000000000"
  Balances:
    TotalIssuance: "1000000000000000000000"

runtime:
  wasm_file: ./runtime/target/release/wbuild/node-runtime/node_runtime.wasm
```

🔧 Adjust the `endpoint`, `wasm_file` path, and account details as needed for your project.

## 🏃‍♂️ Step 3: Run the Simulation

🖥️ Execute the following command to start your simulation:

```bash
chopsticks
```

🚀 Chopsticks will use the configuration from `chopsticks.yml` to set up and run your simulated network.

## 🔗 Step 4: Interact with the Simulated Network

🕹️ You can now interact with your simulated network using tools like Polkadot.js or custom scripts. The network will be accessible at the endpoint specified in your configuration file.

## 🧪 Step 5: Testing and Experimentation

Use this simulated environment to:
- 🔄 Test runtime upgrades
- 🔬 Experiment with different network configurations
- 🐞 Debug issues in a controlled setting
- ✅ Perform integration tests

## 🎉 Conclusion

🥢 Chopsticks provides a powerful way to simulate and test Substrate-based blockchain networks. By following this tutorial, you've learned how to set up and run a basic simulation. 📚 Explore the Chopsticks documentation for more advanced features and configurations to enhance your blockchain development workflow.
