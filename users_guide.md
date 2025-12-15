# Xnative/Timeline ユーザーガイド / Xnative/Timeline User Guide

**このドキュメントには日本語版と英語版が含まれています。英語版は後半にあります。This document includes both a Japanese version and an English version. The English version is in the latter part.**

## 日本語版

このリポジトリはデータ（JSON）専用です。アプリは別リポジトリ/ホスティングで提供されます。

### はじめに

ネイティブタイムラインは、年表データを視覚的に表示・編集できるWebアプリケーションです。ポップカルチャーやデジタル技術の歴史を年表形式で管理し、個人の体験と照らし合わせることができます。

**GitHubユーザーなら誰でも管理者になれる分散型システム**として設計されており、自分のリポジトリで独自の年表データを管理できます。

### 参照年表機能について
### フキダシ（吹き出し）詳細ガイド

#### 概要
右側のグラフエリアに注釈を配置できるフキダシ機能です。先端（ポインタ）はクリック位置になり、三角テールが自動で最適な辺から接続されます。角丸部分からは出ず、接合位置は辺の中央±1/3の範囲に制限されます。

#### 作成・編集・削除
- 作成: ヘッダーのフキダシ追加アイコンをオン、または Shift+クリック → 右側エリアをクリック
- 編集: 表示モードで鉛筆アイコンをクリック
- 削除: ゴミ箱アイコン（バブル本体・三角テール・継ぎ目カバーを同時に削除）
- 移動: バブルはドラッグで移動、三角はテールをドラッグして先端座標を変更

#### スタイル設定（表示モードのみ）
- 右クリックメニューから以下を変更
  - 色テーマ（数種）
  - 文字サイズ（A-/A+ 連続押し可、下限8px・上限なし）
  - 太字（B トグル）
  - テイル表示/非表示（△ボタン）

#### 表示の調整
- 内側余白は左右対称（上下13px・左右16px）
- 三角テールとバブルの継ぎ目は自動で馴染むよう処理（背景色のシーム＋枠線揃え）

#### スナップショット
- スナップショット保存/復元に対応（位置・テキスト・スタイル・先端座標）
- 復元後、GitHubが新しければ同期をブロックする仕組みに準拠
- 開いているウェブ画面パネルも保存・復元されます（位置、表示中のURL、言語設定など）

#### 画像表示機能
- テキストに「#https://example.com/image.png」の形式で画像URLを記述すると画像を表示
- 「#https://example.com/image.png キャプション」の形式でキャプションも表示可能
- 画像はドラッグ移動・角からのリサイズ（アスペクト比維持）に対応
- 画像のマージンは最小限（フキダシの枠線のみ）
- キャプションはフキダシの文字色・サイズ設定を継承

#### 改行対応
- フキダシ内のテキストで改行が有効
- 入力時の改行が表示時も反映される


#### 参照年表とは
参照年表機能は、メインの年表データに加えて、複数の年表データを同時に表示・比較できる機能です。参照年表のデータは読み取り専用で、編集や削除はできません。

#### 参照年表の設定方法
1. **設定画面で参照年表ファイルパスを指定**
   - 「設定」→「参照年表ファイルパス」に、カンマ区切りで最大10個のJSONファイルパスを入力
   - 例：`timeline_popculture_japan_01.json, timeline_ai_01.json`

2. **URLパラメータで直接指定**
   - URLに `refTimelines`（JSON配列）を追加（重要度も含めて指定可能）
   - 例：
     ```
     nativetimeline201.html?owner=hortense667&repo=nativetimeline&filePath=timeline_digital_japan_01.json&refTimelines=%5B%7B%22owner%22%3A%22hortense667%22%2C%22repo%22%3A%22nativetimeline%22%2C%22filePath%22%3A%22timeline_backglound_01.json%22%2C%22minImportance%22%3A2%7D%5D
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

**ウェブ画面の表示**:
- 詳細一覧の「地球」マークや検索結果の青い項目にマウスオーバーすると、その項目のURLが設定されている場合、ウェブ画面が開きます
- AmazonのURLの場合、URLの後に「&」を付けて画像URLを追加することで、表紙画像が表示されます

#### 2. いまある年表の編集に参加する人（コラボレーター）

**対象**: アクセストークンはないが編集後の「同期」でダウンロードしたデータを提供できる人

**注意**: 現状、この機能への十分な対応はできていませんが、機能としては存在します。

**基本的な操作**:
- 閲覧者の操作に加えて、項目の編集・追加・削除
- 「同期」ボタンでCSVファイルをエクスポート（アクセストークンがない場合）
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
4. 「スナップショット保存」で現在の状態を保存
5. 必要に応じて手順2-4を繰り返し
6. 気に入った状態になったら「セーブ」でCSVファイルとして保存

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
   - または、[nativetimelineのリポジトリ](https://github.com/hortense667/nativetimeline)からサンプルデータを参照

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

#### ステップ3: ネイティブタイムラインでの設定

1. **設定画面を開く**
   - ネイティブタイムラインの「設定」ボタンをクリック

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
   - アクセストークンあり: GitHubのJSONを更新（メッセージ「リモートデータを更新しました」）
   - アクセストークンなし: 変更点のみCSVとしてダウンロード（ボタンは緑に戻ります）

3. **継続的な運用**
   - 編集後は必ず「同期」でGitHubに反映
   - 他のユーザーが編集した場合は「同期」で最新データを取得
   - 重要な編集前は「スナップショット保存」でバックアップを取る

### 推奨運用方針

#### データ管理の方針

1. **定期的なバックアップ**
   - GitHubのバックアップ機能を活用
   - 重要な編集前は必ず「スナップショット保存」を実行
   - 定期的に「同期」でGitHubに反映

2. **バージョン管理**
   - 大きな変更前はGitHubでコミットメッセージを記録
   - 必要に応じてタグやブランチを活用

3. **共同編集の管理**
   - 複数人で編集する場合は事前にルールを決める
   - 編集前に必ず「同期」で最新データを取得
   - 編集後は必ず「同期」で変更を反映
   - 編集前は「スナップショット保存」でバックアップを取る

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

**検索結果の操作**:
- 検索結果として表示される青い項目にマウスオーバーすると、その項目のURLが設定されている場合、詳細一覧の「地球」マークと同じようにウェブ画面が開きます
- 検索結果の青い項目をクリックすると、その項目の注釈がポップアップ表示されます（英語モードのときは英語の注釈、日本語モードのときは日本語の注釈を表示）
- 再度クリックするか、マウスが項目から外れると注釈ポップアップが閉じます

**ワイルドカード検索**:
- 検索ボックスに「*」を入力して検索すると、現在選択されている分野（ジャンル）のすべての項目が検索結果として表示されます
- 重要度フィルターが設定されている場合は、その条件も適用されます

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

**ウェブ画面の表示**:
- 各項目の「地球」マークにマウスオーバーすると、その項目のURLが設定されている場合、ウェブ画面が開きます
- AmazonのURLの場合、URLの後に「&」を付けて画像URLを追加することで、表紙画像が表示されます
  - 例：`https://www.amazon.co.jp/dp/XXXXXXXXXX&https://example.com/image.jpg`
- 検索結果の青い項目にマウスオーバーした場合も同様にウェブ画面が開きます

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

ネイティブタイムラインは、CloudflareやGitHub（データを保管・公開している）、DNSなどの外部サービスに依存しています。これらのサービスに障害が発生した場合の対策について説明します。

#### 事前準備：HTMLファイルの保存

**確実にデモを行いたい場合の事前準備**:

1. **HTMLファイルの保存**
   - 通常のアクセスが可能な状態で、ページ上で右クリック
   - 「名前を付けて保存」を選択
   - HTMLファイルとして保存（例：`nativetimeline_backup.html`）

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

## ライセンス
- データ: 原則 CC BY 4.0。項目単位で CC BY-SA 4.0 の例外がある場合は `CREDIT.md` に明記します。
- 詳細は `LICENSE_DATA.txt` を参照。

## コミュニティとの連携
- **Issues と Pull Request を活用**してください。
- Issues 作成時はテンプレートから該当（内容訂正 / 機能提案 / 不具合報告）を選び、  
  **再現手順・スクリーンショット・参照URL** を添付いただけると助かります。
- フィードバック導線：
  - 一般: https://github.com/hortense667/nativetimeline/issues
  - セキュリティ: `SECURITY.md` の手順に従ってください。

---

## English Version

This repository is for data (JSON) only. The application is provided in a separate repository/hosting.

### Introduction

NativeTimeline is a web application that allows you to visually display and edit timeline data. You can manage the history of pop culture and digital technology in a timeline format and compare it with personal experiences.

Designed as a **distributed system where any GitHub user can become an administrator**, you can manage your own timeline data in your repository.

### About Reference Timeline Feature
### Speech Bubble Detailed Guide

#### Overview
A speech bubble feature that allows you to place annotations in the right graph area. The tip (pointer) becomes the click position, and the triangle tail automatically connects from the optimal edge. It doesn't extend from rounded corners, and the connection position is restricted to within ±1/3 of the edge center.

#### Create, Edit, Delete
- Create: Turn on the speech bubble add icon in header, or Shift+click → Click in right area
- Edit: Click pencil icon in display mode
- Delete: Trash icon (simultaneously deletes bubble body, triangle tail, and seam cover)
- Move: Drag bubble to move, drag tail to change tip coordinates

#### Style Settings (Display Mode Only)
- Change the following from right-click menu:
  - Color theme (multiple options)
  - Font size (A-/A+ continuous press possible, minimum 8px, no maximum)
  - Bold (B toggle)
  - Tail display/hide (△ button)

#### Display Adjustment
- Internal padding is symmetrical (13px top/bottom, 16px left/right)
- Triangle tail and bubble seam are automatically blended (background color seam + border alignment)

#### Snapshots
- Supports snapshot save/restore (position, text, style, tip coordinates)
- After restoration, complies with mechanism to block synchronization if GitHub is newer

#### Image Display Feature
- Display images by writing image URL in text format "#https://example.com/image.png"
- Caption can also be displayed in format "#https://example.com/image.png Caption"
- Images support drag movement and resize from corners (maintains aspect ratio)
- Image margins are minimal (bubble border only)
- Captions inherit speech bubble text color and size settings

#### Line Break Support
- Line breaks are effective in speech bubble text
- Line breaks during input are reflected in display

#### What is Reference Timeline
The reference timeline feature allows you to display and compare multiple timeline data simultaneously in addition to the main timeline data. Reference timeline data is read-only and cannot be edited or deleted.

#### How to Set Up Reference Timeline
1. **Specify reference timeline file path in settings**
   - Enter up to 10 JSON file paths separated by commas in "Settings" → "Reference Timeline File Path"
   - Example: `timeline_popculture_japan_01.json, timeline_ai_01.json`

2. **Direct specification in URL parameters**
   - Add `refTimelines` (JSON array) to URL (can specify importance level)
   - Example:
     ```
     nativetimeline201.html?owner=hortense667&repo=nativetimeline&filePath=timeline_digital_japan_01.json&refTimelines=%5B%7B%22owner%22%3A%22hortense667%22%2C%22repo%22%3A%22nativetimeline%22%2C%22filePath%22%3A%22timeline_backglound_01.json%22%2C%22minImportance%22%3A2%7D%5D
     ```

#### Reference Timeline Features
- **Read-only**: Cannot edit or delete (pencil and trash icons are grayed out)
- **Independent genre management**: Control genre on/off for each reference timeline
- **Visual distinction**: Reference timeline items are displayed in blue
- **Search target**: Items from reference timelines with genres turned on are included in search

#### How to Edit Reference Timeline
To edit reference timeline content, open that file as the main file path in a separate browser tab.

Example:
- Main tab: `timeline_digital_japan_01.json` + Reference: `timeline_popculture_japan_01.json`
- Edit tab: Open `timeline_popculture_japan_01.json` as main and edit

### Usage by Purpose

#### 1. People Who Just Want to View and Operate (Viewers)

**Target**: Cannot add or edit data, but can temporarily add through loading

**Basic Operations**:
- Display and scroll timeline
- Use search function
- Genre and importance filters
- Timeline utilization (aligning event years and birth years)

**Search Result Operations**:
- Hovering over the blue search result items opens a web preview panel (same behavior as the globe icon in the detail list) if the item has a URL
- Clicking a blue search result item displays a popup with the item's note (English note in English mode, Japanese note in Japanese mode)
- Click again or move the mouse away to close the note popup

**Wildcard Search**:
- Entering "*" in the search box displays all items in the currently selected genres as search results
- Importance filter settings are also applied if configured

**Web Preview Panel**:
- Hovering over the globe icon in the detail list or blue search result items opens a web preview panel if the item has a URL
- For Amazon URLs, adding an image URL after "&" displays the cover image
  - Example: `https://www.amazon.co.jp/dp/XXXXXXXXXX&https://example.com/image.jpg`

**Temporary Data Addition**:
- Load data from CSV file using "Load" function
- Can edit, add, delete but saves locally only
- Returns to original state when page is reloaded

#### 2. People Who Want to Participate in Editing Existing Timeline (Collaborators)

**Target**: People who can provide downloaded data after "sync" without access token

**Note**: Currently, this functionality is not fully supported but exists as a feature.

**Basic Operations**:
- Edit, add, delete items in addition to viewer operations
- Export CSV file with "Sync" button (when no access token)
- Provide exported data to administrator

**Limitations**:
- Cannot directly update remote data
- Edits are saved locally only
- No real-time sync with other users

#### 3. People Who Want to Create Their Own Timeline (Local Administrators)

**Target**: People who manage with local data using load and save

**Use Cases**: Suitable for using simple timelines for presentations and analysis

**Basic Operations**:
- All viewer and collaborator operations
- Load data from CSV file with "Load"
- Save current data as CSV file with "Save"
- Complete data management locally

**Recommended Workflow**:
1. Prepare initial data in CSV file
2. Load data using "Load"
3. Edit, add, delete as needed
4. Save current state with "Snapshot Save"
5. Repeat steps 2-4 as needed
6. When satisfied with state, save as CSV file using "Save"

#### 4. People Who Want to Publish Their Own Timeline (GitHub Administrators)

**Target**: People who want to host and publish data on GitHub

**Required Preparation**:
- GitHub account
- Personal Access Token
- Repository creation

### Detailed GitHub Publication Steps

#### Step 1: Prepare GitHub Repository

1. **Create Repository**
   - Log in to GitHub
   - Click "New repository"
   - Enter repository name (e.g., `my-timeline`)
   - Select "Public" or "Private"
   - Click "Create repository"

2. **Place Initial Files**
   - Create `timeline.json` file in repository
   - Can be empty file
   - Or reference sample data from [nativetimeline repository](https://github.com/hortense667/nativetimeline)

#### Step 2: Obtain Personal Access Token

1. **Access GitHub Settings**
   - Click profile image in top right of GitHub
   - Select "Settings"
   - Click "Developer settings" in left sidebar
   - Select "Personal access tokens" → "Tokens (classic)"

2. **Generate New Token**
   - Click "Generate new token" → "Generate new token (classic)"
   - Note: `Native Map Timeline Access` (any name)
   - Expiration: Select appropriate period (recommended: 90 days)
   - Scopes: Check following permissions
     - `repo` (Full control of private repositories)
     - `public_repo` (Access public repositories)

3. **Save Token**
   - Click "Generate token"
   - Copy generated token and save in safe place
   - **Important**: This token will not be displayed again

#### Step 3: NativeTimeline Settings

1. **Open Settings**
   - Click "Settings" button in NativeTimeline

2. **Enter GitHub Information**
   - Personal Access Token: Token obtained in Step 2
   - Repository owner: Your GitHub username
   - Repository name: Repository name created in Step 1
   - File path: `timeline.json` (usually OK as is)

3. **Save Settings**
   - Click "Save" button
   - Settings are saved to local storage

#### Step 4: Data Preparation and Synchronization

1. **Prepare Data**
   - Load data from CSV file using "Load" function
   - Or edit existing data

2. **Initial Sync**
   - Click "Sync" button
   - With access token: Updates GitHub JSON (Message "Remote data updated")
   - Without access token: Downloads changes only as CSV (button returns to green)

3. **Continuous Operation**
   - Always reflect to GitHub with "Sync" after editing
   - Get latest data with "Sync" if others have edited
   - Take backup with "Snapshot Save" before important edits

### Recommended Operation Policy

#### Data Management Policy

1. **Regular Backup**
   - Utilize GitHub's backup function
   - Always execute "Snapshot Save" before important edits
   - Regularly reflect to GitHub with "Sync"

2. **Version Management**
   - Record commit messages on GitHub before major changes
   - Use tags and branches as needed

3. **Collaborative Editing Management**
   - Establish rules beforehand for multiple editors
   - Always get latest data with "Sync" before editing
   - Always reflect changes with "Sync" after editing
   - Take backup with "Snapshot Save" before editing

#### Publication Policy

1. **Data Quality Management**
   - Regularly check data consistency
   - Check for inappropriate content

2. **Update Frequency**
   - Aim for regular updates
   - Add important events promptly

3. **Community Collaboration**
   - Utilize Issues and Pull Requests
   - Actively incorporate user feedback

### Data Format Details

#### CSV Format (For Loading)

**Basic Format**:
