Alternatively to using our simple tool `taomn`, people or companies with existing infrastructure might want to directly run our docker images for more flexibility.

To achieve that, you just need to run our `tao/node` docker image.

This image runs the [Tao go client](https://github.com/taoblockchain/taoblockchain) with some automation added on top.

## Tags

| Environment | Tag        |
| ----------- | ---------- |
| Testnet     | `:testnet` |
| Mainnet     | `:stable`  |

## Environment variables

| Variable        | Required | Default         | Example                                    | Description                                                                                                     |
| --------------- | -------- | --------------- | ------------------------------------------ | --------------------------------------------------------------------------------------------------------------- |
| `IDENTITY`      | False    | Random name     | `my-super-node`                            | The name of your masternode                                                                                     |
| `PASSWORD`      | False    | Random password | `S5G@fS3A8+*g-)ftYc`                       | The password used by the the client to localy encrypt its account                                               |
| `PRIVATE_KEY`   | False    | Random account  | `0xa3f5195...`                             | The private key of the account who will identify the node and receive txs fees                                  |
| `BOOTNODES`     | True     | None            | `enode://4d3...@1.2.3.4:30301,enode://...` | The comma separated list of bootnodes. Find them [here](https://docs.tao.network/general/networks/)             |
| `VERBOSITY`     | False    | 3               | `4`                                        | The level of logging (default one should be enough)                                                             |
| `NETWORK_ID`    | False    | 89              | `88`                                       | The network id of the join your node is joining. Find them [here](https://docs.tao.network/general/networks/)   |
| `WS_SECRET`     | False    | None            | `d$M4J4\5gLAz%Zjn>%`                       | The password to send data to the stats website                                                                  |
| `NETSTATS_HOST` | False    | netstats-server | `https://stats.tao.network`                | The stats website to report to, regarding to your environment                                                   |
| `NETSTATS_PORT` | False    | 3000            | `443`                                      | The port used by the stats website (usually 443)                                                                |
| `ANNOUNCE_TXS`  | False    | None            | `True`                                     | Enable reporting transactions via RPC/WS                                                                        |

## Ports

| Exposed | Protocol | Description               |
| ------- | --------- | ------------------------- |
| `20202` | tcp       | Tao client p2p port |
| `20202` | udp       | Tao client p2p port |
| `8545`  | tcp       | Blockchain RPC            |
| `8546`  | tcp       | Blockchain WS             |

## Filesystem

| Path                  | Content   |
| --------------------- | --------- |
| `/taoblockchain/data`     | Chaindata |
| `/taoblockchain/keystore` | Accounts  |

## Examples
`docker run`

```bash
docker run -d --name masternode \
  -e IDENTITY=$MASTERNODE_NAME \
  -e PRIVATE_KEY=$MASTERNODE_PK \
  -e BOOTNODES=$BOOTNODES \
  -e NETSTATS_HOST=stats.tao.network \
  -e NETSTATS_PORT=443 \
  -e WS_SECRET=$STATS_WS_SECRET \
  -p 20202:20202 \
  -p 20202:20202/udp \
  -v chaindata:/taoblockchain/data \
  tao/node:stable
```

`docker-compose.yml`

```yml
version: "3.4"
services:
  masternode:
    image: tao/node:stable
    environment:
      IDENTITY: $MASTERNODE_NAME
      PRIVATE_KEY: $MASTERNODE_PK
      BOOTNODES: $BOOTNODES
      NETSTATS_HOST: stats.tao.network
      NETSTATS_PORT: 443
      WS_SECRET: $STATS_WS_SECRET
    ports:
      - 20202:20202
      - 20202:20202/udp
    volumes:
      - chaindata:/taoblockchain/data
```
