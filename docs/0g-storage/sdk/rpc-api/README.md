# Go API

0G ships official Go packages that can be embedded into third party desktop and server applications. There is also a [TS API](https://github.com/0glabs/0g-ts-sdk) that can be used to embed 0G Storage into web applications.

### Overview <a href="#overview" id="overview"></a>

0G's reusable Go libraries focus on three main usage areas:

* Simplified client side data uploading and downloading
* Remote storage node/storage kv interfacing
* Local indexing on file distribution metadata

1. [\
   docs](https://geth.ethereum.org/docs)/
2. [developers](https://geth.ethereum.org/docs/developers)/
3. [dapp-developer](https://geth.ethereum.org/docs/developers/dapp-developer)/
4. [native](https://geth.ethereum.org/docs/developers/dapp-developer/native)

## Go API

Last edited on August 23, 2023

Ethereum was originally conceptualized to be the base layer for [Web3](https://ethereum.org/en/web3/), providing the backbone for a new generation of decentralized, permissionless and censorship resistant applications called [dapps](https://ethereum.org/en/glossary/#dapp). The first step towards this vision was the development of clients providing an RPC interface into the peer-to-peer protocols. This allowed users to transact between accounts and interact with smart contracts using command line tools. Geth was one of the original clients to provide this type of gateway to the Ethereum network.

Before long, web-browser-like graphical interfaces (e.g. Mist) were created to extend clients, and client functions were built into websites built using the time-tested HTML/CSS/JS stack. However, to support the most diverse, complex dapps, developers require programmatic access to client functions through an API. This opens up client technologies as re-usable, composable units that can be applied in creative ways by a global community of developers.

To support this, Geth ships official Go packages that can be embedded into third party desktop and server applications. There is also a [mobile API](https://geth.ethereum.org/docs/developers/dapp-developer/mobile) that can be used to embed Geth into mobile applications.

This page provides a high-level overview of the Go API.

_Note, this guide will assume some familiarity with Go development. It does not cover general topics about Go project layouts, import paths or any other standard methodologies. If you are new to Go, consider reading_ [_Getting Started with Go_](https://github.com/golang/go/wiki#getting-started-with-go) _first._

### Overview <a href="#overview" id="overview"></a>

Geth's reusable Go libraries focus on three main usage areas:

* Simplified client side account management
* Remote node interfacing via different transports
* Contract interactions through auto-generated bindings

### Go packages <a href="#go-packages" id="go-packages"></a>

The `0g-storage-client` library is distributed as a collection of standard Go packages straight from its GitHub repository. The packages can be used directly via the official Go toolkit, without needing any third party tools.

The canonical import path for `0g-storage-client` is `github.com/0glabs/0g-storage-client`, with all packages residing underneath.

To install the package, run

```bash
go get -d github.com/0glabs/0g-storage-client
```
