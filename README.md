# Share House OS (EnShare)

「ちょうどいい距離感の暮らしと信用をデザインする」
シェアハウスの入居から退去、日々の自治、そして次の住み替えまでをシームレスに繋ぐ、次世代のシェアハウス統合プラットフォーム（SaaS + Marketplace）です。

## 📖 Project Overview

本リポジトリは、Share House OSを構成する4つのプロダクトを統合管理する **Turborepo (Monorepo)** です。
詳細なビジネスロジックや各プロダクトの要件定義については、[`/docs`](./docs) ディレクトリのMarkdown資料を参照してください。

1. **Core OS**: 統合データベース・Stripe決済基盤・信用スコアエンジン
2. **Resident App**: 住民向け生活・自治アプリ (Mobile)
3. **Owner Console**: オーナー向け業務自動化SaaS (Web)
4. **Acquisition Portal**: 集客・市場向けポータル (Web)

## 🏗️ Architecture & Tech Stack

* **Package Manager:** `pnpm` (推奨)
* **Monorepo Tool:** Turborepo
* **Frontend (Web):** Next.js 16 (App Router), React, Tailwind CSS, shadcn/ui
* **Frontend (Mobile):** Expo (React Native), NativeWind
* **Backend & Database:** Supabase (PostgreSQL, Auth, Edge Functions, Storage, Realtime)
* **Payments:** Stripe Connect

## 📂 Directory Structure

\`\`\`text
share-house-os/
├── apps/
│   ├── resident-app/      # 📱 住民向けモバイルアプリ (Expo)
│   ├── owner-console/     # 💻 オーナー向け管理SaaS (Next.js)
│   └── public-portal/     # 🌐 集客・スカウトポータル (Next.js)
├── packages/
│   ├── core-db/           # 🗄️ Supabase連携・自動生成型定義
│   ├── ui-system/         # 🎨 共通UIコンポーネント (shadcn/ui)
│   ├── eslint-config/     # 🧹 共通Lint設定
│   └── typescript-config/ # 📝 共通TS設定
└── docs/                  # 💡 要件定義書・システムアーキテクチャ図
\`\`\`

## 🚀 Getting Started

ローカル開発環境のセットアップ手順です。

### Prerequisites

* Node.js (v20+)
* pnpm (v8+)
* [Supabase CLI](https://supabase.com/docs/guides/cli)
* Expo CLI

### Installation

1. リポジトリをクローンします。
   \`\`\`bash
   git clone https://github.com/KoenigWolf/share-house-os.git
   cd share-house-os
   \`\`\`

2. 依存関係をインストールします。
   \`\`\`bash
   pnpm install
   \`\`\`

3. 環境変数を設定します。
   各 `apps/*` ディレクトリの `.env.example` を `.env.local` にコピーし、SupabaseおよびStripeのローカルキーを設定してください。

### Running Development Servers

Turborepoを使用して、すべてのアプリケーションを同時に起動します。

\`\`\`bash
pnpm run dev
\`\`\`

* Owner Console: http://localhost:3000
* Acquisition Portal: http://localhost:3001
* Resident App: Expo GoアプリでQRコードをスキャンして起動

特定のアプリのみを起動する場合はフィルターを使用します。
\`\`\`bash
pnpm run dev --filter=owner-console
\`\`\`

## 📚 Documentation (Docs-as-Code)

本プロジェクトは Docs-as-Code のアプローチを採用しています。開発を進める前に、以下のドキュメントを必ず確認してください。

* [01. Core OS (プラットフォーム基盤) 定義書](./docs/01_core_os_requirements.md)
* [02. Resident App (住民向けアプリ) 定義書](./docs/02_resident_app.md)
* [03. Owner Console (オーナー向けSaaS) 定義書](./docs/03_owner_console.md)
* [04. Acquisition Portal (集客ポータル) 定義書](./docs/04_acquisition_portal.md)

## 🔒 Security & RLS

データベースへのアクセスはすべて Supabase の Row Level Security (RLS) を経由します。
ローカルでのDBマイグレーションやRLSのテストについては、`/packages/core-db/README.md` を参照してください。