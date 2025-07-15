---
title: AO DeFi Usecases
platform: ChatGPT DeepResearch (GPT-4o)
date: 2025-07-14
url: https://chatgpt.com/s/t_6875d24328888191b3cd94cf09457b64
tags: [ao, usecase, nft]
translation_tool:
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

# Arweave の Actor Oriented Protocol（AO）における DeFi：詳細な調査

## AO 上の分散型取引所（AMM およびオーダーブック）

**Permaswap（クロスチェーン AMM／DEX）**
Permaswap は、Arweave/AO エコシステムにおける先駆的な DEX であり、高速かつガス不要のクロスチェーン・トークンスワップを可能にしています。Arweave ベースの高速 L2 である everPay の上に構築された Permaswap は、フロントランのないリアルタイムのアトミックオーダーをミリ秒単位で確定させます。2025 年初頭には、AO のネイティブトークン\$AO が Permaswap に上場し、24 時間以内に AO/wAR ペアで 100 万ドル以上の取引量を記録しました。これは、Permaswap が AO にとっての流動性ハブとして重要な役割を果たしていることを示しています。

もともとは AMM スタイルのスワッププロトコルでしたが、Permaswap は現在「Permaswap Spot」という**オーダーブックモジュール**も導入しており、AO 上で初のオンチェーンオーダーブック型 DEX となっています。このハイブリッド設計により、AMM の流動性とオーダーブックの精密さを兼ね備えつつ、AO の並列処理能力を活用して多くの注文を同時に処理できます。これにより、イーサリアムのような逐次実行環境にありがちな混雑の制約を回避しています。

**ArSwap／Perplex、Bark（高性能 DEX）**
Permaswap 以外にも、AO 上では次世代の DEX 構築が進んでいます。_ArSwap_（現在は**Perplex**にリブランド）は、**パーペチュアル契約**や高度な取引機能を提供する予定の AO DEX です。Perplex は、Uniswap v2 型の単純な AMM とは異なり、AO の計算能力を活かした\*\*オンチェーン・デリバティブ（永久先物）\*\*取引を目指しています。

また、**Bark**は Community Labs により AO リリース初日に立ち上げられた初の DEX です。Bark は低遅延かつ高スループットの取引を重視しており、各取引ペアを独立したプロセスとして動作させることで、実際に一部の CEX より高速な決済速度を実現しています。さらに、Bark は高い**コンポーザビリティ**を持ち、例えば EVM や Solana VM を AO 上で実行しているプロセスからも、統一されたメッセージ送信により Bark と取引が可能です。

これらの DEX プロジェクトは、AO が**AMM モデル**と**オーダーブック／パーペチュアルモデル**の両方に対応可能であり、しかも並列実行によりボトルネックのない処理が可能であることを実証しています。

## AO におけるステーブルコイン：Astro USDA プロトコル

**Astro（USDA ステーブルコイン）**
Astro Labs は、Arweave および AO 上で初のネイティブステーブルコインである*USDA*を導入しました。Astro のプロトコルは、Arweave のネイティブトークンである**AR**を担保とする過剰担保モデルに基づいて USDA を発行します。実際には、AR 保有者が AR を「Quantum Bridge」を通じてロックすることで、より少額の USDA をミントできるという仕組みで、これは MakerDAO の CDP モデルに似ています。たとえば、「2 ドル相当の AR を担保に 1 USDA を発行」といった形で、USDA は常に AR の価値によって裏付けられます。

この設計により、AR 保有者は AR を売却せずにステーブルな資産にアクセスすることができ、流動性を引き出すことが可能になります。USDA は、AO 上の取引、レンディング、決済といったあらゆる DeFi 機能を支える基盤通貨となることが想定されています。

Astro は AO を選んだ理由として、**ステーブルコインの発行記録を保存するための permaweb のセキュリティと永続性**、および AO 上での価格オラクルや清算ボットなどの自律型エージェントによる自動化機能を挙げています。Astro チームは、AO によってステーブルコインに**新たな機能**を実装できたと評価しており、2024 年 4 月には AO testnet 上で USDA のローンチを完了しました。

また、Astro のエコシステムには、**Quantum Bridge**と呼ばれる他のステーブルコインを AO にブリッジするための機能も用意されています。これにより、Ethereum などのチェーンから USDC や USDT といった資産を AO に転送し、それぞれ wUSDC などのラップドトークンとして受け取ることが可能です。このマルチチェーン流動性戦略は、カストディプロバイダである Copper との提携によってセキュリティが確保されており、USDA の支援体制を強化すると同時に、AO の DeFi エコシステム全体に主要ステーブル資産へのアクセスを提供しています。

このように、Astro の USDA は、**AO 上での担保型ステーブルコイン**の代表例であり、Arweave の永続ストレージと AO のクロスチェーン連携機能を活かして、安定した DeFi 通貨としての地位を築いています。

## AO におけるレンディングプロトコル

**LiquidOps（過剰担保型レンディング）**
*LiquidOps*は、Arweave および AO 上で構築されている新興のレンディング／借入プロトコルであり、AO DeFi エコシステムにおける基盤的なマネーマーケットを提供します。Arweave のベテラン開発者によって共同設立されたこのプロトコルは、ユーザーが資産（AR やステーブルコインなど）を預けて利息を得たり、担保を提供して借入を行うことを可能にします。

このプロトコルは、Compound や Aave のような過剰担保モデルを採用していますが、AO のアーキテクチャを活かして機能を強化しています。とりわけ、LiquidOps は\*\*「ネイティブ AO 清算」\*\*機構を実装しており、担保不足となったローンの監視や清算が AO 上の自律的なプロセスによって実行されます。

AO の**永続的かつ並列的な実行環境**により、LiquidOps はローンの健全性を常時監視し、清算をオンチェーンで即座に実行することができ、Ethereum のようなネットワークで必要とされるオフチェーンボットを不要にします。

また、LiquidOps は他の開発者が容易に統合できるよう、NPM パッケージや Blueprint モジュールなどの開発ツールも提供しています。これにより、DAO や他の DeFi アプリが LiquidOps に対して貸付の実行や金利の取得などを**メッセージで呼び出す**ことが可能となっています。

テスト段階では、wAR（ラップド AR）やステーブルコインを担保資産としてサポートしており、ユーザーは自らの AR 資産を担保に AO ネイティブな USD を借りることが可能です。こうした仕組みにより、AO DeFi 内での**資本効率性**が向上し、貸し手は持続可能な利回りを得て、借り手は資産を保持したまま資金を引き出すことができます。

LiquidOps は、Ethereum において多数のローン更新がネットワークを圧迫するのとは異なり、AO のスケーラビリティにより複数の借入ポジションや利息計算を同時に処理できます。これにより、AO 上のコア DeFi 機能（レンディング）が、既存の金融ロジックと AO 特有の拡張性を組み合わせて急速に成熟しつつあることを示しています。

## クロスチェーンブリッジと資産接続

AO は Arweave 上に構築された新たなレイヤーであるため、**外部資産のブリッジング**は DeFi の立ち上げにおいて極めて重要です。これを担うのが**AOX**というクロスチェーンブリッジであり、他の L1/L2 ネットワークと AO を接続するために設計されています。

AOX は everVision（everPay を開発したチーム）によって 2024 年中頃にローンチされ、**AO エコシステムに資産をシームレスに持ち込む**ことを目的としています。AOX は\*\*MPC（マルチパーティ計算）\*\*を用いたカストディ型ブリッジで、安全な署名によって資産移転を行います。

2024 年 5 月、AOX はまず Arweave の AR トークンを AO にブリッジする機能を提供しました。これにより、Arweave メインネットに預けられた AR が、AO 上では\*\*wAR（wrapped AR）\*\*として使用可能になります。これにより、時価総額 20 億ドル規模の AR 資産が AO のスマートコントラクト環境で利用可能となりました。年末までに 50,000 以上の wAR が発行され、数万人のユーザーに保有されています。

さらに 2024 年 8 月には、AOX は**Ethereum との接続**を実現。MetaMask などのウォレットから USDC をブリッジして AO 上に持ち込むことが可能となり、**wUSDC**として利用できます。加えて、Ethereum を介さずに**Base や BSC チェーン**から直接 USDC を入金する機能も追加され、ガス代の回避や高速性を実現しました。

AO 上で発行されたすべてのラップドトークン（wAR, wUSDC など）は、AO の**トークン標準**に準拠しており、ネイティブトークンと同様に扱うことができます。ブリッジは双方向に対応しており、将来的には CEX（中央集権型取引所）への直接出金も視野に入れられています。

その他にも、Astro の**Quantum Bridge**は AR やステーブルコインに特化したブリッジであり、Copper によるカストディを通じて高いセキュリティを実現しています。また、\*\*Molecular Execution Machine（MEM）\*\*は Ethereum トークンをより信頼性高く AO に持ち込むための監査済みブリッジとして準備が進んでいます。

2025 年時点では Solana との完全な接続は実装されていないものの、カストディ機構や AO の汎用的なメッセージ設計により、将来的な対応が期待されています。

総じて、AOX を中核とする AO のブリッジング構造は、他のチェーンとの資産接続における**金融的動脈**を形成しています。Ethereum や Base からの USDC ブリッジ、CEX からの直接転送などを可能にし、AO の DeFi が**孤立した島ではなく、マルチチェーン時代の中核拠点**となる基盤を整えつつあります。

## AO 上で DeFi を構築する主な利点

AO のアクター指向設計と Arweave 基盤により、DeFi 構築における独自の利点が多数存在します。

**永続的な状態と履歴**
AO の各プロセス（スマートコントラクト）は Arweave のパーマネントストレージ上に保存されるため、状態が永続的に保持されます。これにより、ユーザーの残高やローン履歴などのデータが消失することなく保持され、すべてのインタラクションが検証可能かつ不変の形で記録されます。

この特性は、DEX やレンディングプールのような DeFi アプリにとって極めて重要であり、アプリが開発者不在でも**半永久的に動作し続ける**ことを可能にします。また、分析や監査にも優れた透明性を提供します。

**並列処理によるスケーラビリティ**
AO は**グローバル VM を持たない並列型アーキテクチャ**を採用しており、あらゆる処理が独立したプロセスとして同時に実行されます。これにより、例えば複数の取引やローン処理が同時に行われても混雑することがなく、**処理能力がノード数に比例してスケール**します。

このスケーラビリティにより、オンチェーン AI 戦略、バッチオークション、高頻度取引といった**高度な DeFi ユースケース**が実現可能になります。

**プロセス間メッセージによるコンポーザビリティ**
AO では、すべてのプロセスがメッセージベースで相互に通信できます。このメッセージ機構は、異なる仮想マシン間でも利用可能であり、Solana VM や EVM で動作するプロセスから、AO ネイティブのステーブルコインや DEX プロセスにメッセージ送信が可能です。

これにより、オンチェーン上で自動取引やクロスプロトコル戦略を構成することが容易になり、DeFi における**新たな統合パターン**が登場しています。

**柔軟な実行環境（Executor／VM の差し替え）**
AO では、任意の実行環境（Executor）をプロセス単位で設定可能であり、ネイティブ Lua プロセスのほか、**EVM**や**Solana VM**といった互換環境も稼働できます。これにより、既存の Solidity コードを AO に移植し、AO の並列性やメッセージ通信機能を活かすことができます。

また、\*\*TEE（Trusted Execution Environment）\*\*対応により、機密性の高い取引処理や注文マッチングを安全なハードウェア上で実行する設計も可能になります。

**標準化されたトークンプリミティブ**
AO は、Arweave の従来環境に不足していたトークン標準（ERC-20 相当）を Blueprint として提供しており、開発者はこれをもとに迅速にトークンを発行・運用できます。USDA、wAR、wUSDC などもこの Blueprint を基にしており、**一貫性と相互運用性のあるトークン発行**が可能です。

これにより、あらゆるトークン取引が記録・検証可能な形で処理され、透明性とセキュリティが保証されます。

**低コストかつスムーズな UX**
everPay や Bundler（例：Liteseed ネットワーク）を活用することで、AO 上の多くのトランザクションは**ガス不要かつ即時決済**が可能です。たとえば Permaswap では、実際の取引が即時に完了し、ユーザーにとって Web2 ライクな滑らかさを実現しています。

さらに、ストレージのコストは初回の少額な AR 支払いで済むため、ガスベースのブロックチェーンとは異なり、**小口取引や高頻度利用に向いた経済設計**となっています。

## AO DeFi の制約と課題

AO は強力な新しいフレームワークを提供していますが、その DeFi 構築にはいくつかの**課題と制約**も存在します。

**エコシステムの初期段階**
AO のメインネットは 2025 年にローンチされたばかりであり、DeFi エコシステムはまだ初期段階にあります。流動性やユーザー数は着実に増加していますが、Ethereum のような成熟 L1 と比べるとまだ規模は小さく、多くのプロトコル（レンディング、パーペチュアルなど）は開発中またはテストネット段階にあります。

開発者やユーザーには、アクターモデルへの**学習コスト**があります。たとえば、EVM 開発者は AO プロセスをスマートコントラクトのように扱うことができますが、それでは AO の並列処理やメッセージ駆動モデルの真価を活かせません。ドキュメントやツール類（AO Cookbook や AO Link など）は改善されつつありますが、まだ発展途上です。

**ブリッジ信頼と複雑性**
現時点での資産ブリッジは、フェデレーション型または中央集権型のコンポーネントを含んでおり、純粋なオンチェーン DeFi に比べて**信頼前提**が必要です。たとえば、AOX の MPC ブリッジは 4 名の署名者で運用されており、これらの運用者のセキュリティに依存しています。

また、Ethereum・Base・BSC など複数のチェーンとの接続を扱う必要があるため、**運用の複雑性**も増加します。ラップドトークンはあくまで元の資産とは別の存在であるため、**流動性の断片化**やアービトラージの困難さも生じます。

Astro は Copper と提携し、Quantum Bridge のカストディを強化していますが、今後はより分散化された信頼レスなソリューションの構築が求められます。

**独自のセキュリティモデル**
AO は従来のブロックチェーンとは異なり、すべてのノードが全ての契約を実行するわけではありません。代わりに、各プロセスは限定的なノード群で処理され、その結果が最終的に Arweave 上に保存されます。

この「楽観的並行性」においては、**不正な実行の検出と解決**が必要となります。AO ではすべてのメッセージが Arweave に記録されるため、事後検証は可能ですが、不正検出やチャレンジ機構のツール整備はまだ発展途上です。

また、信頼性の高い計算のために\*\*TEE（Trusted Execution Environment）**や**検証可能な計算（verifiable computation）\*\*の導入も進められていますが、これらはブロックチェーンでの本格利用としては新しい技術領域です。

**状態とデータのコスト**
Arweave はデータの永続保存を可能にする一方で、書き込みには AR による**一括前払いのコスト**が発生します。DeFi アプリが大量のメッセージや状態更新を発生させる場合、この費用が積み重なる可能性があります。

そのため、プロトコルによってはストレージ費用を賄うためのインセンティブ設計（例：取引ごとの手数料徴収）が必要になります。また、プロセスごとに状態が保存され続ける設計のため、長期的なデータ肥大化への対策（ページング、アーカイブ設計など）も考慮する必要があります。

今後登場予定の**WeaveDrive**など、状態データの柔軟な管理や大容量ストレージの外部化も重要な開発ポイントになります。

**相互運用性と標準化の遅れ**
AO は新しいスタンダード（例：ANS-104 メッセージ形式、0x 形式の AR ウォレットアドレスなど）を導入していますが、一般的なウォレットやツール（ポートフォリオ管理アプリ、ハードウェアウォレットなど）ではまだ広くサポートされていません。

MetaMask との接続や ViewBlock での AO トランザクション表示など、対応は進んでいますが、まだ**業界全体との統合**という点では発展途中です。UX 面では、対応ウォレットが少ないことや、資産管理の煩雑さが短期的な障壁となる可能性があります。

## 総括

これらの課題があるにもかかわらず、AO DeFi は極めて前向きな成長軌道を描いています。アクター指向・並列実行モデルは、他のチェーンでは実現が難しかった複雑な金融 dApp（オンチェーンパーペチュアル、AI 自動取引、並列オーダーブックなど）を可能にしつつあります。

Permaswap、Astro、LiquidOps、AOX といった初期プロジェクトが基礎を築き、実際のユースケースやユーザー数も着実に拡大しています。2025 年 2 月のメインネット公開以降、AO の DeFi エコシステムは急速に成熟しつつあり、Arweave の**永続的な Web ビジョン**に対し、**持続可能な金融レイヤー**を提供し始めています。

AO はクラウドのスケーラビリティとブロックチェーンの信頼性を融合し、分散性・検証可能性・パーミッションレス性を保ちながら、開発者の自由度を飛躍的に高めています。今後数ヶ月で、Executor、メッセージ、トークン Blueprint といった AO の中核構成を活用する**新たな DeFi プロトコル**が続々と登場することでしょう。
