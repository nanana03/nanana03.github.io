# Design — Fuse 6×6（`fuse6x6/index.html`・`fuse6x6/privacy.html`）

Fuse 6×6 だけを縛る系。会社トップ（ルートの `design.md`）・おにコレとは別ブランドなので似せない。

## 発想
**ページそのものが盤面。** アプリの盤（濃い紫の盤・少し明るいマス・数字ごとに色相が回るタイル）
をそのまま版面にする。節はマスに置かれたタイルで、6列の格子に大小の区画として並ぶ。
数字タイルの色は**アプリの式（`fuse-6x6/src/game/format.js` の `tileColor`）が出す値そのもの**。

## Genre / 構造
- genre: playful（夜の盤面）
- macrostructure: **Bento Grid**（6列の格子＝盤。区画の大きさの違いがリズム）
- nav: **N5 floating pill**（屋号・節へのリンク・日本語/EN 切替を1本の錠剤に）
- footer: **Ft2 inline single line**＋数字タイルの段（2→2048 を実色で1列に並べた帯）
- enrichment: 実物のみ＝ストア掲載スクリーンショットから切り出した盤面・パネル8枚の絵
  （アプリの assets を縮小）・アプリ同梱の背景1枚。生成し直した絵や作り物の端末枠は使わない

## Theme（studied from the app・axes＝dark / display-heavy / multi）
アプリ本体の値をそのまま使う（`fuse-6x6/src/ui/theme.js:22-28`）。OKLCH に直さない例外＝製品の色そのものだから。
- `--color-paper`  #14131b（COLORS.bg）
- `--color-board`  #241f31（COLORS.boardBg）
- `--color-cell`   #2f2940（COLORS.cellBg）
- `--color-ink`    #f5f2ff（COLORS.text）
- `--color-sub`    #b9b0d3（COLORS.sub #9a90b5 を本文用に明るくした。セル上で 4.5:1 を確保）
- `--color-accent` #ffc23c（COLORS.accent＝続けるボタンの金）
- タイル色 `--tile-2` … `--tile-2048`＝`tileColor()` の出力（hsl のまま）
- パネル色 `--p-magnet` 等＝`ITEM_STYLE`（`format.js:263-278`）

## Typography
- Display: **Dela Gothic One**（見出し・数字。`text=` で使う字だけ）
- Body: システムの日本語ゴシック／英語は system-ui
- 斜体なし

## Motion（2つまで）
- 「合体」：数字タイルを押すと次の数字へ（2→4→…→32）。80ms の押し込み＋色の切替
- 「準備完了」：パネルの区画にポインタ／フォーカスが来ると、アプリの準備完了と同じ白い2px の枠
- reduced-motion では押し込みを切る（色の切替だけ）

## CTA voice
- 主：金（accent）の角丸ボタン＝アプリの「ライフを使って続ける」と同じ声。文字は `--color-paper`
- 副：セル色のボタン＋金の縁

## privacy.html
- 同じ色・同じ書体で包むだけ。本文（`<article class="legal">` の中）は一字一句変えない。
