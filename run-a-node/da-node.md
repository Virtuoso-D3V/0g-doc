# DA Node

This document outlines the steps to become a DA Signer and run your own DA node.
## DA Signer

To become a DA signer, user need to have enough delegations and register their signer information in the DASigners precompile contract. The registration can be done automatically by running a DA node.

See [DASigners](../docs/0G%20Chain/Precompiles/DASigners.md) for more details.

## DA Node

Each DA signer need to operate a DA node to perform encoded blob data verification, signing and store blob data for further farming and get rewards.

### Hardware Requirement

```
- Memory: 16 GB
- CPU: 8 cores
- Disk: 1 TB NVME SSD
- Bandwidth: 100 MBps for Download / Upload
```

### Installation

```
git clone https://github.com/0glabs/0g-da-node.git
cargo build --release
./dev_support/download_params.sh
```

### Configuration

Create a `config.toml` file and set the following field to proper values:

```toml
log_level = "info"

data_path = "./db/"

# path to downloaded params folder
encoder_params_dir = "params/" 

# grpc server listen address
grpc_listen_address = "0.0.0.0:34000"
# chain eth rpc endpoint
eth_rpc_endpoint = "http://0.0.0.0:8545"
# public grpc service socket address to register in DA contract
socket_address = "https://your.signer.com"

da_entrance_address = "0xDFC8B84e3C98e8b550c7FEF00BCB2d8742d80a69"
start_block_number = 0

# signer BLS private key
signer_bls_private_key = "1"
# signer eth account private key
signer_eth_private_key = ""

enable_das = "false"
```

On the first run of DA node, it will register the signer information in DA contract. To generate a BLS private key if don't have:
```
cargo run --bin key-gen
```
Please keep the generated BLS private key carefully.

### Run

```
./target/release/server --config cargo.toml
```