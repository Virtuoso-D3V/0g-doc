# Go SDK

This page provides a high-level overview of the Go SDK.

0G ships official Go packages that can be embedded into third party desktop and server applications. There is also a [TS API](https://github.com/0glabs/0g-ts-sdk) that can be used to embed 0G Storage into web applications.

### Overview <a href="#overview" id="overview"></a>

0G's reusable Go libraries focus on three main usage areas:

* Simplified client side data uploading and downloading
* Remote storage node/storage kv interfacing
* Local indexing on file distribution metadata

_Note, this guide will assume some familiarity with Go development. It does not cover general topics about Go project layouts, import paths or any other standard methodologies. If you are new to Go, consider reading_ [_Getting Started with Go_](https://github.com/golang/go/wiki#getting-started-with-go) _first._

### Go packages <a href="#go-packages" id="go-packages"></a>

The `0g-storage-client` library is distributed as a collection of standard Go packages straight from its GitHub repository. The packages can be used directly via the official Go toolkit, without needing any third party tools.

The canonical import path for `0g-storage-client` is `github.com/0glabs/0g-storage-client`, with all packages residing underneath.

To install the package, run

```bash
go get -d github.com/0glabs/0g-storage-client
```



We provide two sdks if you want to integrate the 0G Storage into your own application or build on top of it.

1. Go: [https://github.com/0glabs/0g-storage-client](https://github.com/0glabs/0g-storage-client)
2. JS/TS: [https://github.com/0glabs/0g-ts-sdk](https://github.com/0glabs/0g-ts-sdk)

For how to use, you can check our demo video [here](https://youtu.be/USFGNeaO1b8?si=xAAYoSP7hviYIYGi).
