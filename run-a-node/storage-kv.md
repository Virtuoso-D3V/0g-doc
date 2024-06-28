# Storage KV

Detailed steps are provided as a guideline to deploy the Storage KV Client, which is a KV runtime built on top of the log layer.

* [Prerequisite](storage-kv.md#prerequisite)
* [Storage Node](storage-kv.md#storage-node)
* [Storage KV](storage-kv.md#storage-kv)
* [Storage Node CLI](storage-kv.md#storage-node-cli)

### Prerequisite

0G KV interact with on-chain contracts and storage nodes to simulate the KV data streams.

For official deployed contract addresses, visit [this page](../docs/contract-addresses.md).

### Storage KV

#### Hardware Requirement

```
- Memory: 16 GB RAM
- CPU: 4 cores
- Disk: 500GB / 1T NVME SSD
- Bandwidth: 500 MBps for Download / Upload
```

### Storage KV

1. Follow the same steps to install dependencies and rust in [storage node](storage-node.md#id-2.-storage-node)
2. Download the source code

```bash
git clone -b v1.1.0-testnet https://github.com/0glabs/0g-storage-kv.git
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

# storage nodes to download data from, separated by ","
# the provided nodes should cover full data in the storage network
zgs_node_urls
```

5. Run the kv service

```bash
cd run

# consider using tmux in order to run in background
../target/release/zgs_kv --config config.toml
```

Note: The recommended system configuration is the same as the storage node.

### You are all set !