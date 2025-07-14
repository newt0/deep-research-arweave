---
title: ArFleet Overview
platform: ChatGPT DeepResearch (GPT-4o)
date: 2025-07-10
url: https://chatgpt.com/share/686f81ba-835c-8000-b0ee-8caebbe9e786
tags: [ao, prorocol, arfleet, developer]
---

[Prompt]

```markdown
Please conduct a detailed technical investigation into **Arweave’s ArFleet**, specifically from the perspective of **Web3 developers** considering integration into real-world dApps.

### Information Source Prioritization (Only use primary sources published **after July 2024**):

1. GitHub (e.g., [`aoacc/arfleet-js`](https://github.com/aoacc/arfleet-js): codebase, README, examples)
2. Official documentation (ao/acc, Arweave core docs, Community Labs materials)
3. Developer blogs, walkthroughs, and hackathon demos
4. Developer posts on X (formerly Twitter) by ao/acc and Arweave core contributors
5. Publicly shared AMA transcripts, community calls, and presentations

## Output Structure (in Markdown)

### 1. Overview of ArFleet

- Project definition and primary use cases (specifically in the context of Web3 apps)
- Development entity (ao/acc Labs) and its relationship to AO and the Arweave core team
- Current release status (mainnet, alpha, testnet availability)

### 2. Technical Architecture and Integration Design

- System components relevant to developers (Actor-based flow, data handling scope)
- Architecture on AO: how Actors, Processes, and Executors are used
- Supported operations (store, fetch, delete)
- Integration points with Arweave (when and how data is persisted)

### 3. API, SDK, and Tooling

- Available SDKs and APIs (focus on `arfleet-js`)
- JS/TS usage examples (e.g., uploading ephemeral JSON, files)
- Deployment setup: how to install, configure, and start using ArFleet
- Testing options (local dev mode, AO testnet)

### 4. Integration & Usage Examples

- Real dApp integration patterns (e.g., AI agents, dashboards, ephemeral user data)
- Compatibility with other AO actors or external chains
- Supported data formats (binary, JSON, etc.)

### 5. Incentives and Payment Logic

- How developers and users are charged (via \$AO or \$AR)
- How to integrate billing into a dApp (user-pays, subsidized, hybrid models)
- Whether ArFleet has (or plans to have) a native token — and why \[mark as “TBD” if unknown]

### 6. Roadmap & Known Limitations

- Short- and mid-term development plans
- Current constraints (e.g., TTL duration, actor instance limits, storage quotas)

## Output Requirements

- Use **Markdown format**
- Include **reliable source links** in each section
- Include code snippets or diagrams where appropriate
- Clearly mark unknown or speculative information with `[TBD]` or `[To Be Confirmed]`
- State the date of the research clearly at the top (e.g., “As of July 2025”)
```

# [Output]

### 1. Overview of ArFleet

**Definition & Purpose:** ArFleet is a decentralized **temporary storage** protocol built on Arweave’s new AO (Actor-Oriented) compute environment. It enables **time-bound data storage** deals between clients and storage providers, complementing Arweave’s permanent storage by allowing developers to store data **only for a finite period** instead of forever. In practical terms, ArFleet gives Web3 applications a **flexible, cost-effective** option for ephemeral data that doesn’t need perpetual preservation. For example, dApps can use ArFleet for session data, cache files, AI model outputs, message drafts, or any content with a short useful lifetime, avoiding the higher cost of permanent on-chain storage.

**Development & Team:** ArFleet is developed by **ao/acc Labs**, an organization pioneering decentralized compute and storage solutions on Arweave’s stack. AO/ACC Labs works closely with the Arweave core ecosystem: it leverages Arweave’s permanent data layer and the AO compute platform to build ArFleet and other decentralized apps. While not part of the _Arweave core_ protocol, ArFleet is an official ecosystem project (its launch was promoted by Arweave founder Sam Williams) and is a key component of Arweave’s vision for a “Fully Decentralized Stack” (permanent storage via Arweave + temporary storage via ArFleet + compute via AO). In essence, ArFleet extends Arweave’s functionality by adding a **time-limited storage layer** on AO, co-created with support from Arweave community entities like Community Labs and AO developers.

**Release Status:** ArFleet launched an **alpha testnet** in late August 2024. Access to the testnet was initially gated by **Genesis Pass** NFTs (each early user received passes to run ArFleet clients or providers). During testnet, only Genesis Pass holders could participate as storage providers or clients, ensuring a controlled rollout. As of 2025, ArFleet has undergone multiple testnet iterations (e.g. **v0.1.2** of the ArFleet Web app launched in Sep 2024) and optimizations. The AO platform itself **launched on mainnet in February 2025**, enabling the \$AO token and broad availability of AO-based services. ArFleet is expected to transition onto AO mainnet alongside or shortly after AO’s launch. **Mainnet status:** _Likely in progress –_ by mid-2025 ArFleet is still in an early stage on mainnet (initially limited to early adopters), moving out of alpha. Developers can already experiment on the AO **testnet** or with limited mainnet access, using AR (and now AO tokens) for payments. (Full open mainnet access is \[TBD], pending official release updates.)

### 2. Technical Architecture and Integration Design

**Actor-Based Architecture:** ArFleet is built entirely on the **AO actor model**, meaning its logic runs in decentralized “processes” (actors) on the AO compute network. These actors coordinate the storage deals in a trustless manner. In ArFleet, there are two primary roles: **Clients** (users or dApps needing storage) and **Providers** (nodes offering storage). They communicate off-chain when possible (for efficiency), but rely on **on-chain AO actors for critical operations** that require trustless enforcement. Key components include:

- **Marketplace Actor:** A global AO process called the **Marketplace** is used for **provider discovery**. Providers publicly **announce** their service terms here, including their Arweave wallet ID (used as provider identity), network address (IP/port), pricing, maximum storage duration, and challenge interval preferences. Clients query this Marketplace actor to find available providers that meet the requirements of a given storage request. (The Marketplace is essentially a decentralized bulletin board of providers.)

- **Deal Actors (Processes):** Every storage deal between a client and a provider is executed within a **dedicated AO process (actor)**, often referred to as a **Deal** process. When a client decides to store data with a provider, the ArFleet software spawns a new actor (using a known ArFleet deal smart contract code) parameterized with that deal’s terms. This actor holds the **escrow funds** (the client’s payment and the provider’s collateral) and enforces the deal terms. Importantly, all ArFleet deal actors run on the AO network’s decentralized executors, so their state and decisions are **verifiable and consensus-driven** – no central server controls the deal. (AO executors are the nodes that run actor processes in parallel and record their messages/outcomes on Arweave for consensus.)

**Data Flow & Lifecycle:** The end-to-end process for storing data via ArFleet involves several stages (managed by the client software, with on-chain steps at critical points):

1. **Assignment Creation:** The dApp or user creates a **Storage Assignment** – essentially a job describing what to store and under what terms. The client specifies the data pointer (file or payload), desired **storage duration**, how many **copies (redundancy)** to store, and the reward they are willing to pay. This assignment is queued in the ArFleet client.

2. **Provider Matching:** The ArFleet client searches for providers to fulfill the request. It uses the Marketplace actor to list suitable providers (e.g. those advertising enough capacity, supporting the requested duration, and acceptable price). Because the on-chain marketplace info may be slightly stale, the client then directly **pings the provider** off-chain to confirm availability and capacity. Once a suitable provider is confirmed, the client and provider agree to initiate a **Placement** – a pairing of that Assignment with that Provider.

3. **Deal Initialization:** The client now begins the placement. A new placement starts in state `CREATED`. The client opens a connection to the provider and sends a placement request; if the provider accepts, the state becomes `INITIALIZED`. At this point the client **encrypts and prepares the data** for storage:

   - The data is split into fixed-size **chunks** (by default 8 KB chunks) and each chunk is encrypted. A Merkle **tree of the encrypted chunks** is computed, yielding a single root hash. (This Merkle root will be used for verifying proofs.) The system uses multiple encryption layers for security: ArFleet applies an RSA-based encryption on chunks for Sybil resistance and allows optional AES-256 encryption by the user for privacy. After encryption, the placement moves to `ENCRYPTED` state.
   - **Actor Deployment:** Next, the ArFleet client spawns the **Deal actor** on AO. It supplies the ArFleet smart contract code (module) and passes in the deal parameters (e.g. root hash of the data, duration, identities, etc.) to create a new AO process for this deal. The state becomes `PROCESS_SPAWNED` once the on-chain process is created.

4. **Funding & Escrow:** The client now **funds the deal** by depositing the promised reward payment into the newly created deal process (escrow). This typically means sending the specified amount of AR (or other token) into the AO process’s wallet/address. Once funded, the deal actor holds the reward in escrow and the placement status becomes `FUNDED`. At this point, the client’s on-chain obligations are set aside in the deal contract.

5. **Provider Acceptance:** The provider’s ArFleet node is notified (off-chain or via AO messaging) that the deal has been funded and is ready. The provider then **accepts the deal** on their side, which triggers them to lock up the required **collateral** into the deal actor as well. Provider collateral is an amount (set by protocol or negotiation) to be staked as a guarantee. Once the provider accepts and stakes collateral, the deal actor marks the deal as `ACCEPTED` and “activated” – both parties’ funds are now locked on-chain and the storage contract is in effect.

6. **Data Transfer:** After acceptance, the actual data transfer happens **directly between client and provider** off-chain. The client streams the encrypted chunks to the provider node over HTTP or similar, in the `TRANSFERRED` state. (In ArFleet v0.1, this requires keeping the client online until transfer completes, especially for large files.) Once all chunks are uploaded and the provider confirms receipt, the status moves to `TRANSFERRED`.

7. **Completion:** Finally, the provider signals the deal actor that setup is complete. The deal actor verifies that it has the provider’s collateral and all needed info (the deal actor checks that it has been activated properly with both funds). If all is well, the deal is marked `COMPLETED`. At this point, the **storage lease period** officially begins, and the provider must keep the data available until the agreed expiration time.

8. **Storage & Expiration:** The provider stores the encrypted data in its local storage for the duration of the lease. The ArFleet protocol does _not_ persist the file on Arweave; it lives on the provider’s node storage. A **time-to-live (TTL)** was specified in the deal, after which the data is considered expired. Once the expiration is reached (assuming no renewal), the provider is free to delete the data from their disk, and the deal actor can terminate. ArFleet ensures that **data is automatically removed after the expiration** – ephemeral by design. (If the client needs the data longer, they would have to initiate a new deal or renewal _before_ expiry – renewal mechanisms are \[To Be Confirmed].)

**Verification & Challenge Game:** During the active storage period, ArFleet employs a continuous verification game to ensure the provider is indeed storing the data. After the deal is activated, the **Deal actor** on AO periodically issues **random challenges** that require the provider to prove they still have the file. Each challenge consists of the deal actor generating a random bitstring which maps to a specific chunk in the Merkle tree of the file (traversing 0/1 for left/right branches). The provider must respond with a **proof** containing the requested chunk data _and_ the Merkle path (all the hashes from that chunk up to the root). The deal actor verifies this proof against the known root hash stored in the contract. If the chunk data and path hash match the root, the **challenge is passed**. If the provider fails to provide the correct chunk or misses the challenge deadline, the proof is considered failed.

ArFleet’s incentive structure is enforced here:

- For each successful proof, the provider continues the deal uninterrupted (and typically will later claim the reward upon completion).
- For a failed or missed proof, the contract **slashes the provider’s collateral** – a portion of the stake is forfeited as a penalty. Multiple consecutive failures can lead to the provider losing **all their collateral** and effectively nullifying the deal. This slashing mechanism strongly incentivizes providers to **retain the data intact** for the full term of the deal. Notably, all verification happens between the provider and the on-chain deal actor; the client does not need to be online or involved during the storage period.

If the provider honors the deal until expiration, they can gracefully exit and retrieve their remaining collateral and the reward. The deal actor will release the **reward payment to the provider** once all challenges during the term have been passed and the term is complete. If the provider cheated or dropped the data, their collateral is slashed and the reward can be returned to the client or burned (depending on implementation). This entire flow is handled autonomously by the AO-based **smart contract (actor)**, without third-party escrow or manual arbitration.

**Data Handling and Persistence:** Importantly, ArFleet data is **kept off-chain** (on provider nodes) to remain temporary. However, certain **metadata and state are persisted on Arweave** via AO:

- The **Deal actor’s state** (e.g. the Merkle root of the file, challenge records, and payment escrow info) and all messages (transactions) in the AO network are permanently logged to the Arweave chain as part of AO’s design. AO uses Arweave to store a tamper-proof log of all process events – a concept called _holographic state_ – allowing anyone to audit or recompute the state transitions. Thus, each ArFleet deal has a permanent on-chain record (e.g. an Arweave transaction ID for the process creation and subsequent challenge results).
- The **ArFleet Marketplace announcements** might also be stored or anchored on-chain (the Marketplace actor state is on AO, so its updates are also logged permanently). Providers advertise using their Arweave wallet address as ID, linking their identity to Arweave’s crypto wallet system.
- The **actual file content** is _not_ put on Arweave (that would make it permanent, defeating the purpose). Only a content hash (Merkle root) and proofs go on-chain. If a developer does need to later preserve a piece of data initially on ArFleet, they would have to separately upload it to Arweave’s permanent storage. ArFleet’s role is to hold the data off-chain with cryptographic assurances for a limited time.

**Supported Operations:** From a developer’s standpoint, ArFleet supports basic storage CRUD for ephemeral data:

- **Store/Upload:** The primary operation is storing a new piece of data via a deal. Developers specify the file or payload and parameters (duration, redundancy, etc.), and the ArFleet client software orchestrates the deal creation and upload as described above. This is the core workflow of ArFleet.
- **Fetch/Retrieve:** To retrieve data stored in ArFleet, a client (or any authorized party) needs the **content’s identifier and decryption key**. When a file is stored, it is assigned a unique identifier (often the AO process ID or a generated transaction ID) which can be used to locate it. For example, the ArFleet Web app allows private sharing by giving another user the file’s TXID and the AES key used for encryption. Using those, the data can be fetched from the provider network: the ArFleet client (or web worker in browser) contacts the provider holding that TXID and streams the encrypted chunks, then decrypts them in-browser for download. In essence, ArFleet retrieval is done via the network of providers, keyed by the content ID (and only those with the key can decipher private data). There isn’t a global content-addressed lookup like Arweave’s gateways yet; one must either query the original provider or use the network’s discovery mechanism to find which provider still has the chunk. (In practice, the client remembers which providers were used or the Marketplace could be extended to index active deals – details evolving \[TBD].)
- **Delete/Expire:** There is no explicit “delete” API call in ArFleet for clients, because deals are time-limited and expire on their own. Once the TTL is reached, providers will drop the data automatically. A client who wants to terminate early could theoretically stop renewing and perhaps signal the provider (but since payment is pre-paid, they might simply let it run out). If a provider goes offline or wants to opt out, they would incur collateral loss if done unilaterally. Currently, the expectation is that data deletion is handled by **natural expiration**. (Future iterations might allow deal termination by mutual agreement – \[TBD].)

### 3. API, SDK, and Tooling

Developers can interact with ArFleet through several provided tools and SDKs:

- **ArFleet Web App:** A **browser-based client** (hosted at `arfleet.arweave.net` or via Arweave gateways). This web UI allows users to connect an Arweave wallet and easily upload files to ArFleet without installing anything. It’s convenient for quick tests or non-technical users. _Limitations:_ Web browsers can’t handle very large files or background processes well, so the web client imposes file size limits and requires keeping the tab open during upload. As of late 2024 it was in beta (Genesis Pass required), but it demonstrates storing files by paying a small amount of **wrapped AR (wAR)** from a wallet.

- **ArFleet-JS (JavaScript SDK):** A Node.js client library and CLI, geared towards developers and power users. The **arfleet-js** toolkit runs on a local machine or server and offers more control and capability than the web app. It supports larger file uploads, automation, and integration into Node.js backends or scripts. ArFleet-JS is open-source (GitHub: `aoacc/arfleet-js`) and includes both a CLI interface and programmatic modules. To get started, developers clone the repo and install dependencies for both the _backend_ (Node server) and _frontend_ (CLI/UI) components. Running `./arfleet` launches the CLI tool. For example:

  ```bash
  # Clone ArFleet-JS and install
  git clone https://github.com/aoacc/arfleet-js.git
  cd arfleet-js/backend && npm install
  cd ../frontend && npm install
  cd ..  # back to project root

  # Start an ArFleet client node
  ./arfleet client

  # Once running, store a file or directory:
  ./arfleet client store /path/to/myFile.png
  ```

  As shown above, the CLI provides a `store` command to upload a file or even an entire directory (which it will bundle and upload). When launched, the client will output its Arweave/AO **wallet address**; if you are in the testnet phase, you need to **own a Genesis Pass NFT** and transfer it to that address to activate the client. Similarly, running `./arfleet provider` would start a provider node process on your machine (for testing or if you want to become a provider). Under the hood, ArFleet-JS spins up an AO client that connects to the AO network (by default the testnet or localnet, configurable) and handles all protocol steps (contacting providers, spawning deals, etc.).

  _Integration:_ Developers can also integrate ArFleet-JS logic into their own Node.js apps. The repository includes a backend library (written in JS/TS and even some Lua) that could be imported. For instance, a dApp back-end could invoke ArFleet-JS functions to submit a file to ArFleet or fetch one. (Detailed API docs for direct library use are still evolving – currently, many use the CLI or the provided scripts as the interface.)

- **ArFleet-Erlang:** An Erlang implementation of ArFleet’s client/provider. This version is optimized for **high-performance and server-side deployments**. Erlang/OTP is known for handling concurrent network processes efficiently, so ArFleet-Erlang is ideal for those wanting to run a robust provider node or integrate at the infrastructure level. It’s open-source as well (`aoacc/arfleet-erl` on GitHub). While most dApp developers will use the JS SDK or web client, service providers or those needing maximal throughput can run the Erlang version for better scalability. (For example, an exchange or data service might run ArFleet-Erlang to offer storage to its users with minimal overhead.)

- **Provider Setup Tools:** To become a storage provider, one currently uses the same ArFleet-JS or Erlang software in provider mode. The documentation provides a setup guide (generate or provide an Arweave wallet key, run `arfleet provider`, announce on Marketplace, etc.). Providers need to configure their node (bandwidth, storage limits, pricing) and ensure they maintain an Arweave wallet with some funds for collateral. As ArFleet matures, we may see dedicated provider node packages or Docker images for easier deployment \[TBD]. For now, the **ArFleet-JS** repo’s script is the primary way to launch a provider service on the network.

- **Testing and Development:** During the current phase, developers typically test against the **AO testnet**. The AO testnet has been very active (processing hundreds of millions of messages). To use ArFleet on testnet, a Genesis Pass NFT was required, as noted, to prevent overload while in alpha. Developers could obtain a pass via the initial events or from the secondary marketplace (the passes are tradable on Arweave’s BazAR). Once the pass is in hand and transferred to your ArFleet client address, you gain full access to testnet functionality. The client will automatically detect the pass in its wallet and enable network operations.

  For **local development**, since AO is a complex distributed system, there isn’t a trivial “ArFleet local node” simulation yet. However, one could run a local AO node network (the AO team has some tools to run local clusters) \[TBD] and then deploy ArFleet actors there. In practice, most developers will stick to the shared testnet or mainnet environment. The ArFleet docs recommend checking the official docs frequently, as things can change quickly in this phase.

**Example:** Using the ArFleet-JS CLI, suppose a developer wants to upload a JSON snippet or small file temporarily. They would run the store command pointing to that file. The CLI would output an ArFleet **TXID** for the stored data. The developer can then later run a (future) `fetch` command with that TXID to retrieve it, or use the web app and paste the TXID + decrypt key to download it. For programmatic use, one might call the JS library to store data and get back a handle/ID, which the front-end dApp can store and use to retrieve or share the content within its TTL. Code snippet illustration (pseudo-code):

```js
const arfleet = require("arfleet-js-backend"); // hypothetical module usage
// Initialize client (with wallet and maybe pass)
await arfleet.init({ walletPath: "./wallet.json" });
let result = await arfleet.storeData(Buffer.from(JSON.stringify(myObject)), {
  duration: 3600,
});
console.log("Stored TXID:", result.txid);
```

_(Note: Actual API may differ; currently the CLI wraps these calls.)_

Overall, the tooling around ArFleet is rapidly evolving. Developers are encouraged to use the open-source repos and join the Arweave/AO Discord for the latest SDK improvements. The existence of both JS and Erlang implementations also means community contributions in multiple languages are possible, and we may see Python or Rust client libraries emerge in the future \[TBD].

### 4. Integration & Usage Examples

ArFleet unlocks new **integration patterns** for Web3 dApps by providing a decentralized equivalent of ephemeral cloud storage. Some concrete ways developers can leverage ArFleet in real-world applications:

- **AI Agents and On-Chain AI Workloads:** A flagship use-case of AO is running autonomous agents and AI models on-chain. These AI agents often generate intermediate data (e.g. prompt histories, temporary model outputs, caches) that do not need to be stored permanently. ArFleet can serve as a **“scratch disk” or memory layer** for AI agents. For example, an AI agent process on AO could store its short-term conversational context or computation intermediates in ArFleet, retrieving them as needed during its operation, and let them expire when the session is over. This complements Arweave’s permanent storage where final important results or audit logs might be stored. By using ArFleet for ephemeral memory, on-chain agents avoid cluttering Arweave with transient data and reduce costs, while still retaining trustless verifiability during the agent’s run. (This pattern – long-term knowledge on Arweave, short-term working data on ArFleet – provides a **full spectrum storage** solution for on-chain AI. It has been hinted as a key part of the **Fully Decentralized Stack** along with compute.)

- **User Session Data and DApp State:** Consider a Web3 social app or dashboard where user-generated content like drafts, temporary images, or session state should live only for hours or days (for privacy or cost reasons). Such a dApp can integrate ArFleet on the backend to store this **ephemeral user data**. For instance, a decentralized chat application might use Arweave to permanently archive published messages, but use ArFleet to hold “typing… indicators”, ephemeral stories, or expiring attachments that vanish after 24 hours. The front-end could upload these to ArFleet via the dApp’s backend service (using ArFleet-JS), get a link or ID, and share that with other users. Those users can fetch the content from ArFleet as long as it’s valid. This provides a decentralized alternative to using centralized caches or temporary IPFS nodes, with the assurance that the data is cryptographically verified and available for the set duration (or the provider gets penalized).

- **High-Frequency Data Feeds and Oracles:** Some blockchain oracle services produce frequent updates (prices, sensor data) that are only relevant for a short window. Rather than paying to store every tick permanently, an oracle network could use ArFleet to hold recent data points for quick access by dApps, while periodically checkpointing critical data to Arweave. For example, an IoT oracle might stream data into ArFleet (cheap short-term storage), and only write hourly summaries or important events to Arweave. This way, consumers (smart contracts or AO processes) can query the latest values from ArFleet quickly, and the network isn’t burdened with permanence for every minor update. Since ArFleet allows setting **redundancy** (storing N copies on different providers), an oracle could ensure high availability by placing, say, 3 replicas of the feed data across different providers closer to various regions. Compatibility with AO means these oracles (if running as AO actors) can directly interface with ArFleet’s actor processes to fetch or update ephemeral data as part of their operation.

- **Cross-Chain and Web2 Integration:** ArFleet’s design is blockchain-agnostic in terms of what data it can store – it can hold JSON, binaries, images, etc., up to potentially very large sizes (providers can set size limits, but multi-GB should be possible in theory via chunking). This makes it a candidate for any scenario where a dApp or even a Web2 service needs **temporary decentralized storage**. For example, a DAO might run a temporary file drop for proposals – members upload PDFs to ArFleet for a week-long review period, then they expire. Or a multi-chain dApp on Ethereum/Solana could use Arweave for permanent records (via AR.IO gateways) and ArFleet for transient records; since ArFleet runs on Arweave’s stack, any external system that can interact with Arweave (through HTTP APIs or SDKs like Arweave.js or AR.IO) can potentially also interact with ArFleet. In practice, a developer on another chain could call an ArFleet web service or have a small AO agent that bridges between Ethereum events and ArFleet storage. This is still experimental, but the **composability of AO** means an AO actor could listen for Ethereum state (via a relayer) and store something in ArFleet, acting as a trustless bridge.

- **Compatibility with AO Actors:** Since ArFleet itself is composed of AO actors (Marketplace, Deal processes), other AO programs can message them. A developer building an AO-based application (such as a game or a scheduling service) can incorporate ArFleet by spawning deals from within their actor or by querying the Marketplace actor for storage options. For instance, an **AO-based game** could generate a lot of game state that only needs to persist for the match duration – the game’s AO process could spin up ArFleet deals on the fly to store match logs or player data, then delete them when the match ends, keeping Arweave free of clutter. Because AO processes can call each other and even schedule future calls, a game process could schedule a call to an ArFleet deal actor to release reward payment at expiry or to extend the lease if a match goes into overtime, etc. This kind of automation and actor-to-actor communication is a powerful feature of building on AO.

**Supported Data Formats:** ArFleet handles data in a **format-agnostic** way. From a developer’s perspective, you can store **any binary or text data** – files (images, video, archives), JSON blobs, database snapshots, etc. The protocol will chunk and encrypt it uniformly. Internally, ArFleet’s storage format involves a multi-layered approach (Merkle trees, an ArFleet-specific reassembly manifest, RSA-encrypted chunks, etc.), but this is abstracted away. Essentially, the client splits the file into 8 KB **chunks** (by default) and builds a Merkle tree for those chunks. This allows verifiable partial retrievals and proofs. The data is also packaged into **ANS-104 “DataItems”** if needed (Arweave’s bundle format), to leverage existing Arweave tooling for things like hashing and signing. But as a developer, you don’t need to manually format data – you just provide the raw bytes or file, and ArFleet will do the rest.

One consideration is **encryption**: If you want the data to be private, you should encrypt it _before_ or during storage. ArFleet’s client by default encrypts chunks with a unique RSA key (to prevent a malicious provider from serving the same chunk to multiple deals without storing copies, i.e. anti-sybil). However, RSA here is used in a peculiar way (encrypting with private key, decrypt with public) to allow verification; it’s not meant to hide data from the provider (since the provider gets the public key to decrypt). For **privacy**, ArFleet suggests an additional AES-256 encryption of the file content by the client. The AES key is then shared only with authorized downloaders (similar to how one shares a content hash + decryption key in other decentralized storage). The Quick Guide explicitly notes that currently stored data is “available publicly” unless you encrypt it, so sensitive data should be user-encrypted. Future iterations might integrate access control or encryption by default \[TBD].

In summary, ArFleet can be thought of as a **decentralized “temp file” service** that slots neatly into dApps. It provides the performance benefits of off-chain storage (fast, no permanent commitment) while maintaining cryptographic security and decentralization via Arweave/AO. By using ArFleet alongside Arweave, developers can design systems where _permanent_ and _temporary_ data live side by side, each handled by the appropriate layer of the stack. This enables richer Web3 applications – from AI to gaming to social – that were previously difficult because everything had to be either on-chain forever or off-chain in centralized servers. With Arweave+AO+ArFleet, a dApp can truly keep **everything on-chain in some form** (compute, long-term storage, short-term storage) without sacrificing scalability or cost.

### 5. Incentives and Payment Logic

ArFleet’s economic model is designed to align with Arweave’s but for temporary services. Key points:

**Payment by Clients:** The client (data uploader) must **pay a reward** to incentivize providers. By default, this payment is made in **Arweave’s AR token**. ArFleet was explicitly launched to expand \$AR’s utility by enabling spend on temporary storage. For example, if permanent storage of 1 GB costs \~0.75 AR (as of 2024), a temporary 1-month storage via ArFleet might cost only a fraction of that, determined by market pricing from providers. Clients fund the deal’s escrow with the agreed amount at deal creation. If the provider successfully stores the data for the term, that escrowed AR is released to them as **reward**. If the provider fails, typically the remaining reward can be refunded (the protocol details on refund vs burn are being refined \[TBD]).

Notably, the ArFleet protocol is **token-agnostic** at the protocol layer – it supports any mutually agreed token for payments. In other words, a provider could accept payment in an AO-native token or even stablecoins, as long as both sides trust that token and the AO process can hold it. In practice, during testnet and early mainnet, AR has been the base currency (because \$AO wasn’t transferable yet and AR is the common token both know). However, with AO mainnet live, the **\$AO token** (native to the AO compute network) can be used as well. ArFleet is part of the AO ecosystem, so it’s expected that \$AO will become a primary token for compute and possibly for ArFleet fees as well. Indeed, documentation suggests in the long term ArFleet deals could be funded in “any AO token”. As of mid-2025, AR and wAR (wrapped AR on AO) remain common for payments, but \$AO integration is happening as the token is now transferable and exchanges exist. There is **no separate ArFleet-specific token** – ArFleet doesn’t have a governance or utility token of its own (and none is announced, so any such plan is \[TBD]). The design instead leverages Arweave’s currency and AO’s token for economics, keeping it simple and aligned with the underlying platforms.

**Collateral by Providers:** Providers are required to put down a **collateral stake** for each deal. This is usually also in AR or an agreed token. Collateral exists to disincentivize cheating: if the provider fails to prove storage, they lose a portion or all of their stake. The amount of collateral is likely proportional to the deal value or data size (for example, a provider might stake an amount equal to or greater than the reward, or some AR per GB per time unit – specifics are adjustable in protocol \[TBD]). This way, the client is economically “covered” – the provider stands to lose more by cheating than they gain. Both the reward and collateral are escrowed in the AO deal contract, ensuring no party can unilaterally abscond with the funds once the deal starts.

**Pricing Mechanism:** Pricing for storage is essentially **market-driven**. Providers advertise a price per GB per unit time in their announcements. Clients will choose providers that meet their budget. In testnet, pricing was experimental (some early providers may have offered very cheap rates to attract usage). Over time, as more providers join, we expect a marketplace dynamic similar to Filecoin or a decentralized Amazon S3: providers compete on price, reliability, and performance. Because ArFleet storage is not permanent, costs should be much lower than permanent storage – users pay **only for the time used**. If a user only needs 1 GB for a week, they pay for that week, whereas on Arweave they’d have to pay once for forever. This introduces a recurring expense (like “rent”), but significantly reduced for short durations. Payment can be structured in various ways:

- **User-pays model:** The end-user of a dApp directly pays AR/AO for the ArFleet storage their actions consume. For example, if a user uploads a 100 MB file for 1 day via a dApp, the dApp could prompt them to pay, say, 0.01 AR, which goes into the deal contract as reward.
- **Developer-subsidized:** The dApp developer might choose to cover the ArFleet costs to improve UX (similar to how some DApps cover gas with meta-transactions). In this case, the dApp’s backend would use its own AR/AO funds to pay for the deals. The advantage of ArFleet is that these costs are predictable and granular (short-term storage is cheap), so a dev could decide to subsidize, for instance, up to 1MB of ephemeral data per user for free, and only charge if usage exceeds that.
- **Hybrid models:** A dApp could implement a freemium approach – small ephemeral storage uses are free (developer-paid), but larger or longer-term uses require the user to pay (either in AR, AO, or perhaps the dApp’s own token which the backend converts to AR). Because ArFleet deals can technically use any token, there’s a possibility a dApp could abstract the payment in their own token or stablecoin: the dApp would convert behind the scenes or the provider could accept that token. However, this would need coordination and isn’t default – most likely the dApp would just handle conversion and still pay AR to ArFleet under the hood.

**Billing Integration:** For developers, integrating billing involves ensuring the ArFleet client has access to a funding wallet. In ArFleet-JS, by default it generates a wallet (in `~/.arfleet-client/wallet.json`) which you can top-up with AR. You can also replace it with your own Arweave keyfile to use a specific address (like a corporate wallet). When a `store` command is issued, the client will automatically attempt the on-chain funding transaction from that wallet. Thus, a backend service would need to monitor its AR/AO balance and possibly request more funds when low. If a user is paying, the dApp might simply redirect them to sign an Arweave payment to the deal contract (though the current implementation handles it automatically via the client, so likely the user would send AR to the client’s address which then funds the deal – this detail is abstracted).

One must also consider **wAR vs AR vs AO** on testnet vs mainnet. On AO testnet, a wrapped AR token (wAR) was used within the AO environment (since AO is its own chain, AR had to be represented there). On AO mainnet, similarly, AR can be moved into AO’s chain (via a bridge) or one can use AO tokens. The **AO token (\$AO)**, which launched Feb 2025, is now liquid. It’s anticipated that ArFleet deals on mainnet might often use \$AO for convenience (especially for transactions happening entirely within AO’s environment). However, because Arweave’s storage endowment and economics are tied to AR, many providers might still prefer AR. _As of now, assume AR is the default payment on ArFleet, with AO token support emerging._ If ArFleet adds support for other tokens, a dApp could even let users pay in, say, USDC (if providers agree) – but this would likely require an AO bridged version of USDC and is not standard yet.

**Native Token Consideration:** **Does ArFleet have its own token?** – No, **ArFleet does not have a native token** as of 2025. All economic activity is using existing tokens (AR, AO, etc.). There has been no announcement of any ArFleet-specific ERC-20 or similar. The incentive alignment is achieved without a new token: AR’s utility is expanded for temporary storage, and AO’s token can also be utilized. If in future ArFleet introduced some reward token or DAO token, that would be a new development (currently **\[TBD]** and unlikely in the near term).

In summary, ArFleet’s payment logic mirrors a **pay-per-use storage rental**. Developers need to manage AR/AO funds for storage operations. Providers earn those funds as revenue for their service, but risk losing collateral if they don’t perform. This dynamic should lead to a **market equilibrium** where the price of temporary decentralized storage reflects actual supply/demand (e.g., if many providers join, prices drop, benefiting users). For Web3 apps, this means budgeting for storage not just in one-off costs (like permanent storage) but as operational costs over time – though significantly smaller per unit of data. One can also envision **subscription models** built on ArFleet: e.g., a dApp could charge its users a monthly fee in fiat or any token and internally allocate some AR to ArFleet storage for that user’s needs. Since ArFleet deals can be short and renewed, it’s feasible to implement rolling storage contracts that map to Web2-like subscriptions.

### 6. Roadmap & Known Limitations

**Roadmap (Short/Mid Term):** ArFleet is in active development in 2024-2025. After the initial testnet success, the primary short-term goal is achieving a **stable mainnet release** on top of the AO mainnet. The AO mainnet launched in Feb 2025, so ArFleet’s focus is to **deploy its contracts and infrastructure onto mainnet** and remove the Genesis Pass gating to open usage to all developers. We anticipate that in the _short term (H2 2025)_:

- ArFleet will roll out an updated Web App (beyond v0.1.x) available to all Arweave wallet users (not just pass holders). In fact, the weekly update in Sep 2024 already hinted at a web version being live for testers, so a polished public web interface is likely upcoming.
- **Integration with \$AO token** will be finalized, meaning deals can be funded directly with AO and providers stake/earn AO if they choose. Since AO token became transferable in Feb 2025, this likely happens around that time. This will coincide with broader AO ecosystem growth, making AO the default gas for compute and possibly storage.
- More **provider nodes** joining: Initially, only AO/ACC or community testers were running providers. The roadmap likely includes community onboarding, documentation and maybe incentives (maybe via AO or Arweave grants) to encourage individuals or businesses to run ArFleet provider nodes globally. The more providers, the better the network’s capacity and redundancy.
- **Performance improvements:** v0.1.2 already improved upload/encryption speeds and added retry logic on testnet. We expect continued optimization of the client (especially the JS client) for faster chunking, parallel transfers, and support for very large files. The Erlang version will also be refined for throughput.
- **Ease of use features:** e.g., automated deal renewal (if a user wants to extend storage before it expires), better error handling when a provider is unresponsive (maybe auto-failover to a new provider if one fails during setup), and integration with Arweave’s gateway for discovery (maybe listing active deals by content hash, etc. – some of these are speculative \[TBD]).

Mid-term (next 6-12 months), ArFleet might explore:

- **Longer max durations:** Initially, providers might impose relatively short max storage terms (perhaps days or weeks) to limit liability. As the system proves stable, we could see support for multi-month or year-long temporary storage deals. This would still be “temporary” compared to Arweave (which is eternal), but offers a spectrum. For example, a provider might start accepting 6-month deals if demand exists.
- **Decentralized discovery improvements:** Right now, clients rely on the Marketplace actor and then direct contact. The roadmap might include more robust **indexing** of which provider holds which data (maybe a DHT or on-chain index), so that if a client only has a TXID, it can find the provider after the fact. Currently, that might require out-of-band knowledge (the client that uploaded knows the provider’s address). A more decentralized lookup service would improve retrieval, especially if the original client is offline.
- **Interoperability with AR.IO gateways:** Perhaps ArFleet data could be accessed through Arweave gateways if they integrate a feature to proxy ArFleet content. Since AR.IO (the gateway network) is a sister project, it’s possible in the future you might do something like `https://arfleet.arweave.net/<TXID>` to retrieve a file (the gateway could talk to ArFleet providers behind the scenes). This is speculative but would make ArFleet more accessible to regular web apps \[TBD].
- **Security audits and hardening:** Before full production, the smart contracts (AO actors) for ArFleet deals will undergo audits. The verification game will be analyzed for any potential weaknesses (e.g., ensuring the random challenge cannot be predicted, checking if the RSA+Merkle scheme is solid against adversaries, etc.). Any findings will be addressed to ensure the mainnet launch is secure.
- **Community governance or DAO:** Since ArFleet is part of Arweave/AO, any parameter changes (like default challenge frequency, etc.) could be coordinated via community input. There’s no separate ArFleet DAO yet, but the Arweave community and perhaps \$AO holders might govern aspects of it. This is an open area \[To Be Confirmed].

**Current Limitations:**

- **Testnet/Alpha Constraints:** Until full launch, usage is restricted. The Genesis Pass requirement meant only a small set of testers could use ArFleet through 2024. This limits real-world testing to those users. It’s a temporary measure – once lifted, any dApp can integrate freely.
- **Reliance on AO Maturity:** ArFleet inherits the limitations of the AO platform. AO itself is new, so issues like network bugs, documentation gaps, or scaling limits of AO will affect ArFleet. For instance, in testnet, AO handled 130k parallel processes and millions of messages – impressive, but we need to see how it behaves under even larger load on mainnet. If AO had any instability, ArFleet deals could be impacted (e.g., delays in challenge scheduling).
- **Storage Duration & Size Limits:** Presently, providers set limits on how long they’ll store data and how much they can store. In early implementations, **max TTL might be relatively short** (maybe on the order of weeks) until the economic models prove out. Similarly, a provider might only offer, say, 100 GB of space. So a single deal might be capped (if you try to store more, you’d need to split across multiple deals). The web client had an explicit limitation due to browser – not suitable for terabyte-scale uploads. The JS client can handle bigger files, but ultimately bound by provider capacity. Also, the current chunking scheme uses 8KB chunks and creates potentially large manifests for huge files – storing multi-GB in one deal could produce very large Merkle trees (which have to be stored in the AO process state). There may be **practical upper limits** on single-deal size (possibly on the order of a few GB) \[TBD]. For extremely large data, one might chunk it into multiple separate deals or wait for protocol optimizations.
- **Redundancy and Self-Healing:** While ArFleet allows specifying redundancy (N copies), it currently does not automatically **re-replicate** data if a provider fails mid-term. If you asked for 3 copies and one provider goes down permanently (and loses collateral), you’re left with 2 copies; the system doesn’t yet spin up a new third copy automatically. The client or user would have to notice and manually create a new placement with another provider (assuming they still have the data or one of the other providers can share it – which gets complicated). A future improvement could be automated re-balancing: the deal actor could detect a provider failure and allow another to step in, but this is complex and not in v1. So currently, **provider failure may lead to data loss if not enough redundancy**. Developers should plan for an appropriate redundancy factor and possibly monitor their deals.
- **No Fine-Grained Access Control:** Data on ArFleet is essentially public to anyone who knows the content ID, unless encrypted by the user. There’s no built-in mechanism like access control lists or requiring wallets to have permissions. This means any sensitive data **must be encrypted client-side** (which ArFleet facilitates by providing the hooks to encrypt/decrypt, but it’s on the developer to use them). This is similar to Arweave (all data is public, you rely on encryption for privacy). There is mention of “private sharing” via sharing keys out-of-band. In the future, perhaps ArFleet could integrate with decentralized identity or capability systems to share data without sharing keys (like proxy re-encryption, etc.), but nothing like that is implemented yet.
- **UI/UX and Tooling Gaps:** As a new technology, some developer tooling is still **rough**. The ArFleet documentation is in progress (some sections marked draft or “coming soon”). Error messages from the CLI can be cryptic, and setting up the environment (especially the need for a Genesis Pass on testnet) is non-trivial. Over time, expect more polished SDKs, maybe a one-click deploy for providers, and clearer guides. But early adopters should be prepared for a bit of tinkering. Community channels (Discord, forums) are the best support right now.
- **Token Conversion Overhead:** Using AR on AO requires wrapping it (since AO is a separate chain). This introduces some UX complexity – users may need to bridge AR into AO to load their ArFleet wallet. The project has worked around this by the concept of wAR and making the Web UI handle the conversion, but it’s still a hurdle for newcomers. As AO and Arweave ecosystems merge more tightly, this will improve (for example, ArConnect wallet might streamline AO integration).
- **Concurrent Deal Limits:** The AO testnet statistics show a high capacity, but on the application level, there might be limits like “how many deals can one client have open” or “how many active deals can a single provider handle simultaneously”. These are not clearly documented yet and likely being tested. A provider might restrict how many new deals it accepts at once to avoid being overwhelmed. So a dApp doing a batch of thousands of file uploads might need to throttle or spread across providers. These limits will become clearer with time; right now, just be aware that the network is not infinite and you should handle failures or rejections gracefully.

**Future Prospects:** In the longer term, ArFleet could evolve with features such as **secondary markets for storage** (think sub-leasing data or transferring an ongoing deal to a new provider), **layer-2 solutions** on top of ArFleet (someone might build a caching layer that automatically uses ArFleet under the hood for dApps), or deeper integration with Arweave’s query/indexing services so that even temporary data can be indexed (perhaps a unified API where a query can fetch from Arweave or ArFleet depending on the age of data). These are speculative, but show how ArFleet opens the door to a more dynamic data economy on the permaweb.

In conclusion, ArFleet is a significant innovation for Web3 developers: it **fills the gap** between permanent storage and real-time needs. While still young and with some limitations, it is rapidly maturing alongside the AO platform. By carefully considering the current constraints (TTL, provider trust, encryption needs) and following the project’s updates, developers can start integrating ArFleet into dApps to achieve use-cases that were impractical before. The roadmap is promising – as of July 2025, the pieces (AO mainnet, AR.IO gateways, ArFleet beta) are falling into place to make the **Fully Decentralized Stack** a reality, where any application’s compute and data (both long-term and short-term) live on a unified decentralized network.

**Sources:**

- ArFleet Docs – _What is ArFleet?_ and comparison with Arweave
- Community Labs Blog – _Quick Guide to ArFleet_ (Sept 2024)
- ao/acc Labs – Project description
- PermaDAO Medium – _ArFleet Launches as Arweave’s New Temporary Storage_ (Aug 2024)
- Arweave/AO Weekly (Sep 17, 2024) – ArFleet Web v0.1.2 launch
- ArFleet Docs – _ArFleet Protocol_ (overview of parties, enforcement)
- ArFleet Docs – _Lifecycle of a Deal_ (detailed flow)
- ArFleet Docs – _Verification Challenges_
- AR.IO Article – AO’s actor model and logging on Arweave
- ArFleet GitHub (JS) – README and usage guide
- ArFleet Docs – _Getting Started_ (Web vs JS vs Erlang)
- ArFleet Docs – _Genesis Pass_ (testnet access NFT)
- Permaweb Journal – _How Arweave scales (for AO)_ (Mar 2025) (mentions ArFleet and AO integration)
- Medium (Content Guild) – Weekly highlights (FDS stack: AO+Arweave+ArFleet)
- Arrington Capital Blog – _AO Launch Imminent_ (Jan 2025) (context on AO and agents)
- ArFleet Docs – _Data Formats_ (chunking details)
- ChainCatcher/Followin news – AO mainnet launch Feb 8, 2025 (AO token launch context)
