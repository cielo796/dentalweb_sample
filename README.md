# 飯田歯科医院 Webサイト（Astro リプレイス版）

旧 WordPress サイト（`selmadesign.xsrv.jp/wp/`）を **Astro + Tailwind CSS v4** の静的サイトへ置き換えたものです。

## セットアップ

```bash
npm install
npm run dev      # http://localhost:4321
npm run build    # dist/ に静的ファイルを出力
npm run preview  # ビルド結果を確認
```

Node.js 20 以上が必要です。

## 技術構成

| 項目 | 内容 |
| --- | --- |
| フレームワーク | Astro 7（静的出力／SSGのみ、JS はハンバーガーメニューの数行だけ） |
| CSS | Tailwind CSS v4（`@tailwindcss/vite`）＋ `src/styles/global.css` のトークン定義 |
| SEO | `@astrojs/sitemap`、canonical、OGP、JSON-LD（`schema.org/Dentist`） |
| フォント | Noto Sans JP / Noto Serif JP（Google Fonts） |

## ディレクトリ

```
src/
├─ data/clinic.ts        ← 医院情報はすべてここに集約（テキスト修正はまずここ）
├─ layouts/BaseLayout.astro
├─ components/           Header / Footer / PageHero / SectionHeading / HoursTable / CtaBanner
├─ pages/
│   ├─ index.astro       トップ
│   ├─ treatment.astro   診療案内（初診の流れ・自由診療について）
│   ├─ clinic.astro      医院紹介（院長挨拶・設備・医院概要）
│   ├─ access.astro      アクセス（Googleマップ埋め込み）
│   ├─ contact.astro     ご予約・お問い合わせ（フォーム・FAQ）
│   ├─ privacy.astro     プライバシーポリシー
│   └─ 404.astro
└─ styles/global.css
public/                  favicon.svg / robots.txt
```

## 掲載情報の出典

実データはエキテン掲載情報（https://www.ekiten.jp/shop_1363902/ ）に基づいています。
旧サイト本体は取得できなかったため、それ以外は仮の内容です。

**確定情報**：医院名／住所（茨城県取手市白山4丁目1-1）／電話番号（0297-72-2203）／
診療時間 9:00〜17:00・木日祝休診／アクセス（取手駅西口 徒歩8分ほか）／
無料駐車場4台（国道294号沿い）／保険診療のみ・自由診療なし／患者さまの声2件

## 差し替えが必要な箇所（SAMPLE）

画面上に `SAMPLE` バッジが付いている箇所と、`src/data/clinic.ts` 内の `SAMPLE` コメント箇所です。

- [ ] **郵便番号** `302-0034` … 要確認（`clinic.ts` → `postalCode`）
- [ ] **院長名・経歴** … `clinic.ts` → `doctor`
- [ ] **院内設備** … `clinic.ts` → `facilities`
- [ ] **お知らせ** … `clinic.ts` → `news`
- [ ] **写真** … トップのヒーロー、医院紹介の院長写真・設備写真（`public/images/` に配置して差し替え）
- [ ] **お問い合わせフォームの送信先** … `src/pages/contact.astro` の `<form action="#">`（Formspree / Google フォーム等）
- [ ] **お車でのルート案内** … `src/pages/access.astro` の目印テキスト
- [ ] **プライバシーポリシー** … `src/pages/privacy.astro`（雛形のため要確認）
- [ ] **本番ドメイン** … `astro.config.mjs` の `site` と `public/robots.txt`

## デザイン方針

- ブランドカラーはティール系（`--color-brand-*`）。医療系らしい清潔感と落ち着き
- 電話番号を常時視認できる位置（ヘッダー／フッター／各ページ下部CTA）に配置
- モバイルファースト。診療時間表は横スクロールなしで8列表示
- アクセシビリティ：スキップリンク、`aria-current`、フォーカスリング、代替テキスト

## デプロイ

`npm run build` で `dist/` に完全な静的ファイルが出力されます。
Netlify / Vercel / Cloudflare Pages / エックスサーバー（FTPアップロード）いずれにも対応できます。
