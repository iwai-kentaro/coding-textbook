# GitHub CLI (gh) の基礎

## GitHub CLIとは？

GitHubが公式提供するコマンドラインツール。ブラウザを開かずにGitHub操作が可能。

## インストール方法

### Mac（Homebrew使用）
```bash
brew install gh
```

### その他の方法
- 公式サイトからダウンロード
- パッケージマネージャー経由

## 初期設定

### 認証
```bash
gh auth login
```
- ブラウザでGitHubログイン
- トークン生成
- CLI使用許可

## 基本的なリポジトリ作成

### 新規リポジトリ作成
```bash
# 公開リポジトリ
gh repo create my-project --public

# 非公開リポジトリ  
gh repo create my-project --private

# 説明付き
gh repo create my-project --description "プロジェクトの説明" --public
```

### 現在のディレクトリをリポジトリに
```bash
# 現在のディレクトリ名でリポジトリ作成
gh repo create --source=. --public

# カスタム名でリポジトリ作成
gh repo create custom-name --source=. --private
```

## 実践的なワークフロー

### パターン1: 新規プロジェクト開始
```bash
# 1. ディレクトリ作成
mkdir my-new-project
cd my-new-project

# 2. Git初期化
git init

# 3. 初期ファイル作成
echo "# My New Project" > README.md

# 4. 初回コミット
git add .
git commit -m "Initial commit"

# 5. GitHubリポジトリ作成 + push
gh repo create --source=. --public --push
```

### パターン2: 既存プロジェクトをGitHub化
```bash
# 1. プロジェクトディレクトリに移動
cd existing-project

# 2. Git初期化（必要に応じて）
git init

# 3. ファイルをコミット
git add .
git commit -m "Initial commit"

# 4. GitHubリポジトリ作成
gh repo create --source=. --private --push
```

## よく使うコマンド

### リポジトリ管理
```bash
# リポジトリ一覧
gh repo list

# リポジトリ情報表示
gh repo view

# リポジトリ削除
gh repo delete owner/repo-name
```

### プルリクエスト
```bash
# PR作成
gh pr create --title "機能追加" --body "詳細説明"

# PR一覧
gh pr list

# PR確認
gh pr view 1
```

### Issue管理
```bash
# Issue作成
gh issue create --title "バグ報告"

# Issue一覧
gh issue list
```

## ブラウザ操作 vs CLI比較

### ブラウザでのリポジトリ作成
**メリット:**
- 直感的なUI
- 詳細オプションが分かりやすい
- 初心者向け

**デメリット:**
- 画面切り替えが必要
- 手順が多い
- 自動化しにくい

### CLIでのリポジトリ作成
**メリット:**
- ターミナルから離れずに完了
- 手順をスクリプト化可能
- 高速
- プロ感がある

**デメリット:**
- 初期設定が必要
- コマンドを覚える必要がある
- エラー対応が難しい場合がある

## 初学者への推奨

### まずはブラウザから
1. GitHubの基本操作を理解
2. リポジトリ作成の流れを把握
3. Webインターフェースに慣れる

### 慣れてきたらCLI
1. `gh` をインストール
2. 認証設定
3. 簡単なコマンドから試す

### 最終的には両方使い分け
- **新規作成**: CLI（高速）
- **詳細設定**: ブラウザ（確認しながら）
- **日常操作**: CLI（効率重視）

## 注意点

### 認証が必要
- GitHub アカウント必須
- トークン設定が必要
- 初回設定で躓きやすい

### コマンドミス
- リポジトリ名は変更困難
- 公開/非公開の設定間違い
- 削除は慎重に

## 実用例（今回のプロジェクト）

### stacking-app の場合
```bash
cd /Users/kentaro/projects/stacking-app
gh repo create stacking-app --source=. --private --push
```

### coding-textbook の場合  
```bash
cd /Users/kentaro/projects/coding-textbook
gh repo create coding-textbook --source=. --public --push
```

---
*作成日: 2025-08-26*
*学習レベル: GitHub CLI基礎*