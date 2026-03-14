# オーナー向けSaaS（Owner Console）事業・技術定義書

## Share House OS

**作成日：** 2026年3月14日 ｜ **バージョン：** 3.0 ｜ **機密区分：** Confidential

---

## 1. プロダクトの目的と提供価値

### 1.1 位置づけ

Owner Consoleは、シェアハウスオーナー・管理会社が物件運営の全プロセスを一元管理する**SaaSダッシュボード**であり、Share House OSの**直接的な収益源（SaaS月額課金）**を担うフロントエンドプロダクトである。

Core OSの統合データベース・決済基盤・信用スコアエンジンのデータを「オーナー視点」で可視化・操作可能にし、これまで紙・電話・スプレッドシート・複数の外部サービスに分散していた管理業務を単一のWebアプリケーションに統合する。

### 1.2 解決するペイン

| ペイン | 現状の対処法 | Owner Consoleによる解決 |
|---|---|---|
| **契約手続きが紙ベースで煩雑** | 対面での重要事項説明、紙の契約書に押印、郵送での書類やり取り。1件あたり2〜3時間 | 電子契約パイプライン：入居申込 → 本人確認 → 重要事項説明（対面 or ビデオ通話） → 電子署名 → 初期費用Stripe決済 → 家賃サブスクリプション開始。すべてをOwner Console内で完結 |
| **多国籍住民への対応が困難** | 英語が通じず、翻訳アプリで逐一やり取り。要望の見落としが頻発 | 多言語チケットシステム：住民の母国語で送信されたチケットを自動翻訳表示。既読トラッキングで伝達漏れを防止 |
| **空室時の募集がゼロからのやり直し** | ポータルサイトへの再掲載、内見対応、審査、入居手続きの一連を毎回ゼロベースで実行 | アルムナイダイレクトスカウト：Core OSのアルムナイDBから高スコアの退去者を検索し、特別条件での再入居オファーを直接送信。空室期間を大幅短縮 |
| **家賃の手動回収と滞納追跡** | 銀行振込の入金確認を目視チェック。滞納者への連絡はLINE/電話で個別対応 | Stripe自動引き落とし + 滞納自動検知アラート。ダッシュボードで全住民の支払い状況をリアルタイム確認 |
| **House Economyの運用管理** | （該当なし。新概念） | Quest設計、ポイントバジェット設定、Quest完了の承認、月次ポイント精算の自動化をすべてOwner Console上で管理 |
| **住民トラブルの把握と対応** | 住民から直接電話やLINEで相談を受ける。状況把握に時間がかかり、対応が後手に回る | Silent Report一覧で匿名通報をリアルタイムに把握。対応ステータスの管理。Room Condition写真による退去精算のエビデンス確認 |

### 1.3 Owner Consoleが実現するオーナー体験

**日常運営シナリオ：** オーナーがダッシュボードを開くと、「今月の入金率98%（1名未入金）」「未対応チケット3件」「承認待ちQuest 5件」の要約が表示される。未入金者にはワンクリックでリマインド通知を送信。チケットは住民の母国語（ベトナム語）で書かれているが、自動翻訳で内容を即座に把握し、日本語で回答するとベトナム語に翻訳されて住民に届く。

**空室対応シナリオ：** 来月退去予定の住民が出た。オーナーはOwner Consoleの「アルムナイスカウト」機能を開き、スコア700以上・過去に近隣エリアに居住歴のあるアルムナイを検索。3名がヒットし、「初期費用50%オフ」の特別条件でスカウトオファーを送信。翌日、1名が承諾し、空室期間ゼロで次の入居者が確定する。

---

## 2. マネタイズ手法・財務インパクト

### 2.1 SaaS月額課金（主要収益源）

Owner ConsoleはShare House OSの**唯一の直接課金プロダクト**である。物件単位の月額サブスクリプションで収益化する。

| プラン | 月額料金（税抜） | 対象 | 含有機能 |
|---|---|---|---|
| **Starter** | 2,980円/物件 | 小規模オーナー（1〜2物件） | 家賃自動回収、入金管理、滞納アラート、基本ダッシュボード |
| **Standard** | 5,980円/物件 | 中規模オーナー（3〜10物件） | Starter全機能 + House Economy（Quests/Thanks/Buddy）、Room Condition Tracker、Silent Report、多言語チケット |
| **Premium** | 9,980円/物件 | 大規模管理会社（11物件以上） | Standard全機能 + 電子契約パイプライン、Rule Governance、アルムナイスカウト、カスタムレポート、専用サポート |
| **Enterprise** | 要相談 | 50物件以上の管理会社 | Premium全機能 + API連携、SSOシングルサインオン、SLA保証、カスタム開発 |

### 2.2 追加収益ストリーム

| 収益源 | 説明 | 単価 |
|---|---|---|
| アルムナイスカウト成功報酬 | スカウト経由の再入居成約時 | 15,000〜25,000円/件 |
| 電子契約従量課金 | Starterプランでの電子契約利用 | 500円/件 |
| ストレージ追加 | Room Condition写真の保存容量超過分 | 500円/5GB/月 |

### 2.3 財務インパクト

| 指標 | 目標値（Y5） |
|---|---|
| 契約物件数 | 1,850物件 |
| プラン別構成比（Starter/Standard/Premium/Enterprise） | 20% / 45% / 30% / 5% |
| 加重平均月額単価（ARPU） | 約6,800円/物件 |
| 月間SaaS MRR | 約1,258万円 |
| 年間SaaS ARR | 約1.5億円 |
| 月次SaaSチャーン率 | 2.0%（Core OSの信用スコア・アルムナイ機能による改善効果込み） |
| 粗利率 | 85%以上（インフラコストがSupabase + Stripe手数料のみ） |
| LTV/CAC比率 | 7.5x |

### 2.4 オーナーのROI（投資対効果）

Standardプラン（5,980円/月）を導入した場合のオーナーのコスト改善を示す。

| 項目 | Before | After | 差額 |
|---|---|---|---|
| 共用部清掃外注費 | 35,000円/月 | 5,000円/月 | △30,000円 |
| 退去トラブル対応コスト（月按分） | 8,000円/月 | 2,000円/月 | △6,000円 |
| 空室期間のロス（月按分） | 30,000円/月 | 10,000円/月 | △20,000円 |
| 住民間トラブル仲裁コスト（月按分） | 5,000円/月 | 1,000円/月 | △4,000円 |
| 家賃回収事務コスト | 15,000円/月 | 0円/月 | △15,000円 |
| **改善コスト合計** | — | — | **△75,000円/月** |
| SaaS月額料金 | — | +5,980円/月 | — |
| House Economyポイントバジェット | — | +25,000円/月 | — |
| **ネット改善額** | — | — | **△44,020円/月** |

SaaS料金 + ポイントバジェットの支出を差し引いても、オーナーは月額約44,000円のコスト改善を享受できる。

---

## 3. 主要機能一覧

### 3.1 ダッシュボード

| 機能 | 説明 |
|---|---|
| 運営サマリー | 入居率、今月入金率、未対応チケット数、承認待ちQuest数、最新Silent Report件数のリアルタイムサマリー |
| 物件切り替え | 複数物件を管理するオーナー向け。物件間のワンクリック切り替え + 全物件横断ビュー |
| 売上レポート | 月間/年間の売上推移、ポイント還元額、空室率のグラフ表示 |
| アラート | 滞納発生、Silent Report着信、チケット未対応、契約満了間近のプッシュ通知 |

### 3.2 契約自動化パイプライン

| 機能 | 説明 |
|---|---|
| 入居申込の受付 | Acquisition Portalからの申込をOwner Consoleに自動流入。申込者のプロフィール・信用スコア（アルムナイの場合）を表示 |
| 本人確認（eKYC） | 運転免許証・在留カード等の本人確認書類のアップロード → 目視確認（Phase 3以降はAI-OCR連携の可能性） |
| 重要事項説明 | 対面 or ビデオ通話（外部ツール連携）での宅建業法準拠の重要事項説明。説明完了チェックの記録 |
| 電子契約 | デジタル改革関連法（2022年施行）準拠の電子署名。契約書PDFの自動生成 + 双方の電子署名 + タイムスタンプ |
| 初期費用決済 | Stripe Checkout Sessionによる敷金・礼金・仲介手数料のワンタイム決済 |
| 家賃サブスクリプション開始 | 契約成立と同時にStripe Subscriptionを自動作成。翌月からの自動引き落とし開始 |
| パイプラインステータス管理 | 申込 → 本人確認 → 重説 → 契約 → 決済 → 入居開始 の各ステージをKanbanボードで管理 |

### 3.3 多言語チケットシステム

| 機能 | 説明 |
|---|---|
| チケット受付 | 住民がResident Appから送信したチケット（要望・質問・不具合報告）をOwner Consoleに表示 |
| 自動翻訳表示 | 住民の母国語で書かれたチケット本文を、オーナーの表示言語に自動翻訳。原文も並記 |
| 翻訳回答 | オーナーが自国語で回答を入力すると、住民の母国語に翻訳されてResident Appに配信 |
| 既読トラッキング | オーナーの回答を住民が閲覧した時刻を記録・表示。「伝達済み」の確認が可能 |
| カテゴリ分類 | 設備修繕、契約関連、House Economy、騒音・トラブル、一般質問のカテゴリ自動分類 |
| 対応SLA管理 | チケット受付からの経過時間を表示。Premiumプランでは目標応答時間の設定・超過アラート |
| テンプレート回答 | よくある質問に対する多言語テンプレート回答を事前登録。ワンクリック送信 |

**対応言語：** 日本語、英語、中国語（簡体/繁体）、韓国語、ベトナム語

**翻訳エンジン：** Phase 1はDeepL API。Phase 3以降はLLM（Claude API等）を用いた文脈理解翻訳への移行を検討。

### 3.4 House Economy管理

| 機能 | 説明 |
|---|---|
| Quest設計・管理 | Questの新規作成（タイトル、説明、報酬ポイント、頻度、対象曜日）、一時停止、アーカイブ |
| Quest完了承認 | 住民が提出したBefore/After写真を確認し、承認/差し戻し。承認でポイント自動付与 |
| ポイントバジェット設定 | 月間のポイントバジェット上限を物件単位で設定。上限到達時のアラート |
| ポイント消費レポート | 今月のポイント付与総額、Quest別・住民別の内訳、月次推移のグラフ |
| ポイント還元確認 | 月末のポイント → 家賃割引（Stripe Coupon）変換の確認・手動調整 |

### 3.5 アルムナイダイレクトスカウト

| 機能 | 説明 |
|---|---|
| アルムナイ検索 | Core OSのアルムナイDBから、信用スコア・過去入居エリア・退去時期・言語等の条件でフィルタ検索 |
| スコア閲覧 | アルムナイの信用スコアと構成要素の内訳を確認（オプトイン済みのアルムナイのみ） |
| スカウトオファー作成 | 対象アルムナイへの再入居オファーを作成。特別条件（初期費用減免、家賃割引等）をカスタマイズ |
| オファー送信 | メール + プッシュ通知でアルムナイにオファーを配信 |
| オファーステータス管理 | 送信済み → 閲覧済み → 承諾/辞退/期限切れ のステータスを追跡 |
| スカウト成約時フロー | 承諾されたオファーは自動的に契約パイプラインに流入。スカウト手数料の自動精算 |

### 3.6 住民管理

| 機能 | 説明 |
|---|---|
| 住民一覧 | 物件ごとの入居者リスト。入居日、契約満了日、信用スコア、ポイント残高を一覧表示 |
| 住民詳細 | 個別住民の家賃支払い履歴、Quest実績、Thanks受領数、Silent Report被通報履歴（匿名）、信用スコア推移 |
| 入退去管理 | 入居予定者・退去予定者のカレンダー表示。退去手続きの進捗管理 |
| Room Condition確認 | 住民が撮影した入居時/定期/退去時の部屋状態写真を確認。比較ビューでの損傷判定 |

### 3.7 Silent Report管理（オーナー側）

| 機能 | 説明 |
|---|---|
| 匿名通報一覧 | 物件ごとのSilent Report一覧。カテゴリ、日時、ステータスで絞り込み |
| 通報詳細 | 匿名の通報内容、添付証拠、reporter_hash（同一通報者の検知用） |
| 対応ステータス更新 | 受理 → 対応中 → 解決済みのステータス管理。対応内容のメモ |
| 通報パターン分析 | 特定カテゴリの通報頻度推移、同一reporter_hashからの通報パターン検知 |

### 3.8 レポート・分析

| 機能 | 説明 |
|---|---|
| 財務レポート | 月次/年次の売上、入金率、滞納額、ポイント還元額のサマリー |
| 入居率レポート | 物件ごとの入居率推移、空室期間の平均、退去理由の統計 |
| House Economyレポート | Quest消化率、ポイント流通量、Thanks Token交換量の推移 |
| 住民スコア分析 | 物件ごとの平均信用スコア推移、スコア分布、スコアと入居期間の相関 |

---

## 4. 技術要件・アーキテクチャ案

### 4.1 推奨技術スタック

| レイヤー | 技術 | 用途 |
|---|---|---|
| フレームワーク | Next.js (App Router) | SSR + SPAのハイブリッド。SEO不要だがSSRによる初期表示高速化 |
| 状態管理 | Zustand + React Query (TanStack Query) | クライアント状態 + サーバーキャッシュの分離管理 |
| UIライブラリ | shadcn/ui + Tailwind CSS | 高品質なダッシュボードUIを効率的に構築 |
| グラフ/チャート | Recharts or Chart.js | 財務レポート、スコア分析等のデータ可視化 |
| 認証 | Supabase Auth (JWT) + カスタムクレーム | オーナーロールの判定。マルチ物件アクセス制御 |
| データ通信 | Supabase JS SDK (PostgREST) | Core OS DBへのCRUD操作（RLSによるアクセス制御） |
| リアルタイム通信 | Supabase Realtime | チケット更新、Silent Report着信、Quest完了通知のリアルタイム反映 |
| 翻訳 | DeepL API（Phase 1）→ Claude API（Phase 3） | チケットの自動翻訳 |
| 電子署名 | クラウドサイン API or GMOサイン API | 宅建業法準拠の電子契約 |
| PDF生成 | @react-pdf/renderer or Puppeteer | 契約書PDF、レポートPDFの自動生成 |
| ファイルストレージ | Supabase Storage | 本人確認書類、契約書PDF、Room Condition写真 |
| ホスティング | Vercel | Next.jsの最適デプロイ先。Edge Functionとの親和性 |

### 4.2 Owner Console関連のデータベーステーブル

※ Core OSのPostgreSQLデータベース上に存在し、RLS（Row Level Security）でオーナーロールに限定したアクセス制御を行う。

#### 契約パイプライン系

| テーブル | 説明 | 主要カラム |
|---|---|---|
| `applications` | 入居申込 | id, house_id (FK), applicant_id (FK → profiles), source (portal/scout/referral), status (received/screening/kyc/explanation/contract/payment/completed/rejected), applied_at, completed_at |
| `contracts` | 契約情報 | id, house_id (FK), user_id (FK), room_id, rent_amount, deposit_amount, start_date, end_date, status (active/expired/terminated), signed_at, document_url |
| `kyc_documents` | 本人確認書類 | id, application_id (FK), document_type (drivers_license/residence_card/passport/etc), file_url, status (uploaded/verified/rejected), verified_by, verified_at |

#### チケット系

| テーブル | 説明 | 主要カラム |
|---|---|---|
| `tickets` | チケット本体 | id, house_id (FK), user_id (FK), category (maintenance/contract/house_economy/noise/general), subject, body_original (原文), body_translated (翻訳文), original_lang, status (open/in_progress/resolved/closed), priority (low/medium/high/urgent), created_at, resolved_at |
| `ticket_replies` | チケット返信 | id, ticket_id (FK), user_id (FK), body_original, body_translated, original_lang, read_at (既読時刻), created_at |

#### House Economy管理系（オーナー側設定）

| テーブル | 説明 | 主要カラム |
|---|---|---|
| `house_economy_settings` | ハウスごとのポイント経済設定 | id, house_id (FK), monthly_point_budget (INT), point_to_yen_rate (DECIMAL, default 10), auto_settlement (BOOLEAN), updated_by, updated_at |

### 4.3 RLS（Row Level Security）ポリシー設計

```sql
-- オーナーは自分が管理する物件のデータのみアクセス可能
CREATE POLICY "owner_select_own_houses"
ON houses FOR SELECT
USING (
  owner_id = auth.uid()
  OR EXISTS (
    SELECT 1 FROM house_managers
    WHERE house_id = houses.id AND manager_id = auth.uid()
  )
);

-- 契約情報: 物件オーナーのみ閲覧可能
CREATE POLICY "contracts_select_owner"
ON contracts FOR SELECT
USING (
  house_id IN (
    SELECT id FROM houses WHERE owner_id = auth.uid()
    UNION
    SELECT house_id FROM house_managers WHERE manager_id = auth.uid()
  )
);

-- チケット: 物件オーナーは全チケットを閲覧・返信可能
CREATE POLICY "tickets_select_owner"
ON tickets FOR SELECT
USING (
  house_id IN (
    SELECT id FROM houses WHERE owner_id = auth.uid()
    UNION
    SELECT house_id FROM house_managers WHERE manager_id = auth.uid()
  )
);

-- チケット返信の既読トラッキング: 住民がオーナーの返信を閲覧した際にread_atを更新
CREATE POLICY "ticket_replies_update_read"
ON ticket_replies FOR UPDATE
USING (
  EXISTS (
    SELECT 1 FROM tickets t
    WHERE t.id = ticket_replies.ticket_id AND t.user_id = auth.uid()
  )
)
WITH CHECK (
  read_at IS NOT NULL  -- read_atのみ更新可能
);

-- アルムナイ検索: opt_in_scout = true のアルムナイのみオーナーに公開
CREATE POLICY "alumni_select_opted_in"
ON alumni FOR SELECT
USING (
  opt_in_scout = true
  AND EXISTS (
    SELECT 1 FROM houses WHERE owner_id = auth.uid()
    UNION
    SELECT house_id FROM house_managers WHERE manager_id = auth.uid()
  )
);
```

### 4.4 多言語チケットシステムのアーキテクチャ

```
[住民がResident Appでチケット送信]
      │
      ├── body_original: "Máy giặt bị hỏng rồi"（ベトナム語）
      ├── original_lang: "vi"（自動検出 or ユーザー設定の言語）
      │
      ▼
[Supabase Edge Function: translate-ticket]
      │
      ├── DeepL API / Claude API で翻訳
      │     vi → ja: "洗濯機が壊れました"
      ├── body_translated に保存
      │
      ▼
[Owner Console にリアルタイム通知]
      │
      ├── オーナーに日本語の翻訳文 + 原文を並記表示
      │
      ▼
[オーナーが日本語で返信]
      │
      ├── body_original: "修理業者を手配します。明日午後に訪問予定です。"
      ├── original_lang: "ja"
      │
      ▼
[Edge Function: translate-reply]
      │
      ├── ja → vi: "Chúng tôi sẽ sắp xếp thợ sửa chữa. Dự kiến đến vào chiều mai."
      ├── body_translated に保存
      │
      ▼
[Resident App に翻訳済み返信を配信]
      │
      ▼
[住民が返信を閲覧 → read_at を UPDATE]
      │
      ▼
[Owner Console に既読マーク表示 ✓✓]
```

### 4.5 契約パイプラインのステート遷移

```
[入居申込受付]
      │
      ├── source: portal（Acquisition Portal経由）
      ├── source: scout（アルムナイスカウト経由）
      ├── source: referral（既存住民からの紹介）
      │
      ▼
[書類審査（Screening）]
      │
      ├── アルムナイ（スコア700+）→ 審査スキップ → 重説ステージへ
      ├── 新規申込 → 本人確認（eKYC）ステージへ
      │
      ▼
[本人確認（eKYC）]
      │
      ├── 書類アップロード → オーナーが目視確認 → 承認/却下
      │
      ▼
[重要事項説明]
      │
      ├── 対面 or ビデオ通話での宅建業法準拠の重要事項説明
      ├── 説明完了チェック → オーナーが記録
      │
      ▼
[電子契約]
      │
      ├── 契約書PDF自動生成（物件情報 + 住民情報 + 条件を反映）
      ├── クラウドサインAPI → 双方の電子署名 + タイムスタンプ
      │
      ▼
[初期費用決済]
      │
      ├── Stripe Checkout Session → 敷金 + 礼金 + 仲介手数料
      ├── 敷金はCustomer Balanceとして保持（※法務確認要。Core OS定義書の法務注記を参照）
      │
      ▼
[入居開始]
      │
      ├── Stripe Subscription 自動作成（月額家賃）
      ├── house_memberships に新規レコード追加
      ├── Resident App のアクセス権限付与
      ├── Buddy System 自動ペアリング開始
      └── Room Condition Tracker 入居時撮影リマインド送信
```

### 4.6 画面構成（ナビゲーション）

```
[Sidebar Navigation]
├── 📊 ダッシュボード
│   ├── 運営サマリー
│   ├── 今月の入金状況
│   └── アラート一覧
│
├── 🏠 物件管理
│   ├── 物件一覧
│   ├── 物件詳細・設定
│   └── 部屋管理
│
├── 👥 住民管理
│   ├── 住民一覧
│   ├── 住民詳細
│   └── 入退去カレンダー
│
├── 📝 契約パイプライン
│   ├── Kanbanボード（ステージ別）
│   ├── 申込詳細
│   └── 電子契約管理
│
├── 🎯 House Economy
│   ├── Quest管理
│   ├── Quest完了承認
│   ├── ポイントバジェット設定
│   └── ポイント消費レポート
│
├── 💬 チケット
│   ├── チケット一覧
│   ├── チケット詳細（翻訳ビュー）
│   └── テンプレート管理
│
├── 🛡️ Safety
│   ├── Silent Report一覧
│   ├── Room Condition確認
│   └── 通報パターン分析
│
├── 🔍 アルムナイスカウト
│   ├── アルムナイ検索
│   ├── スカウトオファー管理
│   └── 成約履歴
│
├── 💰 ファイナンス
│   ├── 売上レポート
│   ├── 支払い一覧
│   └── 請求管理
│
└── ⚙️ 設定
    ├── アカウント設定
    ├── 物件スタッフ管理
    ├── 通知設定
    └── プラン・課金
```

### 4.7 開発ロードマップ（Owner Console部分）

| フェーズ | 期間 | 対象機能 |
|---|---|---|
| **Phase 1（MVP）** | M1〜M6 | ダッシュボード、住民一覧、家賃自動回収（Stripe Subscription）、滞納アラート、Quest管理・承認、基本チケット（翻訳なし） |
| **Phase 2（Full SaaS）** | M7〜M12 | 多言語チケット（DeepL連携）、既読トラッキング、Room Condition確認、Silent Report管理、ポイントバジェット設定、月次精算の自動化、財務レポート |
| **Phase 3（Premium機能）** | M13〜M18 | 電子契約パイプライン（クラウドサイン連携）、アルムナイスカウト、住民スコア分析、カスタムレポート、Rule Governance管理 |

### 4.8 パフォーマンス・品質要件

| 要件 | 目標値 |
|---|---|
| ダッシュボード初期表示 | < 1.5秒（SSR + インクリメンタルフェッチ） |
| チケット翻訳レスポンス | < 2秒（DeepL API） |
| 同時接続オーナー数 | 500+（Supabase Realtime + Vercel Edge） |
| データのリアルタイム反映 | < 1秒（Supabase Realtime経由） |
| 可用性 | 99.9%（Vercel + Supabase SLAに準拠） |

---

*本書類はOwner Consoleの設計方針を示すものであり、実装段階での詳細設計は別途ADR（Architecture Decision Record）として管理する。*