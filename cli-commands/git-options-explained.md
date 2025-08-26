# Git コマンドオプションの解説

## よく使うGitオプション

### `-c` オプション（create）

#### git switch での使用
```bash
git switch -c new-branch    # 新しいブランチを作成して移動
```

#### git checkout での使用
```bash
git checkout -b new-branch  # 新しいブランチを作成して移動
```

**意味**: create = 作成
**動作**: 新しいブランチを作成 + そのブランチに移動

### オプション有り・無しの比較

#### オプション無し（移動のみ）
```bash
git switch develop
```
- **前提条件**: developブランチが既に存在
- **動作**: 既存ブランチに移動
- **エラー例**: "pathspec 'develop' did not match" → ブランチが存在しない

#### `-c` 付き（作成 + 移動）
```bash
git switch -c develop
```
- **前提条件**: なし（新規作成なので）
- **動作**: developブランチを新規作成 → そこに移動
- **エラー例**: "branch 'develop' already exists" → 既に存在している

## 他のよく使うGitオプション

### `-b` オプション（branch）
```bash
git checkout -b feature-branch
```
**意味**: `-c` と同じ（新しいブランチ作成 + 移動）
**使い道**: `git checkout` の場合は `-b` を使う

### `-d` オプション（delete）
```bash
git branch -d old-branch
```
**意味**: delete = 削除
**動作**: ブランチを削除

### `-D` オプション（force delete）
```bash
git branch -D old-branch
```
**意味**: 強制削除
**動作**: マージされていないブランチも強制削除

### `-r` オプション（remote）
```bash
git branch -r
```
**意味**: remote = リモート
**動作**: リモートブランチのみを表示

### `-a` オプション（all）
```bash
git branch -a
```
**意味**: all = 全て
**動作**: ローカル + リモート の全ブランチを表示

### `-u` オプション（upstream）
```bash
git push -u origin main
```
**意味**: upstream = 上流設定
**動作**: リモートブランチを上流として設定

## 実践例で理解する

### ケース1: 新しい機能を開発開始
```bash
# 現在: main ブランチにいる
git switch -c feature/login
# → feature/login ブランチを作成して移動
```

### ケース2: 既存の開発ブランチで作業再開
```bash
# developブランチが既に存在している
git switch develop
# → 既存のdevelopブランチに移動
```

### ケース3: リモートブランチをローカルに持ってくる
```bash
git fetch  # リモート情報を更新
git switch -c develop origin/develop
# → リモートのdevelopを基に、ローカルにdevelopを作成
```

## オプションの組み合わせ

### 複数オプションの使用
```bash
# ブランチ削除の例
git branch -d feature-1 feature-2 feature-3

# リモート追跡ブランチの詳細表示
git branch -r -v
```

### よく使う組み合わせ
```bash
git log --oneline --graph --all    # ログの見やすい表示
git status --short                 # 状況の簡潔表示
git add --all                      # 全ファイルをステージング
```

## オプションのパターン

### 短縮形 vs フル形式
```bash
# 短縮形
git branch -d old-branch

# フル形式  
git branch --delete old-branch

# 短縮形
git commit -m "メッセージ"

# フル形式
git commit --message "メッセージ"
```

### 一般的なオプション文字の意味
- `-c` : create（作成）
- `-d` : delete（削除）
- `-r` : remote（リモート）
- `-a` : all（全て）
- `-v` : verbose（詳細表示）
- `-f` : force（強制）
- `-u` : upstream（上流設定）
- `-m` : message（メッセージ）
- `-b` : branch（ブランチ）

## 覚え方のコツ

### 1. 英語の頭文字を覚える
- `-c` = **c**reate
- `-d` = **d**elete  
- `-r` = **r**emote

### 2. よく使うパターンを体で覚える
```bash
git switch -c new-feature    # 新機能開発開始時
git add .                    # 変更を全てステージング  
git commit -m "説明"         # コミット作成
git push -u origin branch    # 初回プッシュ
```

### 3. ヘルプで確認する習慣
```bash
git switch --help    # switchコマンドのヘルプ
git commit --help    # commitコマンドのヘルプ
```

## 今回のあなたの状況

### 現状
```bash
git checkout develop
# error: pathspec 'develop' did not match
```
→ developブランチが存在しない

### 解決方法
```bash
git switch -c develop
```
**意味**: developという名前の新しいブランチを作成して、そこに移動する

### 他の方法（同じ結果）
```bash
git checkout -b develop    # 従来の方法
```

## 理解度チェック

以下のコマンドの意味が分かりますか？

1. `git switch main` 
2. `git switch -c feature/user-auth`
3. `git branch -d old-feature`
4. `git push -u origin develop`

**答え**:
1. 既存のmainブランチに移動
2. feature/user-authブランチを新規作成して移動
3. old-featureブランチを削除
4. developブランチをリモートにプッシュして上流設定

---
*作成日: 2025-08-26*
*対象: Gitオプション初心者*
*重要度: ★★★★★*