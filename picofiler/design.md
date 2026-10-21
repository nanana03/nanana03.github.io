# Design — PicoFiler（`picofiler/index.html`）

PicoFiler だけを縛る系。会社トップ（ルートの `design.md`）・Fuse 6×6・おにコレとは別ブランドなので似せない。
（2026-10-21 作成・ユーザー「他のアプリ同様にセンス良く」）

## 発想
**ページそのものがアプリの窓。** アプリの三分割（左にフォルダツリー・右に一覧と中身）をそのまま版面にする。
左の目次は**フォルダツリー**（点線の枝・小さなフォルダの印）で、今いる節を**アプリの選択色**で示す。
節の見出しには**フォルダのタブ**（アイコンの若草色）を付ける。

## Genre / 構造
- genre: editorial（utilitarian）
- macrostructure: **Workbench**（左に固定の道具＝ツリー、右に作業面）
- nav: **N3 side-rail**（＝フォルダツリー。760px 以下では上に移り、横に並べて折り返す）
- footer: **Ft2 inline single line**
- enrichment: 実物のみ＝Vector 掲載用に撮ったスクショ 3 枚（`Product\PicoFiler\_shots\vector\*.png` を 1600px webp に）と
  アプリのアイコン（`picofiler/icons/app.png`）。写っている画像・フォルダは見せる用に作ったもの（`F:\PicoFiler_sample`）。
  偽の窓枠は描かない（スクショは細い枠の `<figure>` だけ）

## Theme（studied from the app・axes＝light（dark は graphite）/ geometric-sans / cool）
アプリ本体の値をそのまま使う（`Product\PicoFiler\picofiler\theme.py` の `mist`・`graphite`）。OKLCH に直さない例外＝製品の色そのものだから（Fuse と同じ）。
- 明るい＝mist：paper #f3f4f6 / surface #ffffff / line #e3e5e8 / ink #1b1d21 / accent #0a64c2 / select #dcebfb・#0b2f57 / hover #eef1f5
  - muted だけ #6b7079 → #5d626b（白地の本文で 4.5:1 を確保）
- 暗い＝graphite（`prefers-color-scheme: dark`）：paper #1c1d20 / surface #222327 / ink #e8e9ec / accent #5aa9ff / select #2c4a6e
- アイコンの 3 色は**面だけ**に使う（字の色にしない）：若草 #8ba792（節のタブ）・黄 #f4bf3a（ツリーのフォルダの印）・橙 #ee8a3c（寄付の節の縦線）

## Typography
- Display: **Zen Kaku Gothic New** 700（Google Fonts・`text=` で使う字だけ＝`_site_redesign_2026-10/nanana03/build_fonts.py`。
  見出しを変えたら必ず流し直す）
- Body: システムの日本語ゴシック
- 斜体なし

## Motion（1 つだけ）
- 目次の「今いる節」をアプリの選択色で示す（IntersectionObserver）。ダウンロードのボタンは 1px 持ち上がるだけ。
- reduced-motion では持ち上がりとなめらかなスクロールを切る。

## CTA voice
- 主：アプリの accent の角丸ボタン「無料でダウンロード」＝GitHub のリリースの setup.exe へ直接。
- 副：文字のリンク（リリースの一覧）。寄付の節＝Amazon ギフトカード（E メール・受取人 nanana03info@gmail.com）＋ Ko-fi（準備中）。アプリの「寄付で応援する」は `#donate` を開く（2026-10-22・peekrvr の名前を出さない）。

## 守ること
- 版・リンクは**公開資産レジストリが正本**。版を上げたらボタンの URL（`v1.0.0`）・「1.0.0」の表記・トップの棚を一緒に直す。
- **Vector と winget は公開されるまでリンクしない**（今は「Vector でも公開の手続き中」の 1 行だけ）。
- 数字を作らない（速さの実測値を載せるなら、実測の日付と条件を添える）。
