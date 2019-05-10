## 機能説明
ミニプログラム体験の流暢さを向上させるため、WeChatはコンパイル後のコードパッケージの大きさを1MB以下に制限します。1MB以上のコードパッケージをアップロードできません。実際的には、ミニプログラムを開発するとき、画像リソースは通常大きな空間を使用し、公式の1MB制限要求を超える可能性が高いです。

COSのWeCOSツールを使用し、ミニプログラムプロジェクト中の画像リソースが自動的にCOSにアップロードされ、WeCOSは自動的にコードの画像リソースアドレスの参照をオンラインアドレスに切り替え、プロジェクトディレクトリの画像リソースを除去し、コードパッケージのサイズを小さくします。

以下では、WeCOSを使用することの関連準備とインストール操作などの構成を説明します。
## 準備作業
1. [Tencent Cloud公式サイト](https://cloud.tencent.com/)に入り、Tencent Cloudアカウントを登録します。ガイドラインについては、[Tencent Cloud登録](/doc/product/378/9603)ページを参照してください。
2. [COSコンソール](https://console.cloud.tencent.com/cos4)にログインし、COSサービスを有効し、[バケット作成](/doc/product/436/6232)を行います。
3. GitHubで[WeCOSツールの取得](https://github.com/tencentyun/wecos)をクリックします。
4. [Node.js公式サイト](https://nodejs.org/)で環境をダウンロードし、インストールします。

## インストールを開始する
以下のコマンド使って、WeCOSツールをインストールします。

```js
npm install -g wecos
```

## 基本構成
ミニプログラムの同じ階層にあるディレクトリに`wecos.config.json`ファイルを作成し、ファイルの構成例は以下のとおりです。

```json
{
  "appDir": "./app",
  "cos": {
    "secret_id": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    "secret_key": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    "bucket": "wxapp-1251902136",
    "region": "ap-guangzhou", 
    "folder": "/"
  }
}
```

region：bucketを作成するときに選択した地域略称。
folder： リソースをbucketの指定のディレクトリに保存する。

### 構成項目説明

| 構成項目    | タイプ           | 説明                                       |
| ------ | ------------ | ---------------------------------------- |
| appDir | String | デフォルトは`./app`、ミニプログラムプロジェクトディレクトリ                       |
| cos    | Object | 必須入力。COSのバケット、地域などの構成情報。[バケット概要](https://cloud.tencent.com/document/product/436/13312)ドキュメントを参照してください。暗号鍵などの情報を[クラウドAPI暗号鍵コンソール](https://console.cloud.tencent.com/cos4/secret)から取得し確認してください |


## 使用開始
構成ファイルの同じ階層にあるディレクトリに以下の使用コマンドを実行します。
```
wecos
```

>!使用コマンドを実行する前、構成ファイルの同じ階層にあるディレクトリに`wecos.config.json`ファイルを作成する必要があります。

## 高度な構成

| 構成項目                 | タイプ            | 説明                                      |
| ------------------- | ------------- | --------------------------------------- |
| backupDir           | String  | デフォルトは`./wecos_backup`、バックアップディレクトリ                |
| uploadFileSuffix    | Array  |  デフォルトは`[".jpg", ".png", ".gif"]`、アップロードされる画像のサフィックス名構成  |
| uploadFileBlackList |Array |  デフォルトは`[]`、画像リソースブラックリスト    |
| replaceHost         | String  |  デフォルトは`''`、指定したドメイン名をtargetHostに切り替えます   |
| targetHost          | String | デフォルトは`''`、カスタムドメイン名を使用します    |
| compress            | Boolean |  デフォルトは`false`、圧縮画像を有効にするかどうか       |
| watch               | Boolean | デフォルトは`true`、プロジェクトディレクトリのリアルタイム監視を有効にするかどうか   |

#### バックアップディレクトリの設定
WeCOSが実行するときに自動的にプロジェクトの画像をCOSにアップロードした後に削除するため、ソースファイルが紛失するおそれがあります。ソースファイルをバックアップする機能を提供します。画像を1枚アップロードすると、プロジェクトの同じ階層にあるディレクトリにこのファイルをバックアップします。以下の構成でバックアップディレクトリ名を変更できます。この機能を使用しない場合、NULL値を設定できます。
```
  "backupDir": "./wecos_backup"
```
#### 画像サフィックスの設定
アップロード画像のフォーマット（例えば、`jpg`形式のみ）を制限する必要があれば、WeCOSによって提供される画像サフィックスの構成項目で定義できます。WeCOSはデフォルトでjpg、png、gifをサポートします。その他の形式（例えば、webp）を追加する場合、以下のようにこの構成項目に追加できます。

```
  "uploadFileSuffix": [".jpg",".png",".gif",".webp"]
```

#### 画像ブラックリストの設定
開発中には特定の画像のアップロードする必要がない場合、WeCOSのブラックリスト構成により実現できます。構成後アップロードプログラムは自動的にそれらの画像を無視します。ブラックリスト構成は、ディレクトリまたはファイル名の書き方をサポートします。

```
  "uploadFileBlackList": ["./images/logo.png","./logo/"]
```

#### カスタムドメイン名
COSファイルリンクに対して独自のドメイン名を使用したいとき、targetHostの構成によってデフォルトドメイン名を置き換えることができます（構成ときに`http://`を省略できる）。

```
  "targetHost": "http://example.com"
```

コード中の画像リンクに対してドメイン名を置き換えるとき、replaceHost targetHostの構成によって実現できます。

```
  "replaceHost": "http://wx-12345678.myqcloud.com",
  "targetHost": "https://example.com"
```

#### 画像圧縮の有効化
画像をCOSにアップロードした後、プログラムパッケージのサイズを軽減したが、画像自体のサイズが大き過ぎでアクセス遅延になると、ユーザーエクスペリエンスにも影響を与えます。
WeCOSは、画像をクラウドにアップロードする基本機能のほかに、[Tencent Cloud Cloud Infinit](https://cloud.tencent.com/product/ci)に基づく画像圧縮機能も提供します。[Cloud Infinitコンソール](https://console.cloud.tencent.com/ci)COSと同じ名前のバケットを作成した後、バケットに入り、仕様ページで画像圧縮機能を有効にした後、リソースは圧縮後にアップロードされます。

```
  "compress": true
```

#### リアルタイム監視の設定
WeCOSは、デフォルトでプロジェクトディレクトリ変化をリアルタイムに監視し、自動的に画像リソースを処理します。開発プロセスにおいて、リアルタイム監視が便利でないと感じる場合、または1回処理だけで停止したい場合、以下のコマンドラインでこの構成を変更できます。プログラムを1回実行した後に終了します。

```
  "watch": false
```

## 詳細な使い方
上記の使い方でニーズを満たすことができない場合、WeCOSはカスタムモジュールの構成操作を提供し、直接参照の方式で個性化ニーズを満足します。構成例は以下の通りです。

```
var wecos = require('wecos');

// option選択可能（String|Object）
// Stringを入力し、構成ファイルパスを指定します
// Objectを入力し、構成項目を指定します
wecos([option]);

// 構成ファイルパスを指定します
wecos('./wecos-config.js');

// 構成項目を指定します
wecos({
    appDir: './xxx',
    cos: {
        ...
    }
});
```

## 関連リソース
- [WeCOS-UGC-DEMO](https://github.com/tencentyun/wecos-ugc-upload-demo) —— ミニプログラムユーザーリソースをCOSにアップロードするDEMO
- [COS-AUTH](https://github.com/tencentyun/cos-auth) —— COS認証サーバーDEMO

