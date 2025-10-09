# ネイティブマップ ユーザーガイド / NativeMap User Guide

**このドキュメントには日本語版と英語版が含まれています。英語版は後半にあります。This document includes both a Japanese version and an English version. The English version is in the latter part.**

## 日本語版

### はじめに

ネイティブマップは、年表データを視覚的に表示・編集できるWebアプリケーションです。ポップカルチャーやデジタル技術の歴史を年表形式で管理し、個人の体験と照らし合わせることができます。

### 参照年表機能について

#### 参照年表とは
参照年表機能は、メインの年表データに加えて、複数の年表データを同時に表示・比較できる機能です。参照年表のデータは読み取り専用で、編集や削除はできません。

#### 参照年表の設定方法
1. **設定画面で参照年表を指定**
   - 「設定」→「参照年表設定」で各参照年表の詳細を入力
   - 各参照年表について以下を指定：
     - リポジトリ所有者（owner）
     - リポジトリ名（repo）
     - ファイルパス（filePath）
     - 最小重要度（minImportance、省略可）
   - 「+ 参照年表を追加」ボタンで最大10個まで追加可能

2. **URLパラメータで直接指定**
   - URLに `refTimelines`（JSON配列）を追加（重要度も含めて指定可能）
   - 例：
     ```
     nativemap201.html?owner=hortense667&repo=nativemap&filePath=timeline_digital_japan_01.json&refTimelines=[{"owner":"hortense667","repo":"nativemap","filePath":"timeline_popculture_japan_01.json","minImportance":2}]
     ```

#### 参照年表の特徴
- **読み取り専用**: 編集・削除は不可（鉛筆アイコンとゴミ箱アイコンがグレーアウト）
- **独立したジャンル管理**: 各参照年表ごとにジャンルのオン/オフを制御
- **視覚的区別**: 参照年表の項目は青色で表示
- **検索対象**: ジャンルがオンになっている参照年表の項目も検索対象に含まれる

#### 参照年表の編集方法
参照年表の内容を編集したい場合は、ブラウザの別タブでそのファイルをメインのファイルパスとして開いて編集してください。

例：
- メインタブ：`timeline_digital_japan_01.json` + 参照：`timeline_popculture_japan_01.json`
- 編集タブ：`timeline_popculture_japan_01.json` をメインとして開いて編集

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

**対象**: 管理者からアクセストークンを受け取り、オンラインで編集・保存できる人。

**できること**:
- 閲覧者の操作に加えて、項目の編集・追加・削除
- 「同期」ボタンでGitHub上のJSONに直接反映（アクセストークン必須）

**注意**:
- 作業開始前に必ず「同期」で最新を取得し、作業後は必ず「同期」で保存してください。

**制限事項**:
- 更新可能な範囲は付与されたGitHub権限（対象リポジトリ）に従います
- ネットワークやGitHub側の制限により同期が一時的に失敗する場合があります

#### 3. 自分で作った年表を公開したい人（GitHub管理者）

この機能はいまのところ非公開ですが将来的には提供していく予定です。

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
*Conjunction is used within labels as an AND condition with other genres (e.g., if the "[Japan]" genre is selected, only events containing that genre will be displayed).

**例**:
```
genre;ANI;アニメ;Animation;
genre;GAM;ゲーム;Game;
genre;JAPAN;日本;Japan;true
```
**Title Definition**:
```
title;title(Japanese);title(English)
```
**Example**:
```
title;日本のカレーの歴史;Japanese Curry History
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

### トラブルシューティング

#### うまくいかないときのチェック項目

**参照年表が表示されない場合**：
1. ファイルパスが正しく設定されているか確認
2. 設定変更後は必ず「保存」ボタンを押しているか
3. ファイルがGitHubリポジトリに存在するか確認
4. ファイルパスにスペースや特殊文字が含まれていないか確認

**同期が失敗する場合**：
1. アクセストークンが正しく設定されているか
2. リポジトリの所有者名とリポジトリ名が正しいか
3. ファイルパスが正しいか
4. ネットワーク接続が正常か

**データが更新されない場合**：
1. ブラウザのキャッシュをクリア
2. 「表示中の全ラベルをクリアしてGitHubから読み込み」を実行
3. 設定を一度リセットして再設定

#### ブラウザのリロードと「表示中の全ラベルをクリアしてGitHubから読み込み」の違い

**ブラウザのリロード**：
- ページ全体を再読み込み
- ローカルストレージの設定は保持される
- 参照年表の設定も保持される
- 編集内容は失われる（未保存の場合）

**「表示中の全ラベルをクリアしてGitHubから読み込み」**：
- ローカルデータを完全にクリア
- GitHubから最新データを再読み込み
- 参照年表も再読み込み
- 編集フラグや削除記録もクリア
- より確実に最新状態にリセット

### 基本的な操作の詳細

#### 年表の表示と操作

**年表の表示**:
- 1940年代から2035年代まで縦スクロールで閲覧
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

注意（重要）:
- 編集モーダルは縦に長い場合があります。必ず一番下までスクロールして「保存」ボタンを押してください。押さない場合、変更は反映されません。
- 編集モーダルと詳細一覧は、上部の何もない部分をドラッグして位置を移動できます。
- 右側のグラフエリア（タイムライン部）をクリックすると、開いている詳細一覧/編集モーダルが閉じます。

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

### About Reference Timeline Feature

#### What is Reference Timeline
The reference timeline feature allows you to display and compare multiple timeline data simultaneously in addition to the main timeline data. Reference timeline data is read-only and cannot be edited or deleted.

#### How to Set Up Reference Timeline
1. **Specify reference timeline details in settings**
   - Go to "Settings" → "Reference Timeline Settings" and enter details for each reference timeline
   - For each reference timeline, specify:
     - Repository owner
     - Repository name
     - File path
     - Minimum importance (optional)
   - Use "+ Add Reference Timeline" button to add up to 10 reference timelines

2. **Direct specification via URL parameters**
   - Add `refTimelines` (JSON array) to the URL (importance can also be specified)
   - Example: `nativemap201.html?owner=hortense667&repo=nativemap&filePath=timeline_digital_japan_01.json&refTimelines=[{"owner":"hortense667","repo":"nativemap","filePath":"timeline_popculture_japan_01.json","minImportance":2}]`

#### Features of Reference Timeline
- **Read-only**: Cannot be edited or deleted (pencil and trash icons are grayed out)
- **Independent genre management**: Control genre on/off for each reference timeline
- **Visual distinction**: Reference timeline items are displayed in blue
- **Search target**: Items from reference timelines with genres turned on are also included in search results

#### How to Edit Reference Timeline
To edit reference timeline content, open that file as the main file path in a separate browser tab.

Example:
- Main tab: `timeline_digital_japan_01.json` + Reference: `timeline_popculture_japan_01.json`
- Edit tab: Open `timeline_popculture_japan_01.json` as main for editing

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

#### 3. GitHub Timeline Publishers (GitHub administrators)

This feature is currently not available, but we plan to offer it in the future.

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
※conjunctionはラベルの中で他のジャンルとAND条件として使用するものです（例：「[日本]」ジャンルが選択された場合、そのジャンルが含まれるイベントのみが表示される）。

**Example**:
```
genre;ANI;アニメ;Animation;
genre;GAM;ゲーム;Game;
genre;JAPAN;日本;Japan;true
```

**Title Definition**:
```
title;title（Japanese）;title（English）
```
**Example**:
```
title;日本のカレーの歴史;Japanese Curry History
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

### Troubleshooting

#### Check Items When Things Don't Work

**When reference timeline is not displayed**:
1. Check if file paths are correctly set
2. Make sure to press "Save" button after changing settings
3. Check if files exist in GitHub repository
4. Check if file paths contain spaces or special characters

**When synchronization fails**:
1. Check if access token is correctly set
2. Check if repository owner name and repository name are correct
3. Check if file path is correct
4. Check if network connection is normal

**When data is not updated**:
1. Clear browser cache
2. Execute "Clear all displayed labels and load from GitHub"
3. Reset settings once and reconfigure

#### Difference Between Browser Reload and "Clear all displayed labels and load from GitHub"

**Browser Reload**:
- Reloads entire page
- Keeps local storage settings
- Keeps reference timeline settings
- Loses editing content (if unsaved)

**"Clear all displayed labels and load from GitHub"**:
- Completely clears local data
- Reloads latest data from GitHub
- Reloads reference timeline
- Clears edit flags and deletion records
- More reliably resets to latest state

### Detailed Basic Operations

#### Timeline Display and Operation

**Timeline Display**:
- Browse from 1940s to 2035s with vertical scrolling
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

Important notes:
- The edit modal can be tall. Scroll to the bottom and click the "Save" button to apply changes. If you don't click Save, changes will not be applied.
- You can drag the header (blank area at the top) of the edit modal and the detail list to reposition them.
- Clicking the right graph area (timeline) closes the currently open detail/edit panels.

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