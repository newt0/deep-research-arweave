---
title: Memetoken on AO
platform: ChatGPT DeepResearch (GPT-4o)
date: 2025-07-17
url: https://chatgpt.com/s/t_688835be8558819195ae5c85c6dfedec
tags: [ao, developer, memetoken]
---

[PROMPT]

```markdown
Please conduct a technical investigation into Memetoken projects built on Arweave’s Actor Oriented Protocol (AO), with a focus on the following:

## Focus Areas

- Representative Memetoken projects: For examples, `$BREAD`, $`$MILK`,  `$SMONEY` , and use cases in 0rbit or Botega
- Token issuance and distribution patterns: Use of Token Blueprints, Dispensers, and event-driven drops via Hooks
- Community-driven meme creation and incentive design: AI/LLM integration, rewards based on engagement (e.g., likes)
- Integration with NFTs and games: Unlockable NFT mints via token holdings, in-game rewards or currencies
- Token design and security considerations: Initial supply/distribution rules, spam prevention, Sybil resistance
- DAO and governance integration: Use as voting tokens, DAO formation driven by meme culture

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

---

# [OUTPUT]

## AO 上の代表的な Memetoken プロジェクト

- `$TRUNK` （AO 初の Memecoin）：2024 年 4 月に AO 初のミームコインとしてローンチ。テストネットのクレジット（$AOCRED）を使って 1:1 の比率で誰でもミント可能というフェアローンチ形式を採用 。コミュニティ主導で価格は急騰（約 0.015 ドル相当から 200 ドルまで上昇）し、AO のソーシャルプラットフォームでのチップとして利用可能に 。

- `$BENCAT`（Bencat コイン）：猫をテーマにした Memetoken。2024 年後半に注目を集めた。事前販売や VC 割当なしの 100%フェアローンチ。ボンディングカーブディスペンサーを用いて供給 。バイラルな猫ミームとマーケティングにより、最大時は時価総額 550 万ドルに到達。AO の DEX が一時的に過負荷になるほどの人気を見せた 。

- `$NAB`（Number Always Bigger）：「価格が常に上がる」設計のミームトークン 。動的供給制御により価格の下限が上がり続けるよう設計 。配布はイールドファーミングやクエストベースで `$wAR` や `$qAR` のステーキングや、Permaswap や Botega などの AO DEX での LP 提供により獲得可能 。

- `$BREAD` & `$MILK`：コミュニティ主導の食べ物系ミームトークン（例："Let's get this bread!"）。詳細なドキュメントは少ないが、Token Blueprint を用いたフェアローンチ形式で短時間に展開され、ソーシャル上で人気。

- `$SMONEY` （Space Money）：完全オンチェーンゲーム「StarGrid Battle Tactics」から生まれた GameFi 系ミームトークン。プレイヤーは勝利によって `$SMONEY` を獲得 。供給量は 200 億、うち 70%がゲーム報酬に割当。エアドロップ、DEX 流動性、コミュニティ報酬にも使用 。「Permaweb Index」に登録されており、AO のステーカーは報酬を `$SMONEY` のミントに回すことができる 。

## AO におけるトークン発行と配布のパターン

- Token Blueprint による簡易ローンチ：AO は ERC-20 に相当する標準トークンの設計図（Blueprint）を提供しており、開発者はこれを使って迅速にミームトークンを展開可能 。Community Labs の*aoWebWallet*では UI 上で自作トークンの作成・デプロイが可能になっている 。

- フェアローンチの仕組み：AO 上の多くのミームトークンは ICO やプレマインを行わず、100%コミュニティ配布を実施。以下のような手法が取られる：

  - _デポジット・トゥ・ミント形式_： `$TRUNK` ではテストネットクレジットを預けることで固定レートでミントが可能だった 。$`$APUS` でも、ステークされたアセットを基にトークンをミントできた 。
  - _ボンディングカーブディスペンサー_：`$BENCAT` では、初期価格が低く購入が進むごとに価格が上昇するボンディングカーブを採用 。
  - _イールド・デリゲーション_：AO の ネイティブトークン報酬を他トークンのミントに充てる機能により、 `$SMONEY` や`$GAME` などの新規トークンがステーカーによりミントされる形式が実現 。

- Hooks によるイベント駆動のトークン配布：

  - _ゲーム内イベント_: StarGrid ではプレイヤーが試合に勝利すると `$SMONEY` がミントされる 。Llama Land では AI 主導ゲームのスコアに基づき$LLAMA を配布 。
  - _DeFi アクション_: `$NAB` では LP 提供やステーキングイベントがトリガーになって報酬が発生 。
  - _ソーシャルイベント_: 今後の展開として、ソーシャルエンゲージメント（例：投稿のいいね数）に応じてミームトークンを自動配布する Hooks の利用が期待されている。実際、Typr では `$TRUNK` を投稿にチップする機能が実装済み 。

## ミーム生成、AI 統合、インセンティブ設計

- コミュニティ主導のミーム文化：AO のミームトークンはコミュニティによる創造力に支えられている。エコシステムでは _「Memethon」_（ミームハッカソン）を開催し、ユーザーがバイラルなコンテンツを制作して報酬を得る機会を提供 。`$BENCAT` のチームは X（旧 Twitter）上で日々猫ミームを投稿し、ファン層を築いた 。

- AI と LLM の活用：AO の 超並列計算と永続ストレージにより、AI エージェントが dApp に参加可能となる。Botega では AI エージェントが DeFi 運用を担い、将来的にはミームトークンの財務管理やマーケットメイクに応用可能 。また、Arche のようなプロジェクトではコミュニティデータで訓練された AI キャラがスレッド内でユーザーと対話するなど、ミーム体験を強化している 。一部のコミュニティは、GPT-4 やカスタム LLM を活用してミーム生成を自動化している。

- エンゲージメントに基づく報酬：多くのミームプロジェクトでは 「いいねで報酬」「投稿で報酬」 といった参加型インセンティブを設計。例えば、あるトークンは投稿のいいね数に応じて配布される、または人気投稿者に自動でドロップされるといった仕組みが構想されている。0rbit のような AO 上のソーシャルアプリはユーザーの投稿データをトラッキングできるため、こうした「バイラル度に応じた報酬」ロジックが実装しやすい。Typr の「ソーシャルエージェント」機能や投票機能もその布石 。

## NFT やゲームとの統合

- トークン保有による NFT のアンロック：AO プロジェクトのいくつかは、ミームトークンと NFT を結びつけている。たとえば Meka NFT コレクションは、NFT 保有者限定のゲーム「Meka City」へのアクセスと、$KREDIT というゲーム内通貨を提供 。また、Permaverse の Dumdum ペットでは、仮想ペットをなでることでポイントを獲得し、これが後に$DUMDUM トークンや NFT 装備のアンロックに繋がる 。つまり、NFT とミームトークンの保有が互いの報酬条件となる設計が増えている。

- ゲーム内通貨としての利用：ミームトークンは AO 上の Web3 ゲーム内通貨としても利用されている。たとえば `$SMONEY` はゲームで勝利することで得られ、使用・交換も可能 。Llama Land の$LLAMA トークンも、AI 主導ゲームのプレイ報酬として発行された。これらのトークンは、ゲーム内の買い物、キャラの強化、イベント参加費などに使用され、プレイ＝報酬＝プレイ強化という循環を作っている。

- トークン保有による体験のゲート化：一部のコミュニティでは、一定数のミームトークンを保有しているユーザーだけが特別な NFT をミントできたり、限定ゲームに参加できたりする トークンゲート形式を採用している。AO のスマートコントラクトでは保有量チェックが可能なため、これは比較的簡単に実現可能。例えば AOuction House では、特定のミームトークン保有者のみが NFT オークションに参加可能な設計が可能 。Hoodrats NFT では、DAO オークションへの参加条件がコミュニティトークン保有に紐付いていた 。

## トークン設計とセキュリティに関する考察

- 供給量と配布ルールの設計：AO 上のミームトークンは、プロジェクトごとにさまざまな供給モデルを採用している。例として `$TRUNK` は最大供給量を 4 万枚に制限し、`$BENCAT` は 10 億枚を上限としながらも 実際に購入された分のみをミントするボンディングカーブ式を採用している。ゲーム系トークンでは `$SMONEY` のように 200 億枚規模の供給量で、ゲーム報酬としてのマイクロペイメントに耐える設計が主流 。多くのトークンが「VC 割当ゼロ」「チーム報酬ゼロ」を明記しており、完全なフェア配布を掲げる 。たとえば`$GAME` トークンは、10 億枚のうち 70%を完全にパブリックに配布すると明言し、プライベートセールや VC 向け配布を完全に排除している 。

- スパムと Sybil 攻撃対策：AO におけるフェアローンチは、複数アカウントを使って無料トークンを不正取得する Sybil 攻撃を回避するために設計されている。多くの場合、 経済的コストを伴う行動が配布条件となる。例えば `$TRUNK` は、AR 保有者（コストが発生する）によってテストネットクレジットを獲得し、それに基づいてミントされる仕組みを採用 。また、ボンディングカーブ式では価格が段階的に上がるため、Sybil 攻撃による大量取得のインセンティブが弱い。さらに、Llama Land では Vouch Protocol（人間性検証）を導入し、Bot による報酬取得を防止 。AO には SIV（Sybil Identity Verification）というプロトコルも存在し、将来的にミームトークンのエアドロップで人間性証明を条件とすることも可能 。

- セキュリティと不正対策：ミームトークンであっても、セキュリティは最重要。標準的な Token Blueprint を使うことで、オーバーフロー対策済みの安全なコントラクトコードが使われている。AO ではトークンバーン履歴を検証できる CoinBurner のようなパブリックツールも提供されており、バーンを通じて価値を高めようとするトークンでも透明性を保てる 。さらに AO の実行モデルは ステーキングとスラッシングによって保護されており、不正なミントやスパム取引を試みるアクターには経済的ペナルティが発生する 。結果として、ミーム的な外見とは裏腹に、AO 上のミームトークンは 堅牢なインフラの上で安全に運用されている。

## DAO とミームコミュニティによるガバナンス

- コミュニティ主体のガバナンス：AO 上のミームトークンは、多くが DAO 的な意思決定体制へと進化している。中央管理者や開発者報酬を持たないことから、自然とコミュニティが運営主体となる。 `$TRUNK` では、AO の創設者が 「TRUNK 保有者によって運営されるウェブページ」 と表現するほどで、その更新やコンテンツはトークン保有者の投票によって管理される方向にある 。このように、ミーム文化に根ざした軽やかな運営であっても、オンチェーンガバナンスの実装が進んでいる。

- 投票トークンとしての利用：ミームトークンはそのまま DAO の投票権として活用される。たとえば、Aolotto では$ALT トークンが Aolotto DAO のガバナンストークンとなっており、宝くじのルールや資金の使い道を決定できる。ArcDAO では`$GAME` トークンを使って、新しい GameFi プロジェクトへの支援先をコミュニティ投票で決定する設計になっている 。このように、 ミームトークンが投票のパワーを持つことで、ジョークでは終わらないコミュニティ運営が実現している。

- ミーム主導の提案活動：ミームトークンの DAO では、遊び心のあるユニークな提案が日々生まれている。提案の例としては、「チャリティーへの寄付を PR に使う」「NFT コレクションをローンチする」「他の AO dApps と連携してチップ機能を実装する」などがある。実際、 `$TRUNK` では Typr 上のチップ通貨として採用される提案が実現している 。このように、 ミーム DAO は、楽しさと実用性の両立を達成するガバナンスモデルとなっている。

## 結論

Arweave の Actor-Oriented Protocol（AO）は、 ユーモアと文化を経済価値に変換するミームトークンの理想的な実験場である。`$BREAD`、$`$MILK`、 `$SMONEY` などのプロジェクトは、堅牢な基盤と遊び心を兼ね備えた Web3 インフラの上で、フェアな分配、参加型設計、そして AI との融合を実現している。Token Blueprint、Dispenser、Hooks などの機構が、ミームトークンの展開とコミュニティ成長を技術的に支えており、 すべての「いいね」「ベット」「勝利」が新たな文化のミントにつながるエコシステムが形成されている。

AO 上のミームトークンは単なるジョークではなく、 価値の民主化と分散型文化創造の実験なのである。
