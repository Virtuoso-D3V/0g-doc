# indexer

The `indexer` subcommand allows you to start a local indexing service for data upload/download. Since we split the file into chunks for data storage and replication, each chunk may be stored on different storage node. A indexing service can track the metadata of the file storage position during upload and use the corresponding storage node to download different chunks to get the whole file. To use it

```bash
./0g-storage-client indexer --endpoint <:port> --nodes <node1_ip>,<node2_ip>
```

Example:

```bash
./0g-storage-client indexer --endpoint :12345 --nodes http://ip1:5678,http://ip2:5678
```

You can run it in backend to start listening to the endpoint and serve.
