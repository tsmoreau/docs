This guide will show you how to start a Waihui DEX on your server.

To start, you need to download Waihui-SDK source code, and it includes two parts:

* [Waihui-SDK](https://github.com/taoblockchain/waihui-sdk): Backend server, API, it requires Mongodb database with rabbitmq.
* [Waihui-SDK-UI](https://github.com/taoblockchain/waihui-sdk-ui): Frontend - DEX UI, requires NodeJs, React

To enable trading for your DEX, you need to register your DEX on TaoRelayer by depositing 25K TAO.

## Quick start
Run this command on an empty server Ubuntu version 16+:
```
bash <(curl -sSL https://tao.network/get-waihui.sh)
```
After finishing the command above, you can see the result:

- See fullnode in the Stats Page (Testnet: https://stats.testnet.tao.network/)
- Open your relayer on browser (http://[SERVER_IP])

!!! Note
    You need to wait for until your fullnode pass the block number that you registered your relayer to see the pairs

## Setup manually

### Prerequisite ###

#### Minimum hardware and software requirements ####

* Processing transactions is mostly CPU bound. Therefore we recommend running CPU
optimized servers.(You can check our base recommendations to create your
fullnode [here](https://docs.tao.network/masternode/requirements/))

    * Directly facing internet (public IP, no NAT)
    * 16 cores CPU
    * 32 GB of RAM
    * SSD Storage

!!! Note
    If you are running a node in Testnet, 8CPU/32GB of RAM is sufficient.

#### Application platform ####

* Go 1.12 or higher
* Docker with the latest version
* Nodejs 8.16.x or higher
* Nginx

#### Networks ####

Your server needs to open these ports:

* 80/443 for HTTP/HTTPs
* 20202 for fullnode

#### All IT systems require maintenance ####

It is of the owner's responsibility to ensure over time that your node has enough:

* Disk space to store the new blockchain data
* Processing power to keep the chain operating at optimal speed
* Monitoring to be able to react quickly in case of a problem
* Security mesures like firewalling, os security patching, ssh via keypairs, etc.


## Prepare RabbitMQ, MongoDB, and Waihui fullnode

Run MongoDB and Waihui Fullnode:

Use this [guide](/masternode/waihui-fullnode/) to run your fullnode and MongoDB on the server.

And run RabbitMQ:

```bash
docker run -d -p 5672:5672 --name rabbitmq rabbitmq:3.8
```

## Basic Deployment ##

### Waihui SDK Backend

Download `waihui-sdk` binary from [Waihui-SDK Github Releases](https://github.com/taoblockchain/waihui-sdk/releases).

E.g:
```
wget https://github.com/taoblockchain/waihui-sdk/releases/download/v1.0.1-beta/waihui-sdk.v1.0.1-beta.linux.amd64 -O waihui-sdk
chmod +x waihui-sdk
```

Or you can build the binary from the source code by following the steps below:

Clone [waihui-sdk](https://github.com/taoblockchain/waihui-sdk.git) to your server:

`$ git clone https://github.com/taoblockchain/waihui-sdk.git`

Go to `waihui-sdk` and create and edit your config file.
```
cd waihui-sdk
cp config/config.yaml.example config/config.yaml
```

We have some parameter that needs to be changed.

* `exchange_address` : Your DEX coinbase (the address you use to register a DEX on TaoRelayer)
* `contract_address` : TaoRelayer smart contract address (Testnet: `0xe7c16037992bEcAFaeeE779Dacaf8991637953F3`)

After customizing your config, you can build SDK backend

```bash
cd waihui-sdk
GO111MODULE=on
go mod download
go build .
```

And run it:
```
./waihui-sdk
```
Note: `waihui-sdk` requires `./config/config.yaml` and `./config/errors.yaml` file to run the service.

To run waihui-sdk as daemon service, you can use `pm2`, `supervisord` or `systemd`.

### Waihui SDK UI ###
Download the site from [Waihui-SDK-UI Github Releases](https://github.com/taoblockchain/waihui-sdk-ui/releases)

E.g:
```
# download
wget https://github.com/taoblockchain/waihui-sdk-ui/releases/download/v1.0.1-beta/waihui-sdk-ui.v1.0.1-beta.testnet.tar.gz
# uncompress
tar xvzf waihui-sdk-ui.v1.0.1-beta.testnet.tar.gz
```

Or you can build the site by following the steps below:

Clone [waihui-sdk-ui](https://github.com/taoblockchain/waihui-sdk-ui.git) to your server:
```bash
git clone https://github.com/taoblockchain/waihui-sdk-ui.git
```
Go to `waihui-sdk-ui` to update the `env` file:
```
cd waihui-sdk-ui
cp .env.sample .env
```
There are some parameters that need to be changed:

- `REACT_APP_ENGINE_HTTP_URL`: url backend, `http://[SERVER_IP_OR_DOMAIN]/api`
- `REACT_APP_ENGINE_WS_URL`: url websocket backend, `ws://[SERVER_IP_OR_DOMAIN]/socket`

You need to have `yarn` and `sass` to build the site, install it:
```
npm install -g yarn sass
```
Build the site:

```bash
cd waihui-sdk-ui
yarn install && yarn build
```

Your DEX UI is created into `./buid` directory. You can setup web server (nginx) and domain to publish your site to internet.

You can use `nginx` to serve the site.

## Setup web server (nginx)

Waihui-SDK backend run on port 8080 in the default. We can use Nginx to serve both Waihui-SDK and Waihui-SDK-UI and publish it to internet.

```
server {
    listen       80;
    server_name  _;

    root /path_to_your_waihui_sdk_ui_build;

    index index.html index.htm;

    # Waihui-SDK API
    location /api {
         proxy_set_header X-Real-IP $remote_addr;
         proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
         proxy_set_header Host $host;
         proxy_pass http://localhost:8080;
    }

    # Waihui-SDK socket
    location /socket {
        auth_basic off;
        proxy_set_header Host $host;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "Upgrade";
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_pass http://localhost:8080/socket;
    }

    # Waihui-SDK UI
    location / {
        try_files $uri $uri/ /index.html;
    }
}
```

After reloading `nginx` with the new configuration. You can access your DEX via `http://SERVER_IP`

## Troubleshot & FAQ

**How to secure my DEX?**

You need to setup HTTPS and INBOUND firewall for your DEX, open only SSH (22), HTTP (80), HTTPS (443), Fullnode RLPX (20202).

You can setup firewall by using software on your server or create firewall on your cloud provider.

**Why doesn't ledger work with my DEX?**

Ledger required HTTPS to work properly with your DEX. On testnet, you can only use HD path `44/60` for your ledger, path `44/889` is only supported on mainnet.

**Error: Cannot get tokens or pairs**

You need to wait for until your fullnode pass the block number that you registered your relayer to see the pairs.

In another case, might you setup Waihui-SDK backend incorrectly. You need to make sure that `exchange_address` in `config/config.yaml` file is your DEX coinbase.
