# タワマン大家 個別相談 LP（青山綜合地所）

日本のお客様向けの静的LP。HTML＋CSS＋素のJSのみで、ビルド不要。

公開URL: https://tawamanoya-aoyama.netlify.app/

```
.
├── site/                 公開されるのはこのフォルダだけ
│   ├── index.html        LP
│   ├── tokushoho/        特定商取引法に基づく表記
│   ├── privacy/          プライバシーポリシー
│   ├── dl/…/*.pdf        特典PDF（LINE でだけ案内する）
│   ├── _headers          特典PDFを noindex にする
│   ├── robots.txt        検索エンジン向け（/dl/ を除外、サイトマップの場所）
│   ├── sitemap.xml       検索エンジンに知らせるページの一覧（ページを増やしたら追記）
│   └── assets/
│       ├── style.css     スタイル
│       ├── form.js       フォーム送信（Google フォーム）
│       ├── tools.js      「数字で確かめる」欄（試算・坪単価グラフ）
│       ├── tower.jpg     プロフィール写真
│       └── seminar-cover.jpg 特典資料の表紙
├── tools/setup-google-form.gs  Google フォームの設問作成スクリプト
├── netlify.toml          Netlify の設定（site/ を配信）
├── CLAUDE.md             Claude Code 向けの作業ルール
└── README.md
```

## Netlify の設定（初回のみ）

1. app.netlify.com →「Add new project」→「Import an existing project」→ GitHub → このリポジトリ
2. 公開するブランチは `main`。ビルドコマンド・公開フォルダは `netlify.toml` から自動で入る（`site/` を配信）
3. 作成後、「Site configuration」→「Change site name」で `tawamanoya-aoyama` にする

ローカル確認:

```bash
python3 -m http.server 8000 -d site
# http://localhost:8000/
```

## 特典の渡し方

アンケートの送信後、サンクス表示に LINE公式アカウント「BAI Capital」の友だち追加ボタンを出します。資料（PDF）は、友だち追加時のあいさつメッセージで次のURLを案内します。

https://tawamanoya-aoyama.netlify.app/dl/poV8ulyWnwWlkAWcUixCB5UL/real-estate-strategy-seminar.pdf

推測されにくいパスに置いているだけなので、URL を知っていれば誰でも取得できます（LP の HTML・JS には書いていません）。検索結果に出ないよう `site/_headers` で noindex にしています。PDF を差し替えるときは同じファイル名で上書きすれば URL は変わりません。URL を無効にしたいときはフォルダ名を変え、LINE のメッセージも直します。

## フォーム

スコアリングの主軸は `income`（世帯年収）・`equity`（自己資金）・`timing`（検討時期）。日本在住のお客様を前提に、在留資格ではなく `occupation`（ご職業）を聞きます。

## 坪単価グラフ

`site/assets/data/market.json` があるときだけ表示されます（ないと欄ごと非表示）。データは国土交通省「不動産情報ライブラリ」の API から作ります。グラフ下の出典・加工した旨・クレジット文は利用約款で求められているので消さないこと。
