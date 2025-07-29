---
title: AI Agent on AO
platform: ChatGPT DeepResearch (GPT-4o)
date: 2025-07-17
url: https://chatgpt.com/s/t_688836a3d2c48191979d200050e8f1c8
tags: [ao, developer, aiagent]
---

[PROMPT]

```markdown
Please conduct a technical investigation into AI Agent projects built on Arweave’s Actor Oriented Protocol (AO), with a focus on the following:

## Focus Areas

- Integration design between AI Agents and the AO architecture
- Representative AI Agent projects implemented on AO
- Autonomous NFT and DeFi operations powered by AI Agents
- Coordination and competition among decentralized AI Agents

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

### Key GitHub Repositories

- [ao-labs/ao](https://github.com/ao-labs/ao)
- [aos](https://github.com/permaweb/aos)
- [HyperBEAM](https://github.com/permaweb/HyperBEAM)

### Explorer & Tools

- [AO Link](https://www.ao.link/)
- [Bazar](https://bazar.arweave.net/) — AO-native NFT marketplace
- [Wander](https://docs.arconnect.io/) — AO-compatible wallet

### Developer & Community Blogs

- [Community Labs Blog](https://www.communitylabs.com/blog)
- [Permaweb Journal](https://permaweb-journal.arweave.net/index.html)

### Twitter (X) — Core Accounts

- [@aoTheComputer](https://x.com/aoTheComputer)
- [@samecwilliams](https://x.com/samecwilliams)
- [@CommunityLabs](https://x.com/CommunityLabs)
- [@fwdresearch](https://x.com/fwdresearch)
- [@aoComputerClub](https://x.com/aoComputerClub)

### Projects on AO

- [0rbit](https://docs.0rbit.co/)
- [Botega](https://botega.arweave.dev/)
```

# [OUTPUT]

## AO Architecture and AI Agent Integration

Arweave’s **AO protocol** is a decentralized, **actor-oriented** compute layer that treats each independent program as an “actor” or process. These AO processes maintain internal state and communicate by exchanging **messages**, with all interactions permanently logged on Arweave’s storage network. This design cleanly separates **computation from storage** – processes run off-chain on various Compute Units, while a tamper-proof log of every input (message) and output is stored on Arweave for verification. AI agents integrate by **running as AO processes**, meaning an AI-driven service (e.g. a trading bot or chatbot) can be deployed into AO’s network as just another actor following the same messaging protocol.

Key architectural components of AO enable seamless AI agent integration:

- **Modular Virtual Machines & Execution** – Each agent process can choose its preferred VM/runtime and consensus rules, yet still interoperate via AO’s unified message format. For example, an AI agent running in a WASM VM or even on a cloud server can “plug into” AO and exchange messages with other on-chain actors.
- **Permanent Logging & Verifiability** – Every action an agent takes (inputs, outputs) is recorded on Arweave. This guarantees an agent’s decisions and data (e.g. model outputs or trades) are auditable and censorship-resistant. Agents cannot lose state or be censored because their state transitions are recoverable from Arweave’s permanent ledger.
- **Autonomous Scheduling** – Unlike typical smart contracts, AO processes can **“wake themselves up”** on a schedule without external triggers. This means an AI agent can be configured as a cron-like process that runs periodically or at specific times. For instance, a trading agent can autonomously activate at 3 AM to check markets and execute strategies while you sleep. This self-scheduling ability is crucial for truly autonomous agents.
- **Trusted Execution for Secrets** – Some agents leverage Trusted Execution Environments (TEE) to securely handle private keys or user data within AO. Using TEEs, a user can grant an AI agent control of their crypto wallet keys in a secure enclave. The agent can then act on the user’s behalf (e.g. executing trades) without exposing secrets, enabling **fully autonomous operation without human intervention**.
- **AI Model Support** – AO’s compute infrastructure is robust enough to run heavy AI workloads. After a WASM upgrade, each Compute Unit can access up to 16 GB of memory, enabling execution of large ML models (comparable to unquantized LLaMA/Falcon LLMs) directly on-chain. Agents can also use **WeaveDrive** to read Arweave-stored datasets as if they were local files – for example, an agent could fetch a trained model or data from Arweave and load it into memory for AI inference. This design “makes it possible to implement smart contracts that integrate AI agents,” letting on-chain programs run AI models and logic as part of their trusted code.
- **Oracles and External Data** – Through projects like **0rbit**, AO agents can trustlessly access any off-chain web data they need. 0rbit is an oracle network on AO that lets processes fetch data from arbitrary URLs, beyond just price feeds. Its decentralized 0rbit Nodes securely handle HTTP requests/responses with no centralized interference. This means an AI agent on AO can, for example, call an external API or scrape web content through 0rbit, incorporate that data into its decisions, and all of this occurs within AO’s verifiable environment. The ability to draw from real-world data greatly expands the scope of autonomous agents (e.g. an agent pulling weather data or social media sentiment to inform its actions).

In summary, AO’s **hyper-parallel, message-passing architecture** provides a flexible sandbox for AI agents. Agents run as independent processes that coordinate via messages, leveraging Arweave for immutable memory and using AO’s scheduling and oracle integrations for autonomy and awareness. This integration design allows AI agents to function as first-class actors in a trust-minimized network, blending on-chain verifiability with off-chain computational freedom.

## Notable AI Agent Projects on AO

Since AO’s testnet launch in 2024, several projects have emerged to showcase **autonomous agents in action**:

- **Autonomous Finance – DCA & Yield Agents:** _Autonomous Finance (AF)_ is a team heavily focused on **Agent-Fi** (agent-driven DeFi). They built a **Dollar-Cost Averaging (DCA) agent** as an early proof-of-concept. The DCA agent is an Autonomous Investment Agent that automatically buys a target asset at regular intervals using a quote currency, executing on decentralized exchanges within AO. Once deployed, the agent manages the user’s funds **without any off-chain signals or human input**, thanks to AO’s cron triggers and on-chain price feeds. The agent’s web dashboard is hosted on the Permaweb, but the trading logic lives entirely in AO – it wakes up on schedule, swaps tokens as per user strategy, and logs the results permanently. AF’s DCA agent demonstrated the viability of “set-and-forget” personal trading bots. (Notably, this early DCA app was later rolled into other platforms like Botega, and AF open-sourced the code as a reference for AO developers.) Beyond DCA, **Autonomous Finance’s roadmap includes** agents for self-balancing index funds, autonomous hedge funds with custom risk profiles, yield aggregation across protocols, on-chain prediction markets, and even high-frequency trading bots. These agents all run as AO processes that monitor on-chain data and execute trades or rebalances when conditions meet, showcasing a range of financial “AI trader” use cases.

- **Botega – Agent-Powered DEX:** **Botega** is the first **“Autonomous Agent-first” decentralized exchange** built on AO. Launched by Autonomous Finance in late 2024, Botega uses a fleet of AI agents under the hood to provide advanced trading features on Arweave’s permaweb. For example, Botega supports trailing stop orders, dynamic DCA strategies, and limit orders – functionalities typically requiring active monitoring by bots. In Botega’s design, the complex exchange logic and **AI trading agents** run as AO processes on the backend. The user interface is a decentralized web frontend on Arweave, but when a user places an order like “sell if price drops 10%,” an autonomous agent process on AO takes over to watch the market and execute that order conditionally. Botega leverages Arweave+AO’s **“full permanent stack”** (permanent UI + on-chain compute) to ensure the DEX is unstoppable and trustless. In short, Botega demonstrates how **DeFi can be run by intelligent agents**: users define intents, and autonomous AO actors carry out the trading strategy. Botega’s success led to it becoming a core trading venue in the AO ecosystem, proving out the concept of **Agent-Fi DEXes** in practice.

- **0rbit – Decentralized Oracle Network:** While not an “AI agent” itself, **0rbit** is a crucial AO project enabling agents to function intelligently. 0rbit is the **first oracle system built on AO**, created by developers in the Arweave community. It allows any AO process to fetch **arbitrary off-chain data** from the web, essentially acting as the “eyes and ears” for AI agents. For example, an agent can query 0rbit to get the latest price of an asset from a Web2 API, or the content of a news webpage, and then use that data in its on-chain logic. Unlike traditional oracles limited to specific feeds, 0rbit can retrieve **any URL’s data** with no preset data type restrictions. A network of 0rbit nodes handles the requests and returns responses to the agent, with cryptographic guarantees and without centralized interference. The advent of 0rbit is considered essential for “building real world applications” on AO, since many AI agents (trading bots, prediction agents, etc.) require real-time external information to make decisions. In summary, 0rbit serves as a **trustless data bridge** for AO’s AI agents, greatly expanding what they can do.

- **Dexi & Data Agents:** **Dexi** is an AO-based data service and another piece of Agent-Fi infrastructure. It aggregates on-chain data about token pools, prices, and asset metadata, and exposes this info to other agents via AO’s message-passing interface. In practice, Dexi acts as a **data provider agent**: end-users can use Dexi’s web frontend for analytics, and other AO agents (bots) can programmatically query Dexi by sending it messages. For instance, a trading agent might ping Dexi to get the latest DEX pool price or liquidity info before executing a trade. AO’s design allows one agent to call another like this, enabling **composability** among agents. Dexi shows how agents can specialize – some gather or index data, while others (like a hedge fund agent) consume that data to act. Such patterns illustrate an emerging **agent ecosystem** where services are modular: one agent can rely on another’s output, all through on-chain, asynchronous messages.

- **Other Emerging Projects:** The AO ecosystem is rapidly expanding, and AI agents are being explored in diverse domains beyond pure finance. For example, **Jobsy** is an AI agent-powered hiring platform (an “AI recruiter”) built on AO and permaweb tools. In gaming and social applications, **Llama Land** introduced an NPC agent called the “Llama Rememberer” – an AI-powered memory aide that players can query in natural language. Even NFT communities are utilizing agents: the **DumDumz NFT** project implemented an “AOction House” for autonomous NFT auctions, and **BazAR** (the primary AO NFT marketplace) now gives each user a **profile agent** on AO. A BazAR profile isn’t just a static address; it’s backed by a smart agent process that could automatically manage the user’s listings, bids, or notifications on their behalf. These examples underscore that any recurring on-chain task or service can be embodied as an AO agent – from finance to social media to marketplaces – and many such experiments are underway.

## Autonomous NFT and DeFi Operations via Agents

One of AO’s most promising applications is enabling **autonomous on-chain operations** in DeFi and NFT markets – essentially self-driving services that can trade, invest, or manage digital assets without constant human micromanagement. Below are key use cases being realized on AO:

- **Autonomous DeFi Investing:** AO agents are tackling yield farming, lending, and trading with minimal human input. A notable example is the **yield optimization agent** running on AO’s testnet, which continuously finds the best lending rates across protocols and reallocates assets accordingly. This agent can monitor multiple lending pools and move a user’s capital to whichever pool offers higher yield, functioning like a decentralized robo-advisor. Another launched agent automatically performs **dollar-cost averaging** trades for users on decentralized exchanges. Users set the asset and interval, and the agent will wake up to buy at each interval, adjusting for slippage and recording all purchases – all without the user needing to sign each transaction. Crucially, these agents **hold users’ funds and keys within secure enclaves (TEE)**, so they can execute trades and interact with DeFi protocols 24/7 on the user’s behalf. This “hands-off” asset management is a new paradigm: your **AI financial advisor** lives on-chain, obeys code (your preset rules), and never tires or misses an opportunity.

- **Agent-Run Exchanges and Market Making:** Traditional exchanges rely on human or bot market-makers to add advanced order types. On AO, exchanges themselves can be built from autonomous agents. **Botega** (the AO-based DEX) is a prime example, offering features like trailing stop-losses and automated DCA that are powered by back-end agents watching price movements. When a user sets a trailing stop order on Botega, an agent process begins tracking the market and will execute the sell when the condition triggers – no centralized server or manual bot needed. Similarly, on **Permaswap (AO’s AMM)**, a recent FusionFi upgrade allows various agent-driven strategies to plug in, standardizing how different **AgentFi** modules connect to liquidity pools. We’re seeing the rise of **Agent Market Makers** – autonomous programs providing liquidity or arbitrage across exchanges. Because AO imposes no global gas limits, an arbitrage agent can run an extensive search or even an ML model on-chain to find cross-market opportunities, then act, all in one go. This could lead to on-chain competition analogous to high-frequency trading, but between decentralized algorithms.

- **Autonomous NFT Auctions & Management:** NFTs on Arweave (often as **atomic assets** with all data on-chain) are also benefiting from AO automation. **BazAR**, the NFT marketplace, uses AO processes to handle core operations like listings, bids, and profile management. Each BazAR user’s profile is backed by an AO agent that can, for instance, automatically accept a bid if it meets certain criteria or update the user’s content listings across the permaweb. Community projects have even run **auction smart agents**: for example, the _DumDumz NFT_ collective launched an “**AOction House**” where an AO process autonomously ran the auction of rare NFTs (handling timing, bid ranking, and final settlement on its own). By letting an impartial on-chain agent execute the auction rules, trust in fairness increased (no seller interference) and auctions could occur at any time without organizers present. More broadly, **autonomous NFT agents** can manage royalties (distributing revenue per on-chain policy), curate galleries (buying/selling according to a strategy), or even breed and evolve NFT game assets on a schedule. All these tasks can be encoded into AO agents that operate continually. The **permanent storage** of Arweave complements this well – an NFT’s metadata lives forever, and an agent can wake up years later and still find the NFT’s state intact to act upon it.

In both DeFi and NFTs, these examples illustrate a theme: **trusted automation**. Instead of relying on off-chain bots or manual oversight, AO allows deploying the logic as an on-chain agent with clear rules and auditability. This opens up a world where your portfolio can rebalance itself, your NFT collection can “manage itself” (e.g. auto-list at a target price), and new financial products can be composed by simply launching new agents that plug into others. The result is a more **autonomous finance (“AgentFi”)** environment – services that run 24/7 with minimal trust and maximal transparency.

## Coordination and Competition in a Decentralized Agent Network

AO’s actor model not only enables individual autonomous agents, but also a **complex society of agents** that can cooperate, compete, and even form entire on-chain economies. The protocol was explicitly designed with **inter-process communication** in mind, so multiple agents can coordinate tasks by messaging each other through AO’s network. This leads to scenarios where decentralized AI agents are both **collaborators and competitors**:

- **Open Coordination via Messaging:** All AO agents speak the same message language, allowing them to call on one another’s services. For example, a trading agent might query a pricing agent (like Dexi) for data, or hire an oracle agent (like 0rbit) to fetch off-chain info. Agents can also orchestrate multi-step workflows – one agent’s output can trigger another agent’s action. AO guarantees eventual delivery and ordering of messages (via its Scheduler units) which provides a reliable channel for coordination. This is analogous to microservices in Web2, but without a central server: an ecosystem of microservice-agents forms organically. If one agent doesn’t have a skill, it can effectively “ask” another agent for help, forming **composable agent services**. As an example, imagine an insurance claim agent that, upon receiving a claim, messages a weather-data agent for verification, and then calls a payment agent to issue payout. All those interactions happen trustlessly on AO’s rails. Such **agent-to-agent coordination** is becoming more sophisticated – indeed, developers are exploring “agent marketplaces” where agents advertise capabilities and autonomously **hire each other’s services** for crypto fees (so one agent might pay another for a successful task completion). This vision is emerging on other platforms as well, hinting at a future **“internet of agents”** where diverse agents form supply/demand for skills and information.

- **Competitive Dynamics:** With many agents operating in the same domain, natural competition arises. The AO whitepaper and community frequently draw parallels to traditional finance, noting that already **over 80% of trades on Nasdaq are executed by bots**. AO’s agent-friendly design suggests on-chain markets will similarly be dominated by AI agents competing for profit. Multiple yield optimizer agents might battle to offer users the best returns, or arbitrage bots might race each other to capture the same price discrepancy. Because AO imposes no global throughput limit (it’s hyper-parallel), there’s room for **many agents to run concurrently** and even to spawn new sub-agents in real time. This creates a **decentralized competitive landscape**: no single agent or operator has a monopoly on a task – anyone can deploy a smarter or faster agent to try to outperform others. For instance, if one lending optimizer agent finds 10% yield, another might deploy an AI model to predict upcoming rate changes and move funds faster, thus outcompeting the first. Agents might also engage in **adversarial behaviors** (much like high-frequency trading algorithms do), such as trying to anticipate others’ moves. AO provides the arena for this competition, with the assurance that all agents play by transparent rules (since their actions are logged and deterministic given inputs). Over time, one can imagine **evolutionary economics** on-chain: only the most efficient or profitable agent strategies survive, creating a feedback loop driving innovation in agent design.

- **Cooperative Networks:** Not all multi-agent interaction is zero-sum. AO also allows for **cooperation and federation** of agents. A group of agents could form a decentralized service collective – for example, a set of oracle agents pooling data to increase reliability, or a team of AI agents dividing a complex task into subtasks (one agent does data gathering, another does analysis, a third handles execution). Because the network is asynchronous and globally accessible, agents can join forces permissionlessly. We’re seeing early signs of this in projects like **Olas’s “agent bazaar”** (though not on AO specifically), where specialized agents find each other to collaborate on-the-fly, each contributing what they’re best at to complete jobs. On AO, similar ideas are discussed under AgentFi and ContentFi frameworks – agents might collectively manage a content repository or co-author analytic reports by passing messages with intermediate results. **Social agents** are another angle: an AO agent could represent a user in social platforms, and multiple user-agents could negotiate or form groups (imagine DAO governance where each voter delegates to an AI agent, and those agents deliberate among themselves before voting). The **message-passing “web” of AO** was explicitly likened to how web pages link together into a larger network – in AO, each agent is autonomous, but their ability to interconnect means they form a **cohesive, web-like system** of collective intelligence.

In summary, AO is fostering an environment where decentralized AI agents are not isolated bots, but participants in a **dynamic agent economy**. They coordinate by sharing data and services, and they compete by pursuing scarce opportunities (be it arbitrage profit, NFT drops, or user attention). This **coordination and competition** is key to AO’s vision of an “open-access supercomputer” – instead of one monolithic program, it’s a swarm of programs interacting. As one analysis put it, programming AI agents on AO enables on-chain services that “**may compete with each other or represent humans against humans**,” expanding the intelligent decision-making in markets from a human-only activity to one dominated by autonomous code. The coming years will likely see the emergence of on-chain agent ecosystems that mirror real-world economies – complete with marketplaces, specialization, collaboration, and competition – all built atop Arweave’s permanent, verifiable compute infrastructure. Each AI agent, in effect, becomes an **economic actor** in a decentralized digital society, and AO provides the town square (and the rules) for all these robot actors to meet and transact.

**Sources:** The information above is synthesized from Arweave’s official AO documentation and whitepaper, community publications, and project case studies. Key references include the AO whitepaper by Sam Williams et al. (June 2024), the Arrington Capital technical deep-dive on AO (Jan 2025), Autonomous Finance’s research on AgentFi and DCA agents, and case studies of live AO projects like Botega and 0rbit. These sources detail the design of the AO protocol and provide real examples of how AI agents are being implemented on Arweave’s network.
