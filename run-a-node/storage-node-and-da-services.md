# Storage Node And DA Services

0G System is composed of multiple components, each with its own functionalities. Detailed steps are provided as a guideline to deploy the whole and complete system.

* [Prerequisite](storage-node-and-da-services.md#prerequisite)
* [Storage Node](storage-node-and-da-services.md#storage-node)
* [Storage KV](storage-node-and-da-services.md#storage-kv)
* [Storage Node CLI](storage-node-and-da-services.md#storage-node-cli)

### Prerequisite

0G Storage and DA services interact with on-chain contracts for blob root confirmation and PoRA mining.

For official deployed contract addresses, visit [this page](../docs/contract-addresses.md).

### Storage Node

#### Hardware Requirement

```
- Memory: 16 GB RAM
- CPU: 4 cores
- Disk: 500GB / 1T NVME SSD
- Bandwidth: 500 MBps for Download / Upload
```

#### Deployment Steps

First step is to deploy the storage node. As a distributed storage system, the system can have multiple instances.

1. Install dependencies

* For Linux

<pre><code><strong>sudo apt-get update
</strong>sudo apt-get install clang cmake build-essential
</code></pre>

* For Mac

```bash
brew install llvm cmake
```

2. Install rustup

```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

3. Install Go

* For Linux

<pre class="language-bash"><code class="lang-bash"><strong># Download the Go installer
</strong>wget https://go.dev/dl/go1.22.0.linux-amd64.tar.gz

# Extract the archive
sudo rm -rf /usr/local/go &#x26;&#x26; sudo tar -C /usr/local -xzf go1.22.0.linux-amd64.tar.gz

# Add /usr/local/go/bin to the PATH environment variable by adding the following line to your ~/.profile.
export PATH=$PATH:/usr/local/go/bin
</code></pre>

* For Mac

Download the Go installer from [https://go.dev/dl/go1.22.0.darwin-amd64.pkg](https://go.dev/dl/go1.19.3.darwin-amd64.pkg).\
Open the package file you downloaded and follow the prompts to install Go.

4. Then download the source code

```bash
git clone -b v0.3.1 https://github.com/0glabs/0g-storage-node.git
```

5. Build the source code

```bash
cd 0g-storage-node
git submodule update --init

# Build in release mode
cargo build --release
```

6. Update the `run/config.toml`

```toml
# enr address, must fill your instance's public ip to support peer discovery
network_enr_address

# p2p port
network_libp2p_port

# rpc endpoint
rpc_listen_address

# peer nodes, we provided two nodes, you can also modify to your own ips
network_boot_nodes = ["/ip4/54.219.26.22/udp/1234/p2p/16Uiu2HAmTVDGNhkHD98zDnJxQWu3i1FL1aFYeh9wiQTNu4pDCgps","/ip4/52.52.127.117/udp/1234/p2p/16Uiu2HAkzRjxK2gorngB1Xq84qDrT4hSVznYDHj6BkbaE4SGx9oS"]

# flow contract address
log_contract_address

# mine contract address
mine_contract_address

# layer one blockchain rpc endpoint
blockchain_rpc_endpoint

# block number to start the sync
log_sync_start_block_number

# location for db, network logs
db_dir
network_dir

# your private key with 64 length
# do not include leading 0x
# do not omit leading 0
# must fill if you want to participate in the pora and get mining reward
miner_key
```

7. Run the storage service

```shell
cd run

# consider using tmux in order to run in background
../target/release/zgs_node --config config.toml
```

### Storage KV

Second step is to launch the kv service.

1. Follow the same steps to install dependencies and rust in [Stage 1](storage-node-and-da-services.md#id-2.-storage-node)
2. Download the source code

```bash
git clone https://github.com/0glabs/0g-storage-kv.git
```

3. Build the source code

<pre class="language-bash"><code class="lang-bash">cd 0g-storage-kv
<strong>git submodule update --init
</strong>
# Build in release mode
cargo build --release
</code></pre>

4. Copy the `config_example.toml` to `config.toml` and update the parameters

```toml
# rpc endpoint
rpc_listen_address
# ips of storage service, separated by ","
zgs_node_urls = "http://ip1:port1,http://ip2:port2,..."

# layer one blockchain rpc endpoint
blockchain_rpc_endpoint

# flow contract address
log_contract_address

# block number to start the sync, better to align with the config in storage service
log_sync_start_block_number
```

5. Run the kv service

```bash
cd run

# consider using tmux in order to run in background
../target/release/zgs_kv --config config.toml
```

Note: The recommended system configuration is the same as the storage node.



### You are all set !
