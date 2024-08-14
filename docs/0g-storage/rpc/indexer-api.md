# Indexer API

### Table of Contents

* [Methods](indexer-api.md#methods)
* [Data Structure](indexer-api.md#data-structure)
  * [ShardedNodes](indexer-api.md#shardednodes)
  * [ShardedNode](indexer-api.md#shardednode)
  * [ShardConfig](indexer-api.md#shardconfig)
  * [IPLocation](indexer-api.md#iplocation)

### Methods

<table><thead><tr><th width="219">Method Name</th><th width="138">Request Type</th><th width="165">Response Type</th><th>Description</th></tr></thead><tbody><tr><td>getShardedNodes</td><td>-</td><td>ShardedNodes</td><td>This gets all the storage nodes whether it's trusted or discovered</td></tr><tr><td>getNodeLocations</td><td>-</td><td>map[string]*IPLocation</td><td>This gets the locations of storage nodes</td></tr><tr><td>getFileLocations</td><td>String</td><td>[]*shard.ShardedNode</td><td>This gets the locations of a data identified by its root</td></tr></tbody></table>

### Data Structure

#### ShardedNodes

<table><thead><tr><th width="167">Field</th><th width="179">Type</th><th>Description</th></tr></thead><tbody><tr><td>Trusted</td><td>[]*ShardedNode</td><td>Trusted storage nodes that are live and serving</td></tr><tr><td>Discovered</td><td>[]*ShardedNode</td><td>Discovered storage nodes in the storage network</td></tr></tbody></table>

#### ShardedNode

<table><thead><tr><th width="211">Field</th><th width="170">Type</th><th>Description</th></tr></thead><tbody><tr><td>URL</td><td>String</td><td>The endpoint of the node</td></tr><tr><td>Config</td><td>ShardConfig</td><td>The sharding config of the node</td></tr><tr><td>Latency</td><td>int64</td><td>The latency of the node in ms</td></tr><tr><td>Since</td><td>int64</td><td>The timestamp when last updated</td></tr></tbody></table>

#### ShardConfig

<table><thead><tr><th width="211">Field</th><th width="197">Type</th><th>Description</th></tr></thead><tbody><tr><td>ShardId</td><td>uint64</td><td>The id of the shard in &#x3C;id>/&#x3C;num></td></tr><tr><td>NumShard</td><td>uint64</td><td>The num of the shard in &#x3C;id>/&#x3C;num></td></tr></tbody></table>

#### IPLocation

<table><thead><tr><th width="211">Field</th><th width="197">Type</th><th>Description</th></tr></thead><tbody><tr><td>City</td><td>string</td><td>The city of the node</td></tr><tr><td>Region</td><td>string</td><td>The region of the node</td></tr><tr><td>Country</td><td>string</td><td>The country of the node</td></tr><tr><td>Location</td><td>string</td><td>The latitude/longitude of the node</td></tr><tr><td>Timezone</td><td>string</td><td>The timezone of the node</td></tr></tbody></table>
