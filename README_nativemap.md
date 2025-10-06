# Native Map 1.0 / ネイティブマップ 1.0

## 日本語版

ネイティブマップは、年表データを視覚的に表示・編集できるWebアプリケーションです。ポップカルチャーやデジタル技術の歴史を年表形式で管理し、個人の体験と照らし合わせることができます。

**GitHubユーザーなら誰でも管理者になれる分散型システム**として設計されており、自分のリポジトリで独自の年表データを管理できます。

## English Version

Native Map is a web application that allows you to visually display and edit timeline data. You can manage the history of pop culture and digital technology in timeline format and compare it with your personal experiences.

It is designed as a **distributed system where any GitHub user can become an administrator**, allowing you to manage your own timeline data in your own repository.

### 主な機能

- **年表の視覚的表示**: 1950年代から2050年代までの年表を縦スクロールで表示
- **多言語対応**: 日本語/英語の切り替えが可能
- **データ編集**: 項目の追加、編集、削除、並び替え
- **検索機能**: ラベルやジャンルによる検索
- **データ同期**: GitHubとの連携による共有データの管理
- **CSV/TSV対応**: データの一括インポート/エクスポート

### Main Features

- **Visual Timeline Display**: Display timeline from 1950s to 2050s with vertical scrolling
- **Multilingual Support**: Switch between Japanese/English
- **Data Editing**: Add, edit, delete, and reorder items
- **Search Function**: Search by labels and genres
- **Data Synchronization**: Shared data management through GitHub integration
- **CSV/TSV Support**: Bulk import/export of data

### 多言語対応

#### 言語切り替え方法
- 右上の「EN」ボタンをクリックして英語表示に切り替え
- URLに `?lang=en` を追加して英語表示でアクセス
- 日本語に戻す場合は「JA」ボタンをクリック、または `?lang=ja` をURLに追加

#### 多言語データ形式
データは日本語と英語の両方の情報を保持できます：

**イベントデータ**
- `label`: 日本語ラベル
- `label_en`: 英語ラベル
- `url`: 日本語URL
- `url_en`: 英語URL
- `note`: 日本語注釈
- `note_en`: 英語注釈

**ジャンルデータ**
- `label`: 日本語ジャンル名
- `label_en`: 英語ジャンル名

表示時は、選択された言語に応じて適切なフィールドが優先表示されます。

### Multilingual Support

#### Language Switching Methods
- Click the "EN" button in the upper right to switch to English display
- Add `?lang=en` to URL to access in English display
- Click "JA" button to return to Japanese, or add `?lang=ja` to URL

#### Multilingual Data Format
Data can maintain both Japanese and English information:

**Event Data**
- `label`: Japanese label
- `label_en`: English label
- `url`: Japanese URL
- `url_en`: English URL
- `note`: Japanese note
- `note_en`: English note

**Genre Data**
- `label`: Japanese genre name
- `label_en`: English genre name

When displaying, appropriate fields are prioritized based on the selected language.

### メタデータ仕様 / Metadata Schema

アプリが読み込むJSONは、ルートに`metadata`と`events`を持つ構造を推奨します（後方互換で旧形式も読めます）。

```
{
  "metadata": {
    "title": { "ja": "ポップカルチャー年表", "en": "POP Culture Timeline" },
    "description": {
      "ja": "この年表は…",
      "en": "This timeline …"
    },
    "initialCreator": "Satoshi Endo",
    "contributors": ["Satoshi Endo", "Hortense Endo"],
    "contact": {
      "administrator": {
        "name": "Satoshi Endo",
        "email": "zzz@65536.net",
        "x": "https://x.com/hortense667",
        "organization": "ZEN University"
      }
    },
    "createdAt": "2025-10-01",
    "version": "1.0",
    "language": ["ja","en"],
    "copyright": "© 2025 Satoshi Endo",
    "license": "CC BY 4.0",
    "licenseUrl": "https://creativecommons.org/licenses/by/4.0/",
    "notes": "Updates from contributors are welcome …"
  },
  "events": { /* 従来のイベントマップ */ }
}
```

#### タイトル参照ルール
- 表示タイトルは`metadata.title.ja`/`metadata.title.en`を優先して使用します。
- 旧形式（`title`/`title_en`）がある場合は後方互換としてフォールバックします。
- 保存時も新形式で`metadata.title.{ja,en}`に書き込みます。

#### 影響範囲
- `events`配下のデータ構造・描画・検索は変更ありません。
- メタデータはヘルプ画面の「編集中のデータ」に表示されます。

### データセット

現在、以下の3つのデータセットが用意されています：

1. **timeline.json** - ポップカルチャー年表
   - アニメ、マンガ、ゲーム、音楽などのポップカルチャーイベント
   
2. **timeline_digital.json** - デジタルの歴史年表
   - コンピュータ、インターネット、デジタル技術の歴史
   
3. **initial_timeline.json** - 独自年表作成用フレーム
   - 空のテンプレート。独自の年表を作成する際の出発点

### Datasets

Currently, the following three datasets are available:

1. **timeline.json** - Pop Culture Timeline
   - Pop culture events such as anime, manga, games, music
   
2. **timeline_digital.json** - Digital History Timeline
   - History of computers, internet, digital technology
   
3. **initial_timeline.json** - Framework for Creating Custom Timelines
   - Empty template. Starting point for creating custom timelines

### 自分で新たに年表を作りたい人へ

**GitHubユーザーなら誰でも管理者になれます！**

このサービスは、GitHubアカウントを持つユーザーが自分のリポジトリで年表データを管理できる分散型システムです。独自の年表を作成・管理したい場合は、以下の手順でセットアップできます。

#### セットアップ手順

1. **GitHubリポジトリの準備**
   - 自分のGitHubアカウントでリポジトリを作成
   - `timeline.json`ファイルを配置（空のファイルでも可）

2. **Personal Access Tokenの取得**
   - GitHubの設定でPersonal Access Tokenを生成
   - リポジトリへの読み書き権限を付与

3. **設定画面での設定**
   - 「設定」ボタンから以下を入力：
     - Personal Access Token
     - リポジトリ所有者（自分のGitHubユーザー名）
     - リポジトリ名
     - ファイルパス（通常は`timeline.json`）

#### 推奨ワークフロー

1. **データの準備**
   - 「ロード」機能でCSVファイルからデータを読み込み、年表を作成

2. **同期でJSON化**
   - 「同期」ボタンでデータをGitHubリポジトリのJSONファイルに保存

**注意：** 同期では時代区分の設定は反映されません。時代区分はローカル設定として管理されます。

#### データ形式

**CSV形式（ロード用）**
```
開始年;終了年;ラベル;label_en;ジャンル;重要度;URL;url_en;注釈;note_en
```

**JSON形式（同期用）**
同期で生成されるJSONファイルには以下の構造が含まれます：
- `events`: 年表データ（年をキーとしたオブジェクト）
- `genres`: ジャンル設定
- `metadata`: メタデータ（作成日時、更新日時など）

#### 利点
- 完全なデータ制御権
- GitHubのバックアップ機能
- 複数ユーザーでの協力可能
- バージョン管理

### アクセストークンの使い分け

#### アクセストークンありの場合
- **管理者・コラボレーター向け**
- リモートの共有年表データを直接更新可能
- 「同期」ボタンでGitHubに変更を反映
- 複数人での共同編集が可能

#### アクセストークンなしの場合
- **一般ユーザー向け**
- リモートデータを直接更新することはできません
- 自分用のデータをロードするか画面で編集してセーブすることで独自の年表を作成
- セーブしたデータをロードして前日までの続きの作業を続けることで年表を更新・活用

### For Those Who Want to Create Their Own Timeline

**Any GitHub user can become an administrator!**

This service is a distributed system where GitHub users can manage timeline data in their own repositories. If you want to create and manage your own timeline, you can set it up following these steps.

#### Setup Steps

1. **Prepare GitHub Repository**
   - Create a repository in your GitHub account
   - Place a `timeline.json` file (empty file is acceptable)

2. **Get Personal Access Token**
   - Generate a Personal Access Token in GitHub settings
   - Grant read/write access to the repository

3. **Configure in Settings**
   - Enter the following from the "Settings" button:
     - Personal Access Token
     - Repository Owner (your GitHub username)
     - Repository Name
     - File Path (usually `timeline.json`)

#### Recommended Workflow

1. **Data Preparation**
   - Use the "Load" function to read data from CSV files and create timelines

2. **Synchronize to JSON**
   - Use the "Sync" button to save data to JSON files in your GitHub repository

**Note:** Era settings are not reflected in synchronization. Era settings are managed as local settings.

#### Data Formats

**CSV Format (for loading)**
```
Start Year;End Year;Label;label_en;Genre;Importance;URL;url_en;Note;note_en
```

**JSON Format (for synchronization)**
The JSON file generated by synchronization includes the following structure:
- `events`: Timeline data (object with years as keys)
- `genres`: Genre settings
- `metadata`: Metadata (creation time, update time, etc.)

#### Benefits
- Complete data control
- GitHub backup functionality
- Collaboration with multiple users
- Version control

### Access Token Usage

#### With Access Token
- **For Administrators and Collaborators**
- Can directly update shared timeline data on remote servers
- Reflect changes to GitHub with "Sync" button
- Collaborative editing with multiple people is possible

#### Without Access Token
- **For General Users**
- Cannot directly update remote data
- Create your own timeline by loading your own data or editing and saving on screen
- Continue updating and utilizing your timeline by loading saved data to continue work from the previous day

### データ形式

#### CSV/TSV形式（新形式）

**イベントデータ**
```
開始年;終了年;ラベル;label_en;ジャンル;重要度;URL;url_en;注釈;note_en
```

**例**
```
1946;;ENIAC;ENIAC;HAR;5;https://ja.wikipedia.org/wiki/ENIAC;https://en.wikipedia.org/wiki/ENIAC;初の大規模電子計算機;First large-scale electronic computer
1983;;任天堂ファミコン;Nintendo Famicom;GAM;5;https://ja.wikipedia.org/wiki/ファミリーコンピュータ;https://en.wikipedia.org/wiki/Nintendo_Entertainment_System;家庭用ゲーム機の革命;Home console revolution
```

**ジャンル定義**
```
genre;CODE;LABEL;label_en;conjunction
```

**例**
```
genre;ANI;アニメ;Animation;
genre;GAM;ゲーム;Game;
genre;JAPAN;日本;Japan;true
```

#### アクセストークンなしの場合の同期形式
削除フラグを含む形式：
```
開始年;終了年;ラベル;label_en;ジャンル;重要度;URL;url_en;注釈;note_en;deleted
```

### Data Format

#### CSV/TSV Format (New Format)

**Event Data**
```
Start Year;End Year;Label;label_en;Genre;Importance;URL;url_en;Note;note_en
```

**Example**
```
1946;;ENIAC;ENIAC;HAR;5;https://ja.wikipedia.org/wiki/ENIAC;https://en.wikipedia.org/wiki/ENIAC;初の大規模電子計算機;First large-scale electronic computer
1983;;任天堂ファミコン;Nintendo Famicom;GAM;5;https://ja.wikipedia.org/wiki/ファミリーコンピュータ;https://en.wikipedia.org/wiki/Nintendo_Entertainment_System;家庭用ゲーム機の革命;Home console revolution
```

**Genre Definition**
```
genre;CODE;LABEL;label_en;conjunction
```

**Example**
```
genre;ANI;アニメ;Animation;
genre;GAM;ゲーム;Game;
genre;JAPAN;日本;Japan;true
```

#### Sync Format for Cases Without Access Token
Format including deletion flag:
```
Start Year;End Year;Label;label_en;Genre;Importance;URL;url_en;Note;note_en;deleted
```

### 使用方法

#### 基本的な操作
1. **年表の表示**: 1950年代から2050年代まで縦スクロールで閲覧
2. **項目の編集**: 項目をクリックして編集モーダルを開く
3. **検索**: 検索ボックスでラベルやジャンルを検索
4. **詳細表示**: 「詳細」ボタンで年別の詳細一覧を表示

#### データの管理
1. **ロード**: CSV/TSVファイルからデータを一括インポート
2. **セーブ**: 現在のデータをCSV/TSVファイルとしてエクスポート
3. **同期**: アクセストークンがある場合はGitHubと同期

#### 年表の活用例
1. **イベント年を合わせる**: ドラッグ専用レーンの水色の丸を上下にドラッグ
2. **生年を合わせる**: 水色の斜め線の左端の丸を生年に合わせる
3. **年齢表示**: 上部に年齢が表示される

### Usage

#### Basic Operations
1. **Timeline Display**: Browse from 1950s to 2050s with vertical scrolling
2. **Item Editing**: Click on items to open edit modal
3. **Search**: Search labels and genres with search box
4. **Detail Display**: Click "Detail" button to show year-by-year detail list

#### Data Management
1. **Load**: Bulk import data from CSV/TSV files
2. **Save**: Export current data as CSV/TSV files
3. **Sync**: Synchronize with GitHub if access token is available

#### Timeline Usage Examples
1. **Align Event Year**: Drag the light blue circle in the drag-only lane up and down
2. **Align Birth Year**: Align the circle at the left end of the light blue diagonal line with your birth year
3. **Age Display**: Age is displayed at the top

### 技術仕様 / Technical Specifications

- **フロントエンド / Frontend**: HTML5, CSS3, JavaScript (ES6+)
- **データ形式 / Data Format**: JSON, CSV, TSV
- **外部連携 / External Integration**: GitHub API
- **対応ブラウザ / Supported Browsers**: Modern browsers (Chrome, Firefox, Safari, Edge)

### ライセンス / License

(c) 2025 Satoshi Endo All Rights Reserved

### サポート / Support

サービスは試験運用中です。問題やご要望がございましたら、GitHubのIssuesまでお知らせください。

Service is in trial operation. If you have any problems or requests, please let us know via GitHub Issues.