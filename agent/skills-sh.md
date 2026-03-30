# skills.sh — オープンエージェントスキルエコシステム

## 概要

[skills.sh](https://skills.sh/) は Vercel が運営する AI エージェントスキルのオープンディレクトリ。
公開されている Skill のランキング（リーダーボード）、セキュリティ監査結果、公式スキル一覧を提供しており、エージェントに導入する Skill を探す起点となるサイト。

---

## リーダーボード

Skill の人気度を匿名テレメトリデータ（`npx skills add` のインストール回数）に基づいてランキング表示する。

### 表示モード

| モード | URL | 説明 |
|---|---|---|
| All Time | [skills.sh](https://skills.sh/) | 累計インストール数による全期間ランキング |
| Trending (24h) | [skills.sh/trending](https://skills.sh/trending) | 直近 24 時間のインストール数ランキング |
| Hot | [skills.sh/hot](https://skills.sh/hot) | 直近の急上昇ランキング（増加量表示付き） |

### All Time ランキング上位（参考: 2026年3月時点）

| 順位 | Skill | リポジトリ | インストール数 |
|---:|---|---|---:|
| 1 | find-skills | vercel-labs/skills | 784.9K |
| 2 | vercel-react-best-practices | vercel-labs/agent-skills | 263.2K |
| 3 | frontend-design | anthropics/skills | 221.5K |
| 4 | web-design-guidelines | vercel-labs/agent-skills | 212.4K |
| 5 | remotion-best-practices | remotion-dev/skills | 189.2K |
| 6 | azure-ai | microsoft/github-copilot-for-azure | 146.8K |
| 7 | agent-browser | vercel-labs/agent-browser | 142.3K |
| 8 | microsoft-foundry | microsoft/github-copilot-for-azure | 141.5K |
| 9 | skill-creator | anthropics/skills | 117.4K |
| 10 | ai-image-generation | inferen-sh/skills | 114.7K |

### Trending (24h) ランキング上位（参考）

| 順位 | Skill | リポジトリ |
|---:|---|---|
| 1 | find-skills | vercel-labs/skills |
| 2 | github-actions-docs | xixu-me/skills |
| 3 | lark-doc | larksuite/cli |
| 4 | frontend-design | anthropics/skills |
| 5 | microsoft-foundry | microsoft/azure-skills |

### 主要リポジトリ別 Skill 集

リポジトリ単位で複数 Skill が公開されている主要プロバイダ:

| リポジトリ | Skill 数（概算） | 主な内容 |
|---|---:|---|
| microsoft/github-copilot-for-azure | 20+ | Azure 全般（AI, Storage, Kubernetes, Compute 等） |
| microsoft/azure-skills | 20+ | Azure サービス別スキル |
| vercel-labs/agent-skills | 10+ | React, Next.js, UI/UX ベストプラクティス |
| anthropics/skills | 10+ | フロントエンド設計, Skill 作成, PPTX 等 |
| inferen-sh/skills | 10+ | AI 画像生成, 各種モデル |
| pbakaus/impeccable | 5+ | コード品質改善（normalize, polish, extract, distill 等） |
| larksuite/cli | 18+ | Lark 関連ドキュメント・ツール |

---

## Official（公式スキル）

[skills.sh/official](https://skills.sh/official) では、技術やプロダクトを開発している企業・組織自身が公開した公式スキルが一覧表示される。
「製品を作った本人が教える使い方」という位置付け。

### 主な公式スキルプロバイダ

| プロバイダ | 説明 |
|---|---|
| [anthropics](https://skills.sh/anthropics) | Claude 向けフロントエンド設計、Skill 作成ツール等 |
| [vercel-labs](https://skills.sh/) | React/Next.js ベストプラクティス、デプロイ、ブラウザ自動化 |
| [microsoft](https://skills.sh/microsoft) | Azure・GitHub Copilot 向け各種クラウドスキル |
| [supabase](https://skills.sh/supabase) | Postgres ベストプラクティス |
| [remotion-dev](https://skills.sh/remotion-dev) | Remotion 動画生成ベストプラクティス |
| [apollographql](https://skills.sh/apollographql) | GraphQL スキル |
| [auth0](https://skills.sh/auth0) | 認証・認可スキル |
| [bitwarden](https://skills.sh/bitwarden) | パスワードマネジャー・AI プラグイン |
| [brave](https://skills.sh/brave) | Brave Search スキル |
| [browser-use](https://skills.sh/browser-use) | ブラウザ自動化 |
| [sentry](https://skills.sh/sentry) | エラー監視・CLI |

---

## Security Audits（セキュリティ監査）

[skills.sh/audits](https://skills.sh/audits) では、公開 Skill に対するセキュリティ監査結果を確認できる。
3 つの監査ソースを組み合わせた複合評価が提供される。

### 監査ソース

| ソース | 評価内容 |
|---|---|
| **Gen** (Agent Trust Hub) | Skill 内容の安全性（`SAFE` / `UNSAFE`） |
| **Socket** | 依存関係のアラート数（`0 ALERTS` 等） |
| **Snyk** | リスクレベル（`LOW RISK` / `MED RISK` / `HIGH RISK` / `CRITICAL`） |

### 監査結果の見方

- **Gen: SAFE** — Skill の内容に悪意のあるコードや指示が含まれていない
- **Socket: 0 ALERTS** — 依存パッケージに既知の脆弱性アラートがない
- **Snyk: LOW RISK** — セキュリティリスクが低い（MED, HIGH, CRITICAL の順にリスクが増加）

### 上位 Skill の監査結果例

| Skill | Gen | Socket | Snyk |
|---|---|---|---|
| find-skills | SAFE | 0 ALERTS | MED RISK |
| vercel-react-best-practices | SAFE | 0 ALERTS | LOW RISK |
| frontend-design | SAFE | 0 ALERTS | LOW RISK |
| web-design-guidelines | SAFE | 0 ALERTS | MED RISK |
| remotion-best-practices | SAFE | 0 ALERTS | MED RISK |

> **注意**: Vercel はエコシステムの安全性維持に努めているが、すべての Skill の品質・安全性を保証するものではない。インストール前に内容を確認することが推奨される。

---

## 対応エージェント

skills.sh に掲載されている Skill は以下のエージェントで利用可能（一部）:

AMP, Antigravity, Claude Code, ClawdBot, Cline, Codex, Cursor, Droid, Gemini, GitHub Copilot, Goose, Kilo, Kiro CLI, Nous Research, OpenCode, Roo, Trae, VSCode, Windsurf 他

---

## CLIからの検索

Web ブラウザを使わず、CLI から Skill を検索することも可能:

```bash
# 対話的に検索（fzf 風）
npx skills find

# キーワードで検索
npx skills find typescript

# リポジトリ内の Skill 一覧を確認
npx skills add vercel-labs/agent-skills --list
```

---

## 参考

- [Skills 公式 HP](https://skills.sh/)
- [Official（公式スキル一覧）](https://skills.sh/official)
- [Security Audits（監査結果）](https://skills.sh/audits)
- [Docs（ドキュメント）](https://skills.sh/docs)
- [CLI リファレンス](https://skills.sh/docs/cli)
- [FAQ](https://skills.sh/docs/faq)
- [GitHub リポジトリ（vercel-labs/skills）](https://github.com/vercel-labs/skills)