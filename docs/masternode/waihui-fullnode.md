This guide shows how to run a Waihui MongoDb Fullnode.

To run the fullnode, you need to have MongoDb instance that enable replica set.

## Start MongoDB
In this tutorial, we will run a mongo instance with Docker. Run this command:
```bash
docker run -d -p 27017:27017 --name mongodb \
    --hostname mongodb mongo:4.2 --replSet rs0
```

Enable Mongodb replica set:

```bash
docker exec -it mongodb mongo --eval "rs.initiate()"
```


## Run a fullnode

Download `tao` version 2.0+ from [Tao Github Release page](https://github.com/taoblockchain/tao2/releases)

E.g:
```
wget https://github.com/taoblockchain/tao2/releases/download/v2.0.0-beta/tao-linux-amd64 -O tao
chmod +x tao
sudo mv tao /usr/bin/
```

Create a coinbase address:
```bash
tao account new
```

Init genesis block:
**Testnet**
```
curl -L https://raw.githubusercontent.com/taoblockchain/tao2/master/genesis/testnet.json -o genesis.json
tao init genesis.json
```

Then run the node:

**Testnet**
```bash
NODENAME=[your_node_name]
tao \
    --bootnodes "enode://ce1191bf9a634e7939676d136816ad84941b079c03d6a96e64cca35852363012169055c6879c644e821dc236a01d0499a1b7ff39e9518dbc00da87c7f1898604@13.251.101.216:30301,enode://cf2d05f71f143d85dce45dae6f74fae0ba56fc5ea1d1c548a095e29a5becb3a1fb93eb33e7b1dec43946dcfe608fd1495a02740af710bc615b90ad60fcc04d14@13.250.94.232:30301" \
    --networkid 89 \
    --rpc --rpccorsdomain "*" --rpcaddr 0.0.0.0 --rpcport 8545 --rpcvhosts "*" \
    --ws --wsaddr 0.0.0.0 --wsport 8546 --wsorigins "*" \
    --rpcapi "personal,db,eth,net,web3,txpool,miner,waihui" \
    --announce-txs \
    --tao-testnet \
    --waihui.dbengine "mongodb" \
    --ethstats "${NODENAME}:anna-coal-flee-carrie-zip-hhhh-tarry-laue-felon-rhine@stats.testnet.tao.network"

```

You node will sync the data from Tao network, you need to wait until your node catch up the latest block. You can check the status in the logs or the stats page.

To save your time, you should download [chaindata snapshot](#testnet-chaindata-snapshot) and override your chaindata.

## Troubleshoot
**Fatal: Failed to write genesis block**

You already inited genesis block for the default datadir. So you need to use another datadir by `--datadir`
```
tao account new --datadir [YOUR_DATADIR]
tao init genesis.json --datadir [YOUR_DATADIR]
```

## Example
**Testnet**
```
wget https://github.com/taoblockchain/tao2/releases/download/v2.0.0-beta/tao-linux-amd64 -O tao
chmod +x tao
sudo mv tao /usr/bin/
tao --version
tao version
curl -L https://raw.githubusercontent.com/taoblockchain/tao2/master/genesis/testnet.json -o genesis.json
tao init genesis.json 
tao account new --datadir /tmp/chaindata
tao init genesis.json --datadir /tmp/chaindata/
NODENAME=testnode02
tao \
    --bootnodes "enode://ce1191bf9a634e7939676d136816ad84941b079c03d6a96e64cca35852363012169055c6879c644e821dc236a01d0499a1b7ff39e9518dbc00da87c7f1898604@13.251.101.216:30301,enode://cf2d05f71f143d85dce45dae6f74fae0ba56fc5ea1d1c548a095e29a5becb3a1fb93eb33e7b1dec43946dcfe608fd1495a02740af710bc615b90ad60fcc04d14@13.250.94.232:30301" \
    --networkid 89 \
    --rpc \
    --rpccorsdomain "*" --rpcaddr 0.0.0.0 --rpcport 8545 --rpcvhosts "*" \
    --ws --wsaddr 0.0.0.0 --wsport 8546 --wsorigins "*" \
    --rpcapi "personal,db,eth,net,web3,txpool,miner,waihui" \
    --announce-txs --tao-testnet --waihui.dbengine "mongodb" \
    --ethstats "${NODENAME}:anna-coal-flee-carrie-zip-hhhh-tarry-laue-felon-rhine@stats.testnet.tao.network" \
    --datadir /tmp/chaindata/

```

## Testnet chaindata snapshot
To speed up syncing chaindata, you can download chaindata snapshot and override your local chaindata.

Download: [Testnet chaindata](https://chaindata-testnet.s3-ap-southeast-1.amazonaws.com/chaindata-testnet.tar)

E.g:
```
# Download
wget -c https://chaindata-testnet.s3-ap-southeast-1.amazonaws.com/chaindata-testnet.tar

# Uncompress
tar xvf chaindata-testnet.tar
```
