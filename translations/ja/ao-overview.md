---
title: AO Overview for Developer
platform: ChatGPT DeepResearch (GPT-4o)
date: 2025-07-11
url: https://chatgpt.com/share/6870d439-e250-8000-925a-1d45e5ff3619
tags: [ao, developer]
---

[PROMPT]

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

# [OUTPUT]

以下に、英語で出力した Arweave AO（Actor-Oriented Protocol）技術レポートの日本語翻訳を段階的に開始します。まずは第一段階として「AO とは何か？SmartWeave との違い」セクションの翻訳をお届けします。

---

# Arweave AO（Actor-Oriented Protocol） 技術概要

## AO とは何か、SmartWeave との違い

Arweave AO（Actor-Oriented）は、Arweave のパーマネントストレージネットワーク上に構築された、分散型の「ハイパーパラレル」計算プロトコルです。「スケールの限界が実質的に存在しない世界コンピュータ」を目指しており、従来の Arweave スマートコントラクトシステム（SmartWeave）が採用していた逐次的でクライアント依存のモデルとは大きく異なります。

- アクターモデル設計：各コントラクトは独立した「プロセス（アクター）」として実行され、自身の状態とメッセージ受信箱（inbox）を保持します。グローバルステートは一切共有されず、すべての通信は非同期のメッセージで行われます。この設計により、SmartWeave の「interaction ログ」による状態決定から、完全なメッセージログ主導型へと移行しています。

- 並列かつ制限のない実行：アクター同士が独立して動作するため、AO は 1 つのグローバル状態マシンによるボトルネックを回避し、大量のコントラクトを並列で実行可能です。Ethereum など従来の VM がすべてのノードで全ての計算を再実行する設計と異なり、AO ではアクターが他のアクターを生成し、処理を分散させることで並列性を実現します。

- グローバルなメモリ空間の排除：AO は共有メモリを持たず、競合状態やロック処理を不要とすることでスケーラビリティと信頼性を高めています。アクターの状態はメッセージ入力に応じて変化し、その全履歴は Arweave に記録され、検証可能かつ改ざん不可能な形で保存されます。

- Arweave ストレージとの統合：AO はすべてのデータおよびメッセージログを Arweave に永続保存し、「唯一の信頼できる記録元」として活用します。すべての入力・出力は Arweave 上で不変の履歴として記録され、計算結果は必要なときに検証可能です。

まとめると、AO は Arweave を「静的なストレージネットワーク」から「アクティブな分散計算基盤」へと進化させる技術です。SmartWeave の「ストレージ中心の計算」モデルをさらに発展させ、完全な並列性と自律プロセスのネットワークによって、複雑な処理（AI 推論、大規模データ処理など）も分散ネットワーク上で可能にします。

## コアコンポーネント：Executor、Actor、Message、Module、Blueprint

- Actor（プロセス）
  AO における「アクター」は計算の最小単位であり、独立したプロセスとして動作するスマートコントラクトのような存在です。各アクターは他のアクターと状態を共有せず、独自の状態（state）とメッセージ受信箱（inbox）を持ちます。アクターは自身で計算を実行し、他のアクターにメッセージを送信したり、新たなアクターを生成したりすることができます。これは CS（計算機科学）の古典的な「アクターモデル」に基づいており、高い並列性と故障耐性を備えています。

- Message（メッセージ）
  AO における通信の基本単位です。メッセージはデータペイロードとタグから構成され、あるアクターから別のアクターに非同期的に送信されます。アクター間の状態共有は禁止されているため、メッセージが唯一の通信手段です。メッセージは標準化された形式（ANS-104 Arweave タグ）で永続的に Arweave に記録され、すべてのやり取りが時系列で残る「メッセージログ」として扱われます。この設計により、プロセス間で疎結合なやり取りが可能となり、並列処理やワークロード分割が実現されます。

- Executor / Compute Unit（実行ノード）
  「Executor」とは、アクターのコードを実際に実行して状態更新を行うコンポーネントです。AO ではこの役割を担うノード群を「Compute Unit（計算ユニット）」と呼びます。これらのノードは Arweave 上のメッセージを読み取り、対象アクターのコードを実行し、状態更新および新たなメッセージ出力を生成します。AO は計算と合意形成（consensus）を分離しているため、すべてのノードが全契約を再実行する必要はありません。代わりに、実行ノードはその結果に対する証明（attestation）を添付し、経済的インセンティブ（ステーキングなど）によって信頼性を担保します。代表的な Executor 実装が「HyperBEAM」で、Erlang 製の高性能ノードソフトウェアです。

- Messenger / Scheduler Unit（メッセージ配信・順序付け）
  Executor 以外にも、メッセージ処理に特化したユニットがあります：

  - Messenger Unit（MU）：ユーザーまたはアクターから送られるメッセージを受信し、検証後に正しい宛先プロセスへとルーティングする役割を担います。
  - Scheduler Unit（SU）：メッセージにタイムスタンプや順序を付け、それを Arweave 上のトランザクションとして記録する役割を担います。この仕組みにより、ネットワーク全体で一貫した処理順序が保証されます。

- Module（仮想マシンおよびライブラリ）
  AO は「マルチ VM（仮想マシン）」アーキテクチャを採用しており、1 つの言語や実行環境に依存しません。代表的なターゲットは WebAssembly（Wasm）であり、Rust、C/C++、JavaScript など多数の言語でスマートコントラクトを記述可能です。現時点では Lua が標準実装（AOS）として採用されており、Lua スクリプトは Wasm にコンパイルされて実行されます。また、各プロセスは標準モジュール（暗号ライブラリ、JSON、Base64 等）にアクセス可能で、AO 環境での共通機能として提供されます。

- Blueprint（設計テンプレート）
  Blueprint とは、特定のユースケースに特化したアクターのコードテンプレートのことです。例えば、Token Blueprint を使用すれば、標準的な ERC20 風のトークンをすぐに発行できます。Blueprint は CLI から簡単に読み込み・カスタマイズ可能で、初学者やプロトタイピング段階の開発者にとって大きな助けとなります。実際に Community Labs が提供する AO Cookbook には、複数の Blueprint が収録されています。

## 開発の背景と主要貢献者

- 起源と思想
  Arweave における AO 構想は 2020 年に始まりました。コロナ禍中に Sam Williams（Arweave 創業者）とその開発チームが「ニュートラルかつ分散的な計算ログ」の可能性を模索したのが発端です。これは、すべてのプログラムの状態を入力ログの積み上げから再現可能にする、という構想に基づいています。

このアイデアは SmartWeave という形で最初に具体化され、Arweave 上でコントラクトと相互作用ログを永続保存し、それをクライアント側で読み解くことで「状態」を計算するというモデルが提案されました。SmartWeave は原理的には有効であるものの、速度や双方向性に課題がありました。

そうした中で登場したのが「Storage Consensus Paradigm（SCP）」という概念で、これは EverVision Labs の創業者 Outprog（伊藤恭平）によって提唱されました。彼は、Arweave 上に記録されたあらゆる種類のデータログを合意形成（consensus）の基礎と見なすという新たな発想を提示しました。

Sam Williams と Outprog の協力により、このアイデアは実装段階に入り、SmartWeave ベースの拡張では限界があると判断され、クリーンな新アーキテクチャとして「AO（Actor-Oriented）」が開発され始めました。その最初の実装が Lua ＋ Wasm による「AOS（Arweave Operating System）」です。

- 主要貢献者

  - Sam Williams
    Arweave 創業者であり、Forward Research の CEO。AO プロトコルのビジョンを提唱し、ホワイトペーパーの執筆を主導した人物。彼の主張では、AO は Ethereum が目指した「ワールドコンピュータ」を現実にするものであり、スマートコントラクトの限界を超える分散計算環境を目指しています。

  - Outprog（伊藤恭平）
    EverVision の創業者であり、everPay や Permaswap などの開発で知られる。彼は AO の前身となる SCP（ストレージ合意形成パラダイム）を提唱し、SmartWeave からの思想的飛躍をリードしました。また、彼の提案により、AO ベースの分散決済や DeFi 実装が具体化されました。

  - Forward Research チーム
    Sam を中心に、Ivan Morozov（Autonomous Finance）、Tom Wilson & Tyler Hall（Hyper.io）、Vincent Juliano、Alberto Navarro らが AO プロトコルと各種ツール群を開発。Tom とチームは特に「HyperBEAM」という高並列 Erlang 製ノードソフトを開発し、AO の性能面を支えています。

  - Community Labs（創業者：Tate Berenbaum）
    Arweave および AO エコシステムに特化した Web3 スタジオ。ArConnect（現 Wander）や AO 対応ステーブルコイン「Astro」、さらに開発者教育コンテンツ（AO Bootcamp、Cookbook）を多数提供。2024 年 4 月には「ao Ventures」という AO 開発特化インキュベータも立ち上げました。

  - ao/acc Labs（AO Compute Club）
    2024 年に誕生した、AO 上に dApp を構築するオープンコミュニティ。代表作は ArFleet（AO ベースのコンテンツホスティング/ソーシャルサービス）であり、AO の実用可能性を示す事例を多数展開しています。

- 開発のマイルストーン

  - 2024 年 2 月末：AO 初のパブリックテストネット（通称「Legacynet」）がリリースされ、初週で 3,000 以上のプロセスがデプロイされるなど爆発的な反響を得ました。

  - 3 月〜4 月：AO Cookbook（技術資料・チュートリアル）、\$CRED テストネット報酬、Community Labs 主導のブートキャンプや Hackathon が展開され、0rbit や AO 上のミームコイン、ゲームなど多数のプロジェクトが誕生。

  - 2024 年夏以降：AO-Core v1.0（本番仕様プロトコル）と HyperBEAM（次世代 Executor）の登場により、ネットワーク構造が高度に分化（Messenger, Scheduler, Compute の 3 ユニットに分離）し、将来のステーキング・スラッシング制度の導入を見据えた本格的な準備段階に突入。

  - メインネットの予定：2025 年 2 月。AO-Core + HyperBEAM の本番投入が予定されており、トークン転送可能性やステーク報酬が解禁される見込み。これにより、AO プロセスの実行やメッセージ処理に参加するノードが自由に登場できる、完全な分散ネットワークへと移行します。

## 現状と今後の展望

2025 年初頭時点で、AO はメインネットローンチを目前に控えています。テストネット（Legacynet）ではすでに数百万のメッセージが処理され、数百のプロセスが並列稼働しています。AI 推論のような複雑な計算も、信頼最小化された環境で処理され、AO の可能性が現実に示されています。

開発者はすでに CLI（AOS CLI）や Web IDE（BetterIDEa）を用いて、AO 上にプロセスをデプロイできます。さらに、dApp 統合を支援する JavaScript SDK「AO Connect」や、ローカルテストを可能にするフレームワーク「WAO」などのツール群も整備されつつあります。

また、以下のような主要プロジェクトが AO に統合・実装されつつあり、その応用範囲の広さを物語っています：

- everPay 2.0（分散型クロスチェーン決済）
- Permaswap DEX（分散型取引所）
- 0rbit（AO ベースのオラクル）
- Astro USD（AO ネイティブのステーブルコイン）
- Wander（AO 対応ウォレット）

AO の登場は、Web3 にとって一つの転機です。従来の L1 ブロックチェーンでは実現が困難だった「大規模計算」や「リアルタイム処理」が、AO により分散環境下で実行可能になったからです。

たとえば、AI モデルのデプロイやクラウド的なマイクロサービスの展開、自律エージェントの構築などが、オンチェーンかつ検証可能な形で実現可能です。Sam Williams が語るように、Ethereum は分散型金融（DeFi）を可能にしましたが、AO は「分散型クラウドコンピューティング」の時代を拓きます。

今後の数ヶ月は次のような取り組みが進められる見込みです：

- ネットワークのセキュリティ強化（監査やスラッシング設計）
- ステーキングによるノード参加のインセンティブ化
- テストネット上で成功したプロジェクトの本番移行
- AO トークンの本格的なユーティリティ化とインセンティブ設計

もしこの構想が成功すれば、Arweave の「パーマウェブ」は、静的なデータ図書館から、自律的かつ生きたクラウドコンピュータへと進化することになるでしょう。それはまさに、次世代 Web3 アプリケーションの基盤であり、AI とブロックチェーンの交差点に立つ未来型の分散基盤です。
