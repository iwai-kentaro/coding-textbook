# リポジトリの分離戦略

## なぜ別々のリポジトリが良いのか？

### 1. 目的の明確な分離

#### stacking-app（開発リポジトリ）
- **目的**: アプリケーション開発
- **変更頻度**: 開発中は高頻度（1日数回〜数十回）
- **共有対象**: チームメンバー、ユーザー、ポートフォリオ閲覧者
- **ブランチ戦略**: feature → develop → main
- **コミットメッセージ**: 機能追加、バグ修正中心

#### coding-textbook（学習リポジトリ）
- **目的**: 学習内容の蓄積・体系化
- **変更頻度**: 学習のタイミング（週数回程度）
- **共有対象**: 自分、将来の自分、他の学習者
- **ブランチ戦略**: main中心（シンプル）
- **コミットメッセージ**: 学習内容の追加・整理

### 2. 独立したライフサイクル

#### 開発プロジェクトの流れ
```
企画 → 設計 → 開発 → テスト → リリース → 保守 → 終了
```

#### 学習プロジェクトの流れ  
```
学習 → 記録 → 整理 → 復習 → 追加学習 → 継続...
```

### 3. 権限とアクセス管理

#### stacking-app
- **公開範囲**: ポートフォリオとして公開する可能性
- **協業**: 将来的にチーム開発の可能性
- **機密性**: プロダクトの秘匿情報を含む場合がある

#### coding-textbook
- **公開範囲**: 学習の軌跡として完全公開可能
- **協業**: 個人学習が中心、時々共有
- **機密性**: 基本的に全てオープン

### 4. コミット履歴の純粋性

#### 混在した場合（悪い例）
```
feat: ユーザー登録機能追加
docs: Git基礎を学習ノートに追加  
fix: バリデーションのバグ修正
docs: React Hooksについて追記
feat: ログイン機能実装
docs: 今日学んだCSS Grid
```
→ 開発の流れが見えにくい

#### 分離した場合（良い例）
**stacking-app**
```
feat: ユーザー登録機能追加
fix: バリデーションのバグ修正  
feat: ログイン機能実装
```

**coding-textbook**
```
docs: Git基礎の学習内容追加
docs: React Hooksの使い方整理
docs: CSS Gridの実践例追加
```
→ それぞれの目的が明確

## 実際のディレクトリ構造と管理

### 推奨構造
```
/Users/kentaro/projects/
├── stacking-app/           # 開発プロジェクト
│   ├── .git/              # 独立したGitリポジトリ
│   ├── src/
│   ├── package.json
│   └── README.md          # プロジェクトの説明
└── coding-textbook/        # 学習プロジェクト  
    ├── .git/              # 独立したGitリポジトリ
    ├── git/
    ├── cli-commands/
    └── README.md          # 学習の記録
```

## Git初期化の手順

### stacking-app の初期化
```bash
cd /Users/kentaro/projects/stacking-app
git init
git add .
git commit -m "Initial commit: プロジェクト開始"
```

### coding-textbook の初期化
```bash
cd /Users/kentaro/projects/coding-textbook  
git init
git add .
git commit -m "Initial commit: 学習教科書プロジェクト開始"
```

## GitHubでの管理

### リポジトリ命名の提案
- `kentaro/stacking-app` : アプリ開発用
- `kentaro/coding-textbook` : 学習記録用（または `learning-notes`）

### 公開設定の提案
- **stacking-app**: Private → 完成後にPublic
- **coding-textbook**: Public（学習の軌跡として）

## 長期的なメリット

### 1. ポートフォリオ効果
- **stacking-app**: 開発スキルの証明
- **coding-textbook**: 学習意欲と継続力の証明

### 2. キャリア発展
- 転職時に両方のリポジトリを提示
- 技術的スキル + 学習能力の両方をアピール

### 3. コミュニティ貢献
- coding-textbook が他の学習者の参考に
- 自分の学習体験が価値を生む

## 覚えるべきポイント

1. **目的が違えばリポジトリも分ける**
2. **コミット履歴の純粋性を保つ**
3. **それぞれ独立したライフサイクルで管理**
4. **将来の公開・共有を考慮した設計**

---
*作成日: 2025-08-26*
*学習レベル: Git管理戦略*