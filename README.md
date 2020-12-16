# Filecoin Plus
## Introduction
Filecoin Plus aims to maximize the amount of useful storage that Filecoin can and will support. Filecoin Plus puts power in the hands of clients and incentivizes participants to bring demand into the network. Client needs and legitimate use cases will shape the goods and services produced on Filecoin. This includes accelerating the proliferation of products and compliant use cases on Filecoin with both geographic and use case diversity. 

## Overview
Filecoin Plus is a pragmatic solution to the technically challenging problem of verifying that a particular set of data is useful in a permissionless, incentive-compatible, and pseudonymous network. By adding a layer of social trust and providing leverage to storage clients, Filecoin Plus makes the network more decentralized and accelerates the proliferation of high-quality services on the network. Offering additional reward incentives for storing a Filecoin Plus Client’s deals also ensures reward subsidies go where they are needed most – encouraging legitimate use of the network.

### The Principles of Filecoin Plus are defined as:
- Decentralization and Diversity
- Transparency and Accountability
- Community Governance
- Low-Cost Dispute Resolution
- Limited Trust Earned over Time
- Terms of Service
- A Useful Storage Network

## Terminology
### DataCap
DataCap, when allocated to a client, can be spent by the client in storage deals with miners. These deals carry a higher deal quality multiplier, which increases the “quality adjusted power” of the storage miner on the network (yielding better block rewards for the miner over time). In short, miners are heavily incentivized to take deals from Clients who use DataCap to pay for their deals. 

DataCap is granted in batches to Notaries, who in turn, allocate it to responsible clients that spend the DataCap to fund storage deals. DataCap is consumed as it is used to make deals. 

### Notary
Notaries are selected to serve as fiduciaries for the Filecoin Network, and are responsible for allocating DataCap to clients with legitimate storage use cases. The base responsibilities of notaries include: 
- Allocate DataCap to clients in order to subsidize reliable and useful storage on the network.
- Verify that clients receive a DataCap commensurate with the level of trust that is warranted based on information provided.
- Ensure that in the allocation of the DataCap no party is given excessive trust in any form that might jeopardize the network.
- Follow operational guidelines, keep record of decision flow, and respond to any requests for audits of their allocation decisions.

You can find a list of the active Notaries [here](https://filecoinplus.on.fleek.co) who can allocate DataCap. 

Notaries are selected through an application process described [here](https://github.com/filecoin-project/notary-governance/tree/main/notaries#application--selection-process). If approved, [Root Key Holders](https://github.com/filecoin-project/notary-governance/tree/main/root-key-holders#overview) (executors of the decisions made by the community on-chain) grant Notary status and associated DataCap amounts. Those interested in becoming Notaries should apply to this role by filing an Issue in the [Notary Governance Repo](https://github.com/filecoin-project/notary-governance/).

Notaries are given autonomy in their decision making process and encouraged to allocate DataCap based on their best judgement. However, Notaries should expect to answer any potential questions about previous allocation decisions before receiving future DataCap to distribute. 

Additionally, to prevent conflicts of interest, Notaries should not allocate DataCap to clients over which they control the private keys. In the event this is an issue, the Notary should contact another Notary (in the same geography or aligned to the same use case) to handle the allocation for that specific client.

_See additional information [here](https://github.com/filecoin-project/notary-governance/tree/main/notaries#overview)._

### Client
Clients are active participants of the network with DataCap allocation for their use cases. Clients can use their DataCap to incentivize miners to provide additional features and levels of services that meet their specific requirements. In doing so, storage related goods and services on Filecoin are made more valuable and competitive over time. Clients are vetted by Notaries to ensure the client receives DataCap commensurate with their reputation and needs, and that the Client responsibly allocates that DataCap. Obtain verification and DataCap allocation from a Notary. Deploy DataCap responsibly in accordance with the Principles. Follow operational guidelines, keep record of decision flow, and respond to any requests for audits of their allocation decisions.

Specific details on the suggested framework for responsible DataCap allocation are described in the [repository](https://github.com/filecoin-project/notary-governance). It is expected that clients who intend to receive greater amounts of DataCap may be asked to provide evidence for responsible spending of their previous allocation before receiving more.

## Using DataCap
### How to Get DataCap
Clients can get DataCap by making a request to a Notary - you can find a list of active Notaries on the [Filecoin Plus Registry](https://filecoinplus.on.fleek.co). Notaries may specialize in the types of requests they’ll choose to support - some may hand out small amounts of DataCap freely, while others may support larger requests (but also require more due diligence).

You can also find a list of notaries on-chain by using the the following command, which will return a list of addresses and their corresponding DataCap that can be allocated: 

```
lotus-shed verifreg list-verifiers
``` 

At a minimum, every Notary will require an on-chain Filecoin address where they can send the DataCap you request. A client can initialize their address by sending a minimal amount of filecoin to it, e.g. as a result of purchasing some FIL from an exchange.

_Note: As of now, DataCap allocations are a single use credit on a Filecoin address. If you receive an allocation and require more, you should make a new request with a new address that you have initialized like above._

### How to Spend DataCap
Once you have an address with DataCap, you can make deals using DataCap in lieu of Filecoin as payment. Because miners receive a deal quality multiplier for taking FIL+ deals, many miners offer special pricing and services to attract Clients who use DataCap to make deals.

By default, when you make a deal with an address that has DataCap allocated, you will spend DataCap when making the deal. 

If making deals through the [API](https://github.com/filecoin-project/lotus/blob/master/documentation/en/api-methods.md#ClientStartDeal), make sure when calling `ClientStartDeal` that the `VerifiedDeal` parameter is set to `true`. 

```
[
  {
    "Data": {
      "TransferType": "string value",
      "Root": {
        "/": "bafy2bzacea3wsdh6y3a36tb3skempjoxqpuyompjbmfeyf34fi3uy6uue42v4"
      },
      "PieceCid": null,
      "PieceSize": 1024
    },
    "Wallet": "f01234",
    "Miner": "f01234",
    "EpochPrice": "0",
    "MinBlocksDuration": 42,
    "ProviderCollateral": "0",
    "DealStartEpoch": 10101,
    "FastRetrieval": true,
    "VerifiedDeal": true
  }
]
```

If making deals from the command line, make sure to pass the flag `--verified-deal=true` as a parameter.

```
 lotus client deal --verified-deal=true
```

### Finding Miners to Take FIL+ Deals
There are a few difference ways in which a client can find a miner to take a FIL+ storage deal:
- This [issue](https://github.com/filecoin-project/notary-governance/issues/8) has a list of miners involved in the discussion below that advertise details about their services
- Join the [#fil-plus](https://filecoinproject.slack.com/archives/C01DLAPKDGX) channel on Filecoin Slack to discuss storage options
- Hop into the network with your node and query miners (using `query-ask`) to check their verified deal prices

### Best Practices
As a client who has received DataCap for making storage deals on Filecoin, this [issue](https://github.com/filecoin-project/notary-governance/issues/9) is a great starting point. A few of the key thoughts shared in the issue include: 

- Store multiple copies of data across different data centers, and perhaps even regions, to ensure your data is reliably stored
- Distribute your storage deals across different miners so your data is more likely to be accessible long term
- Ask for features (like fast retrieval) that would make your experience better - clients a lot of leverage in this ecosystem
- Stay in compliance with miners’ stated Terms of Service and Content Policy

## Resources
FIP introducing Filecoin Plus:
https://github.com/filecoin-project/FIPs/blob/master/FIPS/fip-0003.md

Notary Governance Repo (includes links to bi-weekly Governance Calls):
https://github.com/filecoin-project/notary-governance

Filecoin Plus interaction model: 
