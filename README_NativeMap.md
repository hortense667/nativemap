# NativeMap 1.0 / ネイティブマップ 1.0

**このドキュメントには日本語版と英語版が含まれています。英語版は後半にあります。
This document includes both a Japanese and an English version. The English version is in the latter part.**

## 日本語版

このリポジトリは **NativeMap 用のデータ**（JSON）のみを収録しています。アプリ本体のコードは別管理です

### 主な機能

ネイティブマップは、年表データを視覚的に表示・編集できるWebアプリケーションです。ポップカルチャーやデジタル技術の歴史を年表形式で管理し、個人の体験と照らし合わせることができます。

- **年表の視覚的表示**: 1868年代から2050年代までの年表を縦スクロールで表示
- **多言語対応**: 日本語/英語の切り替えが可能
- **データ編集**: 項目の追加、編集、削除、並び替え
- **検索機能**: ラベルやジャンルによる検索
- **データ同期**: GitHubとの連携による共有データの管理
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

#### データの管理
- **ロード**: CSV/TSVファイルからデータを一括インポート（設定 → データ管理）
- **同期**:
  - アクセストークンあり: GitHubのJSONを更新（完了メッセージ: 「リモートデータを更新しました」）
  - アクセストークンなし: 変更点のみをCSVとしてエクスポート（エクスポート後、同期ボタンは緑になります）
- **参照年表**: 複数の年表データを同時に表示・比較（読み取り専用）
- **スナップショット**: 現在の状態（データ、フキダシ、設定）を保存・復元。気軽に自分の年表を作り始めることができます

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

### 技術仕様

- **フロントエンド**: HTML5, CSS3, JavaScript (ES6+)
- **データ形式**: JSON, CSV, TSV
- **外部連携**: GitHub API
- **対応ブラウザ**: Modern browsers (Chrome, Firefox, Safari, Edge)

## ライセンス
- データ: 原則 **CC BY 4.0**。一部の短い説明文がソースの共有条件に該当すると判断した場合、当該項目のみ **CC BY-SA 4.0** として `CREDIT.md` に明記します。
- 詳細: `LICENSE_DATA.txt`, `CREDIT.md` を参照

## サポート / Support
問題やご要望、**年表の内容訂正**は GitHub Issues へ:  
https://github.com/hortense667/nativemap/issues

Use these labels:
- `data-correction`（内容訂正）
- `feature-request`（機能提案）
- `bug`（不具合）

セキュリティ上の懸念は `SECURITY.md` をご確認ください。

---

## English Version

This repository contains only **data (JSON) for NativeMap**. The application code itself is managed separately.

### Main Features

NativeMap is a web application that allows you to visually display and edit timeline data. You can manage the history of pop culture and digital technology in a timeline format and compare it with personal experiences.

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

#### Data Management
- **Load**: Bulk import data from CSV/TSV files (Settings → Data Management)
- **Sync**:
  - With access token: Update GitHub JSON (completion message: "Remote data updated")
  - Without access token: Export changes only as CSV (sync button turns green after export)
- **Reference Timeline**: Display and compare multiple timeline data simultaneously (read-only)
- **Snapshot**: Save and restore current state (data, speech bubbles, settings). Easily start creating your own timeline.

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
https://github.com/hortense667/nativemap/issues

Use these labels:
- `data-correction` (content correction)
- `feature-request` (feature suggestions)
- `bug` (issues)

For security concerns, please check `SECURITY.md`.
