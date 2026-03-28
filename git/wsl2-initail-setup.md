
# WSL2（Ubuntu）で GitHub Fine-grained Token を使う手順

## 0. Windows に Git for Windows をインストールする

最初に、**Windows 側に Git for Windows をインストール**します。  
これは、WSL2 から **Git Credential Manager** を利用できるようにするためです。

---

## 1. WSL2 の Ubuntu に Git をインストールする

```bash
sudo apt update
sudo apt install -y git
```

---

## 2. Git の基本設定を行う

```bash
git config --global user.name "あなたの名前"
git config --global user.email "あなたのメールアドレス"
```

---

## 3. Windows 側の Git Credential Manager を使う設定を行う

```bash
git config --global credential.helper "/mnt/c/Program\ Files/Git/mingw64/bin/git-credential-manager.exe"
git config --global credential.https://github.com.useHttpPath true
```

---

## 4. Git と Git Credential Manager が使えることを確認する

```bash
git --version
/mnt/c/Program\ Files/Git/mingw64/bin/git-credential-manager.exe --version
```

---

## 5. GitHub で Fine-grained Token を作成する

```text
Resource owner: 対象リポジトリの所有者
Repository access: Only select repositories
Permissions:
  - clone / fetch / pull だけなら Contents: Read
  - push も行うなら Contents: Read and write
```

---

## 6. HTTPS でクローンする

```bash
git clone https://github.com/OWNER/REPO.git
```

認証を聞かれたら以下を入力します。

```text
Username: GitHub のユーザー名
Password: Fine-grained Token
```

---

## 7. クローン後に確認する

```bash
cd REPO
git remote -v
git fetch
```

