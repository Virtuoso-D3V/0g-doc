# Storage Node API

### Table of Contents

* [Methods](storage-node-api.md#methods)
* [Data Structure](storage-node-api.md#data-structure)
  * [SegmentWithProof](storage-node-api.md#segmentwithproof)
  * [DataRoot](storage-node-api.md#dataroot)
  * [Segment](storage-node-api.md#segment)
  * [FileInfo](storage-node-api.md#fileinfo)
  * [Transaction](storage-node-api.md#transaction)

### Methods

<table><thead><tr><th width="225">Method Name</th><th width="138">Request Type</th><th width="165">Response Type</th><th>Description</th></tr></thead><tbody><tr><td>uploadSegment</td><td>SegmentWithProof</td><td>-</td><td>This uploads segment to storage node</td></tr><tr><td>uploadSegments</td><td>[SegmentWithProof]</td><td>-</td><td>This uploads multiple segments at the same time to the storage node</td></tr><tr><td>downloadSegment</td><td>DataRoot, usize, usize</td><td>Segment</td><td>This download the segment by locating the data with the merkle root, start&#x26;end index</td></tr><tr><td>downloadSegmentWithProof</td><td>DataRoot, usize</td><td>SegmentWithProof</td><td>This downoads segment with the merkle proof</td></tr><tr><td>getFileInfo</td><td>DataRoot</td><td>FileInfo</td><td>This gets the file information given the data merkle root</td></tr><tr><td>getFileInfoByTxSeq</td><td>u64</td><td>FileInfo</td><td>This gets the file information by querying the correponsing sequence index</td></tr></tbody></table>

### Data Structure

#### SegmentWithProof

<table><thead><tr><th width="167">Field</th><th width="144">Type</th><th>Description</th></tr></thead><tbody><tr><td>root</td><td>DataRoot</td><td>File merkle root</td></tr><tr><td>data</td><td>[u8]</td><td>file data</td></tr><tr><td>index</td><td>usize</td><td>segment index</td></tr><tr><td>proof</td><td>FileProof</td><td>Merkle proof whose leaf node is the segment root</td></tr><tr><td>file_size</td><td>usize</td><td>file size</td></tr></tbody></table>

#### DataRoot

`DataRoot = H256`

#### Segment

`Segment = [u8]`

#### FileInfo

<table><thead><tr><th width="211">Field</th><th width="170">Type</th><th>Description</th></tr></thead><tbody><tr><td>tx</td><td>Transaction</td><td>file transaction</td></tr><tr><td>finalized</td><td>bool</td><td>whether the file is finalized</td></tr><tr><td>is_cached</td><td>bool</td><td>whether the file is cached</td></tr><tr><td>uploaded_seg_num</td><td>usize</td><td>number of the segments</td></tr></tbody></table>

#### Transaction

<table><thead><tr><th width="211">Field</th><th width="197">Type</th><th>Description</th></tr></thead><tbody><tr><td>stream_ids</td><td>[u256]</td><td>file transaction</td></tr><tr><td>data</td><td>[u8]</td><td>transaction data</td></tr><tr><td>data_merkle_root</td><td>DataRoot</td><td>merkle root of the data</td></tr><tr><td>merkle_nodes</td><td>[(usize, DataRoot)]</td><td>[(subtree_depth, subtree_root)]</td></tr><tr><td>start_entry_index</td><td>u64</td><td>index of the start entry</td></tr><tr><td>size</td><td>u64</td><td>data size</td></tr><tr><td>seq</td><td>u64</td><td>sequence number</td></tr></tbody></table>
