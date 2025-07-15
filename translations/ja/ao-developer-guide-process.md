---
title: Guide to Developing an AO Process
platform: ChatGPT DeepResearch (GPT-4o)
date: 2025-07-11
url: https://chatgpt.com/s/t_687489baa57c81918f13de7504116917
tags: [ao, developer]
---

[PROMPT]

```markdown
Please conduct a technical investigation into developing AO Processes for Arweave's AO protocol using Lua.

## Focus Areas

- How to use ao-cli, ao-sdk, and Hooks to build and deploy custom Processes
- How to set up local development and testing environments
- How to structure Executors and manage message flows
- How to use and compose AO Modules (e.g., token, counter, etc.)
- Recommended project templates and GitHub repositories
- Debugging and monitoring tools available to Lua developers

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

# Lua で構築する Arweave AO プロセス開発ガイド

## AO とそのプロセスの概要

Arweave の AO プロトコルは、**ハイパーパラレルなコンピュート環境**を提供します。そこでは多くの独立したプロセスが 1 つの統合ネットワーク上で並列的に動作します。各 AO プロセスは、それぞれに独立した状態（"メモリーカード"）を持ち、**メッセージの送受信**だけで他のプロセスと通信します。この設計は Erlang の軽量プロセスモデルに着想を得ており、グローバルな共有状態は存在しません。すべてのプロセス間通信は非同期メッセージで行われます。

AO は、すべてのメッセージと実行履歴を Arweave の Permaweb に記録することで、検証可能な信頼レスなコンピューティングを実現します。開発者は、1 つの AO プロセスを立ち上げることで、実質的に**中立かつ永続的なスマートコントラクトとしてのサーバー**を起動することができます。

## 開発環境のセットアップ

**1. AO CLI（aos）のインストール：**
最も簡単な開始方法は、AO 開発 CLI をインストールすることです。これはシェルスクリプトとして配布されており、Docker が必要です：

```bash
curl -L https://install_ao.g8way.io | sh
```

このコマンドで `ao` 開発ツールが導入されます。その後、ターミナルで `aos` を実行することで、インタラクティブな AO シェルを起動できます。初回実行時には、Arweave ウォレットに紐づいたデフォルトプロセスが自動的に作成または接続されます（特定のウォレットを指定するには `--wallet <keyfile>` を使用）。

**2. プロセスの起動：**
新しい AO プロセスを作成するには、`aos <プロセス名>` を実行します。たとえば、`aos chatroom` とすると “chatroom” という名前のプロセスが生成されます（既に存在すればそれに接続）。最初の実行では、Arweave 上にプロセス登録のトランザクションが発行され、Process-Name や Owner などのタグが記録されます。`--cron 2-minutes` のようにオプションを付けると、2 分ごとにプロセスが自動実行されるようになります。`--tag-name` / `--tag-value` で独自タグも追加可能です。

**3. Lua コード（Hooks/Handlers）の読み込み：**
`aos` シェル内では、`.load my_process.lua` を実行することで、Lua ファイルをプロセスに読み込めます。もしくは以下のように起動時にまとめて複数ファイルを読み込むことも可能です：

```bash
aos myProcess --load handler1.lua --load handler2.lua
```

このコマンドで `myProcess` プロセスが起動し、同時に複数の Lua ソースファイルが読み込まれます。また `.load-blueprint token` のように、あらかじめ用意された「ブループリント」を読み込むことで、標準的なトークンコントラクトのような定型処理を即座に組み込むこともできます。

**4. AO Dev-CLI ワークフロー：**
`aos` に加え、プロジェクト単位で開発するための開発者向け CLI も存在します。`ao init <プロジェクト名>` でプロジェクトをスキャフォールディングし、`ao build` で Lua コードを WebAssembly にコンパイルします。このコンパイル作業では、Lua インタプリタを内包した WASM バイナリが生成されます。

このプロセスを Arweave 上にデプロイするには、以下のようにコマンドを実行します：

```bash
ao publish -w wallet.json path/to/project.wasm
```

これにより、WASM モジュールが Arweave トランザクションとしてアップロードされ、新しい AO プロセスが生成されます。

**5. AO Connect SDK：**
Node.js やブラウザなどから AO プロセスとプログラム的に連携したい場合は、`ao Connect` JavaScript/TypeScript SDK が利用できます。この SDK では `spawnProcess(...)` でプロセス生成、`send(processId, message)` でメッセージ送信、さらにはローカル dry-run によるステートの取得などが可能です。ウェブ dApp との統合を行う場合に非常に有効です。

## ローカル開発とテスト環境の構築

AO プロセスを実運用前に**ローカルまたはテストネットで検証する**ことが推奨されます。これにより、手数料の浪費や不具合の早期発見を防げます。以下のようなツールがローカル開発を支援します：

- **WAO (Wizard AO)：**
  AO のためのインメモリ・エミュレータ兼 SDK です。プロセスのローカル実行環境をゼロレイテンシかつ無料で提供し、開発サイクルを飛躍的に高速化します（最大 1000 倍速とされる）。Lua 内の `ao.log(...)` を即座にターミナル出力へリダイレクトしたり、Arweave のストレージを仮想化して即時にデータ読み出しが可能です。
  さらに WAO では、プロセスの状態をフォークして複数の分岐を同時にテストすることもできます。

導入コマンド例：

```bash
yarn add wao
# または
npx wao
```

- **ローカル AO ユニット：**
  WAO は、インメモリだけでなく、永続的なローカル AO ノードも立ち上げ可能です。これにより、`localhost` ベースのエンドポイントでフロントエンドから AO プロセスに接続でき、本番環境を模したエンドツーエンドテストが可能になります。

- **BetterIDEa Web IDE：**
  インストール不要でブラウザ上から AO コードの編集・デプロイが可能な Web IDE。プロセスの実行やログの確認も GUI で行え、簡易プロトタイピングに最適です。

- **VS Code プラグインと設定：**
  Lua や Teal のシンタックスサポート、コード補完、`ao build` 等のタスク自動化などが可能なプラグインセットが利用できます。AO Cookbook に推奨構成があります。

- **ArLocal／テストネット利用：**
  より本格的なローカルシミュレーションを行いたい場合は、Arweave のローカルノード（ArLocal）と AO ノード一式（Scheduler, Compute など）を組み合わせて開発できます。ただし WAO の簡便性が優れているため、通常は WAO のみで完結できます。

## Executor とメッセージフローの構造化

AO プロセスは**イベント駆動**型で設計されます。グローバルなループ処理ではなく、**受信メッセージに反応する"ハンドラ（Executor）"**を複数登録しておくスタイルです。

Lua における AO では、`Handlers` グローバルオブジェクトを通じてフックを追加します：

```lua
Handlers.add("RegisterUser",
  function(msg) return msg.Action == "Register" end,
  function(msg)
      table.insert(Users, msg.From)
      ao.send({Target = msg.From, Data="OK", Action="Registered"})
  end)
```

この例では、「Register」というアクションを持つメッセージを受信したとき、`Users` テーブルに送信者アドレスを登録し、返信メッセージを送っています。

**メッセージ処理の基本ポイント：**

- **Inbox と Handler の役割分担：**
  受信メッセージは、条件に合致するハンドラがあれば即座に処理され、なければ Inbox（未処理メッセージのキュー）に格納されます。Inbox は CLI や AO Link 等で確認可能で、後からハンドラを追加して処理することもできます。

- **非同期メッセージ処理とレスポンス：**
  `ao.send({...})` はデフォルトで非同期の一方向送信です。レスポンスを必要とする場合は、以下のパターンが存在します：

  - `msg.reply(...)`：受信メッセージに対する返信（メッセージ ID を保持）
  - `ao.send({...}).receive()`：メッセージ送信後、対応する返信をブロックして待機
  - `msg.forward(...)`：別プロセスへの委譲後に最終的な返信を元のプロセスへ返すパターン（A→B→C→A）

- **Receive 関数による一時的リスナー：**
  `Receive(pattern)` 関数を使えば、特定パターンのメッセージが届くまで待機する同期的な処理が可能です。

- **ステート管理：**
  プロセス内の Lua 変数はメッセージ間でも永続されます。`count = 0` のようなグローバル変数を使って状態を保持し、複数のハンドラから共有することが可能です。

- **Cron 実行（自動化）：**
  `--cron` オプションを用いることで、一定間隔で自動的にメッセージを受信することが可能です。これにより、チャート監視や取引の自動実行など、**エージェント型処理**を構築できます。

## AO モジュールの活用と組み合わせ（トークン、カウンターなど）

AO の大きな利点は**モジュール性**にあります。以下の方法で、標準プロセスの再利用や、複数プロセスの連携によって、複雑なアプリケーションを構築することができます。

- **ブループリント（標準プロセステンプレート）：**
  AO Cookbook には、トークン、投票、ステーキングなどの一般的なコントラクトに対応した**再利用可能なブループリント**が提供されています。

例：トークンブループリント
以下のコマンドで、標準的なトークンプロセスを構築できます：

```bash
.load-blueprint token
```

このブループリントには、`balance`、`transfer`、`mint` などの基本的なトークン機能がすべて実装されたハンドラが含まれており、即座に使用できます。さらに、`Handlers.list` で登録された全ハンドラを確認できます。
必要に応じて、例えば`freeze` 機能の追加や `transfer` 制限の導入など、ロジックを拡張することも可能です。

- **プロセス間の構成：**
  AO はプロセス同士が**疎結合で非同期通信**できるため、機能ごとにプロセスを分離し、互いに連携させる設計が推奨されます。

例：

- `tokenProcess` → トークンロジックのみを担当
- `chatroomProcess` → チャット投稿を処理
- `chatroomProcess` が `tokenProcess` に `balance` メッセージを送り、トークン保有者のみメッセージ投稿を許可する、などの**トークンゲート**が可能

このように、トークンプロセスを共通部品として複数アプリに組み込むなど、柔軟な構成が可能です。

- **外部モジュールの組み込み（C/C++など）：**
  AO dev-cli は、Lua スクリプトに加えて**ネイティブモジュール（WASM）**を統合できます。

例：`aos-sqlite` モジュール
SQLite をプロセス内部に組み込み、Lua から `require("sqlite")` として SQL クエリを実行できます。
これにより、より構造化されたデータ管理（例：リーダーボード、オンチェーン DB）を実現可能です。

将来的には、HTTP クライアント（例：0rbit）、LLM 連携など、より高度なモジュールの展開も想定されており、独自のモジュールを構築してプロセスにロードすることも可能です。

- **カウンターの例（最小構成）：**
  コミュニティが提供している `ao-counter` チュートリアルでは、シンプルなインクリメント処理を行うプロセスが紹介されています。

例えば以下のように、`AddNew` というアクションで送信者を記録し、カウントアップするような設計です：

```lua
Handlers.add("AddUser",
  function(msg) return msg.Action == "AddNew" end,
  function(msg)
      count = count + 1
      table.insert(users, msg.From)
  end)
```

このプロセスとトークンプロセスを組み合わせれば、「トークン保有者のみがカウントを押せる」というようなロジックも構築できます。

## スターターテンプレートと主な GitHub リポジトリ

AO 開発にあたって活用可能なテンプレートとツールは以下の通りです：

- **`create-ao-dapp`：**
  React フロントエンド + Teal(Lua)バックエンド + SQLite を備えた**フルスタック dApp テンプレート**。
  以下のコマンドで即座にスキャフォールディング可能：

```bash
npx create-ao-dapp@latest
```

状態管理、CRUD 処理、WASM ビルド、WAO テストなどがすべて統合されており、開発のベースとして非常に優秀です。

- **`teal-ao-starter`：**
  Teal（型付き Lua）に特化したテンプレート。静的型チェックによる安全性を重視する開発者に最適です。

- **`create-ao-contract`：**
  コントラクトロジックに集中したテンプレート。以下のコマンドでセットアップ：

```bash
npx create-ao-contract@latest
```

Busted テストフレームワーク、WAO による高速テスト、`ao-deploy` による本番デプロイなど、CI 向け構成が初期から整っています。

- **`ao-deploy`：**
  ビルド済み WASM を指定して、Arweave へプロセスを一括デプロイ可能なユーティリティ。CI/CD パイプラインとの統合も想定されています。

- **事例リポジトリ：**

  - `ao-labs/ao`：AO の公式モノレポ。Lua サンプル多数
  - `HyperBEAM`：Erlang 実装版 AO ノード
  - `Permaswap`：分散型取引所
  - `AstroUSD`：AO 上のステーブルコインプロジェクト
  - `0rbit`：HTTP クライアントオラクル
  - `Awesome AO`：テンプレ、ツール、事例集の総合カタログ

## AO プロセスのデバッグとモニタリング

AO プロセスを本番環境にデプロイした後、その動作をリアルタイムでモニターし、不具合がないか確認することは非常に重要です。以下に主なデバッグ手法とツールを紹介します。

- **AO Link Explorer：**
  [AO Link](https://www.ao.link/) は、AO プロセスの状態を可視化できる Web ベースのエクスプローラーです。プロセス ID を入力すると、下記情報が確認できます：

  - プロセスのタグ情報（名前、所有者など）
  - Inbox/Outbox にあるメッセージ履歴
  - `ao.log()` によるログ出力
  - インタラクティブにメッセージを送信して状態確認（疑似 dry-run）

この UI を使えば、ハンドラの動作確認やリプライメッセージの有無などを、CLI なしで簡単にチェックできます。

- **ログ出力 `ao.log()`：**
  Lua コード中で `ao.log("text")` または `ao.log(table)` のように書くことで、任意のデバッグ情報をログとして出力できます。これはプロセスの実行ログに記録され、AO Link や SDK のレスポンス経由で確認可能です。

ただし、本番環境では無駄なログ出力は Arweave の保存コストになるため、必要最小限に留めるのが望ましいです。ローカル開発中は、WAO を使えばログ出力が即座にターミナルに表示されるため、よりスムーズに確認できます。

- **プロセス状態の確認（State Inspection）：**
  プロセス内の状態（カウンター値、テーブル内容など）を取得するには、以下のいずれかの方法を使います：

  - `dryrun`：読み取り専用のメッセージを送信し、状態を取得（＝ Ethereum での view 関数に近い）
  - `Info` など専用のハンドラを用意し、現在の状態を返す
  - HyperBEAM 環境では、HTTP 経由での状態取得も可能（今後主流になる予定）

- **パフォーマンス監視：**
  AO プロセスには実行時間やメモリ制限があります。無限ループや過剰な計算量により実行が中断される場合もあります。これらのリソース上限は `config.yml` で設定され、CLI や AO Link でエラー内容を確認できます。

また、AO SDK の詳細モードを使えば、メッセージ処理に要した時間、レスポンスサイズなどのメタデータも取得可能です。

- **コミュニティとサポート：**
  AO 開発者コミュニティは Discord や X（旧 Twitter）で活発に活動しています。困ったときには `@ao_builders` や `@aoComputerClub` などに相談するのも有効です。

また、Community Labs や AO Ventures のブログでは、実装例や設計解説が公開されており、既知の落とし穴やベストプラクティスも学べます。Cookbook の FAQ セクションや Permaweb フォーラムも定期的にチェックすることをおすすめします。
