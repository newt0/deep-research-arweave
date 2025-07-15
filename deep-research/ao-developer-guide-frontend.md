---
title: AO and Frontend Integration
platform: ChatGPT DeepResearch (GPT-4o)
date: 2025-07-14
url:
tags: [ao, developer, nextjs]
---

[PROMPT]

```markdown
Please conduct a technical investigation into integrating AO-based applications with a frontend built in Next.js and TypeScript.

## Focus Areas

- How to connect to AO Actors and Processes using Wander, Beacon, or ao-sdk
- How to implement wallet connection and signature handling on the client side
- How to send messages or interact with Actors from the browser
- How to display real-time updates or state responses from AO
- Boilerplate repositories and frontend templates for AO-integrated dApps

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

# [OUTPUT]

# Integrating AO-Based Applications with Next.js and TypeScript

Integrating **AO (Actor Oriented)** smart contracts with a Next.js frontend involves connecting your web app to AO processes (actors), handling wallet signatures, sending messages to those actors, and rendering live state updates. This enables building rich **dApps** (e.g. autonomous AI agents or DeFi platforms) on Arweave’s AO network with a modern React/TypeScript frontend. Below, we break down key integration steps and resources.

## Connecting Next.js Frontend to AO Actors and Processes

To communicate with AO processes from Next.js, use the **AO Connect SDK** (`@permaweb/aoconnect`). This JavaScript/TypeScript library runs in both Node (server) and browser contexts, letting you spawn processes, send messages, and fetch outputs. Key points:

- **Installation:** Install via npm: `npm install @permaweb/aoconnect`. The SDK exports functions like `spawn`, `message`, `result`, `results`, etc., which can be imported directly or via a `connect()` initializer.

- **Default vs Custom Network:** By default, simply importing from `@permaweb/aoconnect` connects to the AO **mainnet** (HyperBEAM network). For custom setups (local testnet or specific nodes), use `connect()` with URLs for your Messenger Unit (MU), Compute Unit (CU), or Arweave gateway. For example:

  ```ts
  import { connect } from "@permaweb/aoconnect";
  const { spawn, message, result } = connect({
    MU_URL: "http://localhost:4002",
    CU_URL: "http://localhost:4004",
    GATEWAY_URL: "http://localhost:4000",
  });
  ```

  This targets local AO units for development. Omitting parameters uses the default network endpoints.

- **Identifying Processes:** Each AO actor/process is identified by an Arweave transaction ID (TxID). For example, a deployed process has a TxID that you’ll use as the `process` (target) in API calls.

- **Server vs Client Usage:** The AO SDK works on **server-side** (Node) and **client-side**. You can invoke read operations (e.g. fetching process state or results) during Next.js server-side rendering, but **writing operations (sending messages)** require a user signature (private key) and thus run on the client side in most cases. Next.js can pre-fetch public state without a wallet, but user-triggered interactions (which must be signed) happen after hydration on the client.

- **SSR Considerations:** Avoid directly using browser globals during server-side rendering. If you import `aoconnect` in a Next.js page, wrap calls that access `window` (e.g. wallet access) in `typeof window !== 'undefined'` checks or use dynamic imports for client-only modules. For purely read-only data, you can safely call AO SDK methods (like `results`) from `getServerSideProps` or API routes using a backend wallet or none if not required.

## Wallet Connection and Signature Handling (Wander vs. Beacon)

AO requires every message to be **cryptographically signed** by a wallet key. This ensures trustless execution. There are multiple ways to integrate wallet signing in a Next.js app:

- **Wander (ArConnect) Browser Extension:** **Wander** (formerly ArConnect) is the primary browser wallet for Arweave/AO. It injects an API into `window.arweaveWallet` for dApps to request permissions and signatures. Steps to integrate:

  - Install the Wander extension (Chrome, etc.) and prompt the user to connect. Use `await window.arweaveWallet.connect([...permissions...], appInfo?)` to request needed permissions (e.g. `ACCESS_ADDRESS`, `ACCESS_PUBLIC_KEY`, `SIGN_TRANSACTION`, `SIGNATURE`). This will popup the wallet for user approval.

  - Once connected, you can retrieve the active address (`window.arweaveWallet.getActiveAddress()`) if needed, or directly use signing methods.

  - **Sign messages:** Use the wallet’s `signDataItem` API to sign AO messages. The AO SDK provides a helper to wrap this. For example:

    ```ts
    import { message, createSigner } from "@permaweb/aoconnect";
    // after user connects wallet:
    const signer = createSigner(globalThis.arweaveWallet);  // create a signer using the injected wallet
    await message({
      process: "<ProcessTxID>",
      tags: [ { name: "Action", value: "DoSomething" }, ... ],
      signer: signer,
      data: "optional payload"
    });
    ```

    Here `createSigner(globalThis.arweaveWallet)` returns a signer function that calls the extension’s `signDataItem` under the hood. The AO SDK will invoke `window.arweaveWallet.signDataItem({ data, tags, target, ... })` to get a signed data item, which it then sends as a message. The user will see the Wander popup to confirm the signature if not pre-authorized. **Note:** The `SIGN_TRANSACTION` permission is required for signing data items.

  - Wander/ArConnect keeps private keys in the extension, **never exposing them to the dApp**. This provides a secure, seamless login flow: your Next.js app delegates signing to the wallet extension rather than handling keys directly.

- **Wander Connect (Embedded Wallet SDK):** As an alternative to relying on the browser extension UI, **Wander Connect** is a library that embeds wallet functionality and social login flows directly in your app. You install `@wanderapp/connect` and initialize it in your React app to present a wallet interface. For example, `const wander = new WanderConnect({ clientID: "YOUR_APP_ID" });` sets up a wallet instance. Wander Connect offers a customizable, white-labeled modal for users to login or create wallets (with email/social accounts) and then returns a wallet instance you can use to sign transactions – under the hood it’s still using the Wander infrastructure but with a custom UI in-app. This can simplify UX (especially for new users without the extension) while still ensuring keys never leave the wallet’s secure context. The usage is similar – after initialization and user login, you call the provided methods to sign transactions or messages, and it will handle the cryptography via the Wander backend.

- **Beacon Wallet (AO-Sync, Mobile/Desktop Wallet):** **Beacon** is another wallet platform for Arweave/AO, with a focus on security (2FA, multisig) and cross-device usage. It’s available as a mobile app and desktop app. To connect a Next.js dApp with Beacon, use the **AO Sync SDK** (`@vela-ventures/ao-sync-sdk`), which communicates with Beacon via MQTT/WebSockets. Key integration steps:

  - Install `@vela-ventures/ao-sync-sdk` and create a `WalletClient`. e.g.:

    ```ts
    import WalletClient from "@vela-ventures/ao-sync-sdk";
    const walletClient = new WalletClient();
    await walletClient.connect({
      permissions: ["ACCESS_ADDRESS", "ACCESS_PUBLIC_KEY", "SIGN_TRANSACTION"],
      appInfo: { name: "MyApp", logo: "https://.../logo.png" },
      brokerUrl: "wss://aosync-broker-eu.beaconwallet.dev:8081",
    });
    ```

    This triggers a connection flow – typically yielding a QR code that the user scans with their Beacon mobile app to link the session. After scanning, the wallet pairs with the dApp.

  - Once connected, your app can request signatures through `walletClient`. For instance, `await walletClient.signDataItem(dataItem)` or `signTransaction(tx)` will prompt the Beacon wallet (on the user’s device) to approve and sign, then return the signed result. The AO Sync SDK handles the networking and ensures the signing happens within the secure wallet app.
  - Beacon is well-suited for mobile-first dApps or use cases needing extra security (e.g. multisig, biometric 2FA). It delegates all signing and key handling to the Beacon wallet, similar to how WalletConnect works for Ethereum dApps. The trade-off is a slightly more complex connection flow (scanning QR or deep linking).

- **Direct Keyfile (Developer Mode/Server):** In non-production scenarios or automated scripts, you might use a raw Arweave keyfile (JWK JSON) to sign messages. For example, on Node/SSR you can load a wallet file and use `createSigner(jwk)`. However, **never expose a user’s private key in the browser or bundle** – in production, always rely on Wander or Beacon so the user’s keys remain secure. Direct key usage is mostly for backend automation or testing. For instance, a Next.js API route could hold a service wallet to spawn processes or perform scheduled tasks on AO (with caution). The AO SDK’s `createSigner` works with both an injected wallet or a JWK depending on the argument.

**Signing is mandatory:** In AO’s mainnet, **all messages must be signed** by a valid Arweave (or Ethereum) key. The AO SDK enforces this – you provide a signer function whenever you call `message()` or `spawn()`. AO supports Arweave-native signatures and even Ethereum signatures for cross-chain identity, but commonly you’ll use Arweave keys via the above wallets. By using Wander or Beacon integration, you ensure the signing happens in a secure environment (extension or external app). Your Next.js app only handles the signed data item or transaction ID, never the raw private key.

## Sending Messages to AO Processes from the Browser

Once the wallet is connected and a signer available, your app can **send messages to AO actors** to invoke their functionality:

- **Message Format:** An AO **message** is essentially a signed data item (ANS-104 bundle format) with optional tags, target, data, etc. The `@permaweb/aoconnect` library abstracts this. You typically call the `message()` function with:

  - `process`: the target process’s TxID (the actor you are messaging).
  - `tags`: an array of key-value tags providing input parameters or action identifiers (these are delivered to the process’s handlers).
  - `data`: (optional) a payload string or bytes.
  - `signer`: the signer function (from `createSigner` or `createDataItemSigner`) that will sign the message.

  For example:

  ```ts
  await message({
    process: "abc123...ProcessTxID",
    tags: [
      { name: "Action", value: "Transfer" },
      { name: "To", value: "alice" },
      { name: "Amount", value: "100" },
    ],
    data: "",
    signer: createSigner(window.arweaveWallet),
  });
  ```

  This will construct a DataItem with those tags and send it to the AO network addressed to the given process. Under the hood, the library signs the DataItem (using the provided signer, which invokes the wallet) and publishes it to Arweave (either directly or via a bundler). The returned promise resolves when the message is accepted (it typically returns an object or logs the message ID).

- **Spawning New Processes:** In addition to sending messages to existing actors, you can create (spawn) new AO processes from the frontend – for example, deploying a user-specific agent or a new smart contract instance. The `spawn()` function requires:

  - `module`: the TxID of the **module** (code blueprint) to instantiate. (In AO, a “module” is like the contract code package.)
  - `scheduler`: the Arweave address of a scheduler unit to assign the process to (this might be a known scheduler’s wallet address; often provided in docs or by the network).
  - `signer`: your signer (to sign the spawn request, since spawning is a special message).

  Example:

  ```ts
  const newProcessId = await spawn({
    module: "<ModuleTxID>",
    scheduler: "<SchedulerWalletAddress>",
    signer: createSigner(window.arweaveWallet),
  });
  console.log("Spawned new process:", newProcessId);
  ```

  This will deploy a new process on AO and return its new TxID once confirmed. In practice, spawning is less common from a user-facing app (it might be done during development or by admin scripts), but **some dApps let users create new agents/contracts on the fly** (e.g. launching a new DAO or AI agent), in which case this is how to do it. Ensure the user understands they are publishing a new contract (and will pay the Arweave fees for it).

- **Using the correct Signer:** The AO Connect SDK’s convenience `createSigner`/`createDataItemSigner` will choose the right method based on environment. With an injected browser wallet, it uses `window.arweaveWallet.signDataItem` as shown above. This returns a `Uint8Array` of the signed message, which AO SDK then bundles and sends. If you were to implement a custom signing (for example, integrating a hardware wallet), you would need to produce a signed dataItem in the same format. But using the provided helpers with Wander or Beacon covers most cases.

- **Next.js Integration Pattern:** In a Next.js + TypeScript app, you might create a React context or hooks for AO interactions. For instance, on page load you could initialize the AO SDK (perhaps using `connect()` if custom config) and when the user clicks an action (like “Send Message” or “Execute Trade”), you:

  1. Ensure wallet is connected (if not, prompt via Wander or Beacon connect flow).
  2. Call the `message()` function with appropriate tags/data and the signer from the connected wallet.
  3. Optionally, handle the promise to update UI state (e.g., indicate transaction pending or display the returned message ID).

  Because Next.js uses SSR, keep all wallet-dependent calls in effects or event handlers (so they run on client). You can define the AO SDK usage in a utility module, but if it directly accesses `window` (for the global wallet), import it dynamically on client side. Using React’s `useEffect` to instantiate and store `globalThis.arweaveWallet` signer after the component mounts is a good approach.

## Displaying Real-Time Updates and AO State in the UI

A compelling feature of AO-based dApps is reacting to state changes from the on-chain processes (actors) in real time. There are several ways to fetch and display process state or outputs:

- **Query Process Results:** Every message sent to an AO process produces a **Result** – a JSON object with any outputs, and any follow-up messages or spawns the process issued in response. You can fetch these results using the AO SDK:

  - Use `result({ process: <ID>, message: <msgID> })` to get the specific result of a given message (by its message ID and the target process ID). This returns an object with `Output` (the process’s response payload, if any), `Messages` (any messages the process sent out), `Spawns` (if it created new processes), and `Error` (if an error occurred). For example, after sending a message, you can call `const res = await result({ process: pid, message: msgId });` and then use `res.Output` to update the UI with the response.
  - Use `results({ process: <ID>, ...pagination })` to get a list of recent results (e.g. the last N results or results in time order). This is useful to display a history of interactions or the latest state changes. You can paginate through results using the returned cursor as shown in the SDK docs.

  In a Next.js app, you might call `results()` on page load (possibly server-side for initial props) to get the current state or recent events, and then subscribe for new ones on the client.

- **Monitoring for New Messages:** The AO network operates asynchronously, but you can simulate “real-time” by polling or subscribing:

  - **Polling:** One simple approach is to periodically call `results({ process: ID })` from the client to see if new results have appeared (perhaps filtering by a tag like an incremental counter or timestamp in the results).
  - **SDK Monitor (Cron):** The `aoconnect` library provides a `monitor()` function, but this is specifically for starting the **Cron message ingestion** on a Messenger Unit. In practice, `monitor()` is used to initiate listening for scheduled (Cron) messages on a process (making sure the process’s scheduled tasks run). It’s not a general WebSocket subscription for all messages. For real-time UI updates not related to cron, you’ll likely use polling or the approach below.
  - **Arweave Subscriptions:** Under the hood, AO messages are posted to Arweave. You could use Arweave’s GraphQL subscription or a service like **ao.link** to watch for new transactions to a given process. For instance, `ao.link` is an explorer that shows live messages and results. However, incorporating this directly is complex; relying on the AO SDK to fetch state is simpler.

- **Direct State Reads (HyperBEAM Patch):** The latest AO architecture (HyperBEAM mainnet) introduces a powerful feature to expose process state via HTTP for **instant reads**. A process can push parts of its state to a special **cache device** so that frontends can fetch it without running a computation each time. In practice:

  - The contract (process) sends a `~patch@1.0` message containing key-value pairs of state data it wants to expose.
  - The HyperBEAM network then makes that data accessible at a REST endpoint. For example, if a process with ID `XYZ` patches a key `balance: 100`, a URL like `https://<hyperbeam-node>/<process-id>~process@1.0/compute/cache/balance` will return `100` immediately.
  - This mechanism **replaces the need for frequent `dryrun` calls** to read state. It’s ideal for things like token balances, leaderboards, or any state that changes and needs to be fetched often.

  For your Next.js app, if the AO process supports patch (you’d know from its documentation or by design), you can simply use `fetch()` to that URL to get live state. For example, a DeFi dashboard might fetch the order book or pool state via a GET request to the process’s exposed state endpoint, achieving real-time updates with minimal latency.

- **Dry-Run (Simulate Read):** If a process doesn’t expose state via patch and you don’t want to post a message, you can use the `dryrun()` function. Dry-run sends a read-only query to a process and returns the result without actually persisting any message or changing state. This is useful for queries like “get balance of X”:

  ```ts
  const res = await dryrun({
    process: "<ProcessID>",
    tags: [
      { name: "Action", value: "Balance" },
      { name: "Account", value: "alice" },
    ],
    data: "",
  });
  console.log("Balance query result:", res.Output);
  ```

  The `dryrun` result structure is the same `Result` object. The important distinction is it doesn’t post a transaction – it just simulates the message on a CU and returns the output directly. This can be invoked from SSR or client to read state on demand. Keep in mind dry-runs still require a signer in mainnet (they are effectively signed HTTP messages). If using `dryrun` on the server, you’d need a key – but often you can design your contract with `~patch` for public data to avoid that requirement.

- **Updating the UI:** Once you obtain result data or state, update your React state accordingly. Because AO is asynchronous, consider using a loading indicator while waiting for a message result. For near-real-time feeds (like a chat or live game state), use a combination of initial data load (`results()` in `getServerSideProps` or on mount) and then polling or subscribing for new results every few seconds. Given Arweave’s transaction finality, there might be a short delay (several seconds) from sending a message to seeing its confirmed result; design your UI/UX to account for this (perhaps optimistic updates or status messages).

**Example – AI Chat Agent:** Suppose you have an AO process that acts as an AI chatbot. Your Next.js frontend could send user questions as messages (with a tag like `{"Action": "Ask", "Question": "Hello?"}`) to the agent process. The agent might respond by returning an output message (e.g. an answer string). Your app would call `message(...)` with the user’s question and then either poll `result()` for the answer or watch the agent’s state. Once the answer is available (the result’s `Output`), you display it in the chat UI. To make this feel real-time, you might show a “typing...” indicator while polling. If the agent frequently updates its state (like streaming partial answers), leveraging the patch device could allow you to fetch those interim results via HTTP without multiple transactions.

**Example – DeFi Dashboard:** For a DEX on AO (like **Botega**, an agent-driven exchange), your Next.js app would let users send trade orders as AO messages (e.g. an order placement with tags `Action: "Swap", Amount: ...`). The DEX processes them and updates its order book state. By using `results()` or an exposed state endpoint, the frontend can retrieve the latest prices, liquidity, etc. If many users trade in real-time, you might rely on patch-based state reads for efficiency, and possibly use WebSockets connected to a service that pushes updates (for advanced use). However, a simpler approach is to periodically refresh the state via the AO SDK or HTTP endpoints, given Arweave’s throughput is not on the order of thousands of TPS.

## Boilerplate Repositories and Templates for AO dApps

To jump-start development, consider using community-supported **boilerplates** that integrate AO with a frontend:

- **`create-ao-dapp`:** A starter kit CLI to scaffold a new AO dApp project. Running `npx create-ao-dapp@latest` sets up a monorepo with a sample AO **backend process** (Lua code, tests, deployment config) and a **React/Next.js frontend** application in TypeScript. The frontend is pre-configured to interact with the example process (for instance, a simple counter or token). This kit simplifies the setup of development environment (including tools like Bun, Docker for building the process) and demonstrates end-to-end integration.

- **`ao-starter-kit` (Autonomous Finance):** The project underlying `create-ao-dapp`. It provides a comprehensive boilerplate with **directory separation** for backend (in `/ao` folder) and frontend (in `/apps` folder). It includes example processes (e.g., a “Hello World” or counter) and a React app that connects to them. This is a great learning resource to see how an AO process is coded and tested, and how the frontend calls it. The README guides through building and deploying the AO process with the CLI (using `aoform` for deployments).

- **`teal-ao-starter`:** Similar to the above, but showcases using **Teal**, a strongly-typed dialect of Lua, for writing AO contracts. This is useful if you prefer type safety in contract logic. The starter includes tooling to compile Teal to Lua and then to WASM for AO. It likely also pairs with a frontend to interact with the Teal-based contract.

- **`create-ao-contract`:** A CLI tool focused on scaffolding just the AO contract side with testing and deployment setup. If you already have a frontend and only need to create a new AO process project (with boilerplate for tests, etc.), this can be handy. It doesn’t generate a frontend, so you’d integrate it with your Next.js app manually.

- **`ao-deploy`:** A script/CLI by Community Labs for automating AO contract deployment (publishing to the network). In a Next.js context, you might use this in your CI or scripts when you update the contract code.

- **Web IDE – BetterIDEa:** An online IDE at **ide.betteridea.dev** with native AO integration. It allows you to write and test AO processes in the browser, and could be useful for quickly prototyping logic which you then integrate into your app. Not directly a boilerplate, but a dev tool.

- **Testing Framework – WAO:** **WAO (Wizard AO)** is an in-memory AO testing SDK. This lets you simulate AO processes and message flows locally (without posting to Arweave) for faster iteration. You can write tests for your process logic that run in Node. While not directly related to the Next.js frontend, having a solid test suite for your AO backend will make integration much smoother (you can be confident the contracts behave as expected when the front-end sends messages).

- **Example Projects:** Reviewing existing AO dApps can provide patterns for integration:

  - **Botega (Autonomous DEX)** – showcases an **autonomous agent** handling trades; likely their frontend (if open source) demonstrates messaging patterns for financial transactions.
  - **AOX (Bridge)** and **Bazar** – other live dApps using AO; they might not have public code, but their behavior can inspire how you design your app’s interactions.
  - **0rbit** (oracle data feeder) – might illustrate how an AO process can be called to fetch external data, and the frontend triggers those calls.
  - **Astro (AstroUSD stablecoin)** – an AO-based stablecoin where frontend shows how to initiate token mint/burn via AO messages.

  Many of these projects are referenced in community blogs and the Awesome-AO repo. While not boilerplates, understanding their architecture can guide your integration (e.g., an AI agent app will have a different UI approach than a DeFi swap, but both use the same core AO connection principles).

### Additional Tips:

- **Security:** Always ensure that signing operations are done through the user’s wallet. Never send private keys to your Next.js server or client. Wander and Beacon are designed to keep keys safe. Also, validate inputs before sending to AO (the network will persist these messages permanently on Arweave).

- **Performance:** Because Next.js can pre-render pages, leverage that for any data that can be fetched without a user signature. For example, a public leaderboard or aggregate stats from an AO process could be fetched in `getStaticProps` or `getServerSideProps` via `results()` or HTTP GET, and included in the HTML. This reduces load on the client. Then, on the client, update dynamically if new info comes in.

- **Consistency:** Remember that AO’s state updates are eventually consistent (relying on Arweave transaction confirmations). Design your UI/UX to handle slight delays. Provide feedback like transaction IDs or links to explorers (e.g., **AO Link** at [ao.link](https://www.ao.link/) can show message status) so power users can verify their actions.

- **Learn from the Community:** The **AO Cookbook** and **Community Labs blog** are excellent resources for up-to-date code examples. The cookbook’s guides for sending messages, reading results, etc., were referenced here and can be consulted for deeper details (e.g., handling errors, advanced messaging patterns). Engaging with the AO builders community (Discord, the `@ao_builders` and `@CommunityLabs` X accounts) can also help as you encounter integration challenges.

By combining Next.js’s robust frontend capabilities with AO’s powerful parallel compute, you can create dApps where users interact through a familiar web interface while complex decentralized logic runs on the AO network. With proper wallet integration and state handling, your application can provide a smooth experience bridging Web2 frontend and Web3 autonomous compute.

**Sources:**

- Official AO Cookbook – _JavaScript aoconnect usage and examples_
- AO Connect SDK Documentation (NPM/Cookbook) – _Connect options, signing, dry-run, etc._
- Wander (ArConnect) Docs – _Wallet permissions and `signDataItem` usage_
- AO Sync SDK (Beacon) README – _Beacon wallet integration features and usage_
- Autonomous Finance AO Starter Kit – _Boilerplate with React app and AO process_
- Awesome AO Repository – _List of starter kits and tools (create-ao-dapp, teal-ao-starter, etc.)_
- HyperBEAM Patch Device Guide – _Exposing process state via HTTP for real-time reads_
