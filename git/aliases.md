# Git おすすめエイリアス設定

よく使う Git コマンドをエイリアスに登録することで、入力の手間を減らし作業効率を向上させることができます。  
このページでは、開発者コミュニティで広く推奨されているエイリアス設定をまとめています。

---

## エイリアスの設定方法

### コマンドで設定する場合

`git config --global` コマンドを使って設定します。

```bash
git config --global alias.<エイリアス名> '<元のコマンド>'
```

### `~/.gitconfig` を直接編集する場合

`~/.gitconfig` を開き、`[alias]` セクションに追記します。

```ini
[alias]
	st = status
	co = checkout
```

---

## 基本コマンドの短縮（定番エイリアス）

日本・海外問わず、ほぼすべての開発者が設定する定番です。

| エイリアス | 元のコマンド | 説明 |
|---|---|---|
| `st` | `status` | 変更状態の確認 |
| `co` | `checkout` | ブランチ切り替え・ファイル復元 |
| `sw` | `switch` | ブランチ切り替え（Git 2.23以降の推奨コマンド） |
| `br` | `branch` | ブランチ一覧・作成・削除 |
| `ci` | `commit` | コミット |
| `cm` | `commit -m` | コミットメッセージを直接指定してコミット |
| `df` | `diff` | 変更差分の確認 |
| `ad` | `add -A` | すべての変更をステージに追加 |

```bash
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.sw switch
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.cm 'commit -m'
git config --global alias.df diff
git config --global alias.ad 'add -A'
```

---

## よく使うオプション付きコマンドのエイリアス

### ログ関連

```bash
# 直前のコミット内容を確認
git config --global alias.last 'log -1 HEAD'

# シンプルな1行ログ（ブランチ分岐も可視化）
git config --global alias.lg 'log --oneline --graph --decorate --all'

# カラー付きで見やすいログ（コミットハッシュ・ブランチ・メッセージ・日時・著者を表示）
git config --global alias.lgg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
```

| エイリアス | 元のコマンド | 説明 |
|---|---|---|
| `last` | `log -1 HEAD` | 直前のコミット情報を表示 |
| `lg` | `log --oneline --graph --decorate --all` | 全ブランチを1行・グラフ形式で表示 |
| `lgg` | `log --color --graph --pretty=format:...` | カラー付きの見やすいグラフログ |

### コミット修正

```bash
# 直前のコミットメッセージや内容を修正（コミットメッセージは変更しない）
git config --global alias.amend 'commit --amend --no-edit'

# 直前のコミットメッセージを変更
git config --global alias.reword 'commit --amend'
```

### ステージ操作

```bash
# ステージを取り消す（git add の取り消し）
git config --global alias.unstage 'reset HEAD --'
```

### スタッシュ

```bash
# 変更を一時保存
git config --global alias.sta stash

# 一時保存した変更を復元
git config --global alias.stp 'stash pop'
```

### プッシュ

```bash
# 現在のブランチを origin にプッシュ
git config --global alias.poh 'push origin HEAD'
```

### 設定確認

```bash
# 設定中のエイリアス一覧を表示
git config --global alias.alias '!git config --get-regexp ^alias\.'
```

---

## まとめ：`~/.gitconfig` への一括設定例

上記のエイリアスをまとめて設定したい場合は、`~/.gitconfig` の `[alias]` セクションに以下を追記してください。

```ini
[alias]
	# 基本コマンドの短縮
	st     = status
	co     = checkout
	sw     = switch
	br     = branch
	ci     = commit
	cm     = commit -m
	df     = diff
	ad     = add -A

	# ログ
	last   = log -1 HEAD
	lg     = log --oneline --graph --decorate --all
	lgg    = log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit

	# コミット修正
	amend  = commit --amend --no-edit
	reword = commit --amend

	# ステージ操作
	unstage = reset HEAD --

	# スタッシュ
	sta    = stash
	stp    = stash pop

	# プッシュ
	poh    = push origin HEAD

	# エイリアス一覧
	alias  = !git config --get-regexp ^alias\\.
```

---

## 参考

- [Git 公式ドキュメント - Git エイリアス](https://git-scm.com/book/ja/v2/Git-%E3%81%AE%E5%9F%BA%E6%9C%AC-Git-%E3%82%A8%E3%82%A4%E3%83%AA%E3%82%A2%E3%82%B9)
- [Gitエイリアスを設定してよく使うコマンドを簡略化する方法 - エキサイト TechBlog](https://tech.excite.co.jp/entry/2024/07/16/155247)
- [Git Aliases for Developers: 25+ Time-Saving Shortcuts for Your Workflow](https://weirdion.com/posts/2025-04-21-supercharging-your-git-aliases-my-developer-setup/)
- [A better git log - Coderwall](https://coderwall.com/p/euwpig/a-better-git-log)
