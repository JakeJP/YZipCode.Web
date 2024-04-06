# 陽気に郵便番号検索 [Web]

## 陽気に郵便番号検索とは

**陽気に郵便番号検索** は C# .NET で作られた、日本郵便の全国郵便番号データをを元に、
データの整形とデータのXMLファイルへの変換・保存、検索機能のライブラリ、
HTMLフォーム上での住所入力アシストなどをセットした開発プロジェクトのパッケージです。

- [陽気に郵便番号検索 [SDK]](https://github.com/JakeJP/YZipCode.SDK)
  一連のソースコードと開発環境を公開しています。

- [陽気に郵便番号検索 [WebAPI]](https://github.com/JakeJP/YZipCode.Web) **※本バージョン**
  既存のHTMLフォームに簡単に郵便番号検索・住所検索機能を追加するための Javascript ライブラリ。

![](images/yzipcode-web.gif)

## Web バージョン

**陽気に郵便番号検索 Web** は、ウェブデザイナーが郵便番号・住所入力をする既存のウェブフォームに簡単に入力補助機能を追加する方法を提供します。

特徴としては

- 既存の様々な郵便番号・住所入力HTMLフォームに入力補助機能を追加
- JavascriptとCSSファイルの参照と、数行の初期化処理の追加のみで実装
- 郵便番号データはクラウド上で管理（サーバー不要）
- 郵便番号データは常に最新（メンテナンスフリー）

このリポジトリにはプログラムコードは含まれていません。既存のHTMLに機能を追加する方法を以下に解説しています。

※自前で郵便番号データの管理（データ作成）とWebAPIサーバーを立ち上げたい場合はSDKを参照してください。

### WebAPI 版 ウェブフォームウィジェットの機能

- 郵便番号 → 住所 の検索・サジェスト・自動補完
- 住所 → 郵便番号 の検索・サジェスト・自動補完

## 動作サンプル

実際の[動作サンプルはこちら](https://yzipcode.yo-ki.com/index.html) を御覧ください。

## 導入方法

### 前提条件

- HTML で書かれた住所入力用のフォームが対象です。javascript と
  スタイルシート読み込みのタグ、初期化のための数行の javascript を挿入できればフレームワークは問いません。

### 1. javascript と css スタイルシートの参照をページ内に追加します。

通常は `head` タグ内に記述を追加します。

```html
<script src='https://yzipcode.yo-ki.com/js/yokinsoft.zipcode.js'></script>
<link rel="stylesheet" type="text/css" href="https://yzipcode.yo-ki.com/css/yokinsoft.zipcode.css" />
```

### 2. 導入したいウェブフォームを選定します。

この javascript ライブラリは様々な形式の住所入力フォームに対応することが可能です。
ここでは、例として次のような住所入力フォームがあるとします。(スタイルに Bootstrapの記述を使っています)

```html
<form id="sampleForm1">
    <div class="input-group mb-3">
        <div class="input-group-text">〒</div>
        <input autofocus name="zipcode" placeholder="郵便番号" autocomplete="off" autofill="false" class="form-control" />
        <input type="button" class="btn btn-success" value="住所を検索" />
    </div>
    <div>
        <div class="row">
            <label class="form-label">住所</label>
            <div class="">
                <input name="address" class="form-control" />
            </div>
        </div>
        <div class="mb-3">
            <label for="sample0-business" class="form-label">事業所名</label>
            <input name="business" class="form-control yz-address-business-name" />
        </div>
    </div>    
</form>
```

フォームの中から

- 郵便番号を入力する要素
- 住所を入力する要素
- 事業所名を入力する要素

を決めます。要素は1つだけの テキストボックス の場合や複数の テキストボックスから構成される場合もあります。

初期化プログラムの記述で、要素の指定は Javascript の querySelector が認識する書式か要素のIDそのものを使います。
この例では input 要素にIDはついていないので、form の id を使って特定する方法を取ります。
要素の指定は css でおなじみの指定方法です。idの指定は `#` から始まる文字列, input 要素をそれぞれ指定します。
郵便番号欄は `#sampleForm1 input[name=zipcode]` , 住所欄は `#sampleForm1 input[name=address]`, 事業所欄は
`#sampleForm1 input[name=business]` となります。

### 3. ウィジェットの初期化の Javascript を記述します。

検索機能を有効にするフォーム要素を指定して、`YZipCode` クラスを初期化します。

`YZipCode` クラスを初期化します。初期化の場所は、指定するフォームの後、またはフレームワークなどを使ってページ全体が初期化された後に
実行される部分に挿入します。

```html
<script>
  new YZipCode({
    zipcode: ['#sampleForm1 [name=zipcode]', '#sampleForm1 [value=住所を検索]'],
    address: '#sampleForm1 [name=address]',
    business: '#sampleForm1 [name=business]'
  });
</script>
```

この例では郵便番号部分は２つの INPUT 要素で構成されるため、配列を使います。住所部分は１つの INPUT 要素のみなので 文字列 で指定します。

以上で、郵便番号検索ウィジェットは有効になりました。
さらに詳しいオプションなど設定方法は以下の詳細を参照してください。

## 利用規約・ライセンス(暫定版)

陽気に郵便番号検索 WebAPI 版は郵便番号データとその検索システムをクラウド上にホスティングしています。
2024年現在このシステムは実験的に無償・フリーで公開しています。

### WebAPIは公開。匿名利用可能。

本サービスのWebAPIはどなたも商用、非商用かかわらず匿名で使用することができます。使用開始にはユーザー登録などは要りません。
ただし、本サービスの変更などに関するお知らせを受信するためにユーザー登録をおすすめします。

### 無保証

本サービスは実験的に運用している都合、サービスの停止、不具合、終了、仕様変更などに関していかなる保証もいたしません。

### プライバシー

本サービスの性質上サーバーへ郵便番号、ユーザーの入力した住所の一部文字列が送信されます。
本システムではセンシティブな情報である、住所の文字列がクライアントWebブラウザー上に残らないような
仕組みを取り入れています。またサーバー上ではユーザーが入力した住所の文字列は基本的に保存されません。
ただし、統計処理に必要な関連した情報が記録される場合があります。

### 将来のサービス提供方式の変更

現在このサービスは実験的に無償で公開しています。サーバー運用の負荷、コストを考慮して将来サービスの提供形式を
変更する可能性があります。本サイトからの告知に注目願います。

### 独自サーバー構築のすすめ

高可用なサービスを求める場合は、SDKを使って独自のサーバーを立てることをおすすめします。
独自のサーバー構築に関しては有償にてサポートが可能ですのでお問い合わせください。

## 様々なカスタマイズ

ここでは、基本的な設定オプションについて記述します。詳細に渡るカスタマイズについてはSDKのドキュメントを参照ください。

----

### 住所入力フォームの基本概念

基本要素

- 郵便番号 7桁の郵便番号は 123-4567 または 1234567 と表現されます。
- 住所 都道府県→市区町村→その他の地域→番地・建物名・部屋番号など の階層構造を持ちます。市区町村は、「市」＋「区」が合わさった形式の場合もあります。
- 事業所 郵便番号が個別に割り当てられている事業所名。javascript ライブラリでは省略することも可能です。

HTML上の要素

- 郵便番号： １つまたは２つのテキストボックス、検索実行用のボタン。ボタンは省略可能。
- 住所：　住所の構成要素の分割に応じて　１つ～４つの テキストボックス、検索実行用のボタン。都道府県の選択は SELECT も可能。ボタンは省略可能。

ボタンは明示的に検索を呼び出す場合に使用します。

### `YZipCode` オプション

#### HTMLフォーム構成要素の指定

- **zipcode** : string | `Array<string>`
- **address** : string | `Array<string>`
- **business** : string | `Array<string>`

#### 動作に関するオプション

- **autofill** : true | false
 郵便番号または住所文字列の入力時、住所が一意に決定する場合にフォームに自動的に文字列を挿入します。
- **autosuggest** : true | false 郵便番号または住所文字列の入力の際、複数の候補がある場合ドロップダウンリストでその候補を表示します。

いずれのオプションも `false` が指定された場合は、ボタンによる検索操作のみの動作になります。

#### その他のオプション

- **language** : 'ja' | 'en'  言語指定。デフォルトではブラウザの言語に依存します。

#### 例

```html
<script type="text/javascript">
    var helper = new YZipCode({
        zipcode: ['#sampleFormEng [name=zipcode]', '#sampleFormEng [value=住所を検索]'],
        address: ['#sampleFormEng [name=address]', '#sampleFormEng [value=郵便番号を検索]'],
        business: ['#sampleFormEng [name=business]'],
        language: 'en'
    });
</script>
```

さらに詳細な設定内容はSDKのドキュメントを参照してください。

