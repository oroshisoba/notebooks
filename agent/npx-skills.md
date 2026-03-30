# Skills を利用した Agent Skill の管理

## 概要

Agent Skills は、AI コーディングエージェントに特定の能力を追加するための再利用可能なパッケージ。
`SKILL.md` ファイルで定義されたプロシージャル知識（手順的知識）をエージェントに提供し、コード生成パターン・ドメイン専門知識・ツール連携などを実現する。

Skills は `npx skills` CLI で管理する。インストール不要で `npx` から直接実行できる。

### 主な特徴

- **モジュラー・コンポーザブル**: 必要な Skill だけ選んで導入できる
- **マルチエージェント対応**: GitHub Copilot, Claude Code, Cursor, Codex, Windsurf など 40 以上のエージェントに対応
- **プロジェクト / グローバルスコープ**: チーム共有（プロジェクト）と個人利用（グローバル）を使い分け可能
- **オープンエコシステム**: Vercel 公式 Skill に加え、コミュニティ Skill も [skills.sh](https://skills.sh/) で公開されている

---

## 対応エージェントと配置先パス

主要なエージェントの対応状況とインストール先パス:

| エージェント | 識別子 | プロジェクトパス | グローバルパス |
|---|---|---|---|
| GitHub Copilot | `github-copilot` | `.agents/skills/` | `~/.copilot/skills/` |
| Claude Code | `claude-code` | `.claude/skills/` | `~/.claude/skills/` |
| Cursor | `cursor` | `.agents/skills/` | `~/.cursor/skills/` |
| Codex | `codex` | `.agents/skills/` | `~/.codex/skills/` |
| Windsurf | `windsurf` | `.windsurf/skills/` | `~/.codeium/windsurf/skills/` |
| Cline | `cline` | `.agents/skills/` | `~/.agents/skills/` |
| Roo Code | `roo` | `.roo/skills/` | `~/.roo/skills/` |
| OpenCode | `opencode` | `.agents/skills/` | `~/.config/opencode/skills/` |
| Gemini CLI | `gemini-cli` | `.agents/skills/` | `~/.gemini/skills/` |

全エージェント一覧は [GitHub リポジトリの README](https://github.com/vercel-labs/skills) を参照。

> **Note**: CLI はインストール済みのエージェントを自動検出する。検出されない場合は、インストール先エージェントの選択プロンプトが表示される。

---

## CLI 基本操作

### Skill のインストール (`add`)

```bash
npx skills add <owner/repo>
```

#### ソースフォーマット

```bash
# GitHub shorthand（最も一般的）
npx skills add vercel-labs/agent-skills

# Full GitHub URL
npx skills add https://github.com/vercel-labs/agent-skills

# リポジトリ内の特定 Skill へのパス
npx skills add https://github.com/vercel-labs/agent-skills/tree/main/skills/web-design-guidelines

# GitLab URL
npx skills add https://gitlab.com/org/repo

# ローカルパス
npx skills add ./my-local-skills
```

#### 主要オプション

| オプション | 説明 |
|---|---|
| `-g, --global` | グローバルスコープにインストール |
| `-a, --agent <agents...>` | 対象エージェントを指定（例: `claude-code`, `codex`） |
| `-s, --skill <skills...>` | 特定の Skill のみインストール（`'*'` で全 Skill） |
| `-l, --list` | インストールせず利用可能な Skill を一覧表示 |
| `--copy` | シンボリックリンクでなくコピーでインストール |
| `-y, --yes` | 確認プロンプトをスキップ |
| `--all` | 全 Skill を全エージェントにインストール |

#### 使用例

```bash
# リポジトリ内の Skill 一覧を確認
npx skills add vercel-labs/agent-skills --list

# 特定の Skill のみインストール
npx skills add vercel-labs/agent-skills --skill frontend-design --skill skill-creator

# 特定のエージェントにインストール
npx skills add vercel-labs/agent-skills -a claude-code -a github-copilot

# CI/CD 向け非対話インストール
npx skills add vercel-labs/agent-skills --skill frontend-design -g -a claude-code -y

# 全 Skill を全エージェントにインストール
npx skills add vercel-labs/agent-skills --all
```

### インストールスコープ

| スコープ | オプション | パス | 用途 |
|---|---|---|---|
| プロジェクト | （デフォルト） | `./<agent>/skills/` | プロジェクトにコミットしてチームで共有 |
| グローバル | `-g` | `~/<agent>/skills/` | 全プロジェクトで利用する個人設定 |

### インストール方式

| 方式 | 説明 |
|---|---|
| シンボリックリンク（推奨） | 各エージェントから正規コピーへのシンボリックリンクを作成。単一ソースで管理でき、更新が容易 |
| コピー（`--copy`） | 各エージェントに独立したコピーを作成。シンボリックリンク非対応環境向け |

### Skill 一覧の表示 (`list`)

```bash
# インストール済み Skill の一覧（プロジェクト＋グローバル）
npx skills list

# グローバルのみ
npx skills ls -g

# エージェントでフィルタ
npx skills ls -a claude-code -a cursor
```

### Skill の検索 (`find`)

```bash
# 対話的検索（fzf 風）
npx skills find

# キーワード検索
npx skills find typescript
```

### Skill の更新確認・実行 (`check` / `update`)

```bash
# 更新有無の確認
npx skills check

# 全 Skill を最新に更新
npx skills update
```

### Skill の削除 (`remove`)

```bash
# 対話的に選択して削除
npx skills remove

# 名前指定で削除
npx skills remove web-design-guidelines

# 複数削除
npx skills remove frontend-design web-design-guidelines

# グローバルスコープから削除
npx skills remove --global web-design-guidelines

# 特定エージェントから削除
npx skills remove --agent claude-code cursor my-skill

# 全 Skill を確認なしで削除
npx skills remove --all
```

### Skill 雛形の作成 (`init`)

```bash
# カレントディレクトリに SKILL.md を作成
npx skills init

# サブディレクトリに作成
npx skills init my-skill
```

---

## 主要 Skill カテゴリ

Vercel 公式で提供されている Skill のカテゴリと代表的な Skill:

### React / Next.js

| Skill | 説明 |
|---|---|
| `vercel-react-best-practices` | React / Next.js パフォーマンス最適化ガイドライン（40 以上のルール） |
| `vercel-composition-patterns` | スケーラブルな React コンポジションパターン |
| `next-best-practices` | Next.js のファイル規約、RSC 境界、データパターン等のベストプラクティス |
| `next-upgrade` | Next.js を最新バージョンにアップグレードするガイド |
| `turborepo` | JavaScript/TypeScript モノレポ向けビルドシステムガイド |

### AI SDK

| Skill | 説明 |
|---|---|
| `ai-sdk` | AI SDK を使った AI 機能（エージェント、チャットボット、RAG）構築支援 |
| `ai-elements` | shadcn/ui ベースの AI ネイティブアプリ向けコンポーネントライブラリ |

### Design / UI

| Skill | 説明 |
|---|---|
| `web-design-guidelines` | Web Interface Guidelines 準拠のレビュー（100 以上のルール） |
| `building-components` | アクセシビリティ・コンポーザブル API・テーマ対応の UI コンポーネント構築 |

### Deployment

| Skill | 説明 |
|---|---|
| `vercel-deploy` | Vercel への即座デプロイ（40 以上のフレームワーク自動検出） |
| `vercel-cli` | Vercel CLI によるプロジェクト管理・デプロイ |

### Browser Automation

| Skill | 説明 |
|---|---|
| `agent-browser` | AI エージェント向けブラウザ自動化（ナビゲーション、フォーム入力、スクリーンショット、データ抽出） |

### Utility

| Skill | 説明 |
|---|---|
| `find-skills` | skills.sh ディレクトリから Skill を検索・インストール |
| `before-and-after` | Web ページの前後スクリーンショット比較ツール |

全 Skill 一覧は [skills.sh](https://skills.sh/) または `npx skills find` で検索可能。

---

## 独自 Skill の作成

Skill は `SKILL.md` ファイルを含むディレクトリとして構成する。

### SKILL.md の基本構造

```markdown
---
name: my-skill
description: この Skill の目的と利用シーン
---

# My Skill

エージェントに従わせる指示をここに記述する。

## When to Use

この Skill が適用されるシナリオを記述する。

## Steps

1. 最初にこれを行う
2. 次にこれを行う
```

### 必須フィールド（YAML frontmatter）

| フィールド | 説明 |
|---|---|
| `name` | 一意な識別子（小文字、ハイフン可） |
| `description` | Skill の簡潔な説明 |

### オプションフィールド

| フィールド | 説明 |
|---|---|
| `metadata.internal` | `true` に設定すると通常の検出から非表示。`INSTALL_INTERNAL_SKILLS=1` 時のみ表示・インストール可能 |

```yaml
---
name: my-internal-skill
description: 内部専用の Skill
metadata:
  internal: true
---
```

### Skill の配置先（リポジトリ内での検出パス）

CLI は以下の場所を順に検索する:

- ルートディレクトリ（`SKILL.md` がある場合）
- `skills/`
- `skills/.curated/`
- `skills/.experimental/`
- `skills/.system/`
- 各エージェント固有のディレクトリ（`.agents/skills/`, `.claude/skills/` 等）

上記に見つからない場合は再帰検索が実行される。

### 雛形の生成

```bash
npx skills init my-skill
```

---

## テレメトリ

CLI はデフォルトで匿名テレメトリデータを収集する（Skill 名、ファイル、タイムスタンプのみ。個人情報・デバイス情報は含まない）。

### オプトアウト方法

```bash
# 環境変数で無効化
DISABLE_TELEMETRY=1 npx skills add vercel-labs/agent-skills
```

| 環境変数 | 説明 |
|---|---|
| `DISABLE_TELEMETRY` | テレメトリを無効化 |
| `DO_NOT_TRACK` | テレメトリ無効化の代替手段 |
| `INSTALL_INTERNAL_SKILLS` | `1` に設定すると `internal: true` の Skill を表示・インストール可能 |

> CI 環境ではテレメトリは自動的に無効化される。

---

## トラブルシューティング

### "No skills found"

リポジトリに有効な `SKILL.md` ファイルが存在し、frontmatter に `name` と `description` の両方が記載されていることを確認する。

### Skill がエージェントに読み込まれない

- Skill が正しいパスにインストールされているか確認する（`npx skills list` で確認可能）
- エージェントのドキュメントで Skill 読み込みの要件を確認する
- `SKILL.md` の frontmatter が正しい YAML 形式であることを確認する

### パーミッションエラー

インストール先ディレクトリへの書き込み権限があることを確認する。

---

## 参考

- [Skills 公式 HP（Vercel Docs）](https://vercel.com/docs/agent-resources/skills)
- [skills.sh（Skill ディレクトリ・リーダーボード）](https://skills.sh/)
- [skills.sh ドキュメント](https://skills.sh/docs)
- [skills.sh CLI リファレンス](https://skills.sh/docs/cli)
- [skills.sh FAQ](https://skills.sh/docs/faq)
- [GitHub リポジトリ（vercel-labs/skills）](https://github.com/vercel-labs/skills)
- [Agent Skills 仕様](https://agentskills.io/)
- [GitHub Copilot Agent Skills ドキュメント](https://docs.github.com/en/copilot/concepts/agents/about-agent-skills)
