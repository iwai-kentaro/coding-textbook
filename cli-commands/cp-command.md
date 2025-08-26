# CLIでのディレクトリコピー方法

## 基本的なコピーコマンド

### cp コマンドの基本構文
```bash
cp [オプション] コピー元 コピー先
```

### ディレクトリのコピーに必要なオプション

#### -r (recursive: 再帰的)
- **なぜ必要？**: ディレクトリの中身（サブディレクトリやファイル）も全てコピーするため
- **使い方**: `cp -r 元ディレクトリ 新ディレクトリ`

## よく使う組み合わせオプション

```bash
cp -r     # 再帰的コピー（基本）
cp -rp    # パーミッション（権限）も保持
cp -rv    # 詳細表示（何がコピーされたか表示）
cp -rn    # 上書きしない（既存ファイルを保護）
```

## 実際の使用例

### 基本的なディレクトリコピー
```bash
# stacking-appを同じ階層にコピー
cp -r stacking-app stacking-app-backup

# 別の場所にコピー
cp -r stacking-app /Users/kentaro/projects/stacking-app
```

### 安全なコピー（推奨）
```bash
# パーミッション保持 + 詳細表示
cp -rpv stacking-app /Users/kentaro/projects/stacking-app
```

## 実践例: プロジェクト移動手順

### Step 1: projectsディレクトリ作成
```bash
mkdir -p /Users/kentaro/projects
```

### Step 2: プロジェクトをコピー
```bash
cp -rpv /Users/kentaro/stacking-app /Users/kentaro/projects/
```

## 注意点とコツ

### ⚠️ 注意すること
- **コピー先が既に存在する場合**: 中身が混在する可能性
- **隠しファイル**: .gitフォルダなども含めてコピーされる
- **権限**: -pオプションで元のファイル権限を保持

### 💡 安全なやり方
1. まずコピー先ディレクトリの確認
2. -nオプションで上書き防止
3. -vオプションで進行状況確認

### 自分自身をコピーする際の注意
現在のディレクトリの中にいる場合は、まず親ディレクトリに移動：
```bash
# 1. 現在位置確認
pwd

# 2. 親ディレクトリに移動  
cd ..

# 3. stacking-appが見えることを確認
ls | grep stacking

# 4. コピー実行
cp -rpv stacking-app ~/projects/
```

---
*作成日: 2025-08-26*
*学習プロジェクト: stacking-app*