Please check our official communication channels for announcements regarding updates and technical notices.

Here are the base recommendations for running a masternode candidate:

## Minimum hardware requirements {#hardware .unnumbered}

Processing transactions is mostly CPU bound.
Therefore we recommend running CPU optimized servers.

- Directly facing internet (public IP, no NAT)
- 16 cores CPU
- 32GB of RAM
- SSD storage

!!! note
    If you are running a node on the Testnet, 2CPU/8GB of RAM is sufficient.

We recommend using popular cloud providers as their reliability and uptime are close to 100%.
These servers would be a good starting point:

- **DigitalOcean**: CPU optimized droplet 32GB/16CPU
- **Amazon EC2**: C5 instance
- **Google Cloud Engine**: n1-highcpu-16

Setting up a masternode candidate on a weaker machine might result in poor performance, significantly impacting an owner's rewards and the chain's performance.

If you have found other production-grade environments, please come chat with us on our [Gitter](https://gitter.im/taoblockchain).

!!! info Performances
    A masternode has to continuously process a large amount of data (validations, block creation, etc). 
    Your masternode needs to be able to handle the load or your rewards will be negatively impacted.
   

## Maintenance {#maintenance .unnumbered}

All IT systems require maintenance.

It is the owner's responsability to ensure over time that your node has enough:

- disk space to store the new blockchain data
- processing power to keep the chain operating at optimal speed
- monitoring to be able to react quickly in case of problem
- security mesures like firewalling, os security patching, ssh via keypairs, etc.

This is a non exhaustive list.
