# Design — 路線価めくり（`rosenka/index.html`）

路線価めくりだけを縛る系。会社トップ・理論めくり・おにコレ・Fuse 6×6・PicoFiler・ミチボシとは別ブランドなので似せない。
`privacy.html`・`terms.html`・`support.html` は `~/rosenka/docs/store/build_site.py` が下書きから書き出す法務ページ（このファイルの対象外・公開側を直接直さない）。

## 発想
**国税庁のサイトでたどる 5 段を、年分と住所の 1 行にする。**
- 最初の帯＝アプリの見出しと同じ「夜の家」（紺の地に家の絵 `img/house.jpg`＝アプリの `assets/ui/hero.jpg`）。
- 帯にかかるカード＝左に「都道府県 › 市区町村 › 町名 › 索引図 › 図の番号」の階段、右に「令和8年分＋東京都千代田区丸の内一丁目9番1号 → 15022」。例はアプリの実物の画面写真と同じ住所・同じ図番号（作らない）。
- 下は Split Studio：文と本物の画面写真を左右に置き、段ごとに入れ替える（住所・地図・現在地・倍率地域）。

## Genre / 構造
- genre: editorial（utilitarian）
- macrostructure: **Split Studio**
- nav: **N12 banner + retract**（琥珀の帯＝配信の状態のお知らせ。下へ送ると引っ込む・× で閉じて localStorage に覚える）
- footer: **Ft4 dense colophon**（出典・加工の注記・背景地図の表記・連絡先）
- enrichment: アプリの家の絵＋本物の画面写真 4 枚（`docs/store/screenshots/iphone_02〜05` を幅 640 の JPEG に）。作り物の端末枠は描かない

## Theme（studied from the app）
アプリの `apps/mobile/src/theme.ts`（「夜の家」2026-11-17）の値そのまま。値と字と地の比は `tokens.css`。
- 紺 #1e4f6d／紙 #eef5f8／墨紺 #14242f／補足 #53636d／リンク #20536e
- 色を付けるのは街灯の琥珀 #f0b135 の 1 色だけ（お知らせの帯・箇条の印・Pro の点）

## Typography
- Display: **BIZ UDPGothic** 700（Google Fonts・日本語は文字の範囲ごとに分けて配られる）＝税務・業務の書類の調子
- Body: システムの日本語ゴシック
- 見出しは `word-break: auto-phrase`。斜体なし

## Motion
- お知らせの帯の出入り（transform 280ms `--ease-out`）だけ。reduced-motion で 0

## 守ること
- **路線価図そのものを載せない**（ストアの説明文の決まり＝`~/rosenka/docs/store/appstore_metadata_draft.md` 冒頭）。画面写真は検索・地図（地理院タイル）・結果の一覧だけ
- **国税庁の公式と誤解させない**：「ご注意」に「公式アプリではありません」を残す。国税庁の名前・ロゴを屋号の位置に使わない
- 奥付の背景地図の文は `~/rosenka/packages/core/src/notice.ts` の `BACKGROUND_MAP_NOTICE` と一字一句同じ（ゼンリンの条件・W216）。出典の行は `apps/mobile/App.tsx` の出典の欄と同じ
- 値段・無料の件数・年分は ASC の商品・`quota.ts`・`years.ts` が正本。ストアの説明文にない機能を書かない
- **配信の状態（お知らせの帯・最初の帯の 3 つの丸札・表の「配信」）は公開されたら直す**。App Store・Google Play で公開されたら本物のバッジに替え、会社トップの棚に載せる
- 確かめた幅＝320・375・414・768・1280（横のはみ出し 0・2 行に折れるリンク 0）
