# KV API

#### Instantiating a client <a href="#instantiating-a-client" id="instantiating-a-client"></a>

The client is an instance of the Client struct which has associated functions that wrap requests to the Storage Node RPC API endpoints.

A client is instantiated through the following example.

<pre class="language-go"><code class="lang-go">import (
<strong>    "github.com/0glabs/0g-storage-client/kv"
</strong>    "github.com/0glabs/0g-storage-client/node"
)
<strong>
</strong><strong>// create a node client
</strong><strong>client, err := node.NewClient("http://localhost:6789")
</strong>if err != nil {
    fmt.Println(err)
    return
}

// create the kv client with the node client
kvClient := kv.NewClient(client)
</code></pre>

#### Interacting with the client <a href="#interacting-with-a-client" id="interacting-with-a-client"></a>

Similar to [Storage Node API](kv-api.md#interacting-with-a-client), a user can call KV client RPC with the following example

```go
import (
    "context"
)

ctx := context.Background()
streamIds, err := kvClient.GetHoldingStreamIds(ctx)
// this api is used to check whether the kv operation is truly successful
// on the kv node, so this transaction is not the onchain transaction
// but rather the kv db operation.
isSuccessful, err := kvClient.GetTransactionResult(ctx, <seq_number>)
```

#### Writing data to client <a href="#querying-client-for-data" id="querying-client-for-data"></a>

The write operation of Storage KV is actually similar to writing file to storage node. It will first stream the key-value pairs to streaming data. Then it encodes the data to the same format that a file data has. After data processing, it calls the same API with the storage node upload operation to send the data to storage node. An example of Storage KV write is as follows.

<pre class="language-go"><code class="lang-go"><strong>import (
</strong><strong>    "github.com/0glabs/0g-storage-client/common/blockchain"
</strong><strong>    "github.com/0glabs/0g-storage-client/contract"
</strong><strong>)
</strong><strong>
</strong><strong>// Important! Use storage node ip
</strong><strong>zgsClient, err := node.NewClient("http://localhost:5678")
</strong>if err != nil {
<strong>    fmt.Println(err)
</strong>    return
}

// Create a blockchain client
privateKey := "0x"
blockchainClient := blockchain.MustNewWeb3("https://rpc-testnet.0g.ai", privateKey)
defer blockchainClient.Close()
blockchain.CustomGasLimit = 1000000

// Create a flow contract instance
FlowContractAddr := "0x8873cc79c5b3b5666535C825205C9a128B1D75F1"
flow, err := contract.NewFlowContract(common.HexToAddress(FlowContractAddr), blockchainClient)
if err != nil {
    fmt.Println(err)
    return
}

// Create batch upload client of kv
batcher := kv.NewBatcher(math.MaxUint64, []*node.Client{zgsClient}, flow)
// Set the key-value pairs
// Pass in the stream id that user wants to use for current kv operations
batcher.Set(common.HexToHash("0x000000000000000000000000000000000000000000000000000000000000f2bd"),
    []byte("TESTKEY0"),
    []byte{69, 70, 71, 72, 73},
)
batcher.Set(common.HexToHash("0x000000000000000000000000000000000000000000000000000000000000f2bd"),
    []byte("TESTKEY1"),
    []byte{74, 75, 76, 77, 78},
)
err = batcher.Exec(context.Background())
if err != nil {
    fmt.Println(err)
    return
}
</code></pre>

In the example, the stream id is a string that is predefined or created by authorized users to use for data uploading/downloading operations. Data in different stream ids are isolated. A user needs to keep the id to download the previous uploaded data.

#### Querying data from client <a href="#querying-client-for-data" id="querying-client-for-data"></a>

```go
import (
    ethCommon "github.com/ethereum/go-ethereum/common"
)
// Set the stream id of the kv client. This needs to be the same as the id
// when you uploaded the data
streamId := ethCommon.HexToHash("0x000000000000000000000000000000000000000000000000000000000000f2bd")
key := []byte("TESTKEY0")
// The data is fetched in chunks
// Call GetValue to easily get full data from remote kv instance
val, _ := kvClient.GetValue(ctx, streamId, key)
fmt.Println(string(val.Data))
```

#### Full API List&#x20;

The full list of client methods can be found [here](https://pkg.go.dev/github.com/0glabs/0g-storage-client@v0.3.0/kv#Client).
