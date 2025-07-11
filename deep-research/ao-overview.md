---
title: AO Overview for Developer
platform: ChatGPT DeepResearch (GPT-4o)
date: 2025-07-11
url: https://chatgpt.com/share/6870d439-e250-8000-925a-1d45e5ff3619
tags: [ao, developer]
---

[Prompt]

```markdown
Please conduct a technical investigation into Arweave’s AO (Actor Oriented Protocol) from the perspective of Web3 developers.

## Focus Areas

- What is AO? Core design principles, execution model, and how it differs from SmartWeave.
- Core components: Executors, Actors, Messages, Modules, and Blueprints — their roles and interactions.
- Development background: Philosophy, key contributors (e.g. Sam Williams), and affiliated organizations (Forward Research, Community Labs, ao/acc).
- Release history and milestones: Alpha, beta, and mainnet phases, plus notable updates.

## Restrictions

- Only include English-language sources published after February 2024.
- Exclude general Arweave/SmartWeave content unless directly relevant.

## Output Format

- Markdown
- Clear headings, bullet points

## Prioritized Sources

### Core Docs

- [AO Website](https://ao.arweave.dev/)
- [AO Whitepaper](https://5z7leszqicjtb6bjtij34ipnwjcwk3owtp7szjirboxmwudpd2tq.arweave.net/7n6ySzBAkzD4KZoTviHtskVlbdab_yylEQuuy1BvHqc)
- [AO Cookbook](https://cookbook_ao.g8way.io/)
- [AO CLI Docs](https://github.com/permaweb/ao/blob/main/dev-cli/README.md)
- [ao Connect SDK](https://github.com/permaweb/ao/tree/main/connect)

### Key GitHub Repositories

- [ao-labs/ao](https://github.com/ao-labs/ao)
- [HyperBEAM](https://github.com/permaweb/HyperBEAM)
- [aos](https://github.com/permaweb/aos)
- [aoacc](https://github.com/aoacc)

### Explorer & Testing Tools

- [AO Link](https://www.ao.link/)

### Developer Insights & Blogs

- [Community Labs Blog](https://www.communitylabs.com/blog)
- [AO Ventures Blog](https://www.aoventures.io/blog)
- [Permaweb Journal](https://permaweb-journal.arweave.net/index.html)

### Twitter (X) — Core Accounts

- [@aoTheComputer](https://x.com/aoTheComputer)
- [@samecwilliams](https://x.com/samecwilliams)
- [@CommunityLabs](https://x.com/CommunityLabs)
- [@fwdresearch](https://x.com/fwdresearch)
- [@TateBerenbaum](https://x.com/TateBerenbaum)
- [@ao_builders](https://x.com/ao_builders)
- [@aoComputerClub](https://x.com/aoComputerClub)

### Supplemental Developer Resources

#### Additional GitHub Repositories

- [create-ao-dapp](https://github.com/Autonomous-Finance/ao-starter-kit)
- [create-ao-contract](https://github.com/pawanpaudel93/create-ao-contract)
- [ao-deploy](https://github.com/pawanpaudel93/ao-deploy)
- [teal-ao-starter](https://github.com/Autonomous-Finance/teal-ao-starter)
- [aos-sqlite](https://github.com/permaweb/aos-sqlite)
- [AO module loader](https://github.com/permaweb/ao/blob/main/loader/README.md)
- [AO servers](https://github.com/permaweb/ao/tree/main/servers)
- [Token blueprint (Lua)](https://github.com/permaweb/aos/blob/main/blueprints/token.lua)
- [BetterIDEa](https://ide.betteridea.dev/) — Web IDE with AO integrations
- [WAO](https://github.com/weavedb/wao) — In-memory AO testing framework

#### Secondary Twitter (X) Accounts

- [@arweaveindia](https://x.com/arweaveindia)
- [@arweaveny](https://x.com/arweaveny)
- [@apus_network](https://x.com/apus_network)
- [@arweaveny](https://x.com/arweaveny)
- [@vela_ventures](https://x.com/vela_ventures)
- [@beaconwallet](https://x.com/beaconwallet)
- [@AstroUSD](https://x.com/AstroUSD)
- [@perma_dao](https://x.com/perma_dao)
- [@Arc_AO](https://x.com/Arc_AO)

#### Projects on AO

- [0rbit](https://docs.0rbit.co/)
- [Wander (ex-ArConnect)](https://docs.arconnect.io/)
- [Botega](https://botega.arweave.dev/)
- [Permaswap](https://github.com/permadao/permaswap)
- [AOX](https://aox.xyz/#/)
- [Bazar](https://bazar.arweave.net/)
- [Astro](https://docs.astrousd.com/)
```

---

# Output

Great. I’ll investigate Arweave’s AO protocol (Actor Oriented Protocol) with a technical focus tailored for Web3 developers.

The report will include:

- AO’s core design principles, execution model, and how it diverges from SmartWeave
- Deep dive into AO components: Executors, Actors, Messages, Modules, Blueprints
- Development background including key figures (e.g. Sam Williams), and affiliated organizations (Forward Research, Community Labs, ao/acc)
- Detailed release history: alpha, beta, mainnet phases, and important updates
- Practical insights and recommendations for Web3 developers on how to integrate or build on AO

I’ll prioritize English-language sources published after February 2024, referencing official documentation, GitHub, blogs, and key community channels. I’ll share the findings with you in a markdown-formatted document.

# Arweave AO (Actor-Oriented Protocol) – Technical Overview

## What is AO and How Does It Differ from SmartWeave?

**Arweave AO (Actor-Oriented)** is a decentralized, _hyper-parallel_ computing protocol built atop Arweave’s permanent storage network. It aims to function as a “global supercomputer” without practical scale limits. Unlike Arweave’s earlier smart contract system (SmartWeave), which relied on sequential on-chain interactions and client-side computation, AO introduces an **actor model** execution paradigm:

- **Actor-Oriented Design:** Each contract is an independent _process (actor)_ with its own private state and mailbox (inbox). Actors do **not share global state**; all inter-contract communication happens via asynchronous message passing. This abandons SmartWeave’s “interaction” model in favor of _message logs_ that can originate from users or other processes.
- **Parallel & Unbounded Execution:** Because actors run independently and communicate only through messages, AO can execute **many contracts in parallel** without the bottlenecks of a single global state machine. (By contrast, in Ethereum’s VM every node repeats all computations, acting like a “world calculator” rather than a truly parallel computer.) AO contracts can spawn new actors and distribute workloads, achieving massive concurrency.
- **No Global Memory Space:** AO avoids a global shared memory; this improves scalability and avoids contention. All contract state changes are driven by message inputs and logged on Arweave for consensus and permanence. The network reaches agreement on the ordering and availability of messages (using Arweave’s data consensus) rather than every node recomputing every state transition. This lazy evaluation model means nodes don’t need to perform all computations to agree on state transitions (similar in spirit to SmartWeave’s approach, but greatly extended).
- **Integration with Arweave Storage:** AO leverages Arweave as a **single source of truth** for data and message logs. All process inputs/outputs (messages) are persisted on Arweave’s permaweb, ensuring verifiable and tamper-proof history. Arweave acts as “hard drive” for AO, providing permanent data storage that AO processes can read and write to without trust.

**In summary**, AO transforms Arweave from a passive storage network into an **active compute platform**. It builds on SmartWeave’s idea of off-chain computation but introduces autonomous, concurrent processes that can cooperatively compute on on-chain data via message passing. This opens the door to running complex workloads (like AI model inference, big-data processing, etc.) on a decentralized network, something impractical with SmartWeave’s sequential model or typical blockchain VMs.

## Core Components: Executors, Actors, Messages, Modules, Blueprints

- **Actors (Processes):** In AO, an _actor_ is the fundamental unit of computation – essentially a smart contract or program running as an independent process. Each actor maintains its own state (not shared with others) and a mailbox (inbox) for incoming messages. Actors can perform local computation, send messages to other actors, and spawn new actors. This model (inspired by the classic Actor Model in CS) provides inherent concurrency and fault isolation: no shared memory means no locks or race conditions, and communication is purely via messages.

- **Messages:** Messages are the **asynchronous communication mechanism** in AO. A message is a data packet (with an optional payload and tags for context) that one actor sends to another. Messages are the only way to invoke behavior or transfer data between actors – an actor cannot directly read or write another’s state. All messages conform to a standard format (ANS-104 Arweave tags) and are permanently stored on Arweave (the “message log”) via the Scheduler, so every interaction is timestamped and immutable. The message-passing design enables **loose coupling** between processes and high throughput: many messages can be in flight concurrently. For example, if a computation is too large, one actor can split the work by sending subtasks as messages to multiple worker actors, then aggregate results – this _parallelizes_ work which, on a single-threaded blockchain VM, would be sequential.

- **Executors / Compute Units:** “Executors” refer to the nodes and components that actually **run actor code** and update state in AO. In the AO architecture, specialized nodes called **Compute Units (CU)** fulfill this role. Compute Units retrieve ordered messages from Arweave, execute the target actor’s code (using the appropriate VM), and produce an updated state and any output messages. They are essentially the “workers” that perform computations on behalf of the network, akin to decentralized CPU nodes. Because AO decouples computation from consensus, not every network node runs every contract. Instead, **executor nodes opt in to run processes**, and their results can be verified via cryptographic proofs and economic incentives (staking) rather than by redundant re-execution on all nodes. Notably, AO’s reference executor is **HyperBEAM**, a high-performance node software (written in Erlang) that runs AO processes and validates results in the AO-Core network. Compute Units provide _verifiable computation_: they attach attestations (proofs of execution) so that other nodes can trust the results without re-running everything.

- **Messenger and Scheduler Units:** Alongside the executors, AO’s network is composed of other **specialized units** that handle message routing and ordering:

  - **Messenger Units (MU)** are responsible for receiving incoming messages (from users or other actors), validating them (e.g. checking signatures), and routing them to the appropriate destination process. MUs act like the “network interface” – ensuring messages are delivered to the network correctly.
  - **Scheduler Units (SU)** sequence messages and anchor them on Arweave’s blockweave. The SU assigns each message a timestamp/order and writes it to Arweave as a transaction (the message log). This provides a canonical order of execution while leveraging Arweave’s consensus on data permanence. In effect, the Scheduler is like a _mempool and block producer_ for AO messages: it batches and commits messages so that all Compute Units agree on the execution sequence. By recording messages on-chain, AO achieves eventual consistency and verifiability of process state without a monolithic global VM.

- **Modules (Virtual Machines & Libraries):** AO is designed to be **modular and polyglot**. Instead of prescribing one programming language or VM, AO allows multiple execution environments (“modules”) to plug into the system. The common target is WebAssembly (Wasm): AO processes are compiled to Wasm modules, which the Compute Unit executes. Wasm provides a secure, sandboxed runtime with near-native speed and support for many languages (Rust, C/C++, Go, JavaScript, etc.). The first implementation (AOS) uses **Lua** – smart contracts are written in Lua, then compiled to Wasm for execution. Developers aren’t limited to Lua; AO’s _meta-VM_ design lets alternative VMs run as long as they conform to AO’s state and message interface. For example, a JavaScript VM or a Python runtime could be introduced as modules running within AO-Core. In addition to execution VMs, AO provides standard library modules to processes: e.g., JSON parsing, cryptography, base64, and other utility libraries are available for use in contracts (these are accessible via the `aos` environment). This modular approach gives developers flexibility in language choice and extends AO’s capabilities by simply adding new module support, all while maintaining a unified message format and state model across the network.

- **Blueprints:** Blueprints are developer-friendly **code templates** for common AO contract patterns. Essentially, a blueprint is a pre-built set of actor handlers and state structure that implements a typical use-case, which a developer can quickly instantiate and customize. For example, the **Token Blueprint** provides all the logic for a fungible token contract (minting, transfers, balances) so you can launch a token on AO with minimal effort. Other blueprints exist for things like chatrooms, voting systems, staking, etc., serving as starting points or reference implementations. Using a blueprint is as simple as loading it into your AO process (via the CLI command like `.load-blueprint token`) – this injects the pre-defined handlers into your actor, which you can then tweak or extend. Blueprints lower the barrier to entry for developers, allowing them to **bootstrap standard dApps quickly** before diving into custom logic. They also promote best practices by providing audited, community-vetted code for common patterns. (For instance, Community Labs has published blueprints for tokens, voting, and more in the AO Cookbook.) In summary, a blueprint is a **“smart contract template”** – a convenient shortcut to spin up typical contracts in the AO environment.

## Development Background and Key Contributors

**Origins and Philosophy:** Arweave’s journey toward AO began in 2020. During the COVID lockdown, Sam Williams (Arweave’s founder) and his team envisioned a “neutral decentralized computing log” – a system that could deduce any program’s state from an append-only log of inputs. This led to the creation of **SmartWeave** (mid-2020) as a proof-of-concept: SmartWeave showed that you could have on-chain contracts on Arweave by storing interactions and computing state on demand in a trustless way. SmartWeave’s success proved the concept of storage-based consensus for computation, but it had limitations in speed and interactivity. The AO project emerged to **generalize and massively scale** that concept. A community developer, _Outprog_ (founder of EverVision Labs), proposed the **Storage Consensus Paradigm (SCP)** – an idea to treat _all_ kinds of data logs on Arweave as consensus material, not just contract interactions. Outprog’s writings on SCP in 2021 laid theoretical groundwork for AO. Meanwhile, Sam Williams and a small team (which would become Forward Research) began formal development of AO (then sometimes called “Arweave OS”) in 2021. By late 2022 they had a breakthrough: the actor-oriented architecture with message passing was proven to be horizontally scalable in theory. They realized that trying to bolt this onto the existing SmartWeave/Warp framework was impractical – a clean-slate architecture was needed. This culminated in building **AOS (Arweave Operating System)**, the first implementation of AO’s compute network, using Lua and Wasm.

**Key Contributors:**

- **Sam Williams** – Arweave’s founder and CEO of **Forward Research**. Sam is the visionary behind AO and has been actively leading its design and development. Forward Research (founded 2022, after an Arweave event in Asia) is an R\&D incubator focused on Arweave and AO projects. Under Sam’s leadership, Forward Research developed the AO-core protocol and reference implementations (AOS, and later HyperBEAM). Sam authored the AO whitepaper and often describes AO as fulfilling the original “world computer” vision that earlier blockchains aspired to.
- **Outprog (Kyohei Ito)** – Founder of EverVision (creators of everPay and Permaswap) and an early thought leader for AO. He contributed the idea of using Arweave’s storage layer as the base for a decentralized compute paradigm (SCP) and collaborated with Sam on early designs. EverVision also bootstrapped **PermaDAO**, a community organization that helped evangelize AO in its early days. Outprog’s involvement ensured AO’s design would suit real-world dApps (everPay is integrating AO’s message standard to achieve full decentralization of its cross-chain payments).
- **Forward Research Team:** Aside from Sam, the AO whitepaper lists Ivan Morozov (Autonomous Finance), Tom Wilson & Tyler Hall (of Hyper.io), Vincent Juliano, Alberto Navarro, etc. – a mix of Arweave core developers and external collaborators. This team built the core protocol and initial tooling. Notably, **Tom Wilson** and team developed **HyperBEAM**, the Erlang-based AO node software, and worked on the **Scheduler (SuperSU)** component. **Ivan Morozov** contributed to bridging AO with existing smart contract platforms, ensuring modularity.
- **Community Labs:** A Web3 development studio that became a major contributor to the Arweave/AO ecosystem. Community Labs (founded by Tate Berenbaum) focuses on onboarding developers to Arweave. They created tools like the ArConnect (now **Wander**) wallet and **Astro** (a stablecoin protocol), and they have been early adopters of AO for building decentralized apps. In April 2024, Community Labs launched **“ao Ventures”**, an incubator program to foster AO-based projects. They also produce educational content (guides, blog posts, bootcamps) to teach developers AO – for example, the _AO Bootcamp_ series and cookbook references. Community Labs’ involvement helps drive grassroots adoption of AO by funding hackathons and supporting new builders.
- **ao/acc Labs:** This is a community-driven initiative (often called the **AO Compute Club** or AO Labs) that emerged in 2024 to build open-source dApps on AO. The ao/acc Labs group leverages Arweave’s storage + AO’s compute to demonstrate what the “dynamic permaweb” can do. One of its flagship projects is **ArFleet** (an Arweave-based content hosting and social platform on AO). With an ethos of open collaboration, ao/acc Labs exemplifies the growing developer community around AO. (The group’s Twitter @aoaccorg announced the AO mainnet and showcases community-built experiments.)

**Development Milestones:** AO’s development progressed from concept to testnet rapidly:

- After internal prototyping, the **first public testnet (Alpha)** of AO – nicknamed **Legacynet** – launched at the end of February 2024. The announcement on Feb 27, 2024 was met with huge interest: within \~3.5 weeks, **over 3,000 developers** had spun up AO processes, and the ecosystem saw an explosion of AO-based experiments. (This coincided with a surge in Arweave’s AR token price, reflecting market excitement.) The Legacynet phase provided free compute resources (courtesy of Forward Research and others) and allowed the team to gather feedback on AO’s performance and developer experience.
- In March–April 2024, several key events took place: the **AO Cookbook** (technical docs and tutorials) was released, a testnet token called **\$CRED** was introduced to reward early participants, and community hackathons/kickoffs were organized. Early dApps such as 0rbit (an oracle service on AO) and a flurry of AO “memecoins” and games popped up, showing the versatility of the platform.
- Over mid to late 2024, AO development entered a **beta phase** focusing on scalability and hardening. The core team rolled out **AO-Core v1.0** (the production-ready protocol) on testnet and introduced **HyperBEAM (beta)** as the next-generation execution engine. HyperBEAM, written in Erlang for high concurrency, greatly improved throughput and reliability for AO processes. The network architecture evolved into three dedicated subnets (MU, SU, CU) with plans for an **operator staking system** to economically secure each role. In other words, by late 2024 the pieces were in place for a fully decentralized launch: the protocol spec was finalized, and attention turned to security audits and incentive alignment (e.g. slashing conditions for bad actors, “watchmen” nodes to monitor execution correctness).
- **Mainnet Launch (planned for Feb 2025):** The AO team targeted **February 2025** for the official mainnet release of AO. This corresponds to deploying AO-Core + HyperBEAM in a live, incentivized network where third-party nodes can participate freely and the AO token becomes transferable. To bootstrap adoption, AO has its own native token with a fixed supply of 21 million (inspired by Bitcoin’s scarcity). Starting from the testnet launch (Feb 2024), AO tokens have been continuously **emitted to AR holders** as a reward for supporting the network. Specifically, 33% of AO issuance goes to AR holders (distributed per block in a gradually halving schedule), and the remaining \~66% to aoETH holders (a wrapped staking token). By mainnet, about 2.1 million AO will be in existence, and those accrued tokens held by users become liquid. After mainnet, AR holders will continue to receive a portion of AO emissions until the cap is reached. This mechanism has been running throughout the test phase to decentralize token ownership.

In the lead-up to mainnet, the team has dubbed the test network as **“Legacynet”** and the new protocol as **“AO-Core mainnet”**. The difference is dramatic: Legacynet (Alpha) relied on centralized free nodes and had known limitations in speed, whereas AO-Core (powered by HyperBEAM) brings a **modular, high-performance compute layer** ready for production use. By mainnet, AO will support a **staking and slashing** model to ensure that messenger, scheduler, and executor nodes behave honestly (malicious or faulty nodes will lose stake), thereby securing the network economically in addition to Arweave’s data consensus.

## Current Status and Future Outlook

As of early 2025, AO is on the cusp of mainnet launch. The testnet has proven the concept with millions of messages processed and hundreds of parallel processes running (even complex AI demos) in a trust-minimized way. Developers can already experiment by deploying processes on the AO testnet using the AOS CLI or web IDEs like BetterIDEa. Key tooling – such as **AO Connect** (JavaScript SDK for dApp integration) and **WAO** (an in-memory AO testing framework) – is maturing, making it easier to build and test AO contracts off-chain. The ecosystem is rapidly expanding: projects like **everPay 2.0**, **Permaswap DEX**, **0rbit oracle**, **Astro USD** stablecoin, and **Wander** (wallet) are either integrating AO or building natively on it, showcasing use cases from DeFi to gaming to social media.

**AO’s launch marks a milestone for Web3:** it attempts to deliver a _“world computer”_ that truly scales, by separating storage (Arweave) from computation (AO) and innovating on the actor model for smart contracts. For Web3 developers, AO offers the ability to write decentralized applications that require **significant computation or real-time interactivity** – things not feasible on traditional L1 blockchains. For example, one can deploy autonomous agents, cloud-like web services, or AI models on AO that interact with users and other agents continuously, all while results are verifiable on-chain. The core principles of AO (massive parallelism, modular VM support, and permanent storage integration) position it as a powerful platform for the next generation of dApps, especially at the intersection of blockchain and AI.

As Sam Williams and others have noted, while Ethereum made decentralized finance possible, AO opens the door to **decentralized cloud computing**. This means developers could run anything from machine learning workloads to large-scale simulations on a trustless network and have outcomes immutably recorded. The coming months will focus on hardening the network (security audits and gradual decentralization of the MU/SU/CU subnets), onboarding node operators (incentivized by AO rewards), and migrating early adopter projects from testnet to mainnet. If successful, Arweave’s AO could transform the permaweb from a _library of permanent data_ into a **living, autonomous cloud** – fulfilling the vision of a unified, decentralized computer for Web3. 🚀

**Sources:**

- Arweave AO Whitepaper (June 2024) – _“The AO Protocol: A Decentralized Open-Access Supercomputer”_
- AO Cookbook – _“AO Specs and Architecture”_ (actor model overview, message passing); _Bootcamp 4: AO Fundamentals_ (actor model, units, tokenomics)
- _Permaweb Journal – “AO 101: Intro to the Hyper Parallel Computer”_ (Core components and mainnet vs. legacynet)
- _Medium (PermaDAO) – “The Future of AO” interview_ (Sam Williams & Outprog discuss AO history and design philosophy)
- _PANews – “AO is about to be released: Can Arweave regain momentum?”_ (AO testnet, mainnet timeline, and token distribution)
- _Gate.io Research – “Arweave AO Hyper-Parallel Computing – One Month After Launch”_ (Early network stats, dev uptake, and ecosystem projects)
- _Community Labs Blog – “ao Ventures Demo Day Recap”_ (Community Labs incubator for AO projects, April 2024)
- _ao/acc Labs_ – Official site (community apps on AO) and GitHub repos (e.g. ArFleet) for ecosystem tools.
