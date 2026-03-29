# it-build

GitHub Copilot の社内SE向け仕事用エージェントチーム。
`/support` 一本で、運用・開発・レビュー・ユーザーサポート・ナレッジ管理に対応する。

---

## 使い方

```
/support
```

起動すると **運用サポートコンダクター** が依頼内容を確認し、最適な部門に振り分ける。

依頼例は [`examples/`](examples/) フォルダを参照。

---

## 構成

```
it-build/
├── .copilot-plugin/
│   └── plugin.json          # ルートプラグイン定義（/support コマンド）
├── plugins/
│   ├── Support/             # 運用・保守系（コンダクター本体）
│   │   └── skills/support/
│   │       ├── SKILL.md     # 全部門への振り分けロジック
│   │       └── departments/
│   │           ├── ops.md       # 運用監視部
│   │           ├── dev.md       # 保守開発部
│   │           ├── infra.md     # インフラ部
│   │           ├── docs.md      # ドキュメント部
│   │           └── security.md  # セキュリティ部
│   ├── Review/              # レビュー系
│   │   └── skills/review/departments/
│   │       ├── code.md      # コードレビュー部
│   │       ├── design.md    # 設計レビュー部
│   │       ├── sql.md       # SQLレビュー部
│   │       └── doc.md       # ドキュメントレビュー部
│   ├── UserSupport/         # 社内ユーザーサポート系
│   │   └── skills/usersupport/departments/
│   │       ├── pc.md        # PC・端末サポート部
│   │       ├── app.md       # アプリ操作サポート部
│   │       ├── account.md   # アカウント・権限管理部
│   │       └── network.md   # ネットワーク・接続サポート部
│   └── Knowledge/           # ナレッジ管理系
│       └── skills/knowledge/departments/
│           ├── organize.md      # ナレッジ整理部
│           ├── standardize.md   # 標準化・手順書部
│           ├── faq.md           # FAQ管理部
│           └── template.md      # テンプレート管理部
├── context/                 # 社内固有のコンテキスト情報
│   ├── systems.md           # 社内システム一覧
│   ├── tech-stack.md        # 技術スタック
│   ├── network.md           # ネットワーク・インフラ構成
│   ├── rules.md             # 社内ルール・申請フロー
│   └── output-format.md     # 部門別出力フォーマット定義
├── examples/                # サンプル依頼集
│   ├── support-examples.md
│   ├── review-examples.md
│   ├── usersupport-examples.md
│   └── knowledge-examples.md
├── README.md
└── LICENSE
```

---

## 振り分け一覧

| 依頼の種類 | 担当部門 |
|---|---|
| 障害対応・バッチ異常・監視 | 運用監視部 |
| バグ修正・コード改修・テスト | 保守開発部 |
| サーバ・ネットワーク・クラウド | インフラ部 |
| 手順書・報告書・変更申請書 | ドキュメント部 |
| 権限・監査・セキュリティリスク | セキュリティ部 |
| コードのレビュー依頼 | コードレビュー部 |
| 設計書・要件のレビュー依頼 | 設計レビュー部 |
| SQL・DBのレビュー依頼 | SQLレビュー部 |
| ドキュメントのレビュー依頼 | ドキュメントレビュー部 |
| PC・端末トラブル | PC・端末サポート部 |
| 社内システム・Office操作 | アプリ操作サポート部 |
| アカウント発行・権限申請 | アカウント・権限管理部 |
| VPN・社内LAN・接続トラブル | ネットワーク・接続サポート部 |
| ナレッジの整理・分類 | ナレッジ整理部 |
| 作業の標準化・手順書作成 | 標準化・手順書部 |
| FAQ作成・問い合わせのナレッジ化 | FAQ管理部 |
| テンプレートの作成・管理 | テンプレート管理部 |

---

## セットアップ

### 1. コンテキスト情報の記入（必須）

`context/` フォルダの各ファイルに社内環境の情報を記入する。
これを埋めることで、AIの回答が社内固有の内容になる。

| ファイル | 記入内容 |
|---|---|
| [context/systems.md](context/systems.md) | 使用中のシステム・バッチ・外部連携 |
| [context/tech-stack.md](context/tech-stack.md) | 言語・DB・クラウド・CI/CDツール |
| [context/network.md](context/network.md) | IPレンジ・サーバ一覧・VPN情報 |
| [context/rules.md](context/rules.md) | 変更管理・障害対応・セキュリティルール |

### 2. GitHub Copilot に読み込ませる

GitHub Copilot Chat で `/support` と入力して起動する。

---

## TODO

### 高優先度
- [ ] `context/systems.md` に社内システム情報を記入する
- [ ] `context/tech-stack.md` に技術スタックを記入する
- [ ] `context/network.md` にネットワーク・サーバ構成を記入する
- [ ] `context/rules.md` に社内ルール・申請フローを記入する

### 中優先度
- [ ] 各部門ファイル（`departments/*.md`）を実務内容に合わせてカスタマイズする
- [ ] `examples/` のサンプル依頼を実際によく使う依頼に更新する
- [ ] 出力フォーマット（`context/output-format.md`）を社内標準に合わせて調整する

### 低優先度
- [ ] `CHANGELOG.md` を作成してバージョン管理を始める
- [ ] GitHub Actions でプラグインの書式バリデーションを自動化する
- [ ] 新しい部門・チームが必要になったら `plugins/` に追加する
