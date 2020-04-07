## Prerequisites

Have a wallet connected to the Testnet (See [this tutorial](https://taoblockchain.github.io/docs/general/networks/))

## Introduction

With a connected wallet, it's now time to try voting for some masternodes.

## Get some TAO

The Tao Testnet is only to be used for experimentation and development. Coins on the testnet have no value on the production chain and have no market value of their own.


### Using TaoWallet

TaoWallet provides a function called `Earn TAO to test`. It allows you to get 15 TAO on the Testnet. Just click on it and you will see your balance go up.

!!! note
    You can use this function only once. You then have to use the faucet for any extra Testnet TAO needed.

### Other options of obtaining some Tao to use on the testnet

We also have a service called "Faucet" which allows you to get 15 TAO at a time.

Access the faucet site at: [faucet.testnet.tao.network](https://faucet.testnet.tao.network)

Enter your wallet address in the field and tick the `I'm not a robot` box.

Click `REQUEST 15 TAO` and wait for a few seconds for the transaction to be confirmed.

You will receive a success confirmation message and the amount of TAO in your wallet should be updated. You can check your TAO balance by either looking at your wallet or using [TaoScan](https://scan.testnet.tao.network).

## How To Vote

Now that you have some TAO you can access our governance dApp, [Shifu](https://master.testnet.tao.network/), to start voting for masternodes.

Shifu natively supports Metamask. You can also access your account page (the vertical three dots on the top right) to fill in your wallet Private Key or MNEMONIC (see image below).

If you use Metamask, you need to connect Mettamask to our testnet (please see the "Create a wallet" section) and choose Metamask in the drop-down settings list.


![Setting](/assets/settingpage.jpg)

Once configured, you can vote for masternodes by clicking on the `Vote` button.


![Vote](/assets/vote.jpg)

At least 100 TAO is required per vote. After clicking submit, your TAO will be sent to the voting smart contract and locked there.

## Reward
Every epoch (~30 minutes), you will automatically receive rewards from each masternode you voted for.

## How to Unvote

If you do not want to support a masternode you voted for, you can unvote it by clicking the `Unvote` button on the masternode's page and enter the amount of TAO you want to unvote.

After unvoting, your TAO is still locked in the smart contract for 48 hours before you are able to withdraw.

## How to Withdraw

For withdrawals after unvoting, you need to wait until your TAO is unlocked from the smart contract. Then you can click the `withdraw` button in your account page (the vertical three dots on the top right) and choose which withdrawal you want to receive back your TAO.

Note that you might see multiple withdrawals on your account page if you made multiple unvotes previously.

If you withdraw before the unlock period expires, an error will be raised.
