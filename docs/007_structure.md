# structure.md

このファイルが読み込まれたら必ず「structure確認完了！」とユーザーに報告して下さい。

## 概要

QuanteeAdプロジェクトは、
Nxモノレポを使用したマイクロサービスアーキテクチャを採用しています。
フロントエンドにはNext.js App Router、バックエンドにはNestJS、データベースアクセスにはPrismaを使用しています。

## ルートディレクトリ構造

```
quanteeAd/
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

## バックエンド構造 (apps/api)

NestJSバックエンドは、機能ごとにモジュール分割されています。

```
apps/api/
├── src/
│   ├── main.ts                # アプリケーションのエントリーポイント
│   └── app/                   # アプリケーションモジュール
│       ├── app.module.ts      # ルートモジュール
│       ├── accounts/          # アカウント管理モジュール
│       ├── ad-account-integration/ # 広告アカウント連携モジュール
│       ├── ad-accounts/       # 広告アカウント管理モジュール
│       ├── ad-campaigns/      # 広告キャンペーン管理モジュール
│       ├── ad-groups/         # 広告グループ管理モジュール
│       ├── ad-platforms/      # 広告プラットフォーム管理モジュール
│       ├── ad-types/          # 広告タイプ管理モジュール
│       ├── ads/               # 広告管理モジュール
│       ├── ads-api/           # 外部広告APIとの連携
│       │   ├── google/        # Google広告API連携
│       │   ├── meta/          # Meta広告API連携
│       │   └── yahoo/         # Yahoo広告API連携
│       ├── ai-generations/    # AI生成機能モジュール
│       ├── ai-suggestion/     # AIサジェスト機能モジュール
│       ├── analysis-group/    # 分析グループモジュール
│       ├── asset-libraries/   # アセットライブラリモジュール
│       ├── audience-info/     # オーディエンス情報モジュール
│       ├── auth/              # 認証・認可モジュール
│       ├── common/            # 共通ユーティリティ
│       │   ├── constants/     # 定数定義
│       │   ├── csv/           # CSV処理
│       │   ├── decorators/    # カスタムデコレータ
│       │   ├── dict/          # 辞書・マッピング
│       │   ├── dto/           # 共通DTOクラス
│       │   ├── email/         # メール送信機能
│       │   ├── excel/         # Excel処理
│       │   ├── filters/       # 例外フィルター
│       │   ├── guards/        # ガード
│       │   ├── helpers/       # ヘルパー関数
│       │   ├── interceptors/  # インターセプター
│       │   └── uploader/      # ファイルアップロード
│       ├── config/            # 設定モジュール
│       ├── conversion-logs/   # コンバージョンログモジュール
│       ├── cv-settings/       # コンバージョン設定モジュール
│       ├── fees/              # 料金管理モジュール
│       ├── files/             # ファイル管理モジュール
│       ├── invite/            # 招待機能モジュール
│       ├── keyword/           # キーワード管理モジュール
│       ├── metric-sets/       # メトリックセットモジュール
│       ├── metric-values/     # メトリック値モジュール
│       ├── metrics/           # メトリック管理モジュール
│       ├── offline-conversion-logs/ # オフラインコンバージョンログ
│       ├── offline-metrics/   # オフラインメトリック
│       ├── permission/        # 権限管理モジュール
│       ├── prisma/            # Prismaサービス
│       ├── product-info/      # 商品情報モジュール
│       ├── projects/          # プロジェクト管理モジュール
│       ├── queue/             # キュー管理モジュール
│       ├── scheduler/         # スケジューラモジュール
│       ├── sync-ad-resource/  # 広告リソース同期モジュール
│       ├── tenants/           # テナント管理モジュール
│       ├── upload-offline-conversions/ # オフラインコンバージョンアップロード
│       ├── user-accounts/     # ユーザーアカウント管理モジュール
│       ├── user-projects/     # ユーザープロジェクト関連モジュール
│       └── users/             # ユーザー管理モジュール
└── ... (設定ファイル類)
```

### モジュール構造のパターン

各機能モジュールは以下のような構造に従っています：

```
module-name/
├── module-name.controller.ts      # コントローラー（APIエンドポイント定義）
├── module-name.controller.spec.ts # コントローラーのユニットテスト
├── module-name.service.ts         # サービス（ビジネスロジック）
├── module-name.service.spec.ts    # サービスのユニットテスト
├── module-name.module.ts          # モジュール定義
├── module-name.entity.ts          # エンティティ定義（必要な場合）
├── dto/                           # Data Transfer Objects
│   ├── create-something.dto.ts
│   ├── update-something.dto.ts
│   └── ...
└── entities/                      # エンティティ定義（複数ある場合）
```

## フロントエンド構造 (apps/frontend)

Next.js App Routerを使用したフロントエンドアプリケーションです。

```
apps/frontend/
├── src/
│   ├── app/                       # App Router ディレクトリ
│   │   ├── layout.tsx             # ルートレイアウト
│   │   ├── page.tsx               # ルートページ
│   │   ├── (auth)/                # 認証関連ルート
│   │   ├── (private)/             # 認証必須ルート
│   │   ├── api/                   # APIルート
│   │   └── _components/           # ページ間で共有するコンポーネント
│   ├── assets/                    # 静的アセット（画像、アイコン）
│   │   └── icons/                 # アイコンSVG
│   ├── components/                # 共通コンポーネント
│   │   ├── AccountMenu/           # アカウントメニュー
│   │   ├── AdPlatformButton/      # 広告プラットフォームボタン
│   │   ├── AdPreview/             # 広告プレビュー
│   │   ├── AIProgress/            # AI進捗表示
│   │   ├── Breadcrumb/            # パンくずリスト
│   │   ├── Button/                # ボタンコンポーネント
│   │   ├── Charts/                # チャートコンポーネント
│   │   ├── ... (その他UI/機能コンポーネント)
│   │   └── ui/                    # shadcn/ui コンポーネント
│   ├── constants/                 # 定数定義
│   │   └── enum/                  # 列挙型定義
│   ├── hooks/                     # カスタムフック
│   ├── lib/                       # ユーティリティ関数
│   │   ├── api/                   # APIクライアント（Orval生成）
│   │   ├── errors/                # エラーハンドリング
│   │   ├── slices/                # Redux スライス
│   │   └── utils/                 # ユーティリティ関数
│   ├── providers/                 # コンテキストプロバイダー
│   ├── types/                     # 型定義
│   └── middleware.ts              # Next.js ミドルウェア
└── ... (設定ファイル類)
```

### コンポーネント構造

各コンポーネントのフォルダ構造：

```
ComponentName/
├── ComponentName.tsx          # メインコンポーネント
├── index.ts                   # エクスポート定義
└── ComponentNameChild.tsx     # 子コンポーネント（必要な場合）
```

## Prisma構造

データベースモデルとマイグレーションを管理するPrismaの構造：

```
prisma/
├── schema.prisma               # データベーススキーマ定義
├── seed.mjs                    # シードデータ（開発用）
├── seed_prod.mjs               # シードデータ（本番用）
└── migrations/                 # マイグレーションファイル
    ├── migration_lock.toml     # マイグレーションロック
    └── YYYYMMDDHHMMSS_name/    # マイグレーションごとのディレクトリ
        └── migration.sql       # SQLマイグレーションファイル
```

## Terraform構造

インフラストラクチャをコードとして管理するTerraformの構造：

```
terraform/
├── environments/               # 環境ごとの設定
│   ├── dev/                    # 開発環境
│   ├── stg/                    # ステージング環境
│   └── prod/                   # 本番環境
└── modules/                    # 再利用可能なモジュール
    ├── ap-northeast-1/         # 東京リージョン固有のモジュール
    │   ├── codeBuild/          # CodeBuild設定
    │   ├── codePipeline/       # CodePipeline設定
    │   ├── ec2/                # EC2インスタンス設定
    │   ├── ecr/                # ECRリポジトリ設定
    │   ├── ecs/                # ECSクラスター設定
    │   ├── elasticCache/       # ElastiCacheの設定
    │   ├── rds/                # RDS設定
    │   ├── secretsManager/     # SecretsManager設定
    │   ├── sg/                 # セキュリティグループ設定
    │   └── vpc/                # VPC設定
    └── global/                 # グローバルリソースモジュール
        ├── cloudfront/         # CloudFront設定
        ├── cognito/            # Cognito設定
        ├── iam/                # IAM設定
        ├── route53/            # Route53設定
        ├── s3/                 # S3バケット設定
        └── ses/                # SES設定
```

## その他重要な設定ファイル

| ファイル名            | 目的                             |
| --------------------- | -------------------------------- |
| `nx.json`             | Nxモノレポの設定                 |
| `tsconfig.base.json`  | TypeScriptのベース設定           |
| `package.json`        | プロジェクト依存関係管理         |
| `.env.example`        | 環境変数テンプレート             |
| `orval.config.ts`     | API型生成設定                    |
| `Dockerfile.frontend` | フロントエンドのDockerビルド設定 |
| `Dockerfile.backend`  | バックエンドのDockerビルド設定   |
