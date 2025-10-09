# NativeMap 1.0 / ネイティブマップ 1.0

**このドキュメントには日本語版と英語版が含まれています。英語版は後半にあります。
This document includes both a Japanese and an English version. The English version is in the latter part.**

## 日本語版

ネイティブマップは、年表データを視覚的に表示・編集できるWebアプリケーションです。ポップカルチャーやデジタル技術の歴史を年表形式で管理し、個人の体験と照らし合わせることができます。

**GitHubユーザーなら誰でも管理者になれる分散型システム**として設計されており、自分のリポジトリで独自の年表データを管理できます。

### 主な機能

- **年表の視覚的表示**: 1940年代から2035年代までの年表を縦スクロールで表示
- **多言語対応**: 日本語/英語の切り替えが可能
- **データ編集**: 項目の追加、編集、削除、並び替え
- **検索機能**: ラベルやジャンルによる検索
- **データ同期**: GitHubとの連携による共有データの管理
- **CSV/TSV対応**: データの一括インポート
- **参照年表機能**: 複数の年表データを同時に表示・比較可能

### データセット

現在、以下の3つのデータセットが用意されています：

1. **timeline_popculture_japan_01.json** - ポップカルチャー年表
   - アニメ、マンガ、ゲーム、音楽などのポップカルチャーイベント
   
2. **timeline_digital_japan_01.json** - デジタルの歴史年表
   - コンピュータ、インターネット、デジタル技術の歴史
   
3. **timeline_ai_01.json** - AI年表
   - AIの歴史年表


### 基本的な使い方

#### 年表の表示と操作
- 1940年代から2035年代まで縦スクロールで閲覧
- 左側のカラムに年とイベントが表示
- 右側のエリアでドラッグ操作が可能

#### 項目の編集
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

### 年表の活用例

1. **イベント年を合わせる**: ドラッグ専用レーンの水色の丸を上下にドラッグ
2. **生年を合わせる**: 水色の斜め線の左端の丸を生年に合わせる
3. **年齢表示**: 上部に年齢が表示される

### 技術仕様

- **フロントエンド**: HTML5, CSS3, JavaScript (ES6+)
- **データ形式**: JSON, CSV, TSV
- **外部連携**: GitHub API
- **対応ブラウザ**: Modern browsers (Chrome, Firefox, Safari, Edge)

### ライセンス

(c) 2025 Satoshi Endo All Rights Reserved

### サポート

サービスは試験運用中です。問題やご要望がございましたら、GitHubのIssuesまでお知らせください。

---

## English Version

Native Map is a web application that allows you to visually display and edit timeline data. You can manage the history of pop culture and digital technology in timeline format and compare it with your personal experiences.

It is designed as a **distributed system where any GitHub user can become an administrator**, allowing you to manage your own timeline data in your own repository.

### Main Features

- **Visual Timeline Display**: Display timeline from 1940s to 2035s with vertical scrolling
- **Multilingual Support**: Switch between Japanese/English
- **Data Editing**: Add, edit, delete, and reorder items
- **Search Function**: Search by labels and genres
- **Data Synchronization**: Shared data management through GitHub integration
- **CSV/TSV Support**: Bulk import
- **Reference Timeline Feature**: Display and compare multiple timeline data simultaneously

### Datasets

Currently, the following three datasets are available:

1. **timeline.json** - Pop Culture Timeline
   - Pop culture events such as anime, manga, games, music
   
2. **timeline_digital.json** - Digital History Timeline
   - History of computers, internet, digital technology
   
3. **timeline_ai_01.json** - AI Timeline
   - AI history timeline

### Basic Usage

#### Timeline Display and Operation
- Browse from 1940s to 2035s with vertical scrolling
- Years and events are displayed in the left column
- Drag operations are possible in the right area

#### Item Editing
- Click on items to open edit modal
- Edit labels, years, genres, importance, URLs, and notes
- Add, delete, and reorder items in detail list

#### Search and Filter
- Search labels and genres with search box
- Filter display items with genre selection
- Filter by importance level

#### Data Management
- **Load**: Bulk import from CSV/TSV (Settings → Data Management)
- **Sync**:
  - With access token: Updates JSON on GitHub (message: “Remote data updated.”)
  - Without token: Exports only changed items as CSV (Sync button turns green after export)
- **Reference Timeline**: Display and compare multiple timelines (read-only)

### Timeline Usage Examples

1. **Align Event Year**: Drag the light blue circle in the drag-only lane up and down
2. **Align Birth Year**: Align the circle at the left end of the light blue diagonal line with your birth year
3. **Age Display**: Age is displayed at the top

### For Those Who Want to Create Their Own Timeline

**Any GitHub user can become an administrator!**

The document is being prepared and is scheduled to be released soon.

### Technical Specifications

- **Frontend**: HTML5, CSS3, JavaScript (ES6+)
- **Data Format**: JSON, CSV, TSV
- **External Integration**: GitHub API
- **Supported Browsers**: Modern browsers (Chrome, Firefox, Safari, Edge)

### License

(c) 2025 Satoshi Endo All Rights Reserved

### Support

Service is in trial operation. If you have any problems or requests, please let us know via GitHub Issues.