# Design — Nanana Soft（会社トップ `index.html`）

このリポジトリには3つの系がある。**会社トップ＝このファイル**、Fuse 6×6＝`fuse6x6/design.md`、
おにコレ＝`onikore/design.md`。製品は別ブランドなので、系どうしを似せない。
このファイルはトップ（と今後ルートに足すページ）だけを縛る。

## 発想
**棚。** 7つの製品を、実物のアイコンを「棚に置いた物」として並べ、名前と一行の説明は
棚板の下に貼る**棚札**に書く。iOS の棚と Windows の棚の2段。言葉は増やさない。

## Genre / 構造
- genre: editorial（austere）
- macrostructure: **Portfolio Grid**（棚＝グリッド。フィルタの代わりに棚の段で分ける）
- nav: **N2 floating chip**（左上の小さなチップ＝屋号、右にお問い合わせへの1リンク）
- footer: **Ft6 letter close**（窓口を手紙の結びとして置く）
- enrichment: 実物アイコン（App Store の配信アイコン4点＋Windows ソフトの実アイコン3点）。生成画像なし

## Theme（tuned custom・axes＝light / geometric-sans / chromatic-green）
- `--color-paper`   oklch(96.6% 0.008 85)   ／ dark: oklch(17% 0.008 85)
- `--color-ink`     oklch(21% 0.012 85)     ／ dark: oklch(94% 0.008 85)
- `--color-muted`   oklch(44% 0.012 85)     ／ dark: oklch(76% 0.010 85)
- `--color-rule`    oklch(84% 0.010 85)     ／ dark: oklch(34% 0.010 85)
- `--color-board`   oklch(27% 0.014 70)  ＝棚板（ink より少し温かい）／ dark: oklch(72% 0.02 75)
- `--color-accent`  oklch(47% 0.12 155)  ＝リンクだけ ／ dark: oklch(78% 0.13 155)
- `--color-focus`   accent と同じ

## Typography
- Display: **Murecho** 700/800（Google Fonts・`text=` で見出しの字だけ取る＝`build_fonts.py`）
- Body: システムの日本語ゴシック（Hiragino Sans / Yu Gothic UI / Noto Sans JP）＝転送0
- 見出しは roman のみ。斜体なし

## Spacing / Motion
- 4pt 名前付き（`--space-*`）。
- motion は1つだけ：アイコンにポインタを載せると 3px 持ち上がり、棚板の影が縮む（`--ease-out` 220ms）。
  reduced-motion では動かさない。

## CTA voice
- ボタンは作らない。リンクは accent の文字＋下線（棚札の中）。窓口メールは結びの中で大きく。

## 守ること
- 製品の状態・リンクは**公開資産レジストリが正本**。このページで勝手に足し引きしない。
- アイコンは実物だけ（出典は `index.html` 冒頭のコメント）。偽のストアバッジを描かない。
