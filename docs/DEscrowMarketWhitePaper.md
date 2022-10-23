# DEscrow Market Whitepaper

## Introduction

Distributed apps (DApps) promise to revolutionize the way people interact with organizations by putting more power and control in the hands of individual actors by eliminating the traditional gate keepers, replacing them with distributed autonomous organizations (DAOs). However, DAOs have seen limited success outside of financial services that interact strictly with the crypto currencies baking a particular blockchain. We posit they often fall short in a number of areas:

- User Experience and Complexity: Putting more control in the hands of each user often leads to more responsibility for each user to handle.
- Performance and Scalability: Reading and writing from/to the blockchain remains slow by design. A more complicated app will require off-chain handling to scale and remain responsive while handling the number of users for centralized organizations.
- Accountability and Enforcement: Distributed responsibility means there's no central point of contact to resolve issues. Owning a digital asset may or may not doesn't correlate to any enforceable contract in physical space.
- Compliance and Legality: With DApps being relatively recent, they exist in a legal grey area. Replicating the functionality of an existing organizations ultimately leads to legal ambiguity for users spanning across jurisdictions.

Using a hybrid model where some parts of the system are handled off-chain and in physical space may help address some of these issues. But how do we maintain independent ownership and trust based on distributed consensus? DEscrow Market aims to provide a distributed market that tackles the preceding problems while still being independently managed by each actor.

### Escrow Market Actors

First we need to understand how a transaction in digital space translates to physical space. We can explore the constraints by analyzing the actors involved.

#### Buyer

#### Seller

#### Arbiter / Market

## Problem

We want to allows users to buy and sell products with payment being stored in escrow by an arbiter, but with a number of features/constraints:

- Optional Anonymity: Actors should optionally be allowed to remain anonymous at varying degrees depending on their roll in the system.
  - Buyer from/to Seller: A buyer and seller are allowed to maintain full anonymity between each other.
  - Buyer/Seller from/to Arbiter: An arbiter must know from where funds most be transferred to/from.
  - Arbiter: An arbiter may operate anonymously, but they most be publicly addressable (this may expose their identity depending on how they're addressed).
  - External Parties: External parties can view transaction metadata between all parties, but they can't view a buyer/seller's public key. An arbiter's public key is visible.
- Distributed Responsibility: No single point of failure should bring the system down whether the problem occurs in physical or digital space.
  - Jurisdiction Independence: The app shouldn't be dependent on the rules or attributes of any particular location.
  - Market Self-Governance: Markets should be managed by multiple actors with each being equal partners accountable to each other.
  - Open Market Enrollment: A market can be started by any group of people as long as there are enough members to maintain consensus.
    - Segmentation: This allows creating different markets for different product niches and jurisdictions.
    - Compliance: Although the system may be jurisdiction independent, there's no need for a market operator to be.
  - Recourse: Each party must have a method to hold others in the system accountable if the sales/arbitration contract isn't fulfilled.
- Crypto Currencies: A number of crypto currencies (Monero for full anonymity and probably others) should be supported to help facilitate the two previous main bullet points.
- Auditable: Any party should be able to view transactions to ensure each party is behaving as expected.
  - Transaction Metadata: 
  - User Feedback: To help enforce contracts, all parties should be ratable/reviewable per transaction.
  - Partially Open-Source: Any functionality that's involved in performing work in facilitating a transaction either on-chain or off-chain should be open-source for audits. 
    - Interface Independence: A market may implement their own UI or modify the reference design which may not be open-source.
- UX Comparable to Web 2 Apps: The markets themselves should look and feel mostly like existing markets (such as EBay).
  - Performance: Like existing markets, listings should be searchable quickly and have potentially megabytes of data associated with them (images, etc.).
  - Payment: A payment should be submittable through any wallet compatible with supported crypto currencies, but there should be a mechanism in the market UI to trigger a transaction.

DEscrow Market attempts to remedy each point with varying effectiveness.

### Analogs / Inspiration

We can look at existing systems that attempt provide some of the features listed and see how they compare.

#### NFTs

NFTs excel at storing immutable records. This can have many advantages for a market that prioritizes transparency and redundancy. From an escrow market, we can have tokens for:

- Arbiters: A token can claim arbiters with an ID own an address that's verifiable and well-known for parties to access
- Sellers: A token can claim sellers have a set of listings associated with an ID
- Buyers: A token can claim buyers are associated with an ID
- Transactions: A token can link the parties together by their ID and claim a transaction with X attributes (cost, escrow submit date/time, escrow release date/time, status, etc.)
- Transaction Feedback: A token can store an arbiter/seller/buyer ID and their associated feedback for a transaction ID (5 star, optional review, etc.)
- Disputes: A token can link a transaction ID to seller/buyer ID that starts a dispute with associated status

We can audit the trail of these tokens and verify:

- Buyers/Sellers: Can know if a arbiter/market has been in operation for a long time and has had positive remarks (dispute handling, app responsiveness, etc.)
- Buyers: Can know if sellers have a trusted track of sales and resolutions
- Arbiters: Can know if sellers/buyers have a history of transactions or disputes while resolving disputes

Each token must have a one-to-one correspondence between the IDs. Since there's a cost associated with each transaction, there's a strong disincentive to game the system (review farms, etc.).

##### Criticism

Their's no mechanism to enforce ownership of an NFT by itself. Anybody can mint an NFT and say it means the holder owns an asset with on-chain consensus only verifying a transaction occurred. A record is meaningless without a product in hand where each NFT minter governs the rules for what the NFT means. Normally, a minter is a centralized entity with incentives that don't align with the NFT holder (sell for maximum price while maintaining maximum rights on the product), but there's no requirement for this. State laws have not caught up and with the internet spanning jurisdictions, enforcement seems dubious.

#### TOR Markets

TOR offers anonymity through a traditional web application interface albeit usually without client-side JavaScript support and other features we've come to expect. Markets hosted on TOR addresses often operate similarly to centralized markets. Administrators setup the market, maintain the infrastructure/app code, provide support, and resolve disputes. There's a review and feedback process in app for sellers/buyers and off app for markets themselves. The system incentives each party to behave appropriately and for everyone to profit as a result.

##### Criticism

Accessing web apps through TOR adds a high latency to each request, thus, are often quite slow. They don't have user friendly addresses that are easily discoverable. Without scripting capabilities (restricted for security and privacy), we often can't perform techniques to optimize data access and provide a responsive UX.

With markets being centrally controlled, there may be a power imbalance between parties. If a market becomes too popular, they monopolize visibility and access allowing them to dictate the terms for sellers/buyers. There's always a possibility of exit scams as ownership can't be transferred through consensus with some market administrators maintaining majority control.

#### BitTorrent / The Pirate Bay

##### Criticism

## Solution

DEscrow Market proposes a solution to the problem. We will look at each component's responsibility in the order they need to be setup and/or accessed.

![High Level Architecture](DEscrowMarketArchitecture.drawio.svg)

### Arbiter

First lets look at how an _arbiter_ presents a market and escrow interface to buyers and sellers.

#### Market Pool

From the buyer/seller's point of view, an _arbiter_ presents itself as a single addressable entity, but we can't trust one person to arbitrate a transaction. Thus, operators will form together to operate a pool of nodes.

#### Market Shard Group

**TODO** Take this section as notes and ideas for now. To optimize performance and reduce each node's data set size, it seems important to segment the data.

##### Shard Key

- Region ID: We want to segment nodes such that a shard group contains nodes that are evenly distributed across the world, so that regardless of where a user comes from nodes can be accessed in roughly an optimal 
  - Grouping of Geolocation Range
  - Response time to known IP routers by group
  - Hops to known IP routers by group
- Listing ID

##### Replication

To ensure availability, we need to replicate the data across nodes in the shard group.

##### Rebalance

To ensure data integrity, we need to handle nodes leaving and joining the pool.

#### Market Node

#### Market Operator

Each operator has a single vote stake in [arbitration](#disputes) and are equal members to all other operators. They do the work necessary to process buyer/seller request and store the associated data that's not critical to audit transactions on the blockchain.

### Buyer / Seller Client

We must store the data about markets on the blockchain, so that we're not dependent on any node in the market, but from there, most request will be handled by market nodes.

- Get the Market Pool metadata from the blockchain
- Determine the API endpoints for each data set by Region ID
- Get the user's initial data, examples:
  - Settings for the market (default filters, etc.)
  - If seller, get listing statuses
  - If buyer, get watched listings
- Set the initial endpoint if we get a response and cache the data for other endpoints as backups, else try again with another node.

### Seller

#### Listings

### Buyer

### Transaction

#### Smart Contract

#### Disputes

## Conclusion

### Improvements
