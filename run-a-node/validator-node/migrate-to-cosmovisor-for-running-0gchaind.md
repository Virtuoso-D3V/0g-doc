# Migrate to Cosmovisor for Running 0gchaind

This guide will walk you through migrating from using 0gchaind start \[flags] to using Cosmovisor to manage your 0gchaind application. Cosmovisor offers the advantage of handling upgrades automatically without manual intervention.

### Steps to Migrate

#### Step 1: Stop the Currently Running 0gchaind

Before migrating, ensure that the currently running 0gchaind instance is stopped.

#### Step 2: Download the Migration Script

https://raw.githubusercontent.com/0glabs/0g-chain/dev/networks/testnet/init-cosmovisor.sh

#### Step 3: Confirm the Path of 0gchaind

Use the whereis command to confirm the path of your 0gchaind binary: `whereis 0gchaind` If the path returned by whereis 0gchaind is different from the path you are currently using to run 0gchaind, modify the script to use the current path. Open the script and replace the 0gchaind path with your current path.

#### Step 4: Execute the Migration Script

`chmod +x init-cosmovisor.sh`

`./init-cosmovisor.sh (0G_HOME)`

#### Step 5: Start 0gchaind Using Cosmovisor

Start 0gchaind using Cosmovisor with the following command: `cosmovisor start [flags]`

### Troubleshooting

If you encounter any issues, run the following command to check the Cosmovisor configuration: `cosmovisor config`

This command will display the current configuration settings for Cosmovisor, helping you identify and resolve any potential issues.

### Why Migrate to Cosmovisor?

Cosmovisor automates the process of handling upgrades for your blockchain application. By using Cosmovisor, you benefit from:

* Automatic upgrade handling without manual intervention.
* Reduced downtime during upgrades.
* Simplified node management and maintenance.

For more information on Cosmovisor, visit the [Cosmovisor documentation](https://docs.cosmos.network/main/build/tooling/cosmovisor).

Follow these steps to ensure a smooth migration from 0gchaind start \[flags] to using Cosmovisor. If you encounter any issues or need further assistance, refer to the Cosmovisor documentation or seek help from the community.
