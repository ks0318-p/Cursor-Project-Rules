## プロジェクト構成
本プロジェクトは、
Nxモノレポを使用したマイクロサービスアーキテクチャを採用しています。
フロントエンドにはNext.js App Router、バックエンドにはNestJS、データベースアクセスにはPrismaを使用しています。

### ルートディレクトリ構造

```
/
├── apps/                      # アプリケーションコード
│   ├── api/                   # NestJSバックエンドアプリケーション
│   ├── api-e2e/               # バックエンドのE2Eテスト
│   ├── frontend/              # Next.jsフロントエンドアプリケーション
│   └── frontend-e2e/          # フロントエンドのE2Eテスト
├── prisma/                    # Prisma Schema及びマイグレーションファイル
├── terraform/                 # Terraformによるインフラ定義
│   ├── environments/          # 環境別設定
│   └── modules/               # 再利用可能なモジュール
├── github/                    # GitHub関連ファイル
├── customRules/               # カスタムルール定義
└── ... (設定ファイル類)
```
