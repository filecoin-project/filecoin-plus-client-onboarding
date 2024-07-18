<p align="left">
  <img src="docs/_media/Filecoin-plus-logo-color-dark.png" alt="Filecoin Plus Logo" width="320" />
</p>

# This Repo is archived and no longer maintained
This repository for the Fil+ Notaries has been sunset. For Fil+ Allocator Governance discussions, see this [Governance repo](https://github.com/filecoin-project/Allocator-Governance/). For the registry of active allocators, see this [Allocator Registry repo](https://github.com/filecoin-project/Allocator-Registry)

To view other updated reference links for the Fil+ program, please see:

- For information on the open and pending DataCap deals, please see [FIDL's Allocator.tech](https://allocator.tech/).
- For information on support issues or a listing of all current Allocators, please see [Allocator Registry repo](https://github.com/filecoin-project/Allocator-Registry)
- For getting in touch, please reach out in [SLACK](https://filecoin.io/slack)
- Bi-weekly recorded Fil+ governance meetings on [Youtube](https://www.youtube.com/playlist?list=PLp3zrT1ewY0kYN1hJpERMUxTCbFC4yZwN)








## Introduction
Filecoin Plus aims to maximize the amount of useful storage on Filecoin by adding a layer of social trust to the Network. [Clients](#client) can apply to [Notaries](#notary) to receive [DataCap](#datacap), which can be used to incentivize Storage Providers (SPs) to take storage deals. SPs who take deals that are compensated with DataCap receive a 10x to their quality adjusted power - increasing their probability of winning block rewards. Filecoin Plus puts power in the hands of Clients and incentivizes SPs to support real use case on the Network.

## Using DataCap
### How to Get DataCap
Clients can get DataCap by making a request to a Notary - you can find a list of active Notaries on the [Filecoin Plus Registry](https://plus.fil.org/verifiers). Notaries may specialize in the types of requests they’ll choose to support - some may hand out small amounts of DataCap freely, while others may support larger requests (but may also require more due diligence). _**If you're looking to store large data (over 500TiB) - check out the [Large Dataset Notary program](https://github.com/filecoin-project/filecoin-plus-large-datasets), which can grant between 500TiB-5PiB of DataCap.**_

At a minimum, every Notary will require an [on-chain Filecoin address](https://docs.filecoin.io/get-started/lotus/send-and-receive-fil/) to which they can send the requested DataCap. A Client can initialize their address on-chain by sending a minimal amount of Filecoin to it, e.g. as a result of purchasing some FIL from an exchange. As a Client makes deals using DataCap, the balance of DataCap on that address will be depleted. If you run out or need more DataCap allocation, please make a new request using your same address (now that [FIP-0012 is live](https://fips.fission.app/fips/fip-0012/)). 

### How to Spend DataCap
Once you have an address with DataCap, you can make deals using DataCap as a part of the payment. Because SPs receive a deal quality multiplier for taking Fil+ deals, many SPs offer special pricing and services to attract Clients who use DataCap to make deals.

By default, when you make a deal with an address that has DataCap allocated, you will spend DataCap when making the deal. 

If making deals through the [API](https://github.com/filecoin-project/lotus/blob/master/documentation/en/api-methods.md#ClientStartDeal), make sure when calling `ClientStartDeal` that the `VerifiedDeal` parameter is set to `true`. 

If making deals from the command line, make sure to pass the flag `--verified-deal=true` as a parameter.

```
 lotus client deal --verified-deal=true
```

### Checking Remaining DataCap 
Once you have received DataCap to an address, you can check the remaining balance either by visiting a site that enables this (e.g. [verify.glif.io](https://verify.glif.io/)) or by querying your address on a node. 

#### With lotus v1.10.0 ^

```
lotus filplus check-client-datacap f00000
```

#### With lotus v1.9.0 and below
_Note: [Lotus-shed](https://github.com/filecoin-project/lotus/tree/master/cmd/lotus-shed) is a separate package you will need to build and install (`make lotus-shed` in the [Lotus](https://github.com/filecoin-project/lotus) source), although these features are slated to be merged into Lotus._

```
lotus-shed verifreg check-client f00000
```

### Finding Storage Providers to Take Fil+ Deals
The general recommendation for clients on the network is to build several replicas of their data on the network, ideally with different SPs / SP entities to spread risk. From a DataCap distribution perspective, guidance is that clients should engage at least 4 SPs and no single SP ID should receive >30% of a client's allocated DataCap. This aligns SP growth incentives with client needs for reliably storing data on the network longer term.

There are a few difference ways in which a client can find a SP to take a Fil+ storage deal:
- This [issue](https://github.com/filecoin-project/notary-governance/issues/8) has a list of SPs involved in the discussion below that advertise details about their services
- Join the [#fil-plus](https://filecoinproject.slack.com/archives/C01DLAPKDGX) channel on Filecoin Slack to discuss storage options
- Hop into the network with your node and query SPs (using `query-ask`) to check their verified deal prices

### Best Practices
As a client who has received DataCap for making storage deals on Filecoin, this [issue](https://github.com/filecoin-project/notary-governance/issues/9) is a great starting point. A few of the key thoughts shared in the issue include: 

- Store multiple copies of data across different data centers, and perhaps even regions, to ensure your data is reliably stored
- Distribute your storage deals across different miners so your data is more likely to be accessible long term
- Ask for features (like `fast retrieval`) that would make your experience better
- Stay in compliance with Miners’ stated Terms of Service and Content Policy

## Terminology
### DataCap
DataCap, when allocated to a Client, can be spent by the Client in storage deals with miners. These deals carry a higher deal quality multiplier, which increases the “quality adjusted power” of the storage miner on the network (yielding better block rewards for the miner over time). In short, miners are heavily incentivized to take deals from Clients who use DataCap to pay for their deals. 

DataCap is granted in batches to Notaries, who in turn, allocate it to responsible clients that spend the DataCap to fund storage deals. DataCap is consumed as it is used to make deals. 

### Notary
Notaries are selected to serve as fiduciaries for the Filecoin Network, and are responsible for allocating DataCap to clients with legitimate storage use cases. The base responsibilities of notaries include: 
- Allocate DataCap to clients in order to subsidize reliable and useful storage on the network.
- Verify that Clients receive a DataCap commensurate with the level of trust that is warranted based on information provided.
- Ensure that in the allocation of the DataCap no party is given excessive trust in any form that might jeopardize the network.
- Follow operational guidelines, keep record of decision flow, and respond to any requests for audits of their allocation decisions.

You can find a list of the active Notaries [here](https://plus.fil.org) who can allocate DataCap. 

Notaries are selected through an application process described [here](https://github.com/filecoin-project/notary-governance/tree/main/notaries#application--selection-process). If approved, [Root Key Holders](https://github.com/filecoin-project/notary-governance/tree/main/root-key-holders#overview) (executors of the decisions made by the community on-chain) grant Notary status and associated DataCap amounts. Those interested in becoming Notaries should apply to this role by filing an Issue in the [Notary Governance Repo](https://github.com/filecoin-project/notary-governance/).

Notaries are given autonomy in their decision making process and encouraged to allocate DataCap based on their best judgement. However, Notaries should expect to answer any potential questions about previous allocation decisions before receiving future DataCap to distribute. 

Additionally, to prevent conflicts of interest, Notaries should not allocate DataCap to clients over which they control the private keys. In the event this is an issue, the Notary should contact another Notary (in the same geography or aligned to the same use case) to handle the allocation for that specific client.

_See additional information [here](https://github.com/filecoin-project/notary-governance/tree/main/notaries#overview)._

### Storage Client
Clients are active participants of the network with DataCap allocation for their use cases. Clients can use their DataCap to incentivize miners to provide additional features and levels of services that meet their specific requirements. In doing so, storage related goods and services on Filecoin are made more valuable and competitive over time. Clients are vetted by Notaries to ensure the client receives DataCap commensurate with their reputation and needs, and that the Client responsibly allocates that DataCap. Obtain verification and DataCap allocation from a Notary. Deploy DataCap responsibly in accordance with the Principles. Follow operational guidelines, keep record of decision flow, and respond to any requests for audits of their allocation decisions.

Specific details on the suggested framework for responsible DataCap allocation are described in the [repository](https://github.com/filecoin-project/notary-governance). It is expected that clients who intend to receive greater amounts of DataCap may be asked to provide evidence for responsible spending of their previous allocation before receiving more.

### FVM Smart Contracts
Smart contracts can acquire DataCap just like any regular client. To do so, simply enter the f410 address of the smart contract that requires DataCap as the client address when making a request.

The process outlined above is for larger amounts of Datacap > 32 GiBs. For a smart contract's first DataCap allocation, we recommend using auto-verifier [Verify.glif.io](Verify.glif.io) to get 32 GiB of DataCap, as specified [here](https://docs.filecoin.io/store/filecoin-plus/overview/).

It's important to note that DataCap allocations are a one-time credit for a Filecoin address and cannot be transferred between smart contracts. If you need to redeploy the smart contract, you must request additional DataCap. To improve this experience, we are developing an FRC to allow DataCap to be held between redeployments. 

## Resources
FIP introducing Filecoin Plus:
https://github.com/filecoin-project/FIPs/blob/master/FIPS/fip-0003.md

Notary Governance Repo (includes links to bi-weekly Governance Calls):
https://github.com/filecoin-project/notary-governance
