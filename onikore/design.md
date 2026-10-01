# Design — おにコレ（`onikore/index.html`・`onikore/privacy.html`）

おにコレだけを縛る系。会社トップ・Fuse 6×6 とは別ブランドなので似せない。
`tokens.css` は前回（2026-09-17・Stat-Led / Sport）の系で、今回の刷新では読まない（ファイルは残す）。

## 発想
**国道の番号表。** 「459本を集める」の459が何の集まりかを、1号から507号までの番号の地図で見せる。
番号のある459本は国道標識（おにぎり）、番号のない48か所は空き地。59〜100号の大きな空白が
そのまま見える。押すとアプリの路線画面と同じ概要文（`kari-kokudo/src/RouteDetail.js` の `overview()`）が出る。
データはアプリに入っている `kari-kokudo/src/data/kokudo.json`（道路統計年報2025 表26 由来）をそのまま使う。

## Genre / 構造
- genre: editorial（technical / cartographic）
- macrostructure: **Map / Diagram**（番号表がページの背骨。前後の節はそれを支える）
- nav: **N3 side-rail**（広い幅＝左端に縦書きの目次。狭い幅＝上の帯）
- footer: **Ft4 dense colophon**（窓口・リンク・データと標識の出典をまとめて小さく）
- enrichment: 実物のみ＝アプリの実スクリーンショット4枚・シミュレータの録画1本（既存）・
  国道標識の外形（アプリが使う Wikimedia Commons のパブリックドメイン原図のパス）

## Theme（studied from the app・axes＝dark / signage-sans / cool）
アプリの色（`kari-kokudo/src/theme.js:2-12`）。製品の色そのものなので hex のまま。
- `--color-paper` #0C1A29（C.bg）／ `--color-card` #13263B（C.card）／ `--color-line` #22364C（C.line）
- `--color-ink` #E6EEF6（C.text）／ `--color-sub` #A3B6C9（C.sub #8FA6BC を本文用に少し明るく）
- `--color-accent` #5FA4D6（C.accent＝走破済の青）
- `--color-current` #FF9500（MAP.current＝走行中の国道。選択中の番号にだけ使う）
- `--color-shield` #0140FF／白フチ（RouteShield.js の BLUE）

## Typography
- Display: **BIZ UDPGothic** 700（案内標識に近い UD 書体。`text=` で使う字だけ）
- 数字: **Overpass** 800（道路標識の書体 Highway Gothic に由来する書体。数字だけ取る）
- Body: システムの日本語ゴシック

## Motion
- 1つだけ：番号表の標識にポインタ／フォーカス → 橙の輪。押すと詳細が切り替わる（動かさない）
- 録画は画面に入ったときだけ再生。reduced-motion では自動再生しない（コントロールを出す）

## CTA voice
- App Store は Apple 提供の公式バッジ（`img/appstore-badge-ja.svg`・原本のまま）
- Android は Play が否承認中（2026-10-01）のため**リンクを置かない**（コメントアウトを保つ）

## privacy.html
- 同じ色・同じ書体で包むだけ。本文（`<article class="legal">` の中）は一字一句変えない。

## 変更（2026-10-01 第4周）
- 番号表（20列×26段）を**長さの稜線**に置き換えた（ユーザー選択＝PICK `v2_ridge.html`）。459本を総延長の長い順に並べた棒。
- 詳細カードの文は**アプリの路線画面と同じ規則**（`kari-kokudo/src/RouteDetail.js:952-971`）：
  愛称チップ（ROUTE_INFO.alias）→ 紹介文（ROUTE_INFO.desc。無ければ自動概要）→「ⓘ 」＋注記（ROUTE_NOTES）。
  文言は `data/route-text.json`＝`routeNotes.js` から `export_route_text.mjs` で機械的に書き出したもの（手で写さない）。
  初回表示では読まず、稜線が4分の1見えたとき／最初に操作したときに読む。
- 日本語見出しは `word-break: keep-all`＋文節ごとの `<wbr>`、数字＋単位は `.nb`（nowrap）。
