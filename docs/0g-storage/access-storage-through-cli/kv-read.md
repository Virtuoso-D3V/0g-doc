# kv-read

The `kv-read`subcommand reads the user specified keys which were stored in the key-value database from a kv node endpoint. To use it

```
0g-storage-client kv-read \
    --node <kv_node_rpc> \
    --stream-id <stream_id_of_keys> \
    --stream-keys <keys_separated_by_comma>
```

**Example:**

```bash
> 0g-storage-client kv-read \
    --node http:// \
    --stream-id 0x000000000000000000000000000000000000000000000000000000000000f2bd \
    --stream-keys TestKey0,TestKey1

{"TestKey0":"TestValue0","TestKey1":"TestValue1"}
```

