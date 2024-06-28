# DA Retriever

This document outlines the steps to setup your own DA retriever.

### Hardware Requirement

The following hardware specifications are recommended for running a DA retriever:

* RAM: 8 GB
* CPU: 2 cores
* Bandwidth: 100 MBps for Download / Upload

### Installation

1. Install dependencies

* For Linux

    ```bash
    sudo apt-get update
    sudo apt-get install cmake build-essential protobuf-compiler
    ```

* For Mac

    ```bash
    brew install cmake
    ```

2. Install Rust

    ```bash
    curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
    ```

3. Download the source code

    ```bash
    git clone https://github.com/0glabs/0g-da-retriever.git
    ```

<a id="section1"></a>
### Configuration

| Field                                        | Description                                                                                |
|----------------------------------------------|--------------------------------------------------------------------------------------------|
| `log_level`                                  | Set log level.                                                                             |
| `grpc_listen_address`                        | Server listening address.                                                                  |
| `eth_rpc_endpoint`                           | JSON RPC node endpoint for the blockchain network.                                         |

### Run

1. Build in release mode
    ```bash
    cargo build --release
    ```
2. Run retriever

    Update configuration file run/config.toml as required by referencing the [Configuration](#section1).
    Run:

    ```bash
    ./target/release/retriever --config ./run/config.toml
    ```