---
uuid: a39a50ba-fe84-4382-9509-82f36b211619
share: true
---
Inter Planetary Linked Data

#### [[Backlog - Research]]

``` bash

go install github.com/peergos/ipfs-nucleus@main

```

* [GPN19 - Foundations for Decentralization: Data with IPLD - YouTube](https://www.youtube.com/watch?v=totVQXYS1N8)
	* File are just a graph
	* Git is just a blob store
	* Link by hash should be first class
	* Immutable Links are a good primitive
	* Formats shouldn't matter
	* Protocols need Sachems, data description tools
	* Building a git
	* [[CID]] - Content Identity
	* You can replace JSON in API's with IPLD
	* There is a query language like [[GraphQL]]
	* Advanced Layouts?

## 2023-12-29T15:41:27-05:00

* [ResNetLab: Elective Course Module - InterPlanetary Linked Data (IPLD) - YouTube](https://www.youtube.com/watch?v=Sgf6j_mCdjI)
	* Building the next git should take hours and not days
	* Immutability
	* DeDuplication
	* Content Addressing
	* IPLD is extracted from IPFS
	* IPFS is a block store for IPLD
	* Merkle DAGs
		* Markle DAGs only link forward not backward
		* Git, everything in git is blob hashed
		* Markle DAG verse Merkle Tree
		* You can add metadata within the Markle Tree/DAG
	* Connecting Graphs
		* Autonomy of a CID
		* multiformats.io
		* CBOR and JSON have no formal way to link data
	* IPLD and IPFS
		* IPLD uses DAG-PB
	* Beyond File Data:
		* IPLD Datamodel, basically JSON with bytes and link
		* DAG-JSON
			* Basically what I did for Holium
		* DAG-CBOR
		* [[Filecoin]] uses DAG-CBOR

## 2023-12-29T15:59:56-05:00

* [Bluesky and IPLD - Jay Graber - YouTube](https://www.youtube.com/watch?v=jGbBZbl-V8Y)
	* Why
		* Scaling Moderation
		* Algorithmic Choice
		* Curation Health, not Social Delema
		* New Tech allows Decentralization
		* Distribute power
	* [Jay Graber on X: "I wrote an ecosystem review of decentralized social protocols to help inform early @bluesky discussions, published today. Reach out if you have feedback or want to discuss!" / X](https://twitter.com/arcalinea/status/1352316972654944257)
	* Federated verses p2p erses Blockchain
	* [[Bluesk]] run on [[AT Protocol]]

## Tweets

* [(3) Raúl Kripalani on X: "It rests on a number tech choices made throughout Filecoin’s history to keep the protocol modular, future-proof and extensible, e.g. multi-addressing, IPLD. https://t.co/dIpFCdXwz6" / X](https://twitter.com/raulvk/status/1633839400256942080)
* [(3) Ceramic on X: "Interested in learning about how Ceramic uses a timestamp service (e.g ETH) to anchor events in time and produce mutable, consistent streams of IPLD data? ⚓️⚡️ Check out our senior research engineer, @AaronDGoldman, diving in here: https://t.co/EuXjrvSLVR" / X](https://twitter.com/ceramicnetwork/status/1651315760663281664)
* [(3) Fission (@FISSIONcodes) / X](https://twitter.com/FISSIONcodes)