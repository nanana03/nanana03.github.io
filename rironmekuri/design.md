# Design — 理論めくり（`rironmekuri/index.html`・`support.html`・`privacy.html`）

理論めくりだけを縛る系。会社トップ・Fuse 6×6・おにコレ・PicoFiler とは別ブランドなので似せない。

## 発想
**赤シートを、ページの上で本当に動かす。** 最初の画面に見本のページを1枚置き、アプリと同じ赤シート
（`rgba(214,38,38,0.42)`）を重ねる。上端をつまんで下へずらすと上の赤い字が見え、隠れた語句は押すとその語句だけめくれる。
説明より先に、手で仕組みが分かる。見本の文章は当社が書いたもの（実在の教材の文は使わない）。

## Genre / 構造
- genre: editorial（austere・教科書）
- macrostructure: **Marquee Hero**（左に言い切り「赤い字を、隠して覚える。」・右に動く赤シート。下は朱の太線で区切り、教科書の章のように縦に読む）
- nav: **N9 edge-aligned**（左に屋号＋アイコン、右に English だけ）
- footer: **Ft5 statement**（結びの一文「いつもの一冊を、いつもの赤シートで。」）
- enrichment: Tier A＝動く赤シートの見本・マーカー6色の帯・覚え具合の色の帯。作り物の端末枠・スクショ風の絵は描かない

## Theme（studied from the app・axes＝light / classical-serif / warm）
アプリ本体の値をそのまま使う（`Product/RironMekuri/src/theme.ts` の `C`・`MARKER_COLORS`）。OKLCH に直さない例外＝製品の色そのもの。
値は `tokens.css`。主なもの：
- `--color-paper` #F5F2EA（C.paper）／`--color-surface` #FFFFFF／`--color-line` #E3DDD0
- `--color-ink` #1D2023／`--color-sub` #5C6168
- `--color-shu` #C2412D（強調・リンク・朱の太線）
- `--color-sheet` rgba(214,38,38,0.42)（読む画面の赤シート）
- 採点の色 0%→50%→100%＝赤→黄→緑（意味の色。強調には使わない）

## Typography
- Display: **Shippori Mincho B1** 800（見出し・屋号・値段）。教科書・条文の調子＝明朝
- Body: システムの日本語ゴシック
- 見出しの大きさは**列の幅で決める**（`cqi`）。vw・rem で決めると 2 列のとき列に入らず語の途中で折れた（2026-11-01 実測）
- 斜体なし

## Motion
- 赤シートの上端を動かす（ユーザーの操作だけ。勝手には動かさない）
- めくった語句の地が白に変わる 120ms
- reduced-motion ではページ内のなめらかなスクロールを切る

## 言語
- 本文は日本語。下に英語の節（`#en`）＝紹介・よくある質問・連絡先
- 10 言語のサポートは `support.html`。ASC のサポート URL（`…/rironmekuri/#zh-Hans` 等）は、index.html 冒頭のスクリプトで `support.html#…` へ渡す（`#ja`・`#en` はこのページの中）

## 守ること
- 発売前は「App Store で配信の準備中」。**配信が始まったら** App Store のリンク（本物のバッジ）に替え、会社トップの棚に載せる（番人 `site_catalog.py` が見る）
- 値段・無料の範囲は ASC の商品と `_store/appstore_metadata_i18n.json` が正本
- スクリーンショットは、Mac が撮ったストア用の本物だけを使う（まだ載せていない）
