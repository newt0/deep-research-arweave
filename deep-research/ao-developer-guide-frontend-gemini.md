---
title: AO and Frontend Integration
platform: Gemini DeepResearch (gemini-2.5-flash)
date: 2025-07-14
url: deep-research/ao-developer-guide-frontend.md
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

# Technical Investigation: Integrating AO-based Applications with Next.js and TypeScript Frontends

## 1. Introduction to AO and Frontend Integration

This report provides a comprehensive technical investigation into the integration of AO-based applications with modern frontend frameworks, specifically Next.js and TypeScript. The objective is to equip proficient frontend and full-stack developers with the knowledge and practical guidance necessary to build robust decentralized applications (dApps) that seamlessly interact with the AO computing environment.

### 1.1. Understanding AO's Hyper-Parallel Computing Model

AO represents a novel paradigm in decentralized computing, conceived as a singular, unified computing environment operating across a distributed network of heterogeneous nodes. Its architectural design is fundamentally built to support an arbitrary number of parallel processes, which coordinate and interact through an open message-passing layer.1 This design philosophy aims to deliver trustless and cooperative compute services without imposing practical limitations on scale, effectively bridging the verifiable and trust-minimized nature of smart contracts with the immense scalability traditionally associated with centralized cloud computing environments, such as Amazon EC2.1

Unlike conventional blockchain architectures that often face bottlenecks due to sequential processing, AO's hyper-parallel nature allows for concurrent execution of numerous processes. This is achieved by settling all messages, each adhering to a uniform format, onto Arweave's decentralized data layer, thereby creating a resilient computing environment capable of handling diverse workloads and fostering seamless cooperation between processes.1

### 1.2. The Synergy of Next.js and TypeScript for AO dApps

Next.js, a leading React framework, offers a powerful foundation for developing modern web applications. Its feature set includes hybrid static and server-side rendering, integrated CSS support, and robust API routing capabilities, which are crucial for building high-performance and scalable user interfaces.2 The adoption of Next.js for AO dApps allows developers to leverage familiar development patterns and benefit from optimized performance characteristics inherent to the framework.

The integration of TypeScript, a superset of JavaScript, further enhances the development process. TypeScript introduces static type checking, which enables early detection of potential bugs during development, significantly improving code quality, clarity, and maintainability.3 For complex decentralized applications interacting with a nuanced environment like AO, TypeScript's type safety is invaluable in preventing common runtime errors and ensuring data integrity across the application stack. This combination of Next.js's architectural strengths and TypeScript's developer-centric advantages positions them as an ideal pairing for constructing sophisticated and reliable AO dApps.

### 1.3. Report Scope and Key Integration Challenges

This report is exclusively focused on the technical integration of frontend applications with the Arweave AO computing platform. It is important to clarify that the term "AO" can be ambiguous across various technological domains. For instance, "AO" may refer to a specific cryptocurrency (e.g., as tracked on Binance or MEXC 1), or to document management solutions like "AODocs".7 Additionally, various AI-related SDKs and projects also use "AI" or "AO" in their naming conventions.14 This report rigorously filters out and disregards content pertaining to these unrelated "AO" entities, concentrating solely on the Arweave AO computing platform and its associated developer tools and SDKs.

A primary technical challenge in this integration lies in effectively bridging AO's asynchronous, message-passing concurrency model with the typically synchronous and reactive patterns prevalent in modern frontend frameworks like React and Next.js. Developers must navigate the nuances of sending messages to Actors, handling cryptographic signatures, and efficiently querying and displaying real-time state changes from a distributed, eventually consistent system.

## 2. Connecting to AO Actors and Processes

Establishing a connection and interacting with AO Actors and Processes from a Next.js frontend involves utilizing specific SDKs designed for this purpose. The primary tools are @permaweb/aoconnect, @ar.io/sdk, and wao.

### 2.1. Utilizing @permaweb/aoconnect (ao-sdk): The Foundational Interface

The @permaweb/aoconnect library stands as the core JavaScript/TypeScript SDK for direct, low-level interaction with AO Processes. It is engineered to operate seamlessly in both Node.js (server-side) and browser (client-side) environments, making it a versatile choice for Next.js applications.30

#### Initialization and Configuration

Developers can tailor their connection to specific AO components—namely the Messenger Unit (MU), Compute Unit (CU), and GraphQL gateway—by supplying their respective URLs to the connect function. If these URLs are not explicitly provided, the library defaults to standard, predefined endpoints, ensuring a functional connection out-of-the-box.30 This flexibility allows for development against local testnets, custom gateways, or the mainnet.

```TypeScript
import { connect } from "@permaweb/aoconnect";
const { spawn, message, result, dryrun, results, monitor }= connect({
 MU_URL: "https://ao-mu.arweave.net/", // Example Messenger Unit URL
 CU_URL: "https://ao-cu.arweave.net/", // Example Compute Unit URL
 GRAPHQL_URL: "https://arweave.net/graphql", // Example Arweave GraphQL Gateway URL
 GRAPHQL_MAX_RETRIES: 3, // Optional: Number of retries for GraphQL queries
 GRAPHQL_RETRY_BACKOFF: 500, // Optional: Initial backoff for retries in ms
});
```

#### Core API Functions for Process Interaction

The @permaweb/aoconnect library exposes several fundamental functions for interacting with AO processes:

- spawn: This function is used to create and deploy a new AO process onto the network. It necessitates specifying the module (which contains the process's executable code), a scheduler (responsible for orchestrating message execution for the process), and a signer (a cryptographic entity for authenticating the deployment). Developers can also include optional tags and initial data to configure the process upon its creation.30

  ```TypeScript
  const processId= await spawn({ module, scheduler, signer, tags, data });
  ```

- message: This is the primary method for sending data or commands to an existing AO process. It requires the target process ID and a signer for authorization. Optional parameters include an anchor (a 32-byte identifier embedded in the DataItem for traceability), tags (key-value pairs useful for metadata or specifying action types), and data (the actual message payload, often JSON stringified).30

  ```TypeScript
  const messageId= await message({ process, signer, anchor, tags, data });

  ```

- dryrun: The dryrun function enables developers to simulate a message execution against an AO process without committing any changes to the network state. This capability is invaluable for reading the current memory state of a process (e.g., querying a token balance or a specific data point) or predicting the outcome of an action before a potentially costly or state-altering transaction is dispatched. It returns a Result object containing the simulated output.30

  ```TypeScript
  const dryRunResult= await dryrun({
  process: 'PROCESS_ID',
  tags:, // Example: Requesting a balance
  data: '', // Optional data payload for the dry run
  });
  console.log("Dry run output:", dryRunResult.Output);
  ```

- result: This function is utilized to retrieve the definitive outcome of a specific message that has already been evaluated and finalized by an AO Compute Unit. By providing the message ID and the process ID, developers can fetch detailed results, including any Messages generated, new Spawns, the Output of the computation, and any Error information.30

  ```TypeScript
  let { Messages, Spawns, Output, Error }= await result({
  message: "MESSAGE_ID_TO_QUERY",
  process: "PROCESS_ID",
  });
  ```

- results: Designed for fetching a batch of results from a process, the results method is particularly suitable for implementing polling mechanisms to retrieve new updates or historical data. It supports pagination and sorting through parameters such as from (a cursor indicating the starting point), to (a cursor for the ending point), sort (ascending or descending order), and limit (the number of results to return per call).30

  ```TypeScript
  let newMessages= await results({
  process: "PROCESS_ID",
  from: lastSeenCursor, // Cursor from the last fetched message
  sort: "ASC", // Ascending order for new messages
  limit: 25, // Fetch up to 25 new messages
  });
  ```

- monitor: This function allows the initiation of a subscription-like service to continuously ingest "cron messages" from a specified AO process.30 This is a critical capability for building reactive frontends that display real-time updates based on scheduled or continuous events emitted by an AO Actor, enabling dynamic user interfaces.
  ```TypeScript
  const subscription= await monitor({ process: "PROCESS_ID", signer });
  // The 'subscription' object likely provides an event listener for incoming messages.
  // Example: subscription.on('message', (msg)=\> console.log(msg));
  ```

#### Environment Setup for Next.js

The @permaweb/aoconnect library is distributed in both ESM (ECMAScript Modules) and CJS (CommonJS) formats, ensuring broad compatibility across various JavaScript environments, including modern Next.js applications.30 For server-side operations within Next.js or when dealing with specific Webpack bundling configurations, it may be necessary to explicitly import the Node.js-compatible version of the library. For example, one might use

`import { createSigner, message } from "@permaweb/aoconnect/node"; to ensure proper resolution in a Node.js context.30`

### 2.2. Leveraging @ar.io/sdk: Broader Ecosystem Interactions

The @ar.io/sdk is a distinct SDK primarily designed for interacting with the broader ar.io ecosystem. This includes functionalities related to gateways, observers, and the Arweave Name Service (ArNS), in addition to its capabilities concerning AO.32 While it does not directly replace

@permaweb/aoconnect for core AO process interactions, it provides complementary utilities that are essential for building a comprehensive dApp within the Arweave and AO ecosystem.

Developers can initialize the SDK to create either read-only or writeable clients using ARIO.init({ signer }). Providing a signer enables additional write APIs that require cryptographic signing, such as joinNetwork and delegateStake.32 The SDK also offers methods like

getInfo() to retrieve information about the ar.io process itself, providing insights into the network's status and configuration.32

### 2.3. Streamlining Development with wao (Wizard AO SDK)

wao is positioned as a developer-centric SDK that significantly streamlines Arweave/AO development by offering elegant syntax enhancements and seamless message piping.33 It aims to simplify common development patterns and make the coding experience more enjoyable, including facilitating GraphQL operations.

#### Accelerated Testing

A standout feature of wao is its "drop-in aoconnect replacement for tests." This functionality allows Lua scripts, which form the basis of AO processes, to be tested entirely in memory. This in-memory execution is remarkably fast, achieving speeds up to 1000 times faster than testing on the mainnet and 100 times faster than using local development environments like arlocal or ao-localnet.33 This drastic reduction in test execution time dramatically shortens the development feedback loop, enabling more rapid iteration and debugging.

#### Production Code Integration

The AO class within wao is designed for versatility, suitable for both in-memory testing and deployment in production code. This consistency means that once developers are familiar with the wao API for testing, they do not need to learn a separate set of APIs for production, as the interfaces remain identical to @permaweb/aoconnect.33

#### Simplified Message Handling

wao introduces convenient parameters that abstract away common complexities in message handling. The get parameter simplifies "cherry-picking outputs" from complex message results, allowing developers to easily extract specific pieces of data from returned messages with multiple spawned outputs. The check parameter simplifies "determining message success" by automatically tracking down chains of asynchronous messages and lazy-evaluating whether predefined check conditions are met. These features significantly reduce the amount of boilerplate code typically required for parsing results and verifying message outcomes.33

```TypeScript
import { AO, acc } from "wao"; // For production code
const signer= acc.signer; // Example: using a pre-generated test account signer
const myProcess= new AO({ process: "YOUR_PROCESS_ID", signer });

// Send a message and automatically check if 'Data' exists in the reply
await myProcess.m("ActionMessage", { check: true });

// Send a message and extract a specific piece of data
const extractedData= await myProcess.m("QueryMessage", { get: "SpecificTagValue" });
```

The simultaneous existence of @permaweb/aoconnect as the core protocol interface, @ar.io/sdk for broader ecosystem interactions, and wao as a developer experience (DX) layer highlights a maturing ecosystem. The development of wao specifically addresses common pain points in blockchain development, such as slow testing cycles and complex result parsing. This indicates a strategic investment by the AO community in tools that enhance development efficiency and enjoyment. For Next.js developers, this layered toolset offers a richer experience. While @permaweb/aoconnect is indispensable for direct protocol interaction, leveraging wao can significantly accelerate development and testing cycles, particularly for complex AO processes. This allows developers to choose the level of abstraction that best suits their project's needs, promoting faster iteration and higher quality dApps.

## 3. Client-Side Wallet Connection and Signature Handling

Integrating wallets securely with Next.js and TypeScript frontends is paramount for AO applications, enabling users to connect, sign transactions, and interact with Actors. This section details the integration of prominent wallets like Wander and Beacon, focusing on secure connection and signature handling.

### 3.1. Wander (formerly ArConnect) Integration

Wander, previously known as ArConnect, is a non-custodial wallet designed natively for Arweave and AO assets. It functions as a browser extension, a mobile application, and an embedded smart account, offering users a secure and intuitive method to interact with dApps without exposing their private keys.34

#### Integration with @project-kardeshev/ao-wallet-kit

For Next.js and TypeScript applications, the @project-kardeshev/ao-wallet-kit is the recommended solution for integrating Wander and other Arweave-compatible wallets. This kit provides a unified API, abstracting away wallet-specific implementation details and simplifying the developer experience.34

#### Provider Setup

To enable wallet functionality across the entire application, the Next.js application should be wrapped with the<AOWalletKit\> provider component. This provider allows for extensive configuration, including defining required permissions (e.g., ACCESS_ADDRESS, SIGN_TRANSACTION, DISPATCH), providing application metadata (name, logo), configuring the Arweave gateway, and customizing the UI theme to match the dApp's aesthetic.36

```TypeScript
// In your_app.tsx or layout.tsx
import { AOWalletKit } from '@project-kardeshev/ao-wallet-kit';
import type { AppProps } from 'next/app';

function MyApp({ Component, pageProps }: AppProps) {
return (
<AOWalletKit
config={{
        permissions:, // Request necessary permissions
        ensurePermissions: true, // Ensure all requested permissions are granted
        appInfo: { name: "My AO dApp", logo: "/logo.png" },
        gatewayConfig: { host: "arweave.net", port: 443, protocol: "https" },
      }}
theme={{
        displayTheme: "dark", // Or "light"
        accent: { r: 100, g: 150, b: 200 }, // Custom accent color
      }}
>
<Component {...pageProps} />
</AOWalletKit>
);
}
```

export default MyApp;

#### TypeScript Type Support

To ensure robust type safety when developing with Wander/ArConnect, developers should install the arconnect npm package using npm i-D arconnect or yarn add-D arconnect. The TypeScript definitions provided by this package can then be included in the project's tsconfig.json or by adding `<reference types="arconnect" />` to the env.d.ts file, enabling compile-time checks and autocompletion.34

#### Signature Handling

The @project-kardeshev/ao-wallet-kit manages the underlying interactions with window.arweaveWallet, which is the API injected by browser extensions like Wander. It leverages wagmi internally to provide a consistent and abstracted signing experience across various supported wallets.36 While direct examples of

window.arweaveWallet usage within the wanderwallet/Wander GitHub repository were not explicitly detailed in the provided information 37, the kit's purpose is to abstract this complexity, allowing developers to focus on the dApp's core logic.

### 3.2. Beacon Wallet Integration

Beacon is another secure, non-custodial wallet designed to facilitate interactions with both Arweave and AO. It offers a suite of features including streamlined asset management, shared wallets for collaborative fund management, smart notifications, and a crucial "AO-Sync" capability. AO-Sync enables dApps to connect to AO applications securely, ensuring that the user's private key never leaves their device.39

#### Integration with @vela-ventures/ao-sync-sdk

The dedicated JavaScript/TypeScript SDK for integrating with Beacon Wallet for Arweave and AO-based applications is @vela-ventures/ao-sync-sdk.41 This SDK is designed to delegate complex operations such as signing, encryption, and other cryptographic logic directly to the Beacon Wallet, enhancing security and simplifying dApp development.

#### Connection and Authentication

To establish a connection with Beacon Wallet, developers instantiate a WalletClient and invoke its connect method. This method supports requesting various permissions (e.g., ACCESS_ADDRESS, ACCESS_PUBLIC_KEY, SIGN_TRANSACTION) and can generate a QR code for mobile wallet authentication. It requires specifying application information (name, logo) and the Beacon broker URL to facilitate the connection.41

```TypeScript
import WalletClient from "@vela-ventures/ao-sync-sdk";
import { useEffect, useState } from 'react';

const useBeaconWallet= ()=\> {
const[walletClient, setWalletClient\]= useState\<WalletClient | null\>(null);
const[isConnected, setIsConnected\]= useState(false);

useEffect(()=\> {
const client= new WalletClient();
setWalletClient(client);

    client.on("connected", (data)=\> {
      console.log("Beacon Wallet connected:", data);
      setIsConnected(true);
    });
    client.on("disconnected", (data)=\> {
      console.log("Beacon Wallet disconnected:", data);
      setIsConnected(false);
    });

    return ()=\> {
      // Cleanup listeners if component unmounts
      client.disconnect();
    };

},);

const connectWallet= async ()=\> {
if (walletClient) {
try {
await walletClient.connect({
permissions:,
appInfo: { name: "My AO Beacon App", logo: "https://myapp.com/logo.png" },
gateway: { host: "arweave.net", port: 443, protocol: "https" },
brokerUrl: "wss://aosync-broker-eu.beaconwallet.dev:8081", // Beacon's MQTT broker
});
} catch (error) {
console.error("Failed to connect Beacon Wallet:", error);
}
}
};

const disconnectWallet= async ()=\> {
if (walletClient) {
await walletClient.disconnect();
}
};

return { walletClient, isConnected, connectWallet, disconnectWallet };
};
```

#### Signature Handling

Once a connection is established, the walletClient provides methods to securely sign transactions and data items. The signTransaction(transactionData) method is used for signing Arweave transactions, while signDataItem(dataItem) is for signing arbitrary data items. In both cases, the actual signing operation is securely delegated to the Beacon Wallet, ensuring that private keys remain on the user's device.41

```TypeScript
// Example: Signing an Arweave transaction or DataItem using Beacon
const handleSign= async (transactionOrDataItem: any)=\> {
if (walletClient && isConnected) {
try {
const signedResult= await walletClient.signTransaction(transactionOrDataItem); // Or signDataItem
console.log("Signed result:", signedResult);
// Further dispatch the signed transaction/data item
} catch (error) {
console.error("Signing failed:", error);
}
}
};
```

#### QR Code Authentication and Reconnect

The connect method of the Beacon SDK generates a QR code, which serves as a convenient mechanism for initial authentication, particularly for mobile wallet users. Furthermore, the SDK supports automatic reconnection using stored session data. This feature significantly enhances the user experience by eliminating the need for repeated QR code scans for established sessions, allowing users to seamlessly resume their interactions with the dApp.41

### 3.3. General Signature Handling with createSigner from @permaweb/aoconnect

Beyond the specialized wallet SDKs, the @permaweb/aoconnect library offers a versatile createSigner API. This function provides a lower-level, more direct approach to integrating signing capabilities. Given a wallet object (e.g., window.arweaveWallet from a browser extension or a JWK for Node.js environments), createSigner returns a signer function. This returned signer can then be directly passed to aoconnect methods such as message or spawn to cryptographically sign the underlying DataItems or HTTP Signed Messages, enabling authenticated interactions with AO processes.30

```TypeScript
import { createSigner } from "@permaweb/aoconnect";

// For browser environments (e.g., with Wander/ArConnect extension)
const browserSigner= createSigner(globalThis.arweaveWallet);

// For Node.js environments (using a JWK wallet)
// import fs from "node:fs";
// const walletJwk= JSON.parse(fs.readFileSync('path/to/wallet.json').toString());
// const nodeSigner= createSigner(walletJwk);
```

The presence of multiple distinct wallet solutions (Wander, Beacon), each with their own SDKs (@project-kardeshev/ao-wallet-kit, @vela-ventures/ao-sync-sdk), alongside the foundational createSigner from @permaweb/aoconnect, illustrates a developing and increasingly modular wallet ecosystem for AO. The fact that @project-kardeshev/ao-wallet-kit leverages wagmi suggests a strategic move towards unifying the developer experience, akin to how wagmi standardizes Ethereum wallet connections. This modularity offers developers flexibility but also necessitates understanding the nuances of each wallet and its respective SDK. Higher-level kits like ao-wallet-kit are crucial for abstracting wallet-specific complexities, thereby simplifying the integration process for dApp builders. This trend towards abstraction is a positive development for broader adoption, as it lowers the barrier to entry for developers accustomed to more unified Web2 or EVM-based Web3 development patterns.

Table 1: Wallet SDK Comparison for AO Integration

| SDK Name                                | Supported Wallet(s)                                          | Key Features                                                                       | Core Integration Method                    | Signature Handling Methods                                | Next.js/TypeScript Specifics                                |
| :-------------------------------------- | :----------------------------------------------------------- | :--------------------------------------------------------------------------------- | :----------------------------------------- | :-------------------------------------------------------- | :---------------------------------------------------------- |
| @project-kardeshev/ao-wallet-kit        | Wander (ArConnect), Arweave.app, MetaMask, Phantom           | Non-custodial, Customizable UI/Theme, Permissions Management, Internal Wagmi usage | React Provider Component (\<AOWalletKit\>) | signTransaction, signDataItem (via wallet client)         | React Hooks, TypeScript Definitions (arconnect npm package) |
| @vela-ventures/ao-sync-sdk              | Beacon Wallet                                                | Non-custodial, QR Code Authentication, Reconnect Support                           | Class-based WalletClient                   | signTransaction, signDataItem (via wallet client)         | Event-driven architecture, TypeScript support               |
| @permaweb/aoconnect (with createSigner) | Any wallet injecting window.arweaveWallet or providing a JWK | Direct control over signing, Lower-level integration                               | Direct function calls (createSigner)       | createSigner returns a signer function for message, spawn | Browser/Node.js compatible versions, TypeScript support     |

This comparative table provides a concise overview of the primary wallet integration SDKs for AO, assisting developers in selecting the most suitable option for their Next.js dApp based on features and integration patterns. Choosing the right wallet integration is foundational for any dApp, and this table allows developers to quickly assess the strengths and weaknesses of each SDK in the context of AO, optimizing their decision-making process and preventing wasted effort on incompatible or less-than-ideal solutions.

## 4. Sending Messages and Interacting with Actors from the Browser

Interacting with AO Actors from a browser-based Next.js application involves sending messages, which serve as the primary mechanism for communication and state changes within the AO computing environment. This section explores both low-level SDK functions and higher-level abstractions for these interactions.

### 4.1. Direct Interaction with @permaweb/aoconnect Functions

The message function, provided by the @permaweb/aoconnect library, is the cornerstone for sending data and commands to AO Actors directly from a browser-based Next.js frontend.30 This function facilitates the dispatch of arbitrary data and tags to a specified AO

process ID, requiring a signer object (typically obtained from a connected wallet) to cryptographically authenticate the message.

```TypeScript
// Assuming 'aoConnect' is an initialized instance from connect()
// And 'activeSigner' is obtained from a wallet (e.g., Wander, Beacon)
async function sendMessageToActor(processId: string, action: string, dataPayload: any) {
try {
const messageId= await aoConnect.message({
process: processId,
signer: activeSigner,
tags:[{ name: 'Action', value: action }\],
data: JSON.stringify(dataPayload), // Data is often JSON stringified
});
console.log(\`Message sent with ID: ${messageId}\`);
return messageId;
} catch (error) {
console.error("Error sending message:", error);
throw error;
}
}
```

For scenarios demanding more fine-grained control over the signing and dispatch process, @permaweb/aoconnect also offers the signMessage and sendSignedMessage functions. signMessage prepares and signs an AO message, returning a signed message object without immediately sending it to the network. This signed object can then be dispatched at a later time using sendSignedMessage. This two-step process can be advantageous for implementing transaction batching, deferred execution, or integrating with custom signing flows that require user confirmation or additional processing before broadcast.30

```TypeScript
// Example: Prepare and sign a message, then dispatch later
async function prepareAndSend(processId: string, data: string) {
const signedMessage= await aoConnect.signMessage({
process: processId,
signer: activeSigner,
data: data,
});
console.log("Message signed, ready for dispatch.");
//... later...
const dispatchedId= await aoConnect.sendSignedMessage(signedMessage);
console.log(\`Signed message dispatched with ID: ${dispatchedId}\`);
}
```

### 4.2. Streamlined Interaction with wao

wao (Wizard AO SDK) provides a more developer-friendly and concise interface for interacting with AO processes, building upon the foundational functionalities of aoconnect. Its message function (often aliased for brevity, such as p.m in examples) simplifies common tasks by allowing direct, inline checks for message success or the extraction of specific data points from the response. This is achieved through the check and get parameters, which significantly reduce the amount of boilerplate code typically required for message interactions and result parsing.33

```TypeScript
import { AO } from "wao"; // For production use
// Assuming 'aoProcess' is an initialized AO instance from wao
// const aoProcess= new AO({ process: "YOUR_PROCESS_ID", signer: activeSigner });

// Send a message and automatically check if the operation was successful
await aoProcess.m("PerformAction", { check: true });

// Send a query message and extract a specific 'Data' field from the reply
const responseData= await aoProcess.m("QueryData", { get: "Data" });
console.log("Queried data:", responseData);
```

### 4.3. Higher-Level Abstractions: ankushKun/aoxpress and ao-fetch

The ankushKun/aoxpress framework, in conjunction with ao-fetch, introduces a higher-level abstraction for interacting with AO processes. This framework draws inspiration from the familiar Express.js API syntax, aiming to simplify the definition and invocation of handlers on AO Actors. ao-fetch serves as the client-side library for communicating with these aoxpress-defined handlers from JavaScript/TypeScript, allowing frontend developers to interact with them almost as if they were traditional REST API endpoints.42

The roadmap for aoxpress includes ambitious features such as a middleware system, integrated authentication handling, dynamic routing, and even the ability to return HTML pages directly from AO Actors. This vision suggests a future where AO Actors could serve more complex web functionalities directly, potentially lowering the cognitive load for developers transitioning from traditional web development to the AO paradigm.42

The evolution from direct, low-level message passing with aoconnect to convenience wrappers like wao, and further to API-like abstractions such as aoxpress, demonstrates a clear trajectory towards simplifying the developer's interaction model with AO. This progression mirrors the historical development of web technologies, from raw HTTP requests to more structured and developer-friendly interfaces like RESTful APIs and GraphQL. This trend suggests that as the AO ecosystem matures, developers can anticipate increasingly sophisticated and familiar tools that abstract away the unique complexities of message-passing concurrency. For Next.js developers, this implies a smoother learning curve and potentially faster development of rich, interactive dApps, as they can leverage patterns closer to their existing web development expertise, rather than needing a deep understanding of the underlying AO protocol for every interaction.

## 5. Displaying Real-time Updates and State Responses from AO

For dynamic dApp frontends, efficiently querying the state of AO processes and receiving real-time updates or message outputs is critical. This section outlines the primary methods for achieving this.

### 5.1. Querying Process State with dryrun

To retrieve the current state or specific data from an AO process without initiating a state-changing transaction, the dryrun method from @permaweb/aoconnect is the primary tool.30 This function executes a message against the process's current memory state, providing an immediate

Result object without saving any changes to the network. It is ideal for displaying dynamic content such as current token balances, configurations, or predicting the outcome of a hypothetical operation before committing it.

```TypeScript
import { dryrun } from "@permaweb/aoconnect";

async function fetchActorState(processId: string, queryAction: string) {
try {
const response= await dryrun({
process: processId,
tags:[{ name: 'Action', value: queryAction }\],
// Other optional parameters like data, anchor
});
// The 'response' object contains Messages, Spawns, Output, Error
// Developers would typically parse response.Output or specific Messages/Tags for display
return response.Output;
} catch (error) {
console.error(\`Error querying state for ${processId}:\`, error);
return null;
}
}
```

### 5.2. Listening for Message Outputs: Polling and Monitoring

#### Polling with results

For displaying a stream of historical or recent messages and state changes, the results method from @permaweb/aoconnect can be employed as an efficient polling mechanism.30 This method allows developers to fetch a batch of messages from a specific process, enabling them to retrieve new data since a last-seen cursor, sort the results (ascending or descending), and limit the number of messages returned per poll. This approach is well-suited for activity feeds, transaction histories, or periodically updated dashboards where near real-time updates are sufficient.

```TypeScript
import { results } from "@permaweb/aoconnect";
import { useState, useEffect } from 'react';

function useAoProcessMessages(processId: string, pollIntervalMs: number= 5000) {
const[messages, setMessages\]= useState\<any\>();
const[lastCursor, setLastCursor\]= useState\<string\>('');

useEffect(()=\> {
const fetchMessages= async ()=\> {
try {
const response= await results({
process: processId,
from: lastCursor,
sort: "ASC", // Get messages in ascending order
limit: 10,
});
if (response.Messages && response.Messages.length> 0) {
setMessages(prev=\>[...prev,...response.Messages\]);
setLastCursor(response.Messages\[response.Messages.length- 1\].Id);
}
} catch (error) {
console.error("Error fetching AO messages:", error);
}
};

    const intervalId= setInterval(fetchMessages, pollIntervalMs);
    // Initial fetch
    fetchMessages();

    return ()=\> clearInterval(intervalId); // Cleanup on unmount

},[processId, pollIntervalMs, lastCursor\]); // Re-run effect if these dependencies change

return messages;
}
// Usage in a Next.js component:
// const myProcessMessages= useAoProcessMessages("YOUR_PROCESS_ID");
```

#### Subscribing to Cron Messages with monitor

For scenarios demanding more immediate or event-driven updates, particularly from scheduled or recurring events emitted by an AO process, the monitor method can be utilized.30 This function initiates a subscription service to ingest these "cron messages," allowing for near real-time updates in the frontend without the overhead of constant polling. The precise implementation of handling the

monitor stream (e.g., via WebSockets or server-sent events) would depend on the underlying gateway's capabilities and exposed interfaces.

```TypeScript
import { monitor, createSigner } from "@permaweb/aoconnect";

async function subscribeToAoProcess(processId: string, walletSigner: any) {
try {
const subscription= await monitor({
process: processId,
signer: createSigner(walletSigner), // Requires a signer for authentication
});

    // The 'subscription' object is an event emitter or stream
    // Developers would typically attach listeners to handle incoming messages
    subscription.on('message', (message: any)=\> {
      console.log("Received real-time message from AO:", message);
      // Update Next.js component state or use a global state management solution
    });

    console.log(\`Subscribed to process ${processId} for real-time updates.\`);
    return subscription;

} catch (error) {
console.error(\`Error subscribing to process ${processId}:\`, error);
throw error;
}
}
```

### 5.3. Architectural Considerations for Next.js Real-time Display

In a Next.js application, real-time updates from AO are primarily managed within client-side components. React's useState and useEffect hooks are fundamental for managing and displaying incoming data dynamically. For more complex applications, a global state management library (e.g., Zustand, Jotai, or React Context) can be employed to centralize and distribute real-time data across the component tree. It is important to note that Next.js Server Components (introduced in Next.js 13+) are generally suited for static or infrequently changing data, whereas client components are necessary for dynamic, interactive, and real-time UI updates that rely on continuous data streams.

The monitor function for "cron messages" and the results function for polling define the current real-time capabilities within the AO ecosystem.30 This approach differs from traditional WebSocket implementations that provide a continuous stream of all granular state changes. The

ao-emulator 43, while a backend tool, illustrates the underlying need for continuous state reconciliation to achieve a truly "real-time" view of a process. Achieving a truly dynamic and low-latency real-time experience in an AO dApp frontend often involves a combination of these methods:

dryrun for instant reads, results for periodic updates and historical data, and monitor for specific event streams. Developers should be aware that the "real-time" nature is currently more akin to efficient event-based subscriptions and polling rather than a constant, granular state stream for every process. The effectiveness of monitor also depends on the underlying gateway's implementation of cron message delivery.

## 6. Boilerplate Repositories and Frontend Templates for AO-Integrated dApps

To accelerate the development of AO-integrated dApps with Next.js and TypeScript, several boilerplate repositories and frontend templates offer valuable starting points. These resources streamline setup and provide pre-configured environments.

### 6.1. micovi/create-ao-dapp: A Comprehensive Full-Stack Starter

The micovi/create-ao-dapp repository provides a comprehensive boilerplate for developing full-stack AO dApps. It is structured to encompass both the AO backend processes, typically written in Lua, and a React frontend application, offering a holistic starting point for new projects.44

#### Structure and Tooling

The repository systematically organizes backend processes within the ./ao directory and frontend applications within the ./apps directory. It outlines essential prerequisites such as Bun (a fast JavaScript all-in-one toolkit), LuaRocks (a package manager for Lua modules), Busted (a unit testing framework for Lua), and Docker (required for the build process). The boilerplate details commands for building and testing AO processes, and deployment is facilitated through AOForm, a tool for deploying sets of processes to AO.44 The inclusion of TypeScript, accounting for 6.1% of the codebase, indicates a commitment to type safety and modern development practices in the frontend.44 This boilerplate is ideal for developers seeking a complete, opinionated setup that covers both the AO backend logic and the Next.js frontend integration from the ground up, significantly reducing initial configuration overhead.

### 6.2. weavedb/arnext: Bridging Vercel Performance and Arweave Permanence

ArNext is a Next.js-based framework specifically engineered to enable developers to deploy the same application codebase on both Vercel and Arweave.45 This dual deployment strategy allows dApps to leverage Vercel's performance optimizations, such as Server-Side Rendering (SSR), Incremental Static Regeneration (ISR), and Edge CDN, while simultaneously benefiting from Arweave's inherent immutability and censorship resistance, serving as a permanent backup.

#### Addressing PermaApp Limitations

ArNext directly addresses common limitations associated with traditional "PermaApps" (Single-Page Applications deployed directly on Arweave). These limitations often include slow loading of dynamic content due to the absence of SSR, issues with client-side hash routing, and the inability to generate dynamic social media cards, which are crucial for discoverability and engagement.45

#### Hybrid Routing

The framework functions as a multi-page SPA, offering robust SSR capabilities when deployed on Vercel and seamless client-side routing when accessed on Arweave. ArNext provides custom utilities, including Link, useParams, and useRouter, to ensure consistent routing behavior between Next.js's native router and react-router-dom on Arweave, mitigating common navigation challenges.45

ArNext is a crucial tool for Next.js developers who require both the high performance and SEO benefits of traditional web hosting and the immutability and censorship resistance of Arweave for their AO-integrated dApps.

### 6.3. @project-kardeshev/ao-wallet-kit: A Core Wallet Integration Component

While not a full dApp boilerplate, the @project-kardeshev/ao-wallet-kit serves as an essential boilerplate _component_ for any AO-integrated Next.js application.36 It significantly simplifies the complex process of connecting various Arweave-compatible wallets, including Wander (formerly ArConnect), Arweave.app, MetaMask, and Phantom, to the frontend.

#### Unified API

The kit provides a unified API and customizable React components, such as the<AOWalletKit\> provider, for streamlined wallet connection. This abstraction considerably reduces the development effort required for implementing multi-wallet support, allowing developers to focus more on the core logic and user experience of their AO dApp.36

### 6.4. Autonomous-Finance/teal-ao-starter: Typed Backend for AO Processes

The Autonomous-Finance/teal-ao-starter repository focuses on the backend development of AO processes. It provides a starter kit for writing AO Actors using Teal, a superset of Lua that introduces strong typing.46 This offers a development workflow analogous to using TypeScript in JavaScript web development, bringing type safety to the backend logic.

#### Typed Lua Development

The kit facilitates writing type-safe Lua code for AO processes, includes an ao type definition for native AO globals, and leverages tools like Cyan (for Teal compilation) and Squish (for Lua file amalgamation into a single output file suitable for AO deployment).46 While not a frontend boilerplate, this starter kit is highly complementary to Next.js frontend development. It enables the creation of robust, type-safe AO backend processes that the frontend can reliably interact with, improving the overall quality and maintainability of the full-stack dApp.

### 6.5. General Next.js Boilerplates as a Starting Point

Developers can also initiate their AO dApp development by utilizing general-purpose Next.js boilerplates. These include those provided by create-next-app and various Vercel templates.2 Such boilerplates typically come pre-configured with essential modern web development tools, including TypeScript, popular styling frameworks like Tailwind CSS, authentication setups, and comprehensive testing environments.

#### Approach

The approach involves layering the AO-specific integration (SDKs, wallet kits, interaction patterns) on top of this solid, general-purpose Next.js foundation. This strategy offers maximum flexibility, allowing developers to leverage familiar Next.js best practices while gradually incorporating AO-specific functionalities.

The landscape of AO-related boilerplates and starter kits shows a clear trend towards specialization rather than a single monolithic solution. This is evident from the existence of full-stack dApp starters (create-ao-dapp 44), deployment-focused frameworks (
arnext 45), component-level kits for critical functions (ao-wallet-kit 36), and even backend-specific development environments (teal-ao-starter 46). This modularity contrasts with earlier blockchain ecosystems that often relied on single, all-encompassing frameworks. This specialization is a hallmark of a maturing ecosystem, allowing developers to compose their development stack from best-of-breed tools for each layer (frontend, backend, deployment, wallet). For Next.js developers, this means greater flexibility and the ability to optimize for specific project requirements. However, it also implies a need for a deeper understanding of how these various specialized tools interoperate to form a cohesive AO dApp.

Table 2: Recommended AO dApp Boilerplates

| Boilerplate/Kit Name               | Primary Focus                     | Key Technologies                                                 | Key Benefits                                                                                                      | GitHub/NPM Link                                                                                                             |                                                                                                               |
| :--------------------------------- | :-------------------------------- | :--------------------------------------------------------------- | :---------------------------------------------------------------------------------------------------------------- | :-------------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------ |
| micovi/create-ao-dapp              | Full-stack AO dApp development    | Next.js, React, TypeScript, Lua, AOForm, Docker                  | Comprehensive setup for both frontend and backend, pre-configured tooling                                         | [github.com/micovi/create-ao-dapp](https://github.com/micovi/create-ao-dapp) 44                                             |                                                                                                               |
| weavedb/arnext                     | Hybrid Next.js/Arweave deployment | Next.js, React, Vercel, Arweave                                  | Enables high performance (Vercel) and permanence (Arweave) from a single codebase, addresses PermaApp limitations | [github.com/weavedb/arnext](https://github.com/weavedb/arnext) 45                                                           |                                                                                                               |
| @project-kardeshev/ao-wallet-kit   | Unified Wallet Integration        | React, TypeScript, Wagmi, Wander, Arweave.app, MetaMask, Phantom | Simplifies multi-wallet connection and signature handling with a unified API and customizable UI                  | [npmjs.com/package/@project-kardeshev/ao-wallet-kit](https://www.npmjs.com/package/%40project-kardeshev%2Fao-wallet-kit) 36 |                                                                                                               |
| Autonomous-Finance/teal-ao-starter | Type-safe AO Backend Development  | Lua, Teal, Cyan, Squish                                          | Introduces strong typing to Lua-based AO processes, improving backend robustness and maintainability              | [github.com/Autonomous-Finance/teal-ao-starter](https://github.com/Autonomous-Finance/teal-ao-starter) 46                   |                                                                                                               |
| General Next.js Boilerplate        | Standard Web App Foundation       | Next.js, React, TypeScript, Tailwind CSS, Authentication         | Provides a robust, familiar starting point for web development, allowing AO integration to be layered on top      | [nextjs-boilerplate.com](https://nextjs-boilerplate.com/) 47,                                                               | [vercel.com/templates/next.js/nextjs-boilerplate](https://vercel.com/templates/next.js/nextjs-boilerplate) 48 |

This table serves as a decision matrix for developers. By presenting a concise summary of each boilerplate's focus, included technologies, and benefits, it empowers them to quickly identify the most suitable starting point for their project, whether they require a full-stack solution, a specific deployment strategy, or a component-level integration.

## 7. Conclusion

### 7.1. Summary of Key Integration Strategies and Tools

The technical investigation into integrating AO-based applications with Next.js and TypeScript frontends reveals a developing yet increasingly sophisticated ecosystem of tools and strategies. The @permaweb/aoconnect library stands as the foundational SDK, providing essential functions for direct interaction with AO Actors and Processes. This includes spawn for deploying new processes, message for sending data and commands, dryrun for querying current state without committing changes, and results/monitor for retrieving message outputs and facilitating real-time updates.

Client-side wallet connectivity and secure signature handling are effectively managed through specialized SDKs. The @project-kardeshev/ao-wallet-kit offers a unified approach for integrating various Arweave-compatible wallets, including Wander (formerly ArConnect), simplifying complex wallet interactions. Concurrently, the @vela-ventures/ao-sync-sdk provides dedicated integration for the Beacon Wallet, emphasizing secure, non-custodial interactions and QR code authentication. Both kits abstract complex cryptographic operations, significantly enhancing the user and developer experience.

The developer experience is further improved by higher-level abstractions built upon these foundations. wao (Wizard AO SDK) streamlines development and testing with its elegant syntax, simplified message parsing, and remarkably faster in-memory test execution. Emerging frameworks like ankushKun/aoxpress and ao-fetch promise even more familiar, Express.js-like API interactions with AO Actors, aiming to reduce the learning curve for web developers.

For jumpstarting development, several valuable boilerplate repositories and templates are available. micovi/create-ao-dapp offers a comprehensive full-stack setup, encompassing both AO backend processes and a React frontend. weavedb/arnext provides a unique solution for deploying Next.js applications with both Vercel's performance optimizations and Arweave's permanence. Furthermore, component-level kits like @project-kardeshev/ao-wallet-kit modularize the development process, allowing developers to integrate specific functionalities efficiently.

### 7.2. Future Outlook for AO Frontend Development

The current state of AO frontend integration reflects a rapidly evolving ecosystem. The clear trajectory is towards the development of increasingly sophisticated abstraction layers and specialized tools that simplify the inherent complexities of decentralized computing. This strong focus on developer experience is crucial for broader adoption beyond early pioneers, as it lowers the barrier to entry for developers accustomed to more traditional web development paradigms.

As the ecosystem matures, it is anticipated that unified wallet kits will become even more robust, offering broader compatibility and more seamless user flows. Interaction frameworks are expected to provide even more expressive and familiar paradigms, further streamlining the integration process and allowing developers to build rich, interactive dApps with less friction. However, the challenge of disambiguating "AO" from other unrelated technologies in search results and documentation will likely persist, underscoring the ongoing need for clear, precise information and community-driven knowledge sharing. The modular and specialized nature of the current tooling indicates a healthy ecosystem growth, enabling developers to compose their development stack from best-of-breed tools for each layer, ultimately fostering innovation and accelerating the development of the next generation of permanent, hyper-parallel applications.

#### 引用文献

1. AO price today, AO to USD live price, marketcap and chart | CoinMarketCap, 7 月 14, 2025 にアクセス、 [https://coinmarketcap.com/currencies/ao/](https://coinmarketcap.com/currencies/ao/)
2. Next.js by Vercel- The React Framework, 7 月 14, 2025 にアクセス、 [https://nextjs.org/](https://nextjs.org/)
3. Next.js With TypeScript Development- Capicua, 7 月 14, 2025 にアクセス、 [https://www.capicua.com/blog/nextjs-with-typescript](https://www.capicua.com/blog/nextjs-with-typescript)
4. A Guide for Next.js with TypeScript- Refine dev, 7 月 14, 2025 にアクセス、 [https://refine.dev/blog/next-js-with-typescript/](https://refine.dev/blog/next-js-with-typescript/)
5. AO Price Today | AO to USD Live Price, Market Cap & Chart- Binance, 7 月 14, 2025 にアクセス、 [https://www.binance.com/en/price/ao](https://www.binance.com/en/price/ao)
6. Live AO Price, Charts & Market Data- MEXC Exchange, 7 月 14, 2025 にアクセス、 [https://www.mexc.com/price/AO](https://www.mexc.com/price/AO)
7. AODocs | Cloud Document Management, 7 月 14, 2025 にアクセス、 [https://www.aodocs.com/](https://www.aodocs.com/)
8. AODocs API documentation, 7 月 14, 2025 にアクセス、 [https://api.aodocs.com/](https://api.aodocs.com/)
9. API Reference- AODocs API documentation, 7 月 14, 2025 にアクセス、 [https://api.aodocs.com/swagger/index.html](https://api.aodocs.com/swagger/index.html)
10. What are AODocs documents?, 7 月 14, 2025 にアクセス、 [https://support.aodocs.com/hc/en-us/articles/115002366943-What-are-AODocs-documents](https://support.aodocs.com/hc/en-us/articles/115002366943-What-are-AODocs-documents)
11. Use the API to prevent documents being shared publicly on whole domain, 7 月 14, 2025 にアクセス、 [https://support.aodocs.com/hc/en-us/articles/4754601475099-Use-the-API-to-prevent-documents-being-shared-publicly-on-whole-domain](https://support.aodocs.com/hc/en-us/articles/4754601475099-Use-the-API-to-prevent-documents-being-shared-publicly-on-whole-domain)
12. Basics of AODocs APIs, 7 月 14, 2025 にアクセス、 [https://api.aodocs.com/10-key-concepts/20-basics-of-aodocs-apis/](https://api.aodocs.com/10-key-concepts/20-basics-of-aodocs-apis/)
13. REST API AO count- OutSystems, 7 月 14, 2025 にアクセス、 [https://www.outsystems.com/forums/discussion/103536/rest-api-ao-count/](https://www.outsystems.com/forums/discussion/103536/rest-api-ao-count/)
14. AI SDK, 7 月 14, 2025 にアクセス、 [https://ai-sdk.dev/](https://ai-sdk.dev/)
15. What is Azure OpenAI in Azure AI Foundry Models?- Learn Microsoft, 7 月 14, 2025 にアクセス、 [https://learn.microsoft.com/en-us/azure/ai-foundry/openai/overview](https://learn.microsoft.com/en-us/azure/ai-foundry/openai/overview)
16. Modern AI Integration: OpenAI API in Your Next.js App | by Adhithi Ravichandran | Medium, 7 月 14, 2025 にアクセス、 [https://adhithiravi.medium.com/modern-ai-integration-openai-api-in-your-next-js-app-f3a3ce2decf0](https://adhithiravi.medium.com/modern-ai-integration-openai-api-in-your-next-js-app-f3a3ce2decf0)
17. How to integrate aos centrally in nextjs app router? · vercel next.js · Discussion#60913, 7 月 14, 2025 にアクセス、 [https://github.com/vercel/next.js/discussions/60913](https://github.com/vercel/next.js/discussions/60913)
18. How To Deploy Next.js To Cloud Servers: A Step-by-Step Guide- UpCloud, 7 月 14, 2025 にアクセス、 [https://upcloud.com/resources/tutorials/how-to-deploy-next-js-to-cloud-servers-a-step-by-step-guide/](https://upcloud.com/resources/tutorials/how-to-deploy-next-js-to-cloud-servers-a-step-by-step-guide/)
19. Integration with existing nextjs frontend- Wasp- Answer Overflow, 7 月 14, 2025 にアクセス、 [https://www.answeroverflow.com/m/1332958071785263127](https://www.answeroverflow.com/m/1332958071785263127)
20. Create a Next.js App with Real-time AI Voice Using 11Labs SDK- YouTube, 7 月 14, 2025 にアクセス、 [https://www.youtube.com/watch?v=XgBYbn6iRU8](https://www.youtube.com/watch?v=XgBYbn6iRU8)
21. Integrating AI Models Locally with Next.js ft. Jesus Padron- YouTube, 7 月 14, 2025 にアクセス、 [https://www.youtube.com/watch?v=DTEcr3gmauI](https://www.youtube.com/watch?v=DTEcr3gmauI)
22. LangGraph & NextJS: Integrating AI Agents in a Web Stack | Akveo Blog, 7 月 14, 2025 にアクセス、 [https://www.akveo.com/blog/langgraph-and-nextjs-how-to-integrate-ai-agents-in-a-modern-web-stack](https://www.akveo.com/blog/langgraph-and-nextjs-how-to-integrate-ai-agents-in-a-modern-web-stack)
23. Getting started with Next.js- Outstatic, 7 月 14, 2025 にアクセス、 [https://outstatic.com/docs/getting-started-with-next-js](https://outstatic.com/docs/getting-started-with-next-js)
24. How to Integrate Auth0 & Next.js | User Authentication in Next.js with Auth0- YouTube, 7 月 14, 2025 にアクセス、 [https://m.youtube.com/watch?v=16euljI71LM\&pp=ygUKI3Rob2lhdXRobw%3D%3D](https://m.youtube.com/watch?v=16euljI71LM&pp=ygUKI3Rob2lhdXRobw%3D%3D)
25. Build AI-Powered Apps with Next.js: Real-World LLM Integration | iJS- YouTube, 7 月 14, 2025 にアクセス、 [https://m.youtube.com/watch?v=gTsnsfKB-XM\&pp=0gcJCY0JAYcqIYzv](https://m.youtube.com/watch?v=gTsnsfKB-XM&pp=0gcJCY0JAYcqIYzv)
26. Embed App Builder Web SDK in a NextJS Web App, 7 月 14, 2025 にアクセス、 [https://appbuilder-docs.agora.io/sdks/guides/embed_web_sdk_nextjs](https://appbuilder-docs.agora.io/sdks/guides/embed_web_sdk_nextjs)
27. Configuration: ESLint- Next.js, 7 月 14, 2025 にアクセス、 [https://nextjs.org/docs/app/api-reference/config/eslint](https://nextjs.org/docs/app/api-reference/config/eslint)
28. Integrate with Next.js- Nuclia documentation, 7 月 14, 2025 にアクセス、 [https://docs.nuclia.dev/docs/ingestion/how-to/integrate-nextjs/](https://docs.nuclia.dev/docs/ingestion/how-to/integrate-nextjs/)
29. App Router: Adding Authentication- Next.js, 7 月 14, 2025 にアクセス、 [https://nextjs.org/learn/dashboard-app/adding-authentication](https://nextjs.org/learn/dashboard-app/adding-authentication)
30. @permaweb/aoconnect- npm Package Security Analysis- Socket, 7 月 14, 2025 にアクセス、 [https://socket.dev/npm/package/@permaweb/aoconnect](https://socket.dev/npm/package/@permaweb/aoconnect)
31. aoconnect- AO Cookbook, 7 月 14, 2025 にアクセス、 [https://cookbook_ao.g8way.io/guides/aoconnect/aoconnect.html](https://cookbook_ao.g8way.io/guides/aoconnect/aoconnect.html)
32. @ar.io/sdk- npm, 7 月 14, 2025 にアクセス、 [https://www.npmjs.com/package/@ar.io/sdk](https://www.npmjs.com/package/@ar.io/sdk)
33. weavedb/wao: Wizard AO SDK & Testing- GitHub, 7 月 14, 2025 にアクセス、 [https://github.com/weavedb/wao](https://github.com/weavedb/wao)
34. Wander Docs: Welcome to Wander, 7 月 14, 2025 にアクセス、 [https://docs.arconnect.io/](https://docs.arconnect.io/)
35. Wander | The#1 trusted wallet on AO and Arweave, 7 月 14, 2025 にアクセス、 [https://www.wander.app/](https://www.wander.app/)
36. project-kardeshev/ao-wallet-kit- NPM, 7 月 14, 2025 にアクセス、 [https://www.npmjs.com/package/%40project-kardeshev%2Fao-wallet-kit](https://www.npmjs.com/package/%40project-kardeshev%2Fao-wallet-kit)
37. wanderwallet/Wander: ⛵️ Secure wallet management for ...- GitHub, 7 月 14, 2025 にアクセス、 [https://github.com/wanderwallet/Wander](https://github.com/wanderwallet/Wander)
38. 1 月 1, 1970 にアクセス、 [https://github.com/wanderwallet/Wander/tree/production/src](https://github.com/wanderwallet/Wander/tree/production/src)
39. Beacon: AO & Arweave Wallet 4+- App Store, 7 月 14, 2025 にアクセス、 [https://apps.apple.com/gb/app/beacon-ao-arweave-wallet/id6740586070](https://apps.apple.com/gb/app/beacon-ao-arweave-wallet/id6740586070)
40. Beacon: AO & Arweave Wallet on the App Store, 7 月 14, 2025 にアクセス、 [https://download.beaconwallet.app/](https://download.beaconwallet.app/)
41. @vela-ventures/ao-sync-sdk- npm, 7 月 14, 2025 にアクセス、 [https://npmjs.com/package/@vela-ventures/ao-sync-sdk?ref=pkgstats.com](https://npmjs.com/package/@vela-ventures/ao-sync-sdk?ref=pkgstats.com)
42. ankushKun/aoxpress: expressjs like syntax for defining and calling ao handlers- GitHub, 7 月 14, 2025 にアクセス、 [https://github.com/ankushKun/aoxpress](https://github.com/ankushKun/aoxpress)
43. Autonomous-Finance/ao-emulator- GitHub, 7 月 14, 2025 にアクセス、 [https://github.com/Autonomous-Finance/ao-emulator](https://github.com/Autonomous-Finance/ao-emulator)
44. micovi/create-ao-dapp- GitHub, 7 月 14, 2025 にアクセス、 [https://github.com/micovi/create-ao-dapp](https://github.com/micovi/create-ao-dapp)
45. weavedb/arnext: NextJS on Vercel & Arweave- GitHub, 7 月 14, 2025 にアクセス、 [https://github.com/weavedb/arnext](https://github.com/weavedb/arnext)
46. Autonomous-Finance/teal-ao-starter- GitHub, 7 月 14, 2025 にアクセス、 [https://github.com/Autonomous-Finance/teal-ao-starter](https://github.com/Autonomous-Finance/teal-ao-starter)
47. Next JS Boilerplate: Kickstart Your Next.js and React app, 7 月 14, 2025 にアクセス、 [https://nextjs-boilerplate.com/](https://nextjs-boilerplate.com/)
48. Next.js Boilerplate- Vercel, 7 月 14, 2025 にアクセス、 [https://vercel.com/templates/next.js/nextjs-boilerplate](https://vercel.com/templates/next.js/nextjs-boilerplate)

```

```
