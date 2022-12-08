# FirmaChain v0.3.5 Upgrade Notes
This document is a user guide to upgrade FirmaChain from v0.3.3 to v0.3.5.

</br>

## Overview
- Governance Proposal: https://explorer.firmachain.dev/proposals/3
- Target Block Height: `4,806,000`
- Upgrade Type: Soft-fork by governance software upgrade proposal

|                         |  Before  |   After  | Others                                                       |
| ----------------------- | :------: | :------: | --------------------------------------------------------- |
| FirmaChain              |  v0.3.3  |  v0.3.5  | Proposal/3                                                |
| Cosmos SDK              |  v0.44.5 |  v0.45.9 | -                                                         |
| Tendermint              | v0.34.14 | v0.34.21 | -                                                         |
| IBC                     |  v1.2.2  |  v3.3.0  | -                                                         |
| CosmWasm                |     -    |  v0.29.2 | -                                                         |
| Minimum commission rate |    0%    |    5%    | [Proposal/2](https://explorer.firmachain.dev/proposals/2) |

</br>

## Main Chainges
- Support Cosmos SDK 0.45.9
- Support IBC v3.3.0
- Support CosmWasm v0.29.2
- Change 'Minimum Commission Rate'

</br>

## Installation Process
- If you want to use cosmovisor when upgrading the chain, please click on the link below.
- https://firmachain-1.gitbook.io/firmachain/validator-guide/upgrade/cosmovisor-guide

</br>

The `firmachaind` process will automatically be stopped at block height `4,806,000`. But the process will still remain in alive state. So you have to manually kill `firmachaind` process.

```bash
# using binary
> pkill firmachaind

# using system service
> sudo systemctl stop firmachaind
```

</br>

## Backup (optional)
If you are faced with an issue while upgrading the network, you might have to restart from the original version. Therefore, we highly recommend you backup the original version of FirmaChain before upgrading the network. (Per Pruning Default, approximately 200~250 GB expected)
```bash
> tar -cvf firmachain_bak_20221207.tar .firmachain
```

</br>

## Using just firmachain binary
Now you're ready to install the new binary.
```bash
# The installation of go, gcc and make are required in order to continue with the build. (If you have them already installed, you can skip this process)
> sudo snap install go --classic
> sudo apt install gcc
> sudo apt-get install make

# Build binary
> git clone https://github.com/firmachain/firmachain.git
> cd firmachain
> git checkout v0.3.5
> make install
> sudo mv ~/go/bin/firmachaind /usr/local/bin/firmachaind

# Check version
> firmachaind version
0.3.5

> firmachaind version --long
name: FirmaChain
server_name: <appd>
version: 0.3.5-beta2
commit: e76e6a76044c1aec9eb763655acb93ebcd50e8ba
build_tags: ',ledger'
go: go version go1.18.5 linux/amd64
...
cosmos_sdk_version: v0.45.9
```

Once you've completed all of the above without any problems, let's restart the chain.
```bash
# using binary
> firmachaind start

# using system service
> sudo systemctl start firmachaind
```

</br>

## Using Cosmovisor (Optional)
Move the v0.3.5 binary to the appropriate folder space.

```bash
# v0.3.5
mv go/bin/firmachaind $DAEMON_HOME/cosmovisor/upgrades/v0.3.5/bin/firmachaind
```

Once you’ve completed the above step, the chain will automatically restart from the upgraded block height using the new binary.

</br>

## Notes for reference
Please contact us if you are faced with any issues during the upgrade.\
E-mail: contact@firmachain.org
