# Storage API

#### Instantiating a client <a href="#instantiating-a-client" id="instantiating-a-client"></a>

The client is an instance of the Client struct which has associated functions that wrap requests to the Storage Node RPC API endpoints.

A client is instantiated with a raw url through the following example.

<pre class="language-go"><code class="lang-go">import "github.com/0glabs/0g-storage-client/node"

// create instance of a 0g storage client
<strong>cl := node.MustNewZgsClient("http://localhost:5678")
</strong></code></pre>

#### Interacting with the client <a href="#interacting-with-a-client" id="interacting-with-a-client"></a>

The client can now be used to handle requests to the storage node using the full JSON-RPC API. For example, the function `GetStatus()` wraps a call to the `zgs_getStatus` endpoint. To fetch the file info from the client, the following example can be used.

<pre class="language-go"><code class="lang-go">import (
    "context"
    "github.com/ethereum/go-ethereum/common"
<strong>)
</strong><strong>
</strong><strong>ctx := context.Background()
</strong><strong>fileRoot := common.HexToHash()
</strong><strong>fileInfo, err := cl.GetFileInfo(ctx, fileRoot)
</strong>if err != nil {
    return err
}
</code></pre>

To upload files, a user can use the following example

<pre class="language-go"><code class="lang-go"><strong>import (
</strong><strong>    "logrus"
</strong>    "github.com/0glabs/0g-storage-client/indexer"
    zg_common "github.com/0glabs/0g-storage-client/common"
<strong>    "github.com/0glabs/0g-storage-client/transfer"
</strong><strong>    "github.com/ethereum/go-ethereum/common/hexutil"
</strong>    "github.com/0glabs/0g-storage-client/common/blockchain"
    "github.com/0glabs/0g-storage-client/contract"
    "github.com/0glabs/0g-storage-client/core"
<strong>)
</strong><strong>
</strong><strong>// Set the parameters
</strong>args := uploadArgs{
    file:     "test.txt",
    tags:     "0x",
    url:      "https://rpc-testnet.0g.ai",
    indexer:  "http://ip:12345",
    contract: "0xabc", // flow contract address
    key:      "abc", // private key
    expectedReplica: 1,
    finalityRequired:    true,
    skipTx: false,
    taskSize: 10,
    fee: 0, // optional, can remove and let the program to compute the fee automatically
}

// create a flow instance
w3client := blockchain.MustNewWeb3(args.url, args.key)
defer w3client.Close()
contractAddr := common.HexToAddress(args.contract)
flow, err := contract.NewFlowContract(contractAddr, w3client)
if err != nil {
    return
}

// instantiate a indexer client with logging configuration
indexerClient, err := indexer.NewClient(args.indexer, indexer.IndexerClientOption{LogOption: zg_common.LogOption{Logger: logrus.StandardLogger()}})
if err != nil {
    return
}

// set upload options
opt := transfer.UploadOption{
    Tags:             hexutil.MustDecode(args.tags),
    FinalityRequired: args.finalityRequired,
    TaskSize:         args.taskSize,
    ExpectedReplica:  args.expectedReplica,
    SkipTx:           args.skipTx,
    Fee:              args.Fee, // can remove
}

// read the file data
file, err := core.Open(args.file)
if err != nil {
    return
}
defer file.Close()

// upload the file
if err := indexerClient.Upload(ctx, flow, file, opt); err != nil {
    return
}
</code></pre>

To upload a pure bytes array, use the following example

```go
dataArray, err := core.NewDataInMemory([]byte("..."))
if err != nil {
    return errors.WithMessage(err, "failed to initialize data")
}

// upload the byte array
if err := indexerClient.Upload(ctx, flow, dataArray, opt); err != nil {
    return
}
```

#### Full API List&#x20;

The full list of low level client methods can be found at [ZeroGStorageClient](https://pkg.go.dev/github.com/0glabs/0g-storage-client@v0.3.0/node#ZeroGStorageClient). For higher level upload/download functions, please refer to [transfer](https://pkg.go.dev/github.com/0glabs/0g-storage-client@v0.3.0/transfer).
