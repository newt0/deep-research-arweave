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

# Next.js と TypeScript を用いた AO ベースアプリケーションの統合

Arweave の AO（Actor Oriented）スマートコントラクトと Next.js フロントエンドを統合するには、AO プロセス（アクター）への接続、ウォレット署名の処理、メッセージ送信、リアルタイムの状態取得といったステップを踏む必要があります。これにより、AI エージェントや DeFi プラットフォームのような高度な**dApp**を、React/TypeScript ベースのモダンな UI で構築できます。以下に統合ステップとリソースを詳細にまとめます。

## Next.js フロントエンドと AO プロセス／アクターの接続

Next.js から AO プロセスと通信するには、`@permaweb/aoconnect`パッケージを用いた**AO Connect SDK**を使用します。この JavaScript/TypeScript ライブラリは、Node（サーバー）とブラウザの両方で動作し、プロセスの生成、メッセージ送信、出力の取得などが可能です。

- **インストール**：npm 経由でインストール：`npm install @permaweb/aoconnect`。`spawn`、`message`、`result`、`results`などの関数が提供されており、直接インポート可能です。

- **デフォルト接続とカスタム構成**：標準では、`@permaweb/aoconnect`をインポートするだけで AO の\*\*mainnet（HyperBEAM ネットワーク）\*\*に接続されます。ローカル開発やカスタムノードを使う場合は、`connect()`関数で Messenger Unit（MU）、Compute Unit（CU）、Arweave Gateway の URL を指定します：

  ```ts
  import { connect } from "@permaweb/aoconnect";
  const { spawn, message, result } = connect({
    MU_URL: "http://localhost:4002",
    CU_URL: "http://localhost:4004",
    GATEWAY_URL: "http://localhost:4000",
  });
  ```

  引数を省略すると、既定の本番ネットワークが使われます。

- **プロセス識別**：各 AO プロセスは Arweave のトランザクション ID（TxID）で識別されます。フロントエンドから対象プロセスにメッセージを送る際、この TxID を`process`として指定します。

- **サーバー vs クライアント**：AO SDK は**サーバー（Node.js）**と**クライアント（ブラウザ）**の両方で動作します。状態取得などの**読み取り操作**は Next.js の SSR 中に可能ですが、\*\*メッセージ送信（書き込み）\*\*には署名が必要となるため、通常はクライアントサイドで実行されます。SSR では、ウォレット不要の読み取りデータのみを事前取得し、インタラクティブな操作はクライアントで行う構成になります。

- **SSR 互換性の注意点**：Next.js で`aoconnect`を使用する際、SSR 中に`window`などのブラウザグローバルを直接参照しないよう注意が必要です。SSR 中は`typeof window !== 'undefined'`でクライアント判定を行うか、動的インポートを活用してクライアント側のみ読み込むようにします。読み取り専用処理であれば、`getServerSideProps`や API ルートから安全に呼び出すことができます。

## ウォレット接続と署名処理（Wander／Beacon の比較）

AO ではすべてのメッセージに**暗号署名**が必要です。これにより、信頼性のある実行が保証されます。Next.js アプリにおいて、署名を行うためのウォレット統合には複数の選択肢があります。

- **Wander（旧 ArConnect）ブラウザ拡張機能**：Arweave/AO の主要ウォレットであり、`window.arweaveWallet` に API を注入します。

  - 拡張機能がインストールされていれば、ユーザーに接続を促すことが可能です。例：

    ```ts
    await window.arweaveWallet.connect(
      ["ACCESS_ADDRESS", "ACCESS_PUBLIC_KEY", "SIGN_TRANSACTION", "SIGNATURE"],
      { name: "My App" }
    );
    ```

  - 接続後、`window.arweaveWallet.getActiveAddress()` でアドレス取得可能。

  - 署名には、AO SDK の `createSigner()` を活用：

    ```ts
    import { message, createSigner } from "@permaweb/aoconnect";
    const signer = createSigner(globalThis.arweaveWallet);
    await message({
      process: "<ProcessTxID>",
      tags: [{ name: "Action", value: "DoSomething" }],
      data: "",
      signer,
    });
    ```

  - 署名は `signDataItem` API を通じて処理され、署名確認の UI が拡張機能上で表示されます。

- **Wander Connect（埋め込み型ウォレット SDK）**：拡張機能を不要とし、React アプリ内でウォレット機能を提供するライブラリです。

  - `@wanderapp/connect` を導入し、メールや SNS ログインによりウォレットを生成・接続可能。

  - UX を改善したい dApp に適しており、キーは Wander の安全なバックエンドで管理され、dApp 側には露出しません。

- **Beacon Wallet（AO Sync SDK、モバイル／デスクトップ対応）**：2FA やマルチシグにも対応するウォレット。モバイル端末との連携に強みがあります。

  - `@vela-ventures/ao-sync-sdk` を使用し、MQTT/WebSocket 経由で Beacon アプリと接続。

    ```ts
    import WalletClient from "@vela-ventures/ao-sync-sdk";
    const walletClient = new WalletClient();
    await walletClient.connect({
      permissions: ["ACCESS_ADDRESS", "ACCESS_PUBLIC_KEY", "SIGN_TRANSACTION"],
      appInfo: { name: "My App" },
      brokerUrl: "wss://aosync-broker-eu.beaconwallet.dev:8081",
    });
    ```

  - 接続後、QR コードスキャンでペアリングし、`walletClient.signDataItem(dataItem)` 等を通じて署名を実行します。

  - セキュアな署名環境が求められる金融系 dApp やモバイル特化型 UX に適しています。

- **キー直接読み込み（開発・サーバー用途）**：開発中やサーバー処理では、JSON 形式の JWK（鍵ファイル）を使って署名することも可能です。

  ```ts
  import { createSigner } from "@permaweb/aoconnect";
  const signer = createSigner(myJwkJson);
  ```

  - フロントエンドに秘密鍵を含めるのは NG です。署名が必要な処理を API Route 内などサーバー側で実行する用途に限られます。

- **全メッセージに署名が必要**：AO mainnet では署名なしのメッセージは無効です。`message()` や `spawn()` を呼び出す際には、必ず `signer` を指定する必要があります。署名方式は Arweave キーや Ethereum キーに対応していますが、通常は Wander または Beacon が使われます。

Next.js アプリでは、React コンテキストやカスタム Hook でウォレット接続状態を管理し、アクション実行時に署名処理を呼び出すのが一般的です。ウォレット署名関連の処理はすべてクライアント側で実行されるため、SSR では動的インポートや`useEffect`内での初期化が推奨されます。

## ブラウザから AO プロセスにメッセージを送信する

ウォレット接続と署名準備が整ったら、Next.js アプリから AO アクター（プロセス）に**メッセージ送信**を行えます。これにより、スマートコントラクトを介した実行や状態遷移が可能になります。

- **メッセージの構造**：AO におけるメッセージは、署名済みの DataItem（ANS-104 形式）として送信され、タグ・ターゲット・データなどを含みます。`@permaweb/aoconnect`ライブラリがこれらを抽象化してくれます。

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

  - `process`: 実行対象のプロセス ID
  - `tags`: プロセスに渡すパラメータ（例：Action、Amount など）
  - `data`: オプションの文字列／バイナリペイロード
  - `signer`: `createSigner()`等で生成した署名者関数

- **プロセスの生成（spawn）**：既存プロセスへのメッセージ送信だけでなく、新しいプロセスを生成することも可能です。例：新しい AI エージェントやスマートコントラクトインスタンスの生成。

  ```ts
  const newProcessId = await spawn({
    module: "<ModuleTxID>",
    scheduler: "<SchedulerWalletAddress>",
    signer: createSigner(window.arweaveWallet),
  });
  ```

  - `module`: 実行するコードの TxID（青写真となるモジュール）

  - `scheduler`: スケジューラユニットのアドレス

  - `signer`: 署名関数

  - 一般ユーザーによるプロセス生成を UI から可能にする dApp では、この API が使用されます。Arweave の手数料が発生するため、UI 上でその旨を明示するのが望ましいです。

- **署名関数の選択**：`createSigner()` または `createDataItemSigner()` により、環境に応じた署名関数が自動的に選ばれます。ブラウザウォレットを使用している場合は、内部的に `window.arweaveWallet.signDataItem()` を呼び出して署名処理を実行します。

- **Next.js での実装パターン**：Next.js + TypeScript の構成では、React コンポーネントまたはカスタム Hook にて以下を実装することが一般的です：

  1. ページロード時に AO SDK を初期化（`connect()`使用時は環境設定も指定）
  2. ユーザーがアクションを行うと、ウォレット接続確認 → メッセージ送信
  3. メッセージ送信結果（例：TxID）を受け取り、UI に反映

  クライアントサイドでのみウォレット API が利用可能なため、`typeof window !== 'undefined'` や `useEffect` で動的に初期化し、SSR エラーを避ける構成が推奨されます。メッセージ送信ロジックはユーティリティ関数として分離しておくと再利用性が高まります。

## AO のリアルタイム状態や出力を UI に表示する方法

AO ベースの dApp の大きな魅力の一つは、プロセス（アクター）からの**状態変化や出力結果をリアルタイムで取得・表示**できることです。以下の手法を組み合わせることで、状態同期を実現できます。

- **プロセスの結果を取得する**：AO に送信された各メッセージは、それに対応する\*\*Result（結果）\*\*を生成します。この Result には、出力や副次的なメッセージ、プロセス生成、エラーなどの情報が含まれます。

  - 単一メッセージに対する結果の取得には `result()` を使用：

    ```ts
    const res = await result({
      process: "<ProcessID>",
      message: "<MessageID>",
    });
    console.log(res.Output); // 出力結果
    ```

  - 過去の結果一覧を取得するには `results()` を使用：

    ```ts
    const resList = await results({
      process: "<ProcessID>",
      limit: 10,
    });
    ```

    結果の履歴や、特定ユーザーの操作履歴などを表示したい場合に有効です。Next.js では、ページ初期表示時に`getServerSideProps`などで取得しておき、クライアントで後続の更新をポーリングする形が一般的です。

- **新規メッセージの監視**：AO は非同期ネットワークであるため、**リアルタイム性の高い UI**を実現するには次のような手法が用いられます：

  - **ポーリング**：数秒ごとに `results()` を呼び出して更新を確認する方法。結果の中に`timestamp`や`incremental tag`を含めることで、新着を判別可能です。

  - **AO SDK の monitor 機能**：これは主に Cron 対応プロセスのスケジュール実行をトリガーするためのもので、リアルタイム UI 更新用ではありません。

  - **Arweave トランザクションの監視**：AO メッセージは最終的に Arweave に保存されるため、GraphQL や`ao.link`などを通じてトランザクションベースで監視可能。ただしフロントエンドでの実装は複雑なため、SDK ベースでの`results()`ポーリングが現実的です。

- **HyperBEAM による state patch 機能の活用**：AO の HyperBEAM アーキテクチャでは、プロセスが`~patch@1.0`メッセージを送信することで、**HTTP エンドポイント経由で状態を即時取得**できるようになります。

  - 例：プロセス ID `XYZ` が `balance: 100` を patch した場合、次のような URL で取得可能：

    ```
    https://<hyperbeam-node>/<process-id>~process@1.0/compute/cache/balance
    ```

  - この機能は、トークン残高やランキング情報など**頻繁に読み取られる軽量データの即時表示**に最適です。

- **ドライラン（dryrun）による読み取り**：状態の読み取りだけであれば、`dryrun()`を用いることで**メッセージを送信せずに仮想実行**することが可能です。

  ```ts
  const res = await dryrun({
    process: "<ProcessID>",
    tags: [
      { name: "Action", value: "Balance" },
      { name: "Account", value: "alice" },
    ],
    data: "",
  });
  console.log(res.Output);
  ```

  - 実際に Arweave にトランザクションが記録されることはなく、状態のクエリ用として非常に便利です。
  - Mainnet では dryrun でも署名が必要な場合があるため、バックエンドでの利用やサービス用ウォレットと組み合わせると効果的です。

- **UI 更新の実装**：`results()`や`patch`などで取得した状態を React の状態管理で UI に反映させます。非同期処理であることを考慮し、「送信中」「待機中」「応答済み」などのステータス表示を行うと UX が向上します。

  - チャット型の AI エージェントなどでは、ユーザーの入力をメッセージ送信し、結果の`Output`が返るまで`typing...`表示するなどが典型です。
  - DeFi のような取引 UI では、注文処理後に状態をリフレッシュし、流動性や板情報を反映します。

これらの機能を組み合わせることで、**遅延のある Arweave ネットワークを前提としつつも、ユーザーにとってリアルタイムに近い応答性**を提供することが可能です。データ取得方法は、用途に応じて`dryrun`／`result`／`patch`などを適切に選択してください。

## AO dApps 用の Boilerplate リポジトリとテンプレート

開発を迅速に始めたい場合は、AO とフロントエンドの統合が事前に設定された\*\*コミュニティ製の Boilerplate（ひな形）\*\*を活用するのが有効です。

- **`create-ao-dapp`**：CLI ベースのスターターキット。`npx create-ao-dapp@latest` を実行すると、AO の\*\*バックエンドプロセス（Lua コード、テスト、デプロイ設定）**と**React/Next.js フロントエンド（TypeScript）\*\*がセットになったモノレポを自動生成します。

  - カウンターやトークンなどの簡易プロセスが同梱されており、エンドツーエンドの統合例として優秀です。

- **`ao-starter-kit`（by Autonomous Finance）**：`create-ao-dapp`のベースとなっているプロジェクト。`/ao` ディレクトリにバックエンドコード、`/apps` にフロントエンドアプリが分離されており、大規模開発に向いています。

  - CLI ツールによるビルドやデプロイの手順が整っており、実際の開発フローに即した構成です。

- **`teal-ao-starter`**：Lua の型付き派生言語である**Teal**を使った AO コントラクト開発向けのスターター。型安全な開発を重視したい開発者に適しています。

- **`create-ao-contract`**：AO コントラクトのスキャフォルドに特化した CLI ツール。フロントエンドは含まれないため、Next.js など既存のフロントエンドと組み合わせて使用します。

- **`ao-deploy`**：Community Labs 提供の AO コントラクト自動デプロイ用 CLI。CI/CD などで利用され、契約更新や公開処理の自動化に便利です。

- **Web IDE – BetterIDEa**：`https://ide.betteridea.dev/` でアクセス可能な AO 対応のオンライン IDE。コードの記述、テスト、展開がブラウザ上で完結できます。

- **テストフレームワーク – WAO（Wizard AO）**：AO プロセスとメッセージフローを**ローカル環境で高速シミュレーション**できるツール。CI 環境やユニットテストに最適です。

- **実プロジェクト例**：

  - **Botega**：AO ベースの分散型取引所。取引の自動処理を行うエージェント型 dApp の例です。
  - **AOX／Bazar／0rbit／AstroUSD**：AO を活用した DeFi／オラクル／マーケットプレイスなど多様なユースケースがあります。
  - これらのコードが OSS 化されていない場合でも、アーキテクチャ設計の参考になります。

### 補足 Tips：

- **セキュリティ**：署名操作は必ずユーザーのウォレット環境で行いましょう。Wander や Beacon を通すことで、鍵は安全に保持され、アプリ側に漏れることはありません。

- **パフォーマンス**：Next.js のプリレンダリングを活用すれば、公開データを`getServerSideProps`で取得し、初期表示を高速化可能です。クライアントでは動的に更新する構成が推奨されます。

- **整合性**：AO の状態更新には数秒〜数十秒のラグがあります。UI 側で進行状況の表示や取引 ID の提示、AO Link などのエクスプローラへのリンク提供で、信頼性を補完しましょう。

- **コミュニティ連携**：開発途中で問題があれば、AO Cookbook や Community Labs のブログ、`@ao_builders`などの X アカウントが有益です。Discord での質問も活発に行われています。

このように、Next.js と AO を組み合わせることで、**Web2 ライクな UX と Web3 ネイティブな実行モデルの融合**を実現できます。ウォレット連携、状態取得、メッセージ送信を正しく設計すれば、安定した AO アプリケーションを構築可能です。
