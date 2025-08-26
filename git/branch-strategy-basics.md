# Git ブランチ戦略の基礎

## あなたが採用した戦略

### stacking-app の現在の構造
- **main ブランチ**: プロダクション環境（リリース用）
- **develop ブランチ**: 開発メインブランチ（現在ここで作業中）

これは **Git Flow** と呼ばれる代表的なブランチ戦略の一部です！

## なぜこの戦略が良いのか？

### 1. 安全性の確保
- **main**: 常に安定したコード
- **develop**: 開発中でも動作するコード
- 本番環境への誤デプロイを防止

### 2. 並行開発の準備
```
main     ←─ 安定版リリース
  ↑
develop  ←─ 開発統合ブランチ（現在ここ）
  ↑
feature  ←─ 新機能開発ブランチ（将来作成）
```

### 3. チーム開発への展開
- 複数人での開発時に混乱を防止
- レビュープロセスの導入が容易

## 一般的なブランチ戦略比較

### 1. GitHub Flow（シンプル）
```
main ←─ feature ブランチから直接マージ
```
- **適用**: 小規模、頻繁リリース
- **メリット**: シンプル、理解しやすい
- **デメリット**: 大規模には不向き

### 2. Git Flow（今回採用）
```
main     ←─ リリース用
develop  ←─ 開発統合
feature  ←─ 機能開発
hotfix   ←─ 緊急修正
```
- **適用**: 中〜大規模、計画的リリース
- **メリット**: 安全性、役割分担明確
- **デメリット**: 複雑、オーバーヘッド

### 3. GitLab Flow（中間）
```
main ←─ feature ←─ production
```
- **適用**: 継続的デプロイメント
- **メリット**: Git Flowより簡単、GitHub Flowより安全

## あなたのプロジェクトでの実践

### 現在の状況
```bash
# ブランチ確認
git branch
# * develop  ←─ 現在ここ
#   main
```

### 今後の開発フロー

#### 1. 新機能開発時
```bash
# feature ブランチ作成
git checkout -b feature/user-authentication
# 開発作業
# ...
# develop にマージ
git checkout develop
git merge feature/user-authentication
```

#### 2. リリース準備
```bash
# develop の安定版を main にマージ
git checkout main
git merge develop
git tag v1.0.0
```

### 日常的な作業パターン

#### 開発開始時
```bash
git checkout develop
git pull origin develop  # 最新版を取得
git checkout -b feature/new-feature
```

#### 開発完了時
```bash
git checkout develop
git merge feature/new-feature
git push origin develop
git branch -d feature/new-feature  # 不要ブランチ削除
```

## ブランチ命名規則

### 推奨命名パターン

#### feature ブランチ
```
feature/user-login
feature/dashboard-ui  
feature/api-integration
```

#### bugfix ブランチ
```
bugfix/login-error
bugfix/css-layout-issue
```

#### hotfix ブランチ
```
hotfix/security-patch
hotfix/critical-bug
```

## 注意点とベストプラクティス

### 1. ブランチの寿命
- **feature**: 短期間（数日〜1週間）
- **develop**: 長期間（プロジェクト全期間）
- **main**: 永続（削除しない）

### 2. コミットの粒度
```bash
# 良い例
git commit -m "feat: ログイン画面のUI実装"
git commit -m "test: ログイン機能のテスト追加"

# 避ける例  
git commit -m "いろいろ修正"
```

### 3. マージのタイミング
- **頻繁にdevelopと同期**: コンフリクト回避
- **完成してからマージ**: 未完成コードをdevelopに入れない

## coding-textbook との比較

### stacking-app（開発プロジェクト）
- **ブランチ戦略**: Git Flow
- **理由**: 安全性重視、将来の拡張性

### coding-textbook（学習プロジェクト）
- **ブランチ戦略**: GitHub Flow（main のみ）
- **理由**: シンプル、個人学習向け

## 今後の学習ポイント

### 1. ブランチ操作に慣れる
```bash
git branch          # ブランチ一覧
git checkout main   # ブランチ切り替え
git merge develop   # マージ
```

### 2. コンフリクト解決
- 複数ブランチでの作業時に発生
- エディタでの解決方法を覚える

### 3. プルリクエスト
- GitHub上でのレビュー機能
- コードの品質向上

---
*作成日: 2025-08-26*
*実装したブランチ戦略: Git Flow*
*適用プロジェクト: stacking-app*