Please note all Tao2 documentation currently should be considered a draft and some details are subject to revision

# Designed for the Music Economy

As the Tao Network approaches its fourth year of consistent, flawless operation it has become clear that the industry, consumers, and markets have become more sophisticated, the codebase has not and a major technological overhaul is required. The vast experience we have gained serving the interests of the music industry have crystalized the technological requirements of a cryptocurrency which may truly begin to disrupt the power structures which dominate the landscape.  A platform which would enable a “DeFi for music” brings with it not only a set of technological prerequisites, but consensus must remain true to the ethics and ideals of the music industry we have come to serve.  It is towards these noble ends that we are creating the means to manifest that future: Tao2.

![tao](/assets/home.png)

The blockchain industry and the infrastructure of the Internet of Value are being built rapidly around the globe, and to many the atmosphere is eerily similar to the building of the Internet in the late ‘90s, with pioneers and dreamers coming together to build a new future. **Tao** is the first blockchain platform which has dedicated its focus to leveraging the latest of blockchain technologies towards a more democratized, egalitarian future for the music economy.  This upgrade shall acheive this vision through seamlessly merging an ecosystem of applications with cryptographic tokens used by millions of mainstream users with a unique blockchain infrastructure architecture allowing for a fast, secure, frictionless payment and trusted store of value.

The distributed systems which currently dominate the music economy have been researched in a “*permissioned setting*” where the number of participants in the system and their identities are common knowledge. In 2008, Satoshi Nakamoto - “proposed his celebrated “blockchain protocol” which attempts to achieve consensus in a permissionless setting: anyone can join (or leave) the protocol execution (without getting permission from a centralized or distributed authority), and the protocol instructions do not depend on the identities of the players” (see [here](#PassCrypto2017)). Later on, Ethereum with its Ethereum Virtual Machine (EVM) proposed several significant enhancements compared to Bitcoin, including Smart Contracts. Both Bitcoin and Ethereum have some issues, especially with transaction processing performance. In order to construct an efficient and secured consensus protocol for **Tao**, we tackle the following main bottlenecks of classic blockchains:
-   **Efficiency:** Existing blockchains as employed by major cryptocurrencies(e.g., Tao 1.0 or Ethereum) do not scale well to handle a large transaction volume, e.g. Tao 1.0 and Ethereum can handle around 7-10 transactions/second. 
-   **Confirmation times:** The original Tao blockchain took 7.5 minutes per block, and is significantly larger than network latency. Furthermore, a Tao 1.0 block requires 10 subsequent blocks following it so that it can be confirmed; thus it takes on average 1.5 hours for a transaction to be confirmed (with low confidence). While Ethereum uses a shorter block-time, the average confirmation time still remains relatively high, around 13 minutes [Cardano](#Cardano2017). These long confirmation times hinder many important applications (especially smart contract applications).
-   **Unwanted Fork Potential:** The problem of fork chain consumes computational energy, time, and creates potential vulnerabilities for different types of attacks.
-   **Trust** While the systems are trustless, those who create them are not.  As a result, existing music economy stakeholders from across the spectrum have rejected those platforms such as Ethereum for anything more than experimental use.

The Tao project began life in 2015 by directly engaging the most significant music industry stakeholders in order to gain their input as to the pain points present in their industry with the goal of potentially solving them with blockchain technology.  The Tao 1.0 cryptocurrency was launched in 2016 based on these conversations with specific features which were desired by the music industry:
-   **Proof of Stake** Allowing for artists, producers, and labels to participate in network consensus
-   **Masternodes** Allowing for the instant settlement of transactions and enhancing Layer 1 consensus
-   **Tokenization** Allowing for the digital representation of paper contracts as well as advanced automation
-   **Community** – Providing clear focus and dedication to serving the needs of the music industry, while directly engaging fans and artists alike

While these goals were achieved, certain other important aspects of cryptocurrency adoption were neglected.
-   **Market traction** Listings on multiple exchanges
-   **Technological modernization** Keeping in line with the latest in cryptocurrency and blockchain developments
-   **Developer support** Missing tools which would allow developers to create applications using the blockchain

With these lessons now learned, the Tao cryptocurrency protocol will be upgraded to a protocol known as “Tao 2.0” or “Tao2". This document delves into the specifics of Tao2, including its consensus mechanisms, operational performance, and technological features:
-   Random Generals to reduce the proof of stake attack surface, increase data reliability, and reduce fork potential
-   Additional randomization to guarantee fairness and prevent handshaking and Sybil attacks
-   Fast confirmation time and efficient, decentralized checkpoints for transaction finality and minimal potential rebase

To start dealing with these problems, in this paper, we present an overview architectural design of **Tao**’s masternode design called "Shifu". In particular, we propose Delegated Proof of Stake (DPOS) consensus, a Proof-of-Stake (PoS)-based blockchain protocol with a fair voting mechanism, rigorous security guarantees and fast finality. This presents a novel reward mechanism which, with this mechanism, the blockchain has a low probability of forks, fast confirmation times, plus the contributions and benefits of masternodes are fair in the sense that the division of rewards is a fair probabilstic computation.
