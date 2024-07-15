# Storage Node API

#### Instantiating a client <a href="#instantiating-a-client" id="instantiating-a-client"></a>

The client is an instance of the Client struct which has associated functions that wrap requests to the Storage Node RPC API endpoints.

A client is instantiated with a raw url through the following example.

<pre class="language-go"><code class="lang-go">import "github.com/0glabs/0g-storage-client/node"

// create instance of a client
<strong>cl, err := node.NewClient("http://storage-ip:5678")
</strong>if err != nil {
    panic(err)
}
// storage node client can be retrieved by
sn := cl.ZeroGStorage()
</code></pre>

#### Interacting with the client <a href="#interacting-with-a-client" id="interacting-with-a-client"></a>

The client can now be used to handle requests to the storage node using the full JSON-RPC API. For example, the function `GetStatus()` wraps a call to the `zgs_getStatus` endpoint. To fetch the file info from the client, the following example can be used.

<pre class="language-go"><code class="lang-go">import "github.com/ethereum/go-ethereum/common"
<strong>
</strong><strong>fileRoot := common.HexToHash()
</strong><strong>fileInfo, err := sn.GetFileInfo(fileRoot)
</strong>if err != nil {
    return err
}
</code></pre>

&#x20;The full list of client methods can be found [here](https://pkg.go.dev/github.com/0glabs/0g-storage-client@v0.3.0/node#ZeroGStorageClient).
