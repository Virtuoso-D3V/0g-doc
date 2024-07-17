# Access Storage through CLI

There are two ways a user can access the 0G Storage System. The first simple and straightforward way is to use our [web tool](https://storagescan-newton.0g.ai/tool). If a user wants more control on the data location and versioning, he can use 0G Storage CLI to easily upload/download data to 0G Storage System. This section introduces the 0G Storage CLI in detail, including subcommands for storage and kv operations, in order for users to use through terminal. Users can develop their own scripts, e.g. regular log uploading cron jobs, with the CLI tool.

### Installation

1. Download the source code

```bash
git clone https://github.com/0glabs/0g-storage-client.git
```

2. Build the binary (make sure you install [go](https://go.dev/doc/install) first)

```bash
cd 0g-storage-client
go build
```

3. Add the binary to GOPATH

```bash
mv 0g-storage-client ~/go/bin
export PATH=~/go/bin:$PATH
```

### Command Line Entrance

The command-line help listing is reproduced below for your convenience. The same information can be obtained at any time from your own client by running

```bash
0g-storage-client --help
```

```
ZeroGStorage client to interact with ZeroGStorage network

Usage:
  0g-storage-client [flags]
  0g-storage-client [command]

Available Commands:
  completion  Generate the autocompletion script for the specified shell
  download    Download file from ZeroGStorage network
  gateway     Start gateway service
  gen         Generate a temp file for test purpose
  help        Help about any command
  indexer     Start indexer service
  kv-read     read kv streams
  kv-write    write to kv streams
  upload      Upload file to ZeroGStorage network

Flags:
      --gas-limit uint       Custom gas limit to send transaction
      --gas-price uint       Custom gas price to send transaction
  -h, --help                 help for 0g-storage-client
      --log-color-disabled   Force to disable colorful logs
      --log-level string     Log level (default "info")
      --web3-log-enabled     Enable log for web3 RPC

Use "0g-storage-client [command] --help" for more information about a command
```
