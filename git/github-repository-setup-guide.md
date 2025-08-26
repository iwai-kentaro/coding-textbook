# GitHubリポジトリ作成 完全手順書

## 🎯 今回の目標
2つのリポジトリを作成し、ローカルプロジェクトと接続する

1. `stacking-app` (開発プロジェクト用・非公開推奨)
2. `coding-textbook` (学習記録用・公開推奨)

---

## 📋 事前準備チェックリスト

- [ ] GitHubアカウントでログイン済み
- [ ] 現在位置: `/Users/kentaro/projects/coding-textbook`
- [ ] 両方のプロジェクトディレクトリが存在することを確認

**確認コマンド:**
```bash
pwd
ls ../
```

---

## 🌐 Part 1: GitHubでリポジトリ作成（ブラウザ操作）

### Step 1-1: coding-textbook リポジトリ作成

1. **GitHubにアクセス**
   - https://github.com にアクセス
   - ログインしていることを確認

2. **新しいリポジトリ作成**
   - 右上の「+」ボタン → 「New repository」をクリック

3. **設定項目**
   ```
   Repository name: coding-textbook
   Description: プログラミング学習の記録と教科書
   Public/Private: Public (学習記録として公開)
   Add a README file: ✓ チェックしない（ローカルにある）
   Add .gitignore: None
   Choose a license: None
   ```

4. **作成実行**
   - 「Create repository」ボタンをクリック

5. **リモートURLをコピー**
   - 作成後の画面でHTTPS URLをコピー
   - 例: `https://github.com/your-username/coding-textbook.git`

### Step 1-2: stacking-app リポジトリ作成

1. **新しいリポジトリ作成**
   - 再度「+」ボタン → 「New repository」

2. **設定項目**
   ```
   Repository name: stacking-app
   Description: スタッキングアプリの開発プロジェクト
   Public/Private: Private (開発中のため非公開)
   Add a README file: ✓ チェックしない
   Add .gitignore: None
   Choose a license: None
   ```

3. **作成実行 & URL取得**
   - 作成後のHTTPS URLをコピー
   - 例: `https://github.com/your-username/stacking-app.git`

---

## 💻 Part 2: ローカルGit設定

### Step 2-1: coding-textbook のGit初期化

1. **現在位置確認**
```bash
pwd
# 期待値: /Users/kentaro/projects/coding-textbook
```

2. **Git初期化**
```bash
git init
```

3. **ファイルをステージング**
```bash
git add .
```

4. **初回コミット**
```bash
git commit -m "Initial commit: 学習教科書プロジェクト開始

- Git基礎学習教材
- CLIコマンド学習資料  
- リポジトリ管理手順書"
```

5. **リモートリポジトリ追加**
```bash
git remote add origin https://github.com/your-username/coding-textbook.git
```
※ `your-username` を実際のユーザー名に変更

6. **初回プッシュ**
```bash
git branch -M main
git push -u origin main
```

### Step 2-2: stacking-app のGit設定

1. **ディレクトリ移動**
```bash
cd ../stacking-app
pwd
# 期待値: /Users/kentaro/projects/stacking-app
```

2. **現在の状況確認**
```bash
ls -la
git status
```

3. **Git初期化（必要に応じて）**
```bash
# もし .git フォルダがなければ
git init
```

4. **ファイル整理とコミット**
```bash
# 現在の状況を確認
git status

# 必要なファイルを追加（例）
git add CLAUDE.md
# または全て追加
git add .

# 初回コミット
git commit -m "Initial commit: stacking-app開発プロジェクト開始"
```

5. **リモートリポジトリ設定**
```bash
git remote add origin https://github.com/your-username/stacking-app.git
git branch -M main  
git push -u origin main
```

---

## ✅ Part 3: 動作確認

### 確認手順

1. **両方のリポジトリでプッシュ成功確認**
```bash
# coding-textbook で
cd /Users/kentaro/projects/coding-textbook
git remote -v
git log --oneline

# stacking-app で  
cd /Users/kentaro/projects/stacking-app
git remote -v
git log --oneline
```

2. **GitHubで確認**
   - 両方のリポジトリにファイルがアップロードされていることを確認
   - コミットメッセージが正しく表示されていることを確認

---

## 🚨 トラブルシューティング

### よくあるエラーと対処法

#### 1. `git: command not found`
```bash
# Gitのインストール確認
git --version
# インストールされていない場合はHomebrewなどでインストール
```

#### 2. `remote origin already exists`
```bash
# 既存のリモートを削除して再設定
git remote remove origin
git remote add origin https://github.com/username/repo.git
```

#### 3. `authentication failed`
- GitHubのユーザー名・パスワードを確認
- 2段階認証の場合はPersonal Access Token使用

#### 4. `nothing to commit`
```bash
# ファイルが正しくステージングされているか確認
git status
git add .
```

---

## 📝 完了後の状態

成功すると以下の状態になります：

```
/Users/kentaro/projects/
├── stacking-app/           
│   ├── .git/              # Gitリポジトリ（GitHub連携済み）
│   └── ...                # プロジェクトファイル
└── coding-textbook/        
    ├── .git/              # Gitリポジトリ（GitHub連携済み）
    ├── README.md
    ├── git/
    └── cli-commands/
```

**GitHub上:**
- https://github.com/your-username/stacking-app (Private)
- https://github.com/your-username/coding-textbook (Public)

---

## 🎉 次のステップ

リポジトリ作成完了後：
1. 開発環境の整備
2. プロジェクトの本格的な開発開始
3. 学習内容の継続的な記録

---
*作成日: 2025-08-26*
*対象: Git初心者〜中級者*
*推定作業時間: 30分*