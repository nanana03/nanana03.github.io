# Design — 理論めくり（`rironmekuri/index.html`・`support.html`・`privacy.html`）

理論めくりだけを縛る系。会社トップ・Fuse 6×6・おにコレ・PicoFiler とは別ブランドなので似せない。
作り直しの記録（5 周・点数・機械検査）＝`Product/_site_redesign_2026-10/rironmekuri/REVIEW.md`。

## 発想
**ページそのものが理論テキスト、訪れた人が赤シートを持つ。**
- 最初の画面＝**本物の見本ページ**（Mac の見本台本 `RironMekuri/tools/make_store_sample.py` の「所得税法 理論ノート」1・2 ページ目を描いた絵）。
  赤い語は描いた絵の赤い画素から見つけた矩形（1 ページ目 11・2 ページ目 5）。シートはアプリ `src/Reader.tsx` と同じ 3 手順
  （語を紙の白で消す → 半透明の赤 → めくった語だけ元の絵を窓で出す）・濃さ 3 段階（`store.ts` SHEET_ALPHA）。後ろに次のページを傾けて重ね、「次のページへめくる」。
- 下は紙面：**柱**（見本 PDF と同じ「書名〔章〕」の細い線）・**問題番号**（問題1−1…）・**欄外**（右の余白の注）。
- 本文の要の語は赤で刷る（`.ans`）。右下の「赤シートを掛ける」で全部隠れ、**説明そのものが暗記問題になる**。
- 触れる見本：緑シート（暗記マーカーだけ暗く消える）・覚え具合のスライダー（`score.ts` の色・5% 刻み）と連動する「今日まわす理論（見本）」。

## Genre / 構造
- genre: editorial（austere・教科書）
- macrostructure: **Marquee Hero**（左に言い切り・右に本物の見本の束）→ 下は教科書の紙面（柱・問題番号・欄外）
- nav: **N9 edge-aligned**（左に屋号＋アイコン、右に English だけ）
- footer: **Ft5 statement**（「いつもの一冊を、いつもの赤シートで。」）
- enrichment: 実物だけ（見本 PDF を描いた絵）。作り物の端末枠・スクショ風の絵は描かない

## Theme（studied from the app・axes＝light / classical-serif / warm）
アプリ本体の値をそのまま使う（`theme.ts`・`score.ts`・`store.ts`・`Reader.tsx`）。OKLCH に直さない例外＝製品の色そのもの。値と出典は `tokens.css`。
- 紙 #F5F2EA／墨 #1D2023／補足 #5C6168／朱 #C2412D（本文の赤い語・紙の地で 4.59:1）
- 赤シート rgba(214,38,38, 0.30・0.42・0.56)／緑シート rgba(20,140,80,0.42)
- 覚え具合 #D05540 → #E0B034 → #4E9A6A（意味の色。文字色には使わない＝黄の字は白地で 2.26:1）

## Typography
- Display: **Shippori Mincho B1** 800・`palt`。`class="mincho"` の字だけ読む（`_site_redesign_2026-10/rironmekuri/build_fonts.py`＝字を足したら流す）
- Body: システムの日本語ゴシック
- 見出しは**句で折る**（`.ph`＋`word-break: auto-phrase`）。大きさは列の幅で決める（`cqi`）＝vw・rem だと 2 列のとき列に入らない
- 最初の見出しは広い画面で 3 行（赤い字を、／隠して／覚える。）・狭い画面で 2 行
- 斜体なし

## Motion
- ユーザーの操作で動くものだけ（赤シートの上端・めくる・緑シート・スライダー）。めくるときの 220ms のフェード
- reduced-motion では transition・animation を 0 に

## 言語
- 本文は日本語。下に英語の節（`#en`）＝紹介・よくある質問・連絡先
- 10 言語のサポートは `support.html`。ASC のサポート URL（`…/rironmekuri/#zh-Hans` 等）は index.html 冒頭のスクリプトで `support.html#…` へ渡す

## 守ること
- `support.html`・`privacy.html` の本文は一字一句変えない（ASC に登録済み）。検査＝`check.py` の本文一致
- 発売前は「App Store で配信の準備中」。**配信が始まったら** App Store のリンク（本物のバッジ）に替え、会社トップの棚に載せる
- 値段・無料の範囲は ASC の商品と `_store/appstore_metadata_i18n.json` が正本
- 見本の理論名・本文は Mac の見本台本に実在するものだけ（作らない）
