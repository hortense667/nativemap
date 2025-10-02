# ネイティブマップ ユーザーガイド / Native Map User Guide

## 日本語版

### はじめに

ネイティブマップは、年表データを視覚的に表示・編集できるWebアプリケーションです。ポップカルチャーやデジタル技術の歴史を年表形式で管理し、個人の体験と照らし合わせることができます。また、ユーザーが独自の年表を作成することもできます。

### 基本的な使い方

#### 1. 年表の表示と操作

**年表の表示**
- 1950年代から2050年代まで縦スクロールで閲覧できます
- 左側のカラムに年とイベントが表示されます
- 右側のエリアでドラッグ操作が可能です

**スクロール操作**
- マウスホイールまたはスクロールバーで上下にスクロール
- キーボードの上下矢印キーでも操作可能

#### 2. 項目の編集

**項目の編集**
1. 編集したい項目をクリック
2. 編集モーダルが開きます
3. 以下の項目を編集可能：
   - ラベル（日本語・英語）
   - 開始年・終了年
   - ジャンル
   - 重要度（1-5）
   - URL（日本語・英語）
   - 注釈（日本語・英語）
4. 「保存」ボタンで変更を確定

**項目の追加**
1. 詳細一覧で「追加」ボタンをクリック
2. 新しい項目の情報を入力
3. 「保存」ボタンで追加

**項目の削除**
1. 編集モーダルで「削除」ボタンをクリック
2. 確認ダイアログで「OK」を選択

#### 3. 検索機能

**ラベル検索**
- 検索ボックスにキーワードを入力
- 選択中のジャンルのみが検索対象
- リアルタイムで検索結果が更新

**詳細検索**
- 「詳細」ボタンで詳細検索モーダルを開く
- より詳細な条件で検索可能

#### 4. ジャンルフィルター

**ジャンル選択**
1. 「ジャンル選択」ボタンをクリック
2. ジャンル一覧から選択
3. 複数選択可能（AND条件）

**ジャンルの種類**
1.ジャンルは年表ごとに定義できます
2.ジャンルの例（ポップカルチャーの場合）
- ANI: アニメ
- MAN: マンガ
- GAM: ゲーム
- MUS: 音楽
- MOV: 映画
- TV: テレビ
- HAR: ハードウェア
- SOFT: ソフトウェア
- その他多数
3.AND条件とろるなジャンル
ジャンルによる絞り込みの際にAND条件として機能するジャンルを定義できます
ロードデータでは「genre;CODE;LABEL;label_en;conjunction」、リモートDB上のjsonでは「"conjunction": true」で定義します。

#### 5. 重要度フィルター

**重要度の設定**
- 1: 参考程度
- 2: やや重要
- 3: 重要
- 4: かなり重要
- 5: 最重要

**フィルター操作**
- 「重要度」ボタンで重要度別にフィルター
- 複数選択可能

#### 6. 詳細一覧

**詳細一覧の表示**
1. 「詳細」ボタンをクリック
2. 年別の詳細一覧が表示
3. 各項目の詳細情報を確認

**項目の並び替え**
- ドラッグ&ドロップで順序変更
- 「ドラッグで一覧の順序を変更できます」の表示

#### 7. データの同期

**アクセストークンありの場合**
1. 「同期」ボタンでGitHubと同期
2. 編集内容がリモートDBに反映
3. 複数人での共同編集が可能

**アクセストークンなしの場合**
1. 「同期」ボタンでCSVファイルをエクスポート
2. ローカルに保存
3. 「ロード」で編集内容を再現

#### 8. データのインポート/エクスポート

**CSV/TSV形式**
```
開始年;終了年;ラベル;label_en;ジャンル;重要度;URL;url_en;注釈;note_en
```

**例**
```
1946;;ENIAC;ENIAC;HAR;5;https://ja.wikipedia.org/wiki/ENIAC;https://en.wikipedia.org/wiki/ENIAC;初の大規模電子計算機;First large-scale electronic computer
1983;;任天堂ファミコン;Nintendo Famicom;GAM;5;https://ja.wikipedia.org/wiki/ファミリーコンピュータ;https://en.wikipedia.org/wiki/Nintendo_Entertainment_System;家庭用ゲーム機の革命;Home console revolution
```

**ロード機能**
1. 「ロード」ボタンをクリック
2. CSV/TSVファイルを選択
3. データが一括インポート

**セーブ機能**
1. 「セーブ」ボタンをクリック
2. 現在のデータをCSV/TSVファイルとしてダウンロード

#### 9. 多言語対応

**言語切り替え**
- 右上の「EN」ボタンで英語表示に切り替え
- URLに `?lang=en` を追加して英語表示でアクセス
- 日本語に戻す場合は「JA」ボタンをクリック

**多言語データ**
- 日本語と英語の両方の情報を保持
- 表示時は選択された言語に応じて適切なフィールドが優先表示

#### 10. 年表の活用例

**使い方の例（任天堂ファミコン）**
1. **イベント年を合わせる**: ドラッグ専用レーンの水色の丸を上下にドラッグして、左カラムのラベル「83 任天堂ファミコン」と同じ高さに揃えます。縦軸の内側に「1983年」と表示されます。
2. **生年を合わせる**: 水色の斜め線の左端（縦軸と交わる位置）近くの水色の丸を上下にドラッグして、生年（例：1965年生）に合わせます。上部には「18歳」と表示されます。

**同じ操作は赤い丸（赤色ライン）でも行えます。右上の小さな丸ボタンで各ラインの表示をオン/オフできます。**

---

## English Version

### Introduction

Native Map is a web application that allows you to visually display and edit timeline data. You can manage the history of pop culture and digital technology in timeline format and compare it with your personal experiences.

### Basic Usage

#### 1. Timeline Display and Operation

**Timeline Display**
- Browse from the 1950s to the 2050s with vertical scrolling
- Years and events are displayed in the left column
- Drag operations are possible in the right area

**Scroll Operation**
- Scroll up and down with mouse wheel or scroll bar
- Also operable with keyboard up/down arrow keys

#### 2. Item Editing

**Editing Items**
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

**Adding Items**
1. Click "Add" button in detail list
2. Enter information for new item
3. Click "Save" button to add

**Deleting Items**
1. Click "Delete" button in edit modal
2. Select "OK" in confirmation dialog

#### 3. Search Function

**Label Search**
- Enter keywords in search box
- Only selected genres are searched
- Search results update in real-time

**Detailed Search**
- Click "Detail" button to open detailed search modal
- Search with more detailed conditions

#### 4. Genre Filter

**Genre Selection**
1. Click "Genre Selection" button
2. Select from genre list
3. Multiple selection possible (AND condition)

**Genre Types**
1. Genres can be defined for each timeline.
2. Examples of genres (in the case of pop culture):
- ANI: Anime
- MAN: Manga
- GAM: Games
- MUS: Music
- MOV: Movies
- TV: Television
- HAR: Hardware
- SOFT: Software
- Many others
3. Genres with AND condition
You can define genres that function as an AND condition when filtering by genre. In the load data, it is defined as "genre;CODE;LABEL;label_en;conjunction", and in the remote DB's JSON, it is defined as "\"conjunction\": true".

#### 5. Importance Filter

**Importance Settings**
- 1: Reference level
- 2: Somewhat important
- 3: Important
- 4: Quite important
- 5: Most important

**Filter Operation**
- Filter by importance with "Importance" button
- Multiple selection possible

#### 6. Detail List

**Display Detail List**
1. Click "Detail" button
2. Year-by-year detail list is displayed
3. Check detailed information for each item

**Item Reordering**
- Change order with drag & drop
- "Drag to change the order of the list" display

#### 7. Data Synchronization

**With Access Token**
1. Synchronize with GitHub using "Sync" button
2. Edited content is reflected in remote DB
3. Collaborative editing with multiple people is possible

**Without Access Token**
1. Export CSV file using "Sync" button
2. Save locally
3. Reproduce edited content with "Load"

#### 8. Data Import/Export

**CSV/TSV Format**
```
Start Year;End Year;Label;label_en;Genre;Importance;URL;url_en;Note;note_en
```

**Example**
```
1946;;ENIAC;ENIAC;HAR;5;https://ja.wikipedia.org/wiki/ENIAC;https://en.wikipedia.org/wiki/ENIAC;初の大規模電子計算機;First large-scale electronic computer
1983;;任天堂ファミコン;Nintendo Famicom;GAM;5;https://ja.wikipedia.org/wiki/ファミリーコンピュータ;https://en.wikipedia.org/wiki/Nintendo_Entertainment_System;家庭用ゲーム機の革命;Home console revolution
```

**Load Function**
1. Click "Load" button
2. Select CSV/TSV file
3. Data is imported in bulk

**Save Function**
1. Click "Save" button
2. Download current data as CSV/TSV file

#### 9. Multilingual Support

**Language Switching**
- Switch to English display with "EN" button in upper right
- Add `?lang=en` to URL to access in English display
- Click "JA" button to return to Japanese

**Multilingual Data**
- Maintains both Japanese and English information
- Appropriate fields are prioritized for display based on selected language

#### 10. Timeline Usage Examples

**Usage Example (Nintendo Famicom)**
1. **Align Event Year**: Drag the light blue circle in the drag-only lane up and down to align with the label "83 Nintendo Famicom" in the left column. "1983" will be displayed inside the vertical axis.
2. **Align Birth Year**: Drag the light blue circle near the left end of the light blue diagonal line (where it intersects with the vertical axis) up and down to align with your birth year (e.g., 1965). "18 years old" will be displayed at the top.

**The same operation can be performed with the red circle (red line). You can turn the display of each line on/off with the small circle button in the upper right.**

