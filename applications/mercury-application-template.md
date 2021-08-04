# W3F Grant Proposal

* **Project Name:** -
* **Team Name:** -
* **Payment Address:** 0x6ec0D6c005797a561f6F3b46Ca4Cf43df3bF7888 (DAI)

## Project Overview :page_facing_up:
**Mercury** is a fully decentralized pinning service, combining decentralized off-chain storage with on-chain governance and data management to facitate a decentralized storage and delivery ecosystem. 

### Overview
Mercury builds on [previous work](https://github.com/rs-ipfs/substrate) which provides the basis to leverage ipfs as off-chain storage with on-chain verification and tracking via substrate. We intend to expand on this to build an "internet of ipfs clusters" that enables a decentralized data economy, ranging from data creation, consumption, storage, hosting, and delivery. Current solutions for decentralized storage are either lacking in security and privacy or rely on some centralized service. To illustrate this point, consider how the usage of a pinning services necessitates a degree of centralization. Additionally, the modularity and upgradeability provided with substrate would allow us to easily account found API changes or library upgrades (IPFS is still experimental and subject to change). To recap, this proposal:

* expands on IPFS integration for offchain storage by adding incentivization and creating a storage economy for an 'internet of IPFS clusters'
* a fully decentralized and secure storage solution without reliance on a centralized pinning service. 

 In *Mercury*, members of self-governed *provider pools* transparently provide both proof of storage (or capacity)f and proof of replication to ensure that they hold the file. Content creators pay a 'storage' fee (self-determined by the cluster) to pin data in some IPFS cluster (e.g. X coin/kb/sec). Access to the data can be placed behind some condition (e.g. a paywall) that will automatically grant access once the condition is met, after which the consumer can retrieve the content from the cluster to which it's pinned. IPFS clusters are mapped surjectively to addresses within the blockchain, and we will build an 'internet of ipfs clusters', where storage size, bandwidth, availability, fees, etc., are self-determined by the on-chain 'provider' nodes. We refer to a collection of provider nodes mapping to a cluster as a 'pool'. Nodes can provide storage in the same way that a DEX allows you to provide liquidity in the form of key-pairs.

 There are various real world benefits that results from this approach as well. IPFS provides a more resilient and efficient way to access data. Not only does it provide more cost efficient storage and hosting, but also more cost efficient access, as there is no third party that acts as platform owner and maintainer. We also provide a means of passive income for storage providers. Content creators also benefit from a higher degree of freedom, means of support/funding, etc., but also a higher degree of accountability and traceability.

### Project Details

#### Terminology and Use Cases
A **provider** node is any node that is a member of a *pool* and is able to deliver some content as identified by a CID when requested.
A **pool** is a collection of *provider* nodes that all belong to the same IPFS cluster.
A **consumer** node is any node that is requesting data from a *pool*.
An **owner** node is a node that has pinned some data within a *pool*.

A provider node is any node that will reserve some amount of storage for IPFS. A provider, using Mercury, can join multiple IPFS clusters in order to provide storage and delivery.

#### Decentralized Pinning Service
A decentralized pinning service is the heart of the proposal. In order to understand how pinning and retrieving data function we must first understand how data can be stored and transferred offchain and verified on-chain, as well as the incentives for providing storage and access. We'll also analyze some of the pros and cons of this approach, as well as explain why a 'storage economy' may result.

##### Configuring an IPFS cluster with Mercury
IPFS cluster creation is not done within Mercury itself, and must occur independently. So we will assume that there are some pre-existing IPFS clusters, {C<sub>0</sub>, ..., C<sub>k</sub>}.

Since cluster creation happends independently we will support bidirectionality for participating in Mercury. That is, a node can first be part of an IPFS cluster and then join Mercury, or join Mercury and the join an IPFS cluster. 

Suppose you're a node in some IPFS cluster C<sub>j</sub> and you want to provide your storage space by running a mercury node.
Firstly, you must verify your IPFS node address as well as cluster information. What information? not really sure... but we'll need to cryptographically verify that you are you and your cluster is your cluster and the info is correct and trusted...

Provider nodes will ingest data from owners by allowing the owner to join the IPFS network so that they can transfer the file.
When a *pool* pins a file, then there is massive redundancy
Provider nodes will verify that a CID is pinned by calling the `ipfs pin verify` command.

##### Proof of IPFS Cluster membership

##### Proof of Storage/Capacity/Pin

##### Fee Distribution to Provider Pools
All members of a provider reward gets a share of fees paid when pins are created and when data is received. The distribution of the fee should be based on several factors, such as:
  - total storage provided
  - quality of data/transmission/bandwidth

##### Moderation

#### Block Creation

* Mockups/designs of any UI components
  * Should design a sample UI -> streaming decentralized video, audio, etc. (i.e. youtube, spotify)
* Data models / API specifications of the core functionality
  * 30,000-foot view [insert diagram here]
* An overview of the technology stack to be used
  * Substrate: For blockchain development
  * IPFS: For offchain storage
  * polkadot-js: For interacting with the blockchain 
  * rust: language used for developing the blockchain
  * typescript: language used for developing the frontend
* Documentation of core components, protocols, architecture, etc. to be deployed
  * The substrate pallets:
    * The Pool Pallet
      * Track ipfs cluster to substrate node mapping -> each ipfs cluster should be private and membership managed via the blockchain
      * nodes will have to prove their cluster membership and provided storage + bandwidth.
      * potential spec:
        ```
          JoinPool(poolId)      <-- called by provider
          LeavePool(poolId)     <-- called by provider
          PoolStats(poolId)     <-- called by any
          ListPools()           <-- called by any
          Pin(data)             <-- called by owner
          Purge(CID)            <-- called by owner or pool (via governance -> need a mechanism for voting to purge content)
          Download(poolId, CID) <-- called by consumer
        ```
    * The Content Owner Pallet
      * Owners publish their data for sale, along with manage access to the data
        ```
        Publish(CID)               <-- called by owner
        Purge(CID)                 <-- called by owner
        RequestAccess(CID)         <-- called by consumer
        VerifyAccess(CID, Address) <-- called by any
        RemoveAccess(CID, Address) <-- called by owner
        GetAccessibleCIDs(Address) <-- called by consumer
        GetOwner(CID)              <-- called by any
        ```
    * The Consumer Pallet --> needed?
* PoC/MVP or other relevant prior work or research on the topic
  * we will use previous work on substrate/ipfs integration as a basis for the project: https://github.com/rs-ipfs/substrate
* What your project is _not_ or will _not_ provide or implement
  * This is a place for you to manage expectations and to clarify any limitations that might not be obvious
    * Mercury is immutable but not indefinitely *persistent*. That is, your data will only be ensured to be available as long as there is incentive for a pool to hold it. Pinning in this context is still subject to the limitations outlined here: **https://docs.ipfs.io/concepts/persistence/**.


### Ecosystem Fit

Help us locate your project in the Polkadot/Substrate/Kusama landscape and what problems it tries to solve by answering each of these questions:

* Where and how does your project fit into the ecosystem?
  * This project greatly expands on off-chain storage solutions for blockchains.
* Who is your target audience (parachain/dapp/wallet/UI developers, designers, your own user base, some dapp's userbase, yourself)?
  * 1) Developers
  * 2) My own user base
    * a) content creators
    * b) storage providers
    * c) content consumers
* What need(s) does your project meet?
  * The project expands on current off-chain storage capabilities with IPFS. It will enable incentive for nodes to provide storage and pin data, as well as provide low-cost ways for consumers to support creators and for creators to sell content and affordably host it.
  * Fair and transparent governance will do away with the obfuscatory and totalitarian moderation done on today's centralized platforms. Was that a little too harsh?
* Are there any other projects similar to yours in the Substrate / Polkadot / Kusama ecosystem?
  * If so, how is your project different?
    * Yes: https://github.com/rs-ipfs/substrate
  * If not, are there similar projects in related ecosystems?
    * Yes:
      * Pinning services (like Pinata)
      * Filecoin
      * Textile

## Team :busts_in_silhouette:

### Team members

* Name of team leader
  * Tony Riemer
* Names of team members
  * TBD

### Contact

* **Contact Name:** Tony Riemer
* **Contact Email:** tonyrriemer@gmail.com
* **Website:**

### Legal Structure

* **Registered Address:**
  * N/A
* **Registered Legal Entity:**
  * N/A

### Team's experience

Tony Riemer has been a full stack engineer for over five years. After graduating with a degree in mathematics, he entered a contract with FDM, through which he was contracted to Fannie Mae for 2 years. After those two years, he worked an additional year at fannie mae, where he contributed greatly to the "Servicing Marketplace" project, both in development and ideation. After this, he moved to Capital One where he single-handedly built the groundwork and infrastructure for a new case management platform. Anytime you change your name or ssn in a capital one cafe, you're using his software. He is an avid technologist and has experience with a wide range of languages and technologies (please see my github for more details).


### Team Code Repos

* https://github.com/<your_organisation>
* https://github.com/<your_organisation>/<project_1>
* https://github.com/<your_organisation>/<project_2>

Please also provide the GitHub accounts of all team members. If they contain no activity, references to projects hosted elsewhere or live are also fine.

* https://github.com/driemworks

### Team LinkedIn Profiles (if available)

https://www.linkedin.com/in/tony-riemer/

## Development Status :open_book:

If you've already started implementing your project or it is part of a larger repository, please provide a link and a description of the code here. In any case, please provide some documentation on the research and other work you have conducted before applying. This could be:

* links to improvement proposals or [RFPs](https://github.com/w3f/Grants-Program/tree/master/rfp-proposal) (requests for proposal),
* academic publications relevant to the problem,
* links to your research diary, blog posts, articles, forum discussions or open GitHub issues,
* references to conversations you might have had related to this project with anyone from the Web3 Foundation,
* previous interface iterations, such as mock-ups and wireframes.

## Development Roadmap :nut_and_bolt:

This section should break the development roadmap down into milestones and deliverables. Since these will be part of the agreement, it helps to describe _the functionality we should expect in as much detail as possible_, plus how we can verify and test that functionality. Whenever milestones are delivered, we refer to this document to ensure that everything has been delivered as expected.

Below we provide an **example roadmap**. In the descriptions, it should be clear how your project is related to Substrate, Kusama or Polkadot. We _recommend_ that the scope of the work can fit within a three-month period and that teams structure their roadmap as 1 milestone ≈ 1 month.

For each milestone,

* make sure to include a specification of your software. _Treat it as a contract_; the level of detail must be enough to later verify that the software meets the specification.
To assist you in defining it, we have created a document with examples for some grant categories [here](../docs/grant_guidelines_per_category.md).
* include the amount of funding requested _per milestone_.
* include documentation (tutorials, API specifications, architecture diagrams, whatever is appropriate) in each milestone. This ensures that the code can be widely used by the community.
* provide a test suite, comprising unit and integration tests, along with a guide on how to set up and run them.
* commit to providing Dockerfiles for the delivery of your project.
* indicate milestone duration as well as number of full-time employees working on each milestone.
* **Deliverables 0a-0d are mandatory for all milestones**, and deliverable 0e at least for the last one. If you do not intend to deliver one of these, please state a reason in its specification (e.g. Milestone X is research oriented and as such there is no code to test).

> :zap: If any of your deliverables is based on somebody else's work, make sure you work and publish _under the terms of the license_ of the respective project and that you **highlight this fact in your milestone documentation** and in the source code if applicable! **Teams that submit others' work without attributing it will be immediately terminated.**

### Overview

* **Total Estimated Duration:** 4 months
* **Full-Time Equivalent (FTE):**  1 FTE
* **Total Costs:** $10,000 USD

### Milestone 1 — Implement Substrate Modules

* **Estimated duration:** 6 Weeks
* **FTE:**  1
* **Costs:** 4000 DAI

| Number | Deliverable | Specification |
| -----: | ----------- | ------------- |
| 0a. | License | Apache 2.0 / GPLv3 / MIT / Unlicense |
| 0b. | Documentation | We will provide both **inline documentation** of the code and a basic **tutorial** that explains how a user can (for example) spin up one of our Substrate nodes and send test transactions, which will show how the new functionality works. |
| 0c. | Testing Guide | Core functions will be fully covered by unit tests to ensure functionality and robustness. In the guide, we will describe how to run these tests. |
| 0d. | Docker | We will provide a Dockerfile(s) that can be used to test all the functionality delivered with this milestone. |
| 0e. | Article | We will publish an **article**/workshop that explains [...] (what was done/achieved as part of the grant). (Content, 
| 1. | Get rs-ipfs/substrate ready | sync with master, setup + run locally, etc. |
| 2. | Substrate module: Pool Pallet | We will build a pallet that enables that allows us to track ipfs cluster states on-chain, and exposes functionality to establish a pool, join a pool, and leave a pool. Additionally, the pallet will allow us to gather some metrics of the ipfs clusters (ipfs cluster must have tracing enabled) |  
| 3. | Substrate module: Creator Pallet | Advertise content: Encode in a transaction that you own some data and are willing to provide access to it. Allow nodes to purchase content: For a price, nodes can be added to a list of approved nodes who can access the data. Null means any nodes can access the data, [] means no node can.  |  
| 4. | Substrate module: Pool Pallet | Expose functionality to retrieved pinned data by CID based on ownership/access to the data as granted by nodes as of (2b) |


### Milestone 2 — Additional features

* **Estimated Duration:** 6 weeks 
* **FTE:**  1
* **Costs:** 4000 DAI

| Number | Deliverable | Specification |
| -----: | ----------- | ------------- |
| 0a. | License | Apache 2.0 / GPLv3 / MIT / Unlicense |
| 0b. | Documentation | We will provide both **inline documentation** of the code and a basic **tutorial** that explains how a user can (for example) spin up one of our Substrate nodes and send test transactions, which will show how the new functionality works. |
| 0c. | Testing Guide | Core functions will be fully covered by unit tests to ensure functionality and robustness. In the guide, we will describe how to run these tests. |
| 0d. | Docker | We will provide a Dockerfile(s) that can be used to test all the functionality delivered with this milestone. |
| 0e. | Article | We will publish an **article**/workshop that explains [...] (what was done/achieved as part of the grant). (Content, 
| 1.  | | | 
| 2. | | |

### Milestone 3 — Additional features

* **Estimated Duration:** 4 weeks
* **FTE:**  1
* **Costs:** 3000 DAI



## Future Plans

Please include here

Future Enhancements:
* real-time and streaming support
* The pattern for fetching offchain data can be futher generalized beyond file content
  * offchain workers as real-world actions
* interactive application with access to decentralized storage:
  * gaming?
  * google docs

* how you intend to use, enhance, promote and support your project in the short term, and
* the team's long-term plans and intentions in relation to it.


## Additional Information :heavy_plus_sign:

**How did you hear about the Grants Program?** Web3 Foundation Website

Here you can also add any additional information that you think is relevant to this application but isn't part of it already, such as:

* Work you have already done.
  * Tony has previously worked with IPFS, Ethereum (solidity), as well as implemented his own blockchain (in Go).

