# ネイティブマップ ユーザーガイド / NativeMap User Guide

**このドキュメントには日本語版と英語版が含まれています。英語版は後半にあります。This document includes both a Japanese version and an English version. The English version is in the latter part.**

## 日本語版

### はじめに

ネイティブマップは、年表データを視覚的に表示・編集できるWebアプリケーションです。ポップカルチャーやデジタル技術の歴史を年表形式で管理し、個人の体験と照らし合わせることができます。

**GitHubユーザーなら誰でも管理者になれる分散型システム**として設計されており、自分のリポジトリで独自の年表データを管理できます。

### 目的別の使い方

#### 1. 見たり操作するだけの人（閲覧者）

**対象**: データの追加や編集はしないが、ロードにより一時的な追加はできる

**基本的な操作**:
- 年表の表示とスクロール
- 検索機能の利用
- ジャンル・重要度フィルター
- 年表の活用（イベント年・生年の合わせ）

**データの一時的な追加**:
- 「ロード」機能でCSVファイルからデータを読み込み
- 編集・追加・削除は可能だが、保存はローカルのみ
- ページをリロードすると元の状態に戻る

#### 2. いまある年表の編集に参加する人（コラボレーター）

**対象**: アクセストークンはないが編集後の「同期」でダウンロードしたデータを提供できる人

**注意**: 現状、この機能への十分な対応はできていませんが、機能としては存在します。

**基本的な操作**:
- 閲覧者の操作に加えて、項目の編集・追加・削除
- 「同期」ボタンでCSVファイルをエクスポート
- エクスポートしたデータを管理者に提供

**制限事項**:
- リモートデータを直接更新することはできない
- 編集内容はローカルにのみ保存される
- 他のユーザーとのリアルタイム同期は不可

#### 3. 自分で新たに年表を作りたい人（ローカル管理者）

**対象**: ローカルのデータで閉じてロードとセーブで回していく人

**用途**: 簡単な年表をプレゼンや分析に使うなどに適する

**基本的な操作**:
- 閲覧者・コラボレーターの操作すべて
- 「ロード」でCSVファイルからデータを読み込み
- 「セーブ」で現在のデータをCSVファイルとして保存
- ローカルでの完全なデータ管理

**推奨ワークフロー**:
1. 初期データをCSVファイルで準備
2. 「ロード」でデータを読み込み
3. 必要に応じて編集・追加・削除
4. 「セーブ」で編集内容を保存
5. 必要に応じて手順2-4を繰り返し

#### 4. 自分で作った年表を公開したい人（GitHub管理者）

**対象**: GitHubにデータを置いて公開したい人

**必要な準備**:
- GitHubアカウント
- Personal Access Token
- リポジトリの作成

### GitHub公開の詳細手順

#### ステップ1: GitHubリポジトリの準備

1. **リポジトリの作成**
   - GitHubにログイン
   - 「New repository」をクリック
   - リポジトリ名を入力（例：`my-timeline`）
   - 「Public」または「Private」を選択
   - 「Create repository」をクリック

2. **初期ファイルの配置**
   - リポジトリに`timeline.json`ファイルを作成
   - 空のファイルでも構いません
   - または、[nativemapのリポジトリ](https://github.com/hortense667/nativemap)からサンプルデータを参照

#### ステップ2: Personal Access Tokenの取得

1. **GitHubの設定画面にアクセス**
   - GitHubの右上のプロフィール画像をクリック
   - 「Settings」を選択
   - 左サイドバーの「Developer settings」をクリック
   - 「Personal access tokens」→「Tokens (classic)」を選択

2. **新しいトークンの生成**
   - 「Generate new token」→「Generate new token (classic)」をクリック
   - Note: `Native Map Timeline Access`（任意の名前）
   - Expiration: 適切な期間を選択（推奨：90 days）
   - Scopes: 以下の権限にチェック
     - `repo` (Full control of private repositories)
     - `public_repo` (Access public repositories)

3. **トークンの保存**
   - 「Generate token」をクリック
   - 生成されたトークンをコピーして安全な場所に保存
   - **重要**: このトークンは再表示されません

#### ステップ3: ネイティブマップでの設定

1. **設定画面を開く**
   - ネイティブマップの「設定」ボタンをクリック

2. **GitHub情報を入力**
   - Personal Access Token: ステップ2で取得したトークン
   - リポジトリ所有者: 自分のGitHubユーザー名
   - リポジトリ名: ステップ1で作成したリポジトリ名
   - ファイルパス: `timeline.json`（通常はこのままでOK）

3. **設定の保存**
   - 「保存」ボタンをクリック
   - 設定がローカルストレージに保存されます

#### ステップ4: データの準備と同期

1. **データの準備**
   - 「ロード」機能でCSVファイルからデータを読み込み
   - または、既存のデータを編集

2. **初回同期**
   - 「同期」ボタンをクリック
   - データがGitHubリポジトリの`timeline.json`に保存されます

3. **継続的な運用**
   - 編集後は必ず「同期」でGitHubに反映
   - 他のユーザーが編集した場合は「同期」で最新データを取得

### 推奨運用方針

#### データ管理の方針

1. **定期的なバックアップ**
   - GitHubのバックアップ機能を活用
   - 重要な編集前は必ず「同期」を実行

2. **バージョン管理**
   - 大きな変更前はGitHubでコミットメッセージを記録
   - 必要に応じてタグやブランチを活用

3. **共同編集の管理**
   - 複数人で編集する場合は事前にルールを決める
   - 編集前に必ず「同期」で最新データを取得
   - 編集後は必ず「同期」で変更を反映

#### 公開の方針

1. **データの品質管理**
   - 定期的にデータの整合性をチェック
   - 不適切な内容がないか確認

2. **更新頻度**
   - 定期的な更新を心がける
   - 重要なイベントは迅速に追加

3. **コミュニティとの連携**
   - IssuesやPull Requestを活用
   - ユーザーフィードバックを積極的に取り入れる

### データ形式の詳細

#### CSV形式（ロード用）

**基本形式**:
```
開始年;終了年;ラベル;label_en;ジャンル;重要度;URL;url_en;注釈;note_en
```

**例**:
```
1946;;ENIAC;ENIAC;HAR;5;https://ja.wikipedia.org/wiki/ENIAC;https://en.wikipedia.org/wiki/ENIAC;初の大規模電子計算機;First large-scale electronic computer
1983;;任天堂ファミコン;Nintendo Famicom;GAM;5;https://ja.wikipedia.org/wiki/ファミリーコンピュータ;https://en.wikipedia.org/wiki/Nintendo_Entertainment_System;家庭用ゲーム機の革命;Home console revolution
```

**ジャンル定義**:
```
genre;CODE;LABEL;label_en;conjunction
```

**例**:
```
genre;ANI;アニメ;Animation;
genre;GAM;ゲーム;Game;
genre;JAPAN;日本;Japan;true
```

#### JSON形式（同期用）

同期で生成されるJSONファイルには以下の構造が含まれます：

```json
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
  "events": {
    "1946": [
      {
        "label": "ENIAC",
        "label_en": "ENIAC",
        "genre": "HAR",
        "importance": 5,
        "url": "https://ja.wikipedia.org/wiki/ENIAC",
        "url_en": "https://en.wikipedia.org/wiki/ENIAC",
        "note": "初の大規模電子計算機",
        "note_en": "First large-scale electronic computer"
      }
    ]
  },
  "genres": {
    "ANI": { "label": "アニメ", "label_en": "Animation" },
    "GAM": { "label": "ゲーム", "label_en": "Game" }
  }
}
```

**注意**: 同期では時代区分の設定は反映されません。時代区分はローカル設定として管理されます。

### 基本的な操作の詳細

#### 年表の表示と操作

**年表の表示**:
- 1950年代から2050年代まで縦スクロールで閲覧
- 左側のカラムに年とイベントが表示
- 右側のエリアでドラッグ操作が可能

**スクロール操作**:
- マウスホイールまたはスクロールバーで上下にスクロール
- キーボードの上下矢印キーでも操作可能

#### 項目の編集

**項目の編集**:
1. 編集したい項目をクリック
2. 編集モーダルが開く
3. 以下の項目を編集可能：
   - ラベル（日本語・英語）
   - 開始年・終了年
   - ジャンル
   - 重要度（1-5）
   - URL（日本語・英語）
   - 注釈（日本語・英語）
4. 「保存」ボタンで変更を確定

**項目の追加**:
1. 詳細一覧で「追加」ボタンをクリック
2. 新しい項目の情報を入力
3. 「保存」ボタンで追加

**項目の削除**:
1. 編集モーダルで「削除」ボタンをクリック
2. 確認ダイアログで「OK」を選択

#### 検索機能

**ラベル検索**:
- 検索ボックスにキーワードを入力
- 選択中のジャンルのみが検索対象
- ラベル（日本語/英語）のどちらに一致してもヒット
- リアルタイムで検索結果が更新

**詳細検索**:
- 「詳細」チェックボックスをオンにして検索
- 注釈（日本語/英語）も検索対象に含めて検索可能

#### ジャンルフィルター

**ジャンル選択**:
1. 「ジャンル選択」ボタンをクリック
2. ジャンル一覧から選択
3. 複数選択可能（AND条件）

**ジャンルの種類**:
- ANI: アニメ
- MAN: マンガ
- GAM: ゲーム
- MUS: 音楽
- MOV: 映画
- TV: テレビ
- HAR: ハードウェア
- SOFT: ソフトウェア
- その他多数

#### 重要度フィルター

**重要度の設定**:
- 1: 参考程度
- 2: やや重要
- 3: 重要
- 4: かなり重要
- 5: 最重要

**フィルター操作**:
- 「重要度」ボタンで重要度別にフィルター
- 複数選択可能

#### 詳細一覧

**詳細一覧の表示**:
1. 「詳細」ボタンをクリック
2. 年別の詳細一覧が表示
3. 各項目の詳細情報を確認

**項目の並び替え**:
- ドラッグ&ドロップで順序変更
- 「ドラッグで一覧の順序を変更できます」の表示

#### 年表の活用例

**使い方の例（任天堂ファミコン）**:
1. **イベント年を合わせる**: ドラッグ専用レーンの水色の丸を上下にドラッグして、左カラムのラベル「83 任天堂ファミコン」と同じ高さに揃える。縦軸の内側に「1983年」と表示される。
2. **生年を合わせる**: 水色の斜め線の左端（縦軸と交わる位置）近くの水色の丸を上下にドラッグして、生年（例：1965年生）に合わせる。上部には「18歳」と表示される。

**同じ操作は赤い丸（赤色ライン）でも行える。右上の小さな丸ボタンで各ラインの表示をオン/オフできる。**

#### 多言語対応

**言語切り替え**:
- 右上の「EN」ボタンで英語表示に切り替え
- URLに `?lang=en` を追加して英語表示でアクセス
- 日本語に戻す場合は「JA」ボタンをクリック

**多言語データ**:
- 日本語と英語の両方の情報を保持
- 表示時は選択された言語に応じて適切なフィールドが優先表示

### 障害対策とオフライン利用

#### サービス障害への対応

ネイティブマップは、CloudflareやGitHub（データを保管・公開している）、DNSなどの外部サービスに依存しています。これらのサービスに障害が発生した場合の対策について説明します。

#### 事前準備：HTMLファイルの保存

**確実にデモを行いたい場合の事前準備**:

1. **HTMLファイルの保存**
   - 通常のアクセスが可能な状態で、ページ上で右クリック
   - 「名前を付けて保存」を選択
   - HTMLファイルとして保存（例：`nativemap_backup.html`）

2. **保存のタイミング**
   - 重要なプレゼンテーションやデモの前
   - 定期的なバックアップとして
   - 最新のデータが反映された状態で保存

#### オフライン利用方法

**障害発生時の利用手順**:

1. **保存したHTMLファイルを開く**
   - 保存したHTMLファイルをダブルクリック
   - ブラウザで直接開く

2. **設定の調整**
   - 「設定」ボタンをクリック
   - **アクセストークンを空にする**（重要）
   - その他の設定は必要に応じて調整

3. **データの読み込み**
   - 「ロード」機能で事前に準備したCSVファイルを読み込み
   - または、保存時点のデータで利用

#### 注意事項と制限

**重要な注意点**:

1. **同期の不整合**
   - オフライン利用は便宜的な使い方です
   - 復旧のタイミングで同期に不整合が生じる可能性があります
   - アクセストークンは必ず空にして使用してください

2. **データの整合性**
   - オフラインで編集した内容は、サービス復旧後に手動で同期する必要があります
   - 複数人での編集がある場合は、競合が発生する可能性があります

3. **著作権について**
   - HTMLファイルはダウンロード可能ですが、著作権によって保護されています
   - 個人利用・教育目的での利用に限定してください
   - 商用利用や再配布は禁止されています

#### 推奨される運用方針

1. **定期的なバックアップ**
   - 重要なイベント前には必ずHTMLファイルを保存
   - 月1回程度の定期バックアップを推奨

2. **データの二重保存**
   - HTMLファイルの保存
   - CSVファイルでのデータエクスポート
   - 両方の方法でデータを保護

3. **障害時の連絡先**
   - サービス障害が発生した場合は、GitHubのIssuesで報告
   - 緊急時は管理者への直接連絡も検討

---

## English Version

### Introduction

Native Map is a web application that allows you to visually display and edit timeline data. You can manage the history of pop culture and digital technology in timeline format and compare it with your personal experiences.

It is designed as a **distributed system where any GitHub user can become an administrator**, allowing you to manage your own timeline data in your own repository.

### Usage by Purpose

#### 1. Viewers (Read-only users)

**Target**: Users who do not add or edit data, but can temporarily add data through loading

**Basic operations**:
- Timeline display and scrolling
- Using search function
- Genre and importance filters
- Timeline utilization (aligning event years and birth years)

**Temporary data addition**:
- Use "Load" function to read data from CSV files
- Editing, adding, and deleting is possible, but saving is local only
- Returns to original state when page is reloaded

#### 2. Collaborators (Contributors to existing timelines)

**Target**: Users without access tokens but can provide data downloaded after editing through "Sync"

**Note**: Currently, this functionality is not fully supported, but the feature exists.

**Basic operations**:
- All viewer operations plus item editing, adding, and deleting
- Export CSV files using "Sync" button
- Provide exported data to administrators

**Limitations**:
- Cannot directly update remote data
- Edited content is saved locally only
- No real-time synchronization with other users

#### 3. Local Timeline Creators (Local administrators)

**Target**: Users who work with local data using load and save cycles

**Use cases**: Suitable for creating simple timelines for presentations or analysis

**Basic operations**:
- All viewer and collaborator operations
- Load data from CSV files using "Load"
- Save current data as CSV files using "Save"
- Complete local data management

**Recommended workflow**:
1. Prepare initial data in CSV file
2. Load data using "Load"
3. Edit, add, or delete as needed
4. Save edited content using "Save"
5. Repeat steps 2-4 as needed

#### 4. GitHub Timeline Publishers (GitHub administrators)

**Target**: Users who want to publish their timelines on GitHub

**Required preparation**:
- GitHub account
- Personal Access Token
- Repository creation

### Detailed Steps for GitHub Publishing

#### Step 1: Prepare GitHub Repository

1. **Create Repository**
   - Log in to GitHub
   - Click "New repository"
   - Enter repository name (e.g., `my-timeline`)
   - Select "Public" or "Private"
   - Click "Create repository"

2. **Place Initial Files**
   - Create `timeline.json` file in repository
   - Empty file is acceptable
   - Or refer to sample data from [nativemap repository](https://github.com/hortense667/nativemap)

#### Step 2: Get Personal Access Token

1. **Access GitHub Settings**
   - Click profile image in upper right of GitHub
   - Select "Settings"
   - Click "Developer settings" in left sidebar
   - Select "Personal access tokens" → "Tokens (classic)"

2. **Generate New Token**
   - Click "Generate new token" → "Generate new token (classic)"
   - Note: `Native Map Timeline Access` (any name)
   - Expiration: Select appropriate period (recommended: 90 days)
   - Scopes: Check the following permissions:
     - `repo` (Full control of private repositories)
     - `public_repo` (Access public repositories)

3. **Save Token**
   - Click "Generate token"
   - Copy generated token and save in secure location
   - **Important**: This token will not be shown again

#### Step 3: Configure in Native Map

1. **Open Settings**
   - Click "Settings" button in Native Map

2. **Enter GitHub Information**
   - Personal Access Token: Token obtained in Step 2
   - Repository Owner: Your GitHub username
   - Repository Name: Repository name created in Step 1
   - File Path: `timeline.json` (usually OK as is)

3. **Save Settings**
   - Click "Save" button
   - Settings are saved to local storage

#### Step 4: Prepare Data and Synchronize

1. **Prepare Data**
   - Use "Load" function to read data from CSV files
   - Or edit existing data

2. **Initial Synchronization**
   - Click "Sync" button
   - Data is saved to `timeline.json` in GitHub repository

3. **Continuous Operation**
   - Always "Sync" to reflect changes to GitHub after editing
   - Use "Sync" to get latest data when others have edited

### Recommended Operation Policies

#### Data Management Policies

1. **Regular Backups**
   - Utilize GitHub's backup functionality
   - Always "Sync" before important edits

2. **Version Control**
   - Record commit messages in GitHub before major changes
   - Use tags and branches as needed

3. **Collaborative Editing Management**
   - Establish rules in advance when editing with multiple people
   - Always "Sync" to get latest data before editing
   - Always "Sync" to reflect changes after editing

#### Publishing Policies

1. **Data Quality Management**
   - Regularly check data integrity
   - Verify no inappropriate content

2. **Update Frequency**
   - Maintain regular updates
   - Quickly add important events

3. **Community Engagement**
   - Utilize Issues and Pull Requests
   - Actively incorporate user feedback

### Detailed Data Formats

#### CSV Format (for loading)

**Basic format**:
```
Start Year;End Year;Label;label_en;Genre;Importance;URL;url_en;Note;note_en
```

**Example**:
```
1946;;ENIAC;ENIAC;HAR;5;https://ja.wikipedia.org/wiki/ENIAC;https://en.wikipedia.org/wiki/ENIAC;初の大規模電子計算機;First large-scale electronic computer
1983;;任天堂ファミコン;Nintendo Famicom;GAM;5;https://ja.wikipedia.org/wiki/ファミリーコンピュータ;https://en.wikipedia.org/wiki/Nintendo_Entertainment_System;家庭用ゲーム機の革命;Home console revolution
```

**Genre Definition**:
```
genre;CODE;LABEL;label_en;conjunction
```

**Example**:
```
genre;ANI;アニメ;Animation;
genre;GAM;ゲーム;Game;
genre;JAPAN;日本;Japan;true
```

#### JSON Format (for synchronization)

The JSON file generated by synchronization includes the following structure:

```json
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
  "events": {
    "1946": [
      {
        "label": "ENIAC",
        "label_en": "ENIAC",
        "genre": "HAR",
        "importance": 5,
        "url": "https://ja.wikipedia.org/wiki/ENIAC",
        "url_en": "https://en.wikipedia.org/wiki/ENIAC",
        "note": "初の大規模電子計算機",
        "note_en": "First large-scale electronic computer"
      }
    ]
  },
  "genres": {
    "ANI": { "label": "アニメ", "label_en": "Animation" },
    "GAM": { "label": "ゲーム", "label_en": "Game" }
  }
}
```

**Note**: Era settings are not reflected in synchronization. Era settings are managed as local settings.

### Detailed Basic Operations

#### Timeline Display and Operation

**Timeline Display**:
- Browse from 1950s to 2050s with vertical scrolling
- Years and events are displayed in the left column
- Drag operations are possible in the right area

**Scroll Operation**:
- Scroll up and down with mouse wheel or scroll bar
- Also operable with keyboard up/down arrow keys

#### Item Editing

**Editing Items**:
1. Click on the item you want to edit
2. Edit modal opens
3. The following items can be edited:
   - Label (Japanese/English)
   - Start year/End year
   - Genre
   - Importance (1-5)
   - URL (Japanese/English)
   - Note (Japanese/English)
4. Click "Save" button to confirm changes

**Adding Items**:
1. Click "Add" button in detail list
2. Enter information for new item
3. Click "Save" button to add

**Deleting Items**:
1. Click "Delete" button in edit modal
2. Select "OK" in confirmation dialog

#### Search Function

**Label Search**:
- Enter keywords in search box
- Only selected genres are searched
- Hits if either Japanese or English label matches
- Search results update in real-time

**Detailed Search**:
- Check "Detail" checkbox and search
- Notes (Japanese/English) are also included in the search target

#### Genre Filter

**Genre Selection**:
1. Click "Genre Selection" button
2. Select from genre list
3. Multiple selection possible (AND condition)

**Genre Types**:
- ANI: Animation
- MAN: Manga
- GAM: Game
- MUS: Music
- MOV: Movie
- TV: Television
- HAR: Hardware
- SOFT: Software
- And many others

#### Importance Filter

**Importance Settings**:
- 1: Reference level
- 2: Somewhat important
- 3: Important
- 4: Quite important
- 5: Most important

**Filter Operation**:
- Filter by importance with "Importance" button
- Multiple selection possible

#### Detail List

**Display Detail List**:
1. Click "Detail" button
2. Year-by-year detail list is displayed
3. Check detailed information for each item

**Item Reordering**:
- Change order with drag & drop
- "Drag to change the order of the list" display

#### Timeline Usage Examples

**Usage Example (Nintendo Famicom)**:
1. **Align Event Year**: Drag the light blue circle in the drag-only lane up and down to align with the label "83 Nintendo Famicom" in the left column. "1983" will be displayed inside the vertical axis.
2. **Align Birth Year**: Drag the light blue circle near the left end of the light blue diagonal line (where it intersects with the vertical axis) up and down to align with your birth year (e.g., 1965). "18 years old" will be displayed at the top.

**The same operation can be performed with the red circle (red line). You can turn the display of each line on/off with the small circle button in the upper right.**

#### Multilingual Support

**Language Switching**:
- Switch to English display with "EN" button in upper right
- Add `?lang=en` to URL to access in English display
- Click "JA" button to return to Japanese

**Multilingual Data**:
- Maintains both Japanese and English information
- Appropriate fields are prioritized for display based on selected language

### Disaster Recovery and Offline Usage

#### Service Outage Response

Native Map depends on external services such as Cloudflare, GitHub (for data storage and publishing), and DNS. This section explains countermeasures when these services experience outages.

#### Preparation: Saving HTML Files

**Pre-preparation for reliable demonstrations**:

1. **Save HTML File**
   - Right-click on the page when normal access is possible
   - Select "Save as"
   - Save as HTML file (e.g., `nativemap_backup.html`)

2. **Timing for Saving**
   - Before important presentations or demonstrations
   - As regular backups
   - Save when latest data is reflected

#### Offline Usage Method

**Usage procedure during outages**:

1. **Open Saved HTML File**
   - Double-click the saved HTML file
   - Open directly in browser

2. **Adjust Settings**
   - Click "Settings" button
   - **Clear access token** (important)
   - Adjust other settings as needed

3. **Load Data**
   - Use "Load" function to read pre-prepared CSV files
   - Or use data from the time of saving

#### Precautions and Limitations

**Important Notes**:

1. **Synchronization Inconsistency**
   - Offline usage is a convenient method
   - Synchronization inconsistencies may occur at recovery time
   - Always clear access token when using

2. **Data Integrity**
   - Content edited offline needs to be manually synchronized after service recovery
   - Conflicts may occur when multiple people are editing

3. **Copyright**
   - HTML files are downloadable but protected by copyright
   - Limited to personal use and educational purposes
   - Commercial use and redistribution are prohibited

#### Recommended Operation Policies

1. **Regular Backups**
   - Always save HTML files before important events
   - Recommend monthly regular backups

2. **Dual Data Storage**
   - HTML file saving
   - Data export via CSV files
   - Protect data using both methods

3. **Contact During Outages**
   - Report service outages via GitHub Issues
   - Consider direct contact with administrators in emergencies