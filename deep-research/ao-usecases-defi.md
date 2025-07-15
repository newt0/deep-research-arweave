---
title: AO DeFi Usecases
platform: ChatGPT DeepResearch (GPT-4o)
date: 2025-07-14
url: https://chatgpt.com/s/t_6875d24328888191b3cd94cf09457b64
tags: [ao, usecase, nft]
---

[PROMPT]

```markdown
Please conduct a technical investigation into DeFi (Decentralized Finance) projects built on Arweave’s Actor Oriented Protocol (AO), focusing on the following aspects:

## Focus Areas

- Notable DeFi projects implemented on AO (e.g., Permaswap, Astro, AOX)
- Representative examples across major categories such as AMMs, stablecoins, lending, and orderbooks
- Bridge and cross-chain mechanisms connecting AO with other L1/L2 chains (e.g., Ethereum, Solana), if applicable
- Benefits and limitations of implementing DeFi on AO (e.g., state persistence, scalability, token handling)
- Application of AO’s execution architecture (e.g., executors, messages, token blueprints) in DeFi contexts

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

#### Secondary Twitter (X) Accounts

- [@arweaveindia](https://x.com/arweaveindia)
- [@arweaveny](https://x.com/arweaveny)
- [@vela_ventures](https://x.com/vela_ventures)
- [@AstroUSD](https://x.com/AstroUSD)
- [@perma_dao](https://x.com/perma_dao)

#### Projects on AO

- [0rbit](https://docs.0rbit.co/)
- [Botega](https://botega.arweave.dev/)
- [Permaswap](https://github.com/permadao/permaswap)
- [AOX](https://aox.xyz/#/)
- [Astro](https://docs.astrousd.com/)
```

---

# Output

# DeFi on Arweave’s Actor Oriented Protocol (AO): An In-Depth Exploration

## Decentralized Exchanges (AMMs and Orderbooks) on AO

**Permaswap (Cross-Chain AMM/DEX):** Permaswap is a pioneering DEX in the Arweave/AO ecosystem, enabling cross-chain token swaps with high speed and no gas fees. Built on everPay (a fast Arweave-based L2), Permaswap executes atomic orders in real-time with zero front-running and millisecond finality. By adapting everPay to AO’s message standard, Permaswap seamlessly brings multi-chain assets into AO and enables on-chain atomic swaps across networks. In early 2025, \$AO (AO’s native token) was listed on Permaswap, and within 24 hours the AO/wAR pair exceeded \$1M in trading volume – underscoring Permaswap’s role as a liquidity hub for AO. Initially an AMM-style swap protocol, Permaswap has also introduced an **order book** module (“Permaswap Spot”), becoming the first AO DEX with on-chain orderbook functionality. This hybrid design combines AMM liquidity with orderbook features, leveraging AO’s parallel processing to handle many orders without the congestion limits of Ethereum’s serial execution.

**ArSwap/Perplex and Bark (High-Performance DEXs):** Aside from Permaswap, new exchanges are being built on AO to push DeFi capabilities. _ArSwap_ (recently rebranded to **Perplex**) is an upcoming AO DEX aimed at offering **perpetual contracts** and advanced trading features beyond a Uniswap v2 fork. Perplex is expected to leverage AO’s compute power for on-chain derivatives (perpetual futures), showcasing the **orderbook-style** DeFi category on AO. Meanwhile, **Bark** was launched by Community Labs as the first DEX on AO’s release day. Bark emphasizes low-latency, high-throughput trades by running each trading pair in parallel – thanks to AO’s architecture – achieving settlement speeds reportedly faster than some centralized exchanges. Notably, Bark’s design makes it highly composable: any AO process (even an EVM or Solana VM running on AO) can interact with Bark via the unified message-passing layer. This means an EVM-based smart contract process on AO could send trade instructions to Bark, illustrating AO’s _interoperability_ across different VMs. Together, these DEX projects demonstrate that AO can support both **AMM** and **orderbook/perpetual** exchange models, with parallelism allowing many markets to run concurrently without global throughput bottlenecks.

## Stablecoins on AO – The Astro USDA Protocol

**Astro (USDA Stablecoin):** **Astro Labs** introduced _USDA_, the first native stablecoin on Arweave and AO. Astro’s protocol mints USDA through an over-collateralized model using Arweave’s native token **AR** as collateral. In practice, AR holders can lock their AR (via Astro’s “Quantum Bridge”) and mint a lesser amount of USDA, similar to MakerDAO’s CDP model, ensuring USDA is fully backed by the value of AR. This design unlocks liquidity from AR – for example, “for every \$2 of AR deposited, 1 USDA can be minted” (roughly illustrative) – allowing AR holders to access stable assets without selling their AR. USDA is envisioned to be _the_ stable unit powering AO’s DeFi economy, enabling trading, lending, and payments with a value-stable currency. Astro chose AO for its unique benefits: the **permaweb’s security and permanence** for recording stablecoin issuance, and AO’s ability to automate stablecoin functions via autonomous actors (e.g. price oracles, liquidation bots). The Astro team credits AO’s framework for enabling **new capabilities** in a stablecoin, and launched USDA on AO testnet as early as April 2024. Beyond minting USDA, Astro’s ecosystem provides a **Quantum Bridge** that also facilitates bridging other stablecoins _into_ AO. For instance, users can bridge assets like USDC or USDT from Ethereum (or other chains) into AO, receiving wrapped equivalents (wUSDC, etc.) to use alongside USDA. This multi-chain liquidity strategy (partnering with custody provider Copper for security) ensures USDA is well-supported and that AO DeFi has access to major stablecoins. In summary, Astro’s USDA is a prime example of a **collateralized stablecoin on AO**, leveraging Arweave’s permanent storage and AO’s cross-chain connectivity to create a reliable DeFi stable asset.

## Lending Protocols on AO

**LiquidOps (Over-Collateralized Lending):** _LiquidOps_ is an emerging lending/borrowing protocol built on AO (and Arweave) that provides the base-layer money market for the AO DeFi ecosystem. Co-founded by Arweave veterans, LiquidOps allows users to deposit assets (like AR or stablecoins) and earn interest, or borrow against collateral in a trustless manner. The protocol follows a familiar over-collateralization model (similar to Compound/Aave), but takes advantage of AO’s architecture for improved functionality. Notably, LiquidOps implements a _“native AO liquidation”_ process – meaning the monitoring and liquidation of under-collateralized loans are handled by autonomous AO processes. Thanks to AO’s **persistent and parallel execution**, LiquidOps can run continuous background checks on loan health without needing off-chain bots, and trigger liquidations on-chain without congesting a global EVM-like pipeline. The team has also provided developer integrations (an NPM package and blueprint modules) for others to compose on LiquidOps, reflecting the composability of AO’s message-passing (e.g. a DAO or DeFi app could send a message to LiquidOps to open a loan or retrieve interest rates). In testing phases (as of late 2024), LiquidOps supported wrapped assets like wAR (wrapped AR) and stablecoins, enabling users to borrow AO-native USD against their AR, etc.. This lending platform underpins **capital efficiency** in AO DeFi – lenders earn sustainable yields, while borrowers can leverage assets without leaving the AO environment. With AO’s scalability, LiquidOps can handle many parallel borrow positions and interest accrual computations simultaneously, avoiding the bottlenecks seen in Ethereum when many loans update at once. The introduction of LiquidOps signals that core DeFi primitives (like lending) are rapidly maturing on AO, using both **familiar financial logic and novel AO-specific enhancements** (such as on-chain agent liquidators).

## Cross-Chain Bridges and Asset Connectivity

Because AO is a new layer on Arweave, **bridging external assets** is critical to bootstrapping its DeFi. The main conduit for this is **AOX**, a cross-chain bridge designed to connect AO with other L1/L2 networks. Launched in mid-2024 by everVision (the team behind everPay), AOX’s mission is to _“seamlessly bring more assets into the AO ecosystem”_. It acts as a **custodial bridge** using secure MPC (multi-party computation) for signing. In May 2024, AOX went live by enabling Arweave’s AR token to be bridged into AO; AR deposited on the Arweave mainnet is wrapped as **wAR** on AO. This effectively unlocked Arweave’s \~\$2B market cap asset for use in AO smart contracts. By year’s end, over 50,000 wAR had been minted, held by tens of thousands of users. In August 2024, AOX expanded to support **Ethereum**: users could connect with MetaMask and bridge USDC from Ethereum, receiving **wUSDC** on AO. AOX later even allowed direct deposits of USDC from **Base and BSC** chains (bypassing Ethereum’s fees), showcasing a flexibility to integrate multiple networks. All bridged tokens on AO (wAR, wUSDC, etc.) conform to AO’s token standards, so they behave like native tokens for transfers, DeFi, etc. Notably, bridging is _bidirectional_ – AOX plans to let users withdraw back to mainnet or even to centralized exchanges directly. Other cross-chain efforts include Astro’s **Quantum Bridge** (focused on AR and stablecoins, secured by Copper custody), and the _Molecular Execution Machine (MEM)_ which has an audited ERC-20 bridge to bring Ethereum tokens trustlessly into AO soon. While full Solana integration wasn’t live at time of writing, the infrastructure is being laid for multi-chain support (e.g. custody solutions and AO’s generic message format could extend to Solana assets in the future). **In summary**, AO’s bridging architecture (spearheaded by AOX) provides the _financial arteries_ for AO DeFi, connecting value from established chains. It lowers the barrier for users to move assets into AO (even via direct CEX transfer) and ensures AO’s DeFi isn’t an isolated island but rather a hyper-connected hub in the multichain ecosystem.

## Benefits of Implementing DeFi on AO

Building DeFi on AO offers several **unique advantages** due to its actor-oriented design and Arweave foundation:

- **Permanent State and History:** Every AO process (smart contract) lives on Arweave’s permanent data storage, giving it persistent state that doesn’t disappear. This is powerful for DeFi – contracts can retain long-term state (e.g. user balances, loan histories) without costly upkeep, and all interactions are immutably stored. For example, once deployed, an AO process continues to exist indefinitely and can even run autonomously when creators are offline. This permanence assures that a DeFi app like an exchange or lending pool can be truly unstoppable and auditable: its full transaction history and state transitions are recorded on the permaweb, allowing **easy verification and analytics** over time. It also enables novel behavior like contracts that keep operating (or can be taken over by others) even if the original developers stop maintaining them – a guarantee of continuity rarely seen in traditional smart contracts.

- **Scalability via Parallelism:** AO’s **hyper-parallel execution** means there is no single global VM processing all transactions serially. Each DeFi contract is an independent process, so many computations can occur simultaneously without contention. This massively improves throughput and mitigates congestion issues seen on chains like Ethereum. For instance, two trades on different AO DEX pairs, or two separate loan liquidations, can execute in parallel on different nodes – there’s no “global miner ordering” needed as in Ethereum. As a result, AO DeFi can support **high-frequency trading, multiple orderbook markets, and large-scale user activity** without hitting a performance ceiling. Tests show AO handling hundreds of millions of messages with steady performance. This parallelism also allows more complex computations (e.g. pricing models, batch auctions, AI agents for arbitrage) to run on-chain, since they can be distributed across many nodes. In short, AO provides **cloud-like scaling** where adding more nodes increases capacity – a boon for demanding DeFi applications.

- **Inter-Process Composability:** AO introduces a unified message-passing layer that lets any process send messages (calls) to any other. This is analogous to composability in smart contracts, but more flexible – even processes running different virtual machines or languages can communicate via standard messages. In DeFi, this means an **unprecedented level of composability**: an automated strategy process could message a DEX process to execute a trade, then message a lending process to deposit the proceeds, all in one flow. We’re already seeing examples: developers can build **autonomous agents** that act across DeFi protocols on AO (e.g. an agent that arbitrages between Bark DEX and Permaswap, or manages a portfolio) because all are part of the same network of actors. AO’s message layer effectively standardizes integration – no need for complex cross-contract interface logic or off-chain bots, since any AO DeFi service can be **called like an API** by another. This composability extends beyond AO’s native processes: the fact that EVM or CosmWasm chains can run _inside_ AO means an Ethereum contract on AOVM could directly interact with AO-native DeFi apps via messages, bridging ecosystems in one unified environment.

- **Extensibility of Execution (Custom VMs and Executors):** AO’s modular architecture allows different execution environments (“executors”) to plug in. Developers are not limited to one programming model – they can use AO’s native Lua-based processes or spin up an **AOVM (EVM-compatible process)** or even a **Solana VM process**. In DeFi context, this flexibility means teams can port existing Solidity or Cosmos-based protocols into AO with minimal changes (using WeaveVM or CosmWasm on AO), while still benefiting from AO’s scalability. For example, an existing Solidity DEX could run on AO’s EVM module, and still message an AO-native stablecoin process or use AO oracles. This lowers the barrier for DeFi developers to adopt AO, reusing battle-tested code but gaining AO’s performance. Additionally, AO supports trusted execution environments (TEE) as an option, which can boost secure computation for DeFi (e.g. running sensitive algorithms or order matching in a hardware-encrypted enclave). **Custom executors and VMs** make AO a _polyglot DeFi platform_, welcoming diverse codebases and enabling innovative features (like running AI models within DeFi agents, etc., as hinted by projects like Autonomous Finance and RedStone’s CLARA agents).

- **Standardized Token Primitives:** Arweave traditionally had no native token standard beyond AR, but AO fills that gap by providing **Token Blueprints** – pre-built templates equivalent to ERC-20 (for fungible tokens) and ERC-721 (for NFTs). Using the token blueprint, developers can rapidly instantiate tokens on AO with common handlers for transfers, balances, mint/burn, etc.. This has been crucial for AO DeFi: wrapped assets like wAR and wUSDC were created via these standardized contracts, and protocols like Astro’s USDA or LiquidOps leverage them for their own tokens (e.g. stablecoin or interest-bearing tokens). The blueprint approach ensures **consistency and security** (audited base code) and interoperability between tokens. It essentially maps to familiar ERC-20 logic, so DeFi devs and users face a shallow learning curve when handling AO tokens. Moreover, tokens on AO benefit from Arweave’s permanent storage – every token transfer or mint event is stored immutably, which is excellent for transparency and **on-chain compliance/auditing** if needed.

- **Lower Fees & User Experience:** Thanks to designs like everPay and bundlers (e.g. Liteseed network), many AO transactions incur **negligible fees** and fast finality. Users on AO can trade or send tokens often without paying per-tx gas (aside from occasional Arweave storage fees that are fractions of a cent). This Web2-like smoothness (e.g. Permaswap’s swaps feel instant and free of gas) can attract a broader user base. Developers can sponsor storage or batch many actions into one Arweave transaction, making interactions cheap. The **economic model** (one-time storage payment for permanent contract data) means DeFi contracts don’t charge gas for each execution, which opens doors for microtransaction use cases and high-frequency trading that would be cost-prohibitive on gas-based chains.

## Limitations and Challenges of AO DeFi

While AO offers a powerful new framework, building DeFi here comes with some **challenges/limitations** to note:

- **Early-Stage Ecosystem:** AO mainnet launched in 2025, so the DeFi ecosystem is nascent. Liquidity and usage are growing but still small relative to mature L1s. Many protocols (lending, perps, etc.) are just launching or in testnet, which means composability is not as rich as Ethereum yet. Users and developers face a _learning curve_ adopting the actor paradigm. For example, some EVM-based devs initially treat AO processes just like Ethereum contracts – which works (since AO processes can resemble smart contracts) but doesn’t immediately tap into AO’s broader potential. Rethinking dApp architecture to fully exploit parallelism and messaging may take time and community practice. Documentation and tooling are actively improving (with the AO Cookbook, AO Link explorer, etc.), but still evolving.

- **Bridging Trust and Complexity:** Bringing assets into AO currently relies on federated or centralized components, introducing trust assumptions that pure on-chain DeFi tries to minimize. AOX’s MPC bridge, for instance, uses a set of signers (initially 4) to custody and mint wrapped assets. This is a practical approach but not trustless – users must trust the bridge operators’ security. Efforts like MEM’s cross-chain bridge or TEE-based verification might reduce trust over time, but until then, AO DeFi inherits typical **bridge risks** (custodial risk, potential withdrawal limits, etc.). Additionally, supporting multiple chains (Ethereum, Base, BSC, etc.) adds operational complexity. The need for wrapped tokens also means **fragmentation of liquidity** – e.g. wUSDC on AO is separate from native USDC, so arbitrage and smooth convertibility depend on the bridge functioning. The AO community is addressing this by partnering with reputable custodians (e.g. Copper for Astro’s bridge) and planning more decentralized solutions, but it remains a consideration.

- **Unique Security Model:** AO’s security model differs from a traditional blockchain. Not every node executes every contract; instead, processes run on subsets of nodes with results eventually persisted to Arweave. This **optimistic concurrency** approach requires confidence that the network will verify and settle computations correctly. If a malicious node executes a process incorrectly, mechanisms must detect and resolve that. The AO protocol ensures eventual verifiability (all messages are recorded on Arweave for audit), but the tooling for fraud proofs or challenge games is still maturing. DeFi developers must understand these nuances – e.g. ensuring critical financial logic in their process can be deterministically validated by others. The addition of **Trusted Execution Environments** and verifiable computation aims to bolster trust, but these are new technologies in blockchain contexts. Overall, while AO removes gas and increases speed, ensuring that **“parallel != insecure”** is an ongoing engineering focus.

- **State and Data Costs:** Arweave provides permanent storage, but writing data to Arweave carries a one-time cost in AR. DeFi contracts that generate massive amounts of messages or state updates will incur AR fees (albeit small per message). As usage scales, those costs could accumulate. Protocols might need to account for **economic incentives** to cover storage fees (for example, a DEX might need to charge a tiny fee to fund the Arweave storage of trades). The good news is Arweave storage is cheap and priced in a stable endowment model, but it’s not free – this is a different paradigm from ephemeral chain state that is pruned unless gas is paid. Managing on-chain data efficiently (perhaps using AO’s upcoming **WeaveDrive** or offloading large blobs) will be important for DeFi apps that produce lots of data (like high-frequency orderbooks). There’s also the consideration of **state bloat** per process: since each process keeps its own state, a very active DeFi process could grow large. AO’s design avoids a single global state, and storage can scale horizontally, but individual processes must still be designed to handle long-term state growth (through pagination, archiving older data, etc.).

- **Interoperability and Standards:** AO is introducing new standards (ANS-104 messages, AR wallets with 0x addresses, etc.) that may not yet be supported by common crypto wallets and services. For instance, MetaMask can interact with AO via AOX using 0x addresses, but tooling like portfolio trackers or hardware wallets might not immediately recognize AO assets. The ecosystem is rapidly addressing this (ArConnect wallet supports AO tokens natively, and explorers like ViewBlock have added AO views), but **integration with the broader crypto infrastructure** is a work in progress. This could pose a short-term limitation for user experience – e.g. fewer custodial solutions or analytics platforms know about AO yet.

Despite these challenges, the trajectory of AO DeFi is strongly positive. The parallel, actor-oriented model is proving capable of hosting complex financial dApps that were impractical on other chains. Early projects like Permaswap, Astro, LiquidOps, and AOX have demonstrated the core building blocks, and usage is growing week by week. As the AO mainnet gains traction (launched Feb 2025), we can expect its DeFi ecosystem to mature rapidly, benefiting from Arweave’s permanence and AO’s limitless compute scaling. In conclusion, **AO brings a novel blend of web-scale computing and blockchain trust to DeFi**, unlocking high-performance use cases (like on-chain perps, AI-run financial agents, and parallel markets) while introducing new design patterns. It preserves the decentralized ethos – verifiable and permissionless code – but frees developers from many traditional constraints. The coming months will likely see more innovative DeFi protocols on AO, each leveraging features like **executors, messages, and token blueprints** to redefine what on-chain finance can do. The foundations laid by these early projects suggest that AO could become a thriving DeFi hub, complementing Arweave’s vision of a permanent, decentralized web with an equally durable and scalable financial layer.

**Sources:** The information above is drawn from AO’s official documentation and community publications (2024-2025). Key references include the AO whitepaper and cookbook for technical architecture, ecosystem overviews by independent researchers, project reports from PermaDAO’s _Weekly Highlights_ (covering Permaswap’s launch, LiquidOps progress, etc.), and announcements from the teams behind Astro (USDA) and AOX bridges. These connected sources provide a comprehensive, up-to-date picture of DeFi on AO, illustrating both its capabilities and ongoing development.
