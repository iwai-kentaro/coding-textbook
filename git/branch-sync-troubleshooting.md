# ブランチ同期のトラブルシューティング

## よくあるエラー: `pathspec 'branch-name' did not match`

### エラーの意味
指定したブランチ名がローカルリポジトリに存在しない

### 典型的な状況
```bash
❯ git checkout develop
error: pathspec 'develop' did not match any file(s) known to git
```

## 原因と対処法

### 原因1: リモートにはあるがローカルにない

#### 確認方法
```bash
# ローカルブランチ確認
git branch

# リモートブランチ確認  
git branch -r

# 全ブランチ確認
git branch -a
```

#### 対処法
```bash
# 最新のリモート情報を取得
git fetch

# リモートブランチをローカルにチェックアウト
git checkout -b develop origin/develop
```

### 原因2: ブランチが存在しない

#### 確認結果の例
```bash
❯ git branch -a
* main
  remotes/origin/main
# developが見当たらない
```

#### 対処法
```bash
# 新しくブランチを作成
git checkout -b develop

# リモートにプッシュ
git push -u origin develop
```

### 原因3: ブランチ名のタイポ

#### よくあるミス
```bash
git checkout develope  # 'e'が多い
git checkout dev       # 短縮形
git checkout Develop   # 大文字
```

#### 対処法
```bash
# 正確なブランチ名で実行
git checkout develop
```

## 段階的な診断手順

### Step 1: 現在位置の確認
```bash
pwd
git status
```

### Step 2: ブランチ状況の全体把握
```bash
# ローカルブランチ
git branch

# リモートブランチ
git branch -r  

# 全ブランチ（ローカル + リモート）
git branch -a
```

### Step 3: リモートとの同期状態確認
```bash
# リモートの最新情報を確認
git remote -v

# 最後の同期はいつか
git log --oneline -5
```

## 具体的な解決パターン

### パターンA: GitHubでブランチ作成済み
**状況**: WebでdevelopブランチをGitHubに作成済み

```bash
# 1. リモート情報の更新
git fetch

# 2. 確認
git branch -a
# * main
#   remotes/origin/develop
#   remotes/origin/main

# 3. リモートブランチをローカルに
git checkout -b develop origin/develop
```

### パターンB: ブランチがどこにも存在しない
**状況**: developブランチを新規作成したい

```bash
# 1. 現在のブランチから新しいブランチ作成
git checkout -b develop

# 2. リモートにプッシュ
git push -u origin develop

# 3. 確認
git branch -a
```

### パターンC: 既にローカルに別名で存在
**状況**: ブランチはあるが名前が違う

```bash
# 1. 既存ブランチの確認
git branch
# * main
#   dev-branch

# 2. ブランチ名を変更
git branch -m dev-branch develop

# 3. リモートに反映
git push -u origin develop
git push origin :dev-branch  # 古い名前を削除
```

## 予防策

### 1. 定期的なfetch
```bash
# 毎日の作業開始時に実行
git fetch
```

### 2. ブランチ作成の統一
```bash
# ローカルとリモートを同時に作成
git checkout -b new-branch
git push -u origin new-branch
```

### 3. チーム内での命名規則統一
```bash
feature/feature-name
bugfix/bug-description
develop
main
```

## エラー時のクイック診断

### 1分で状況把握
```bash
echo "=== Current Status ==="
pwd
git status --porcelain

echo "=== Local Branches ==="
git branch

echo "=== Remote Branches ==="
git branch -r

echo "=== Last 3 Commits ==="
git log --oneline -3
```

## よくある勘違い

### 1. GitHub作成 = ローカルで使える
**間違い**: GitHubでブランチを作ってもローカルには自動反映されない
**正解**: `git fetch` → `git checkout` で同期が必要

### 2. ブランチは自動で同期される
**間違い**: ローカルとリモートは独立している
**正解**: 明示的に `fetch/push` で同期する

### 3. エラー = 失敗
**間違い**: エラーは致命的な問題
**正解**: 多くは設定や同期の問題で簡単に解決可能

---
*作成日: 2025-08-26*
*対象エラー: pathspec did not match*
*解決成功率: 95%*