# ブランチ移動の全方法

## Git 2.23以降の新しいコマンド体系

### なぜ新しいコマンドが生まれたのか？
`git checkout` は多機能すぎて初心者が混乱しやすかった
- ブランチ切り替え
- ファイル復元
- コミット移動
→ 機能を分離して分かりやすくした

## ブランチ移動の方法

### 1. git switch（推奨・新方式）

#### 基本的な移動
```bash
git switch main        # mainブランチに移動
git switch develop     # developブランチに移動
```

#### 新規作成 + 移動
```bash
git switch -c new-feature    # 作成して移動
git switch -c develop        # developを作成して移動
```

#### リモートから作成 + 移動
```bash
git switch -c develop origin/develop    # リモートブランチから作成
```

#### 前のブランチに戻る
```bash
git switch -            # 前にいたブランチに戻る
```

### 2. git checkout（従来方式）

#### 基本的な移動
```bash
git checkout main      # mainブランチに移動
git checkout develop   # developブランチに移動
```

#### 新規作成 + 移動
```bash
git checkout -b new-feature     # 作成して移動
git checkout -b develop         # developを作成して移動
```

#### リモートから作成 + 移動
```bash
git checkout -b develop origin/develop  # リモートから作成
```

#### 前のブランチに戻る
```bash
git checkout -         # 前にいたブランチに戻る
```

## 各方法の比較

### git switch の特徴
**メリット:**
- 目的が明確（ブランチ切り替え専用）
- エラーメッセージが分かりやすい
- 誤操作しにくい

**デメリット:**
- Git 2.23以降でのみ利用可能
- 古い環境では使えない

**使用例:**
```bash
# 既存ブランチに移動
git switch develop

# 新規ブランチ作成 + 移動
git switch -c feature/login

# リモートブランチから作成 + 移動  
git switch -c develop origin/develop
```

### git checkout の特徴
**メリット:**
- どのGitバージョンでも使用可能
- 歴史が長く、情報が豊富
- 多機能（ブランチ以外も操作可能）

**デメリット:**
- 多機能すぎて混乱しやすい
- ファイル復元との区別が曖昧

**使用例:**
```bash
# 既存ブランチに移動
git checkout develop

# 新規ブランチ作成 + 移動
git checkout -b feature/login

# リモートブランチから作成 + 移動
git checkout -b develop origin/develop
```

## 実践的な使い分け

### 推奨パターン（モダンなやり方）

#### 日常的なブランチ移動
```bash
git switch main        # メインに戻る
git switch develop     # 開発ブランチに移動
git switch -           # 前のブランチに戻る
```

#### 新機能開発開始
```bash
git switch main                    # 安定版に移動
git pull                          # 最新を取得
git switch -c feature/new-login    # 新機能ブランチ作成
```

#### リモートブランチを使った作業
```bash
git fetch                         # リモート情報を更新
git switch -c develop origin/develop  # リモートから作成
```

### 従来パターン（どこでも使える）

```bash
git checkout main
git checkout -b feature/new-login
git checkout -b develop origin/develop
```

## その他のナビゲーション方法

### 1. git log での確認 + 移動
```bash
# ブランチの歴史を確認
git log --oneline --graph --all

# 特定のコミットに移動（detached HEAD）
git checkout <commit-hash>

# ブランチに戻る
git switch main
```

### 2. GUI ツールでの操作
- **VS Code**: 左下のブランチ名をクリック
- **GitHub Desktop**: ブランチタブから選択
- **SourceTree**: 左側のブランチ一覧から選択

### 3. エイリアス設定（ショートカット）
```bash
# .gitconfig に追加
git config --global alias.sw switch
git config --global alias.co checkout

# 使用例
git sw develop     # git switch develop と同じ
git co main        # git checkout main と同じ
```

## エラーパターンと対処法

### ケース1: ブランチが存在しない
```bash
git switch develop
# error: pathspec 'develop' did not match

# 対処法
git fetch                        # リモート情報更新
git switch -c develop origin/develop  # リモートから作成
```

### ケース2: 未保存の変更がある
```bash
git switch main
# error: Your local changes would be overwritten

# 対処法A: 変更を保存
git add .
git commit -m "作業途中の保存"

# 対処法B: 一時保存
git stash
git switch main
git stash pop      # 後で復元
```

### ケース3: リモートブランチと同期していない
```bash
git switch develop
# Already on 'develop'
# Your branch is behind 'origin/develop'

# 対処法
git pull    # リモートの変更を取得
```

## 今回のあなたの状況での推奨解決法

### まず状況確認
```bash
git branch -a    # 全ブランチ確認
git fetch        # リモート情報更新
```

### developブランチに移動
```bash
# 新しい方法
git switch -c develop         # developが存在しない場合
git switch -c develop origin/develop  # リモートにある場合

# 従来の方法  
git checkout -b develop       # developが存在しない場合
git checkout -b develop origin/develop  # リモートにある場合
```

## おすすめ学習順序

1. **まずは git checkout で慣れる**
2. **git switch の存在を知る** 
3. **徐々に git switch に移行**
4. **エイリアスで効率化**

---
*作成日: 2025-08-26*
*Git Version: 2.23以降推奨*
*推奨コマンド: git switch*