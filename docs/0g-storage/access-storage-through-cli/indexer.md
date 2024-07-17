# indexer

Due to the sharding mechanism, when the entire network data volume increases, an upload or download request for a single file may need to transfer data between multiple different storage nodes, how to find suitable storage nodes may become a problem for ordinary users.

Indexer is a service used to provide storage node queries, it is usually run by groups or individuals who maintain some stable storage nodes. It returns the trusted node list it maintains or the node list discovered through the p2p network to the user. To run an indexer service:

```bash
Usage:
  0g-storage-client indexer [flags]

Flags:
      --discover-interval duration            Interval to discover peers in network (default 10m0s)
      --endpoint string                       Indexer RPC endpoint (default ":12345")
      --ip-location-cache-file string         File name to cache ip locations (default ".ip-location-cache.json")
      --ip-location-cache-interval duration   Interval to write ip locations to cache file (default 10m0s)
      --node string                           Storage node to discover peers in P2P network
      --trusted strings                       Trusted storage node URLs that separated by comma
      --update-interval duration              Interval to update shard config of discovered peers (default 10m0s)
```

**Explanation:**

* P2P node discovery is enabled by set `--node`, the indexer service uses peer list of the storage node to update its own node list.

**Example:**

```bash
> 0g-storage-client indexer --endpoint :12345 --trusted http://ip1:5678,http://ip2:5678
```

This command will start an indexer service listening to port 12345.