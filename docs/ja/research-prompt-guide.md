# Deep Research プロンプト設計ガイド

このドキュメントでは、Web3 関連プロジェクトに対して高品質な Deep Research を実行するための、**プロンプト設計の最適化指針**をまとめます。
とくに AO のような Web3 の新興プロトコルに対して、ChatGPT などの LLM で信頼性の高い出力を得るためには、設計段階での工夫が不可欠です。

## 設計原則

### 英語でプロンプトを書く（ただし構想は日本語で）

LLM は英語に最適化されているため、プロンプトは英語で記述・実行します。
一方で、構想や要件定義のフェーズでは、母語（日本語など）で丁寧に思考を整理する方が、意図やニュアンスのズレを防ぐことができます。

### 出力形式の明示

出力形式は必ず以下のように指定します：

- `Markdown`
- `Clear headings and bullet points`

これにより、構造化された読みやすい出力が得られます。絵文字や飾り罫線など、情報構造に寄与しない装飾は排除します。

### 調査対象の明確化（Restrictions）

精度とノイズの排除のため、調査対象には以下の制限を設けます。

- 英語圏の情報に限定する（例：Only include English-language sources）
- 調査対象プロジェクトの発表時期を起点にする（例：Only include sources published after February 2024）
- 関係のない一般情報を除外する（例：Exclude general Arweave content unless directly relevant）

### プロンプトの簡潔化

LLM はプロンプトが冗長だと焦点がブレやすくなるため、下記を意識して設計します。

- 端的かつ明確な表現にする
- 長すぎる段落は避ける
- 不要な修辞やスタイルは除外する（例：絵文字、装飾記号、感嘆表現）

### Focus Areas の設計

Focus Areas は曖昧な抽象表現ではなく、**具体的な問いや構成項目**に落とし込みます。
例えば以下のように書きます：

- What is AO? Core design principles and execution model.
- Core components: Executors, Actors, Messages.
- Release history and notable milestones.

対象プロジェクトにおける重要テーマを**見落とさず、明確に伝える**ことが重要です。

### 情報ソース（Prioritized Sources）の明示

特に Web3 プロジェクトのような未成熟分野では、**信頼性の高いソースを事前に明示すること**が極めて有効です。
以下のような分類で提示します。

- Core Docs（公式サイト、Whitepaper、Cookbook など）
- GitHub（開発中のリポジトリ）
- Blogs / Medium / Journal
- Twitter（開発者本人や公式アカウント）
- Explorers / IDE / サンプルプロジェクト

自動的に網羅されない重要ユースケースや実装事例をカバーするために、**事前に自分でリストアップ**するのが理想です。
もちろん、事前のリストアップにも AI を活用することで効率化できます。
また、一般的に主要な開発者向けツールやフレームワーク、Web3 プロトコル、L1/L2 チェーンには、`awesome xxx` のような GitHub リポジトリに有用な情報ソースがまとめられています。まず`awesome xxx` を土台にして、そこから不要なものを排除したり、最新の動向を追加すると良いでしょう。

### 調査対象読者を明記する

プロンプトの冒頭で対象読者（開発者向け／投資家向け／PM 向けなど）を明示すると、LLM の語彙選択・トーンが最適化されます。
例：

```
Please conduct a technical investigation into [プロジェクト名] from the perspective of Web3 developers.
```

### タスクを分割する

一度のプロンプトで、性質の異なる複数のタスクを同時に実行させるのは NG です。
例えば、リサーチ → 記事化 → 翻訳などを一つのプロンプトで行いがちです。
それぞれのタスクごとに区切って、プロンプトを実行しましょう。

## プロンプト構成テンプレート

以下は、実際のプロンプト作成時に使える構造テンプレートです：

```markdown
Please conduct a technical investigation into [プロジェクト名] from the perspective of [対象読者].

## Focus Areas

- [問い・観点 1]
- [問い・観点 2]
- [問い・観点 3]

## Restrictions

- Only include English-language sources published after [発表時期]
- Exclude [無関係な情報など]

## Output Format

- Markdown
- Clear headings, bullet points

## Prioritized Sources

### Core Docs

- [...]

### Key GitHub Repositories

- [...]

### Developer Blogs / Explorers

- [...]

### Twitter (X) — Core Accounts

- [...]
```
