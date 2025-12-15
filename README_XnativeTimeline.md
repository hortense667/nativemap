# XnativeTimeline 1.0 / ネイティブマップ 1.0

**このドキュメントには日本語版と英語版が含まれています。英語版は後半にあります。
This document includes both a Japanese and an English version. The English version is in the latter part.**

## 日本語版

このリポジトリは **XnativeTimeline 用のデータ**（JSON）のみを収録しています。アプリ本体のコードは別管理です

### 最初に（おすすめの始め方）
- まずは「既にある年表を体験したい」人は、メイン年表に GitHub JSON を使うのが簡単です（owner/repo/filePath をURLで指定）。
- 「自分で年表を作ってみたい」人は、Google Sheets（GAS経由）がおすすめです。スプレッドシートを用意してURLに `sheetApi/sheetId` 等を載せれば、すぐ共有できます。

### 主な機能

ネイティブマップは、年表データを視覚的に表示・編集できるWebアプリケーションです。ポップカルチャーやデジタル技術の歴史を年表形式で管理し、個人の体験と照らし合わせることができます。

- **年表の視覚的表示**: 1868年代から2050年代までの年表を縦スクロールで表示
- **多言語対応**: 日本語/英語の切り替えが可能
- **データ編集**: 項目の追加、編集、削除、並び替え
- **検索機能**: ラベルやジャンルによる検索
- **データ同期/連携**:
  - GitHub JSON との連携（読み込み・同期）
  - Google Sheets（GAS経由）からの読み込みに対応（下記「データソースとURLパラメーター」参照）
 - **ローカルデータモード**: GitHubではなくPC上のJSONを読み書き（テスト/未公開用途）
- **CSV/TSV対応**: データの一括インポート/エクスポート
- **参照年表機能**: 複数の年表データを同時に表示・比較可能
- **フキダシ（吹き出し）**: 右側エリアをクリックして注釈を配置。三角テールはクリック位置を先端にし、バブルの辺から自然に接続。スタイル（色・文字サイズ・太字）変更やドラッグ移動、スナップショット保存/復元に対応。テイルの表示/非表示切り替え、画像表示機能（#URL形式）、改行対応。
- **ホバー表示文字サイズ設定**: ラベル表示エリアにマウスをホバーした際の文字サイズ（年、ラベル名、重要度、注釈）を個別に設定可能。
- **GitHubユーザーなら誰でも管理者になれる分散型システム**として設計されており、自分のリポジトリで独自の年表データを管理できます。

### データセット

現在用意されているデータセットの例：

1. **timeline_popculture_01.json** - ポップカルチャー年表
   - アニメ、マンガ、ゲーム、音楽などのポップカルチャーイベント
   
2. **timeline_digital_01.json** - デジタルの歴史年表
   - コンピュータ、インターネット、デジタル技術の歴史
   
3. **timeline_background_01.json** - 時代背景の歴史年表
   - 参照年表として他の年表と併用するための年表
   
4. **timeline_initial.json** - 独自年表作成用フレーム
   - 空のテンプレート。独自の年表を作成する際の出発点

※ユーザーは独自のデータセットを作ることができ公開することもできます。「自分で新たに年表を作りたい人へ」の項目をご覧ください。


### 基本的な使い方

#### 年表の表示と操作
- 1950年代から2050年代まで縦スクロールで閲覧
- 左側のカラムに年とイベントが表示
- 右側のエリアでドラッグ操作が可能

#### 項目の編集
- ジャンル表記のルール：`[]` は AND 条件、`{}` は「時代区分（genre_era=true）」を意味します。
- 「時代区分設定」画面に「すべての時代区分を登録」ボタンを追加。メイン年表のうち genre_era=true のジャンルが付いた項目を一括登録できます（登録時に表示・塗りON）。
- 起動/リロード時は参照年表をクリアした状態で開始します（参照年表は読み取り専用）。
#### フキダシ（吹き出し）
- ヘッダーのフキダシ追加アイコンをオン（またはShift+クリック）し、右側エリアをクリックで作成
- クリック点＝三角先端。接合位置は辺の中央±1/3範囲で自動調整（角丸は避ける）
- バブル／テールはドラッグ可能。右クリックで色テーマ・A-/A+・B（太字）・テイル切り替えを設定（表示モード）
- 削除アイコンでバブル・三角・継ぎ目カバーも一括削除
- 余白は左右対称（上下13px／左右16px）
- **新機能**: テイルの表示/非表示切り替え、画像表示（#URL形式）、改行対応
- 項目をクリックして編集モーダルを開く
- ラベル、年、ジャンル、重要度、URL、注釈を編集可能
- 詳細一覧で項目の追加・削除・並び替え

注意（重要）:
- 編集モーダルは縦に長い場合があります。必ず下部にある「保存」ボタンを押して反映してください（保存しないと内容は反映されません）。
- 編集モーダルと詳細一覧は、ヘッダー（上部の何もない領域）をドラッグして位置を移動できます。
- 右側のグラフエリアをクリックすると、開いている詳細一覧/編集モーダルが閉じます。

#### 検索とフィルター
- 検索ボックスでラベルやジャンルを検索
- ジャンル選択で表示項目を絞り込み
- 重要度別のフィルター機能
- 検索結果の青い項目にマウスオーバーでウェブ画面を開く（URLが設定されている場合）
- 検索結果の青い項目をクリックで注釈をポップアップ表示
- 検索ボックスに「*」を入力すると、選択されている分野のすべての項目を表示

#### データの管理
- **ロード**: CSV/TSVファイルからデータを一括インポート（設定 → データ管理）
- **同期（メイン年表）**:
  - アクセストークンあり: GitHubのJSONを更新（完了メッセージ: 「リモートデータを更新しました」）
  - アクセストークンなし: 変更点のみをCSVとしてエクスポート（エクスポート後、同期ボタンは緑になります）
- Google Sheets（GAS）モードのとき: 「同期」はシートから再読み込み（表示更新）を行います
- **参照年表**: 複数の年表データを同時に表示・比較（読み取り専用）
- **スナップショット**: 現在の状態（データ、フキダシ、設定、開いているウェブ画面パネル）を保存・復元。気軽に自分の年表を作り始めることができます
- **Amazon画像表示**: AmazonのURLの後に「&」を付けて画像URLを追加することで、ウェブ画面に表紙画像が表示されます
 - **ローカルデータモード**:
   1. 「設定」で「ローカルデータモード」をオン
   2. 「表示中の全ラベルをクリアしてローカルから読み込み」からJSONを選択して読み込み
   3. 編集後は「同期」ボタンでローカルJSONとして保存（ダウンロード）
   4. 参照年表は従来どおりGitHubから読み込まれます

### 年表の活用例

1. **イベント年を合わせる**: ドラッグ専用レーンの水色の丸を上下にドラッグ
2. **生年を合わせる**: 水色の斜め線の左端の丸を生年に合わせる
3. **年齢表示**: 上部に年齢が表示される

### 自分で新たに年表を作りたい人へ

**GitHubユーザーなら誰でも管理者になれます！**

このサービスは、GitHubアカウントを持つユーザーが自分のリポジトリで年表データを管理できる分散型システムです。独自の年表を作成・管理したい場合は、[ユーザーガイド](users_guide.md)をご覧ください。

**気軽に始める方法**:
1. 既存のデータをロードして編集
2. スナップショット保存で現在の状態を保存
3. スナップショット復元でいつでも元の状態に戻す
4. 気に入った状態になったらGitHubに同期して公開

### データソースとURLパラメーター（共有用）

第三者に設定不要で見せたい場合は、URLにパラメーターを付与して共有します。

- メイン年表（GitHub JSON）
  - datasrc=github
  - owner, repo, filePath
  - 例: `?datasrc=github&owner=hortense667&repo=nativetimeline&filePath=timeline_initial.json`

- メイン年表（Google Sheets / GAS）
  - datasrc=sheet
  - sheetApi, sheetId, ev, gn, er, md（タブ名）
  - 例:  
    `?datasrc=sheet&sheetApi=https://script.google.com/macros/s/XXX/exec&sheetId=1AbC...&ev=events&gn=genres&er=eraSettings&md=metadata`

- 参照年表（GitHub/Sheets 混在可）
  - refTimelines=JSON配列（URLエンコード）
  - 各要素（GitHub型）: `{ "sourceType":"github", "owner":"user", "repo":"repo", "filePath":"file.json", "minImportance":2 }`
  - 各要素（Sheets型）: `{ "sourceType":"sheet", "gasApi":"https://.../exec", "sheetId":"xxxxx", "ev":"events", "gn":"genres", "er":"eraSettings", "md":"metadata", "minImportance":2 }`
  - 例（エンコード前）:
    ```
    refTimelines=[{"sourceType":"github","owner":"user1","repo":"repo1","filePath":"file1.json","minImportance":2},
                  {"sourceType":"sheet","gasApi":"https://script.google.com/macros/s/XXX/exec","sheetId":"1AbC...","ev":"events","gn":"genres","er":"eraSettings","md":"metadata","minImportance":3}]
    ```

メイン年表の種別に応じて、不要なパラメーター（GitHub系/Sheets系）はURLから自動的に取り除かれます（設定→「設定を保存」時に付与/整理）。

### Google Sheets（GAS）で用意するシート構成
タブ名は基本値 `events / genres / eraSettings / metadata` を推奨（URLで変更可能）。

- events（年表本体）
  - 必須ヘッダー: `label, label_en, startYear`
  - 任意ヘッダー: `endYear, genre, imp, url, url_en, note, note_en, image`
  - 値の形式:
    - genre: パイプ区切り（例: `ANI|JAPAN|TVP`）
    - imp: 1～5 の整数
    - url/url_en: 単一またはパイプ区切りで複数可
  - フロント側が保存時にTSVをクリップボードへ置くときの並び（参考）:
    `label  label_en  startYear  endYear  genre(pipe)  imp  url  url_en  note  note_en  image`

- genres（ジャンル定義）
  - ヘッダー: `code, label, label_en, conjunction`
  - `conjunction` は AND結合に使う補助（true/false）。ジャンルコードは events.genre と対応します。

- eraSettings（時代区分）
  - ヘッダー: `name, startYear, endYear, color, opacity, enabled, fillEnabled`
  - `enabled`/`fillEnabled`: true/false。視覚背景の表示と塗りのオン/オフ。

- metadata（メタ情報）
  - ヘッダー（例）:
    - タイトル/説明: `title_ja, title_en, description_ja, description_en`
    - 作成者/連絡先: `initialCreator, contributors(パイプ), contact_admin_name, contact_admin_email, contact_admin_x, contact_admin_org`
    - その他: `createdAt, version, language(パイプ), copyright, license, licenseUrl, notes`

### Google Sheets（GAS）モード時の動作
- 詳細一覧の「鉛筆」: 編集モーダルを開き、保存時にTSV形式をクリップボードへコピー → 1秒トースト表示 → 対応セル位置でシートを自動オープン
- 詳細一覧の「ゴミ箱」: ダイアログや画面上削除は行わず、該当セル位置に移動（シートを開く）
- 左カラムの空き領域クリック: その年に近い行のセルへ移動（新規追加用）
- 「同期」: GAS APIから再読み込みして画面を更新
- シートを開く際は設定の events タブを対象にし、行フォーカスはGAS側で返す `_sheetRow/_sheetGid/_sheetTab` を優先（なければ推定）

### 編集可否（editmode）
- URLに `?editmode=ON` がない場合:
  - 詳細一覧の「鉛筆」「ゴミ箱」「追加」はグレーアウト（操作不可）
  - 左カラム空白クリックでも編集モーダルは開かない（Sheetsモードでも移動しない）

### 設定画面の参照年表UI（GitHub/Sheets 両対応）
- 「参照年表（GitHub）」と「参照年表（Sheets）」を分けて入力
- それぞれに「参照年表を追加」ボタン
- 保存すると `refTimelines` にJSONとして保存され、URLにも `refTimelines` が付与されます

### 技術仕様

- **フロントエンド**: HTML5, CSS3, JavaScript (ES6+)
- **データ形式**: JSON, CSV, TSV
- **外部連携**: GitHub API
- **外部連携（追加）**: Google Apps Script（GAS）Web API（Google Sheets読み込み）
- **対応ブラウザ**: Modern browsers (Chrome, Firefox, Safari, Edge)

## ライセンス
- データ: 原則 **CC BY 4.0**。一部の短い説明文がソースの共有条件に該当すると判断した場合、当該項目のみ **CC BY-SA 4.0** として `CREDIT.md` に明記します。
- 詳細: `LICENSE_DATA.txt`, `CREDIT.md` を参照

## サポート / Support
問題やご要望、**年表の内容訂正**は GitHub Issues へ:  
https://github.com/hortense667/nativetimeline/issues

Use these labels:
- `data-correction`（内容訂正）
- `feature-request`（機能提案）
- `bug`（不具合）

セキュリティ上の懸念は `SECURITY.md` をご確認ください。

---

## English Version

This repository contains only **data (JSON) for XnativeTimeline**. The application code itself is managed separately.

### Main Features

XnativeTimeline is a web application that allows you to visually display and edit timeline data. You can manage the history of pop culture and digital technology in a timeline format and compare it with personal experiences.

- **Visual Timeline Display**: Vertical scrolling timeline display from the 1868s to 2050s
- **Multilingual Support**: Toggle between Japanese/English
- **Data Editing**: Add, edit, delete, and reorder items
- **Search Function**: Search by labels and genres
- **Data Synchronization**: Shared data management through GitHub integration
- **CSV/TSV Support**: Bulk import/export of data
- **Reference Timeline**: Ability to display and compare multiple timeline data simultaneously
- **Speech Bubbles**: Place annotations by clicking in the right area. Triangle tails naturally connect from the bubble's edge to the clicked position. Supports style changes (color, font size, bold), drag movement, and snapshot save/restore. Toggle tail display, image display (#URL format), and line breaks.
- **Hover Display Font Size Settings**: Individually set font sizes (year, label name, importance, notes) when hovering over the label display area.
- **Designed as a distributed system where any GitHub user can become an administrator**, allowing management of unique timeline data in their own repository.

### Datasets

Examples of currently available datasets:

1. **timeline_popculture_01.json** - Pop Culture Timeline
   - Anime, manga, games, music, and other pop culture events
   
2. **timeline_digital_01.json** - Digital History Timeline
   - History of computers, internet, and digital technology
   
3. **timeline_background_01.json** - Historical Background Timeline
   - Timeline for use as reference alongside other timelines
   
4. **timeline_initial.json** - Custom Timeline Creation Frame
   - Empty template. Starting point for creating your own timeline

Note: Users can create and publish their own datasets. See the "For Those Who Want to Create Their Own Timeline" section.

### Basic Usage

#### Timeline Display and Operation
- Browse from the 1950s to 2050s with vertical scrolling
- Years and events displayed in the left column
- Drag operations possible in the right area

#### Item Editing
- Genre notation rules: `[]` indicates AND filter, `{}` denotes Era (genre_era=true).
- "Era Settings" includes a "Register all eras" button. It bulk-registers items in the main timeline that have genres with genre_era=true (Display/Fill ON at registration).
- On startup/reload, reference timelines start cleared (reference timelines are read-only).
#### Speech Bubbles
- Turn on the speech bubble add icon in header (or Shift+click) and click in right area to create
- Click point = triangle tip. Connection position auto-adjusts within ±1/3 of edge center (avoiding rounded corners)
- Bubble/tail can be dragged. Right-click to set color theme, A-/A+, B (bold), tail toggle (display mode)
- Delete icon removes bubble, triangle, and joint cover together
- Symmetric margins (13px top/bottom, 16px left/right)
- **New Features**: Toggle tail display, image display (#URL format), line break support
- Click items to open edit modal
- Edit labels, years, genres, importance, URLs, and notes
- Add/delete/reorder items in detailed list

Important Notes:
- Edit modal may be vertically long. Be sure to click "Save" button at bottom to apply changes (changes won't be reflected without saving).
- Edit modal and detailed list can be repositioned by dragging their headers (empty area at top).
- Clicking the right graph area closes any open detailed list/edit modal.

#### Search and Filter
- Search labels and genres using search box
- Filter displayed items by genre selection
- Filter by importance level
- Hover over blue search result items to open web preview (if URL is set)
- Click blue search result items to display note popup
- Enter "*" in search box to display all items in selected genres

#### Data Management
- **Load**: Bulk import data from CSV/TSV files (Settings → Data Management)
- **Sync**:
  - With access token: Update GitHub JSON (completion message: "Remote data updated")
  - Without access token: Export changes only as CSV (sync button turns green after export)
- **Reference Timeline**: Display and compare multiple timeline data simultaneously (read-only)
- **Snapshot**: Save and restore current state (data, speech bubbles, settings, open web preview panels). Easily start creating your own timeline.
- **Amazon Image Display**: Adding an image URL after "&" to an Amazon URL displays the cover image in the web preview panel.

### Timeline Usage Examples

1. **Align Event Years**: Drag blue circles up/down in the dedicated drag lane
2. **Align Birth Year**: Align the circle at the left end of the blue diagonal line with birth year
3. **Age Display**: Age is shown at the top

### For Those Who Want to Create Their Own Timeline

**Any GitHub user can become an administrator!**

This service is a distributed system where users with GitHub accounts can manage timeline data in their own repositories. If you want to create and manage your own timeline, please see the [User Guide](users_guide.md).

**Easy Way to Start**:
1. Load existing data and edit
2. Save current state with snapshot
3. Restore to original state anytime with snapshot
4. Sync to GitHub and publish when satisfied with the state

### Technical Specifications

- **Frontend**: HTML5, CSS3, JavaScript (ES6+)
- **Data Format**: JSON, CSV, TSV
- **External Integration**: GitHub API
- **Supported Browsers**: Modern browsers (Chrome, Firefox, Safari, Edge)

## License
- Data: Generally **CC BY 4.0**. When short descriptions are deemed to fall under source sharing conditions, those specific items are marked as **CC BY-SA 4.0** in `CREDIT.md`.
- Details: See `LICENSE_DATA.txt`, `CREDIT.md`

## Support
Submit issues, requests, and **timeline content corrections** to GitHub Issues:  
https://github.com/hortense667/nativetimeline/issues

Use these labels:
- `data-correction` (content correction)
- `feature-request` (feature suggestions)
- `bug` (issues)

For security concerns, please check `SECURITY.md`.
