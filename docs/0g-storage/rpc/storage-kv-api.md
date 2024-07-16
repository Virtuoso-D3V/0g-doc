# Storage KV API

### Table of Contents

* [Methods](storage-kv-api.md#methods)
* [Data Structure](storage-kv-api.md#data-structure)
  * [ValueSegment](storage-kv-api.md#valuesegment)
  * [KeyValueSegment](storage-kv-api.md#keyvaluesegment)

### Methods

<table><thead><tr><th width="225">Method Name</th><th width="138">Request Type</th><th width="181">Response Type</th><th>Description</th></tr></thead><tbody><tr><td>getStatus</td><td>-</td><td>-</td><td>This checks the node status</td></tr><tr><td>getValue</td><td>[H256, Segment, u64, u64, Option&#x3C;u64>]</td><td>ValueSegment</td><td>This retrieves a value by the key and the stream id</td></tr><tr><td>getNext</td><td>[H256, Segment, u64, u64, bool, Option&#x3C;u64>]</td><td>KeyValueSegment</td><td>This gets the next key-value from the key position</td></tr><tr><td>getPrev</td><td>[H256, Segment, u64, u64, bool, Option&#x3C;u64>]</td><td>KeyValueSegment</td><td>This gets the previous key-value from the key position</td></tr><tr><td>getFirst</td><td>[H256, Segment, u64, u64, Option&#x3C;u64>]</td><td>KeyValueSegment</td><td>This gets the first key-value in a particular stream</td></tr><tr><td>getLast</td><td>[H256, Segment, u64, u64, Option&#x3C;u64>]</td><td>KeyValueSegment</td><td>This gets the last key-value in a particular stream</td></tr><tr><td>getTransactionResult</td><td>[u64]</td><td>String</td><td>This gets the result of a transaction by tx seq</td></tr><tr><td>getHoldingStreamIds</td><td>-</td><td>[H256]</td><td>This gets the stream ids that the kv instance maintains</td></tr><tr><td>hasWritePermission</td><td>[H160, H256, Segment, Option&#x3C;u64>]</td><td>bool</td><td>This checks whether an account has write permission to a key in the stream</td></tr><tr><td>isAdmin</td><td>[H160, H256,  Option&#x3C;u64>]</td><td>bool</td><td>This checks whether an account is admin</td></tr><tr><td>isSpecialKey</td><td>[H256, Segment, Option&#x3C;u64>]</td><td>bool</td><td>This checks whether a key is a special key</td></tr><tr><td>isWriterOfKey</td><td>[H160, H256, Segment, Option&#x3C;u64>]</td><td>bool</td><td>This checks whether an account has write permission to a special key in the stream</td></tr><tr><td>isWriterOfStream</td><td>[H160, Segment, Option&#x3C;u64>]</td><td>bool</td><td>This checks whether an account has write permission to a stream</td></tr></tbody></table>

### Data Structure

#### ValueSegment

<table><thead><tr><th width="159">Field</th><th width="141">Type</th><th>Description</th></tr></thead><tbody><tr><td>version</td><td>u64</td><td>An update prefix of a key in the kv store</td></tr><tr><td>data</td><td>[u8]</td><td>value mapped to the key</td></tr><tr><td>size</td><td>usize</td><td>data total size</td></tr></tbody></table>

#### KeyValueSegment

<table><thead><tr><th width="158">Field</th><th width="165">Type</th><th>Description</th></tr></thead><tbody><tr><td>version</td><td>u64</td><td>An update prefix of a key in the kv store</td></tr><tr><td>key</td><td>[u8]</td><td>key of the kv pair</td></tr><tr><td>data</td><td>[u8]</td><td>value mapped to the key</td></tr><tr><td>size</td><td>usize</td><td>data total size</td></tr></tbody></table>
