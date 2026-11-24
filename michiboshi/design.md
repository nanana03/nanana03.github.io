# Design — ミチボシ（`michiboshi/index.html`）

ミチボシだけを縛る系。会社トップ・おにコレ・Fuse 6×6・PicoFiler・理論めくり・路線価めくりとは別ブランドなので似せない。
`privacy.html`・`terms.html`・`support.html` は手で書いた法務ページ（字と色は同じ `:root` の値・飾りは足さない）。

## 発想
**写真が主役。字は星図の注記。** アプリの画面そのものが夜空なので、本物の画面写真を大きく置き、字は細く少なく添える。
- 最初の段＝屋号と副題を上に、その下に「描き終えた星座」（実際に走った記録・富士見高原）を画面の幅いっぱいに。描いている様子の動画も添える。
- 字を写真に重ねない：星座の線と交差点の名前は写真のどこにでも来る（1024×768 で重なったので外した・11-24）。

## Genre / 構造
- genre: atmospheric（暗い地・にじみは奥付の 1 つだけ）
- macrostructure: **Photographic**（横の写真は全幅、縦の画面写真は 2 枚並べ・字の段は細い帯）
- nav: **N10 floating-on-scroll morph**（最初は透明な帯 → 下へ送ると錠剤。DOM は 1 つ・高さは変えない・背景の不透明度と translateY だけ）
- footer: **Ft1 mast-headed**（アイコン＋屋号＋副題・リンク 4 つ・出典・©）
- enrichment: ASC に出した本物の画面写真 5 枚（`~/Documents/signaldrive-store/shots/` から書き出し）。作り物の端末枠は描かない

## Theme（studied from the app）
アプリ `~/signaldrive/app/App.js` の `C` の値そのまま。値と字と地の比は `tokens.css`。
- 地 #0b0d12／面 #151922／字 #e8eaf0／補足 #8a90a0／線 #2b3140
- リンク #4dbbff（アプリの #22aaff を暗い地で読める明るさに）・星の青 #9fd4ff（箇条の印・副題）
- 信号の緑 #30d158・赤 #ff453a は「青で抜けた／止まった」の説明の字だけに使う

## Typography
- Display: **M PLUS 1** 300 / 500（Google Fonts）。屋号は字間 0.42em（アプリのホームの「ミ チ ボ シ」と同じ見え方）
- Body: システムの日本語ゴシック
- 見出しは roman・斜体なし。句の途中で折らない所は `.nw`（inline-block）で包む

## Motion
- ナビの帯→錠剤（280ms `--ease-out`）だけ。reduced-motion で止める

## 守ること
- 書いてよいのは **ストアの説明文（`~/signaldrive/docs/ストア文言.md`）にあること**だけ。値段は ASC の商品（¥380 買い切り＝`docs/収益モデル.md`）
- **最初の段の絵と動画は、実際に走った記録**（2026-11-24 ユーザーの指示）。記録の元ファイルは git に入れない。
  🔴 **出発地の周りは必ず隠す**＝アプリの `hideNearHome`（`src/match.js`）と同じ関数で隠す。隠した範囲の大きさ・数・距離は**このファイルに書かない**（このファイルも公開されるため・2026-11-24 に外した）＝社内の日報にだけ残す。
  作り方＝記録を `src/viewer.js` の `buildViewerHtml` でアプリと同じ 3D の画面にし、撮影専用の Chrome（空のプロファイル）で描いて録画と最後の図を撮った。
- ほかの画面写真のドライブは**見本**（信号機 DB からたどった架空の道）。注記で「見本のドライブ」と書く
- Android（2026-11-24 追加）：「自動で記録する」は iPhone・iPad だけ（Android 1.0 は手で始める記録だけ＝ユーザー決定）。Android は記録中に通知が出る。購入は Google Play
- 出典は viewer.html（アプリの描写画面）の表記と同じ文。アプリ側を直したらここも直す
- 🔴 **配信の状態（ナビの「近日公開」・最初の段の「日本の App Store で近日公開」）は公開されたら直す。**
  公開を `itunes lookup?id=6838543571&country=jp` で確かめてから、Apple の公式バッジ（App Store で入手）に替え、会社トップの棚に載せる。
  Google Play は公開ページ `play.google.com/store/apps/details?id=com.nanabit.signaldrive` が 200 になってから公式バッジ（Google Play で手に入れよう）に替える（2026-11-24 足した）
- 確かめた幅＝320・375・414・768・1280（横のはみ出し 0・2 行に折れるナビ／奥付のリンク 0・2026-11-24）
