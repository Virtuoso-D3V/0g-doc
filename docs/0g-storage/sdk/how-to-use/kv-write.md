# kv-write

The `kv-write` subcommand writes the user specified key-value pair to the key-value database.

The workflow of KV write is as follows:

1. A user defines the storage node (or indexer) which he/she wants the key-value data to be stored.
2. The user sets the key-value pairs.
3. The SDK will stream the key-value data and encode it to be the same format of a file data.
4. The process is the same as file upload.
5. The KV node will replay the log on the contract and try to update its key-value database if requirements are met.

To use it, run

```bash
./0g-storage-client kv-write \
    --url <blockchain_rpc> \
    --contract <flow_contract> \
    --indexer <indexer_rpc> \
    --node <storage_node_rpcs_separated_by_comma> \
    --stream-id <stream-id> \
    --stream-keys <keys_separated_by_comma> \
    --stream-values <values_separated_by_comma> \
    --task-size <segment_count_in_single_rpc_request> \
    --key <private_key> \
    --expected-replica <n_replica> \
    --version <version_number> \
    (--finality-required) \
    (--skip-tx)
```

**Explanation:**

* `--stream-id` is the stream id defined by the user. A stream id can be considered as a separate key-value db. Data in different stream ids do not share with each other. It mainly serves as a channel for various applications. For example, a user can define its own stream id and use that id for his own application (mysql, shared doc, etc).
* Use either `--node` or `--indexer` to define the storage location.
* `--stream-keys` and `--stream-values` should match the position of a key-value pair.
* `--task-size` is the number of segment to upload for each rpc request to storage node
* `--version` is the version number for each key to control the parallel access to the key. For example, a user is updating a key `b` using the value from key `a`. While updating, he reads that `a` has version number `10`. Also, during the update, another user is updating `a`, and the version number is updated to `20`. Both transactions are submitted on chain with the tx to update `a` before the tx to update `c`. When the kv instance is replaying the onchain logs, it will first update a and set its version number to `20`. Then when it executes the second transaction, it finds that the version of `a` is `10` which is smaller than `20`. So the second transaction is discarded.
* `--finality-required` is the flag for whether to wait for log finality
* `--skip-tx` is the flag for skipping tx if the data is already uploaded before (has same data root)

**Example:**

```bash
> ./0g-storage-client kv-write \
    --url https://rpc-testnet.0g.ai \
    --contract 0x8873cc79c5b3b5666535C825205C9a128B1D75F1 \
    --node https://rpc-storage-testnet.0g.ai \
    --stream-id 0x000000000000000000000000000000000000000000000000000000000000f2bd \
    --stream-keys TestKey0,TestKey1 \
    --stream-values TestValue0,TestValue1 \
    --key abc \
    --finality-required
    
INFO[2024-07-16T20:30:06+08:00] Data prepared to upload                       chunks=1 segments=1 size=142
INFO[2024-07-16T20:30:06+08:00] Data merkle root calculated                   root=0x679d54e08a4c330dd52805355f7fd727ce5d61c3d1a801f628c872bc2963db36
INFO[2024-07-16T20:30:08+08:00] Succeeded to send transaction to append log entry  hash=0x14b5995b4f04eaa0fdf8fc427756e873492be3e5300cf0d5b0da13c078f71ed0
INFO[2024-07-16T20:30:14+08:00] Upload small data immediately                
INFO[2024-07-16T20:30:14+08:00] Begin to upload file                          nodeNum=1 segNum=1
INFO[2024-07-16T20:30:15+08:00] Completed to upload file                      duration=576.900965ms segNum=1
INFO[2024-07-16T20:30:15+08:00] Wait for log entry on storage node            finality=true root=0x679d54e08a4c330dd52805355f7fd727ce5d61c3d1a801f628c872bc2963db36
INFO[2024-07-16T20:30:16+08:00] Log entry is unavailable yet                 
...                    
INFO[2024-07-16T20:31:38+08:00] upload took                                   duration=1m31.538677319s
```

From the console output it is shown that the log of the `kv-write` operation is similar to `upload` except that `kv-write` is for key-values pairs while `upload` is for files.
