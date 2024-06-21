# Storage Node CLI

We provided a [client tool](https://github.com/0glabs/0g-storage-client) if you want to directly interact with the storage node.

1. Download the source code

```bash
git clone https://github.com/0glabs/0g-storage-client.git
```

2. Build the source code

```bash
cd 0g-storage-client
go build
```

3. Run the file upload/download commands

```bash
# file upload
./0g-storage-client upload --url <blockchain_rpc_endpoint> --contract <log_contract_address> --key <private_key> --node <storage_node_rpc_endpoint> --file <file_path>
# file download
./0g-storage-client download --node <storage_node_rpc_endpoint> --root <file_root_hash> --file <output_file_path>
# file download with verfication
./0g-storage-client download --node <storage_node_rpc_endpoint> --root <file_root_hash> --file <output_file_path> --proof
```

Check [Contract Addresses](../docs/contract-addresses.md) for log contract address.

> Note: You need to have the file root in order to download the file

For the storage node rpc endpoint, you could use the team deployed [https://rpc-storage-testnet.0g.ai](https://rpc-storage-testnet.0g.ai) or you could deploy yourself by following the above instructions.

During download, the `file_root_hash` can be retrieved from these places

* When you upload the file, the log will give you an information about the file root. Look for `Data merkle root calculated root=`.
* Locate your transaction with the transaction hash in the [https://storagescan-newton.0g.ai/](https://chainscan-newton.0g.ai/). Check the `Overview -> File Hash` in the tx detail page.
