# DA Node

This document outlines the steps to become a DA Signer and run your own DA node.

## DA Signer

To become a DA signer, users must have sufficient delegations to validators and register their signer information in the DASigners precompile contract. Registration can be automated by operating a DA node.

See [DASigners](<../docs/0G Chain/Precompiles/DASigners.md#terminology>) for more details.

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
eth_rpc_endpoint = "https://rpc-testnet.0g.ai"
# public grpc service socket address to register in DA contract
# http://ip:34000 (keep same port as the grpc listen address)
# or if you have dns, fill https://your.dns.ip
socket_address = "http(s)://<public_ip/dns>:34000"

# data availability contract to interact with
da_entrance_address = ""
# deployed block number of da entrance contract
start_block_number = 0

# signer BLS private key
signer_bls_private_key = ""
# signer eth account private key
signer_eth_private_key = ""

# whether to enable data availability sampling
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
