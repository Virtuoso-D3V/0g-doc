# indexer

The `indexer` subcommand allows a user to start a global indexing service for data upload/download. Since we split the file into chunks for data storage and replication, each chunk may be stored on different storage node. A indexing service can track the metadata of the file storage position during upload and use the corresponding storage node to download different chunks to get the whole file. To use it

```bash
0g-storage-client indexer \
    --endpoint <:port> \
    --trusted <node1_ip>,<node2_ip> \
    --node <node_admin_ip> \
    --update-interval <interval_between_shard_update> \
    --discover-interval <interval_between_node_discovery>
```

**Explanation:**

* trusted

**Example:**

```bash
> 0g-storage-client indexer --endpoint :12345 --node http://ip1:5679 --trusted http://ip1:5678
```

Nothing will print out in the console. You can run it in backend to start listening to the endpoint and serve.
