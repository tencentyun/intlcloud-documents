COSCLIツールは、Windows、Mac、LinuxのOSに対応したバイナリーパッケージを提供します。簡単なインストールと設定を行えば、すぐに使用することができます。

## ダウンロードアドレス

| Githubアドレス                                                  | 国内サイト                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [Windows](https://github.com/tencentyun/coscli/releases/download/v0.12.0-beta/coscli-windows.exe) | [Windows](https://cosbrowser.cloud.tencent.com/software/coscli/coscli-windows.exe) |
| [Mac](https://github.com/tencentyun/coscli/releases/download/v0.12.0-beta/coscli-mac) | [Mac](https://cosbrowser.cloud.tencent.com/software/coscli/coscli-mac) |
| [Linux](https://github.com/tencentyun/coscli/releases/download/v0.12.0-beta/coscli-linux) | [Linux](https://cosbrowser.cloud.tencent.com/software/coscli/coscli-linux) |

>?現在のバージョン番号はv0.12.0-betaです。ツールの最新バージョン、過去のバージョンおよび更新ログを取得したい場合は、[release](https://github.com/tencentyun/coscli/releases)でご確認ください。

## インストール

### Windows

1. [Windows版のCOSCLIをダウンロード](https://github.com/tencentyun/coscli/releases/download/v0.12.0-beta/coscli-windows.exe)します。
2. ダウンロードしたCOSCLI実行可能ファイルを`C:\Users\<ユーザー名>`ディレクトリに移動します。
3. `coscli-windows.exe`を`coscli.exe`にリネームします。
4. `win+r`キーを押して、`実行`プログラムを開きます。
5. ダイアログボックスで、`cmd`と入力し、`Enter`を押してコマンドラインウィンドウを開きます。
6. コマンドラインウィンドウに`coscli --version`と入力します。次の情報がダンプされれば、インストールは成功です。
>? `Windows`システムでは、コマンドラインクライアントによってCOSCLIの使い方も若干異なる場合があります。`coscli [command]`を入力してもCOSCLIが正しく動作しない場合は、`./coscli [command]`の形式をお試しください。
>
```
coscli version v0.12.0-beta
```

### Mac

1. 以下のコマンドを実行し、COSCLIをダウンロードします。
```bash
wget https://github.com/tencentyun/coscli/releases/download/v0.12.0-beta/coscli-mac
```
2. 以下のコマンドを実行して、ファイルをリネームします。
```bash
mv coscli-mac coscli
```
3. 以下のコマンドを実行して、ファイルの実行権限を変更します。
```bash
chmod 755 coscli
```
4. コマンドラインに`./coscli --version`と入力します。次の情報がダンプされれば、インストールは成功です。
```
coscli version v0.12.0-beta
```
>? MacシステムでCOSCLIを使用しているときに、`開発者を検証できないため、「coscli」を開けません`というメッセージが出た場合、`設定>セキュリティとプライバシー>一般`に移動して、`coscliを開く`を選択すると、COSCLIが正常に使用できるようになります。


### Linux

1. [LinuxバージョンのCOSCLIのダウンロード](https://github.com/tencentyun/coscli/releases/download/v0.12.0-beta/coscli-linux)をクリックするか、以下のコマンドを実行して、COSCLIをダウンロードします。
```bash
wget https://github.com/tencentyun/coscli/releases/download/v0.12.0-beta/coscli-linux
```
2. 以下のコマンドを実行して、ファイルをリネームします。
```bash
mv coscli-linux coscli
```
3. 以下のコマンドを実行して、ファイルの実行権限を変更します。
```bash
chmod 755 coscli
```
4. コマンドラインウィンドウに`./coscli --version`と入力します。次の情報がダンプされれば、インストールは成功です。
```
coscli version v0.12.0-beta
```


## パラメータの設定

>!
>- ユーザーには[一時キーを使用](https://intl.cloud.tencent.com/document/product/436/14048)してSDKを呼び出し、一時権限承認方式によってSDK使用の安全性をさらに向上させることをお勧めします。一時キーを申請する際は、[最小権限の原則についてのガイド](https://intl.cloud.tencent.com/document/product/436/32972)に従い、ターゲットバケットまたはオブジェクト以外のリソースが漏洩しないようにしてください。
>- どうしてもパーマネントキーを使用したい場合は、[最小権限の原則についてのガイド](https://intl.cloud.tencent.com/document/product/436/32972)に従って、パーマネントキーの権限範囲を限定することをお勧めします。



`./coscli --help`コマンドを使用して、COSCLIの使用方法をすばやく確認することができます。

初めて使用する場合、COSCLIはデフォルトで`~/.cos.yaml`に設定ファイルを作成しますが、その後で`./coscli config init`コマンドを使用して、COSCLI用の設定ファイルを他の場所にインタラクティブに作成することもできます。

設定ファイルの各設定項目の説明は次のとおりです。

<span id="alias"></span>

| 設定項目        | 説明                                                         |
| ------------- | ------------------------------------------------------------ |
| Secret ID     | キーID。[CAMコンソール](https://console.cloud.tencent.com/cam/capi)から作成および取得できます。 |
| Secret Key     | キーKey。[CAMコンソール](https://console.cloud.tencent.com/cam/capi)から作成および取得できます。 |
| Session Token | 一時キーtoken。一時キーを使用する場合に設定する必要があります。使用しない場合は、`Enter`を押してスキップできます。 |
| APP ID        | APP IDは、Tencent Cloudのアカウント申請が成功した後に取得するアカウント番号で、システムによって自動的に割り当てられ、[アカウント情報](https://console.cloud.tencent.com/developer)から取得することができます。1つのバケットの正式名称は、`Bucket Name`と`APP ID`という2つの要素から構成され、`<BucketName-APPID>`という形式になります。詳細については、[バケット命名ルール](https://intl.cloud.tencent.com/document/product/436/13312)をご参照ください。 |
| Bucket Name   | バケット名です。APP IDとともにバケットの正式名称を構成し、`<BucketName-APPID>`という形式になります。詳細については、[バケット命名ルール](https://intl.cloud.tencent.com/document/product/436/13312)をご参照ください。 |
| Bucket Endpoint | `cos.<region>.myqcloud.com`という形式になります。このうち、regionはバケットの所在リージョンです。詳細については、[リージョンとアクセスドメイン名](https://intl.cloud.tencent.com/document/product/436/6224)をご参照ください。 |
| Bucket Alias  | バケットエイリアスです。設定後、`BucketName-APPID`の代わりに` BucketAlias`を使用すれば、入力が必要なコマンドの長さを短縮できます。この項目が設定されていない場合、`BucketAlias`の値は`BucketName-APPID`の値となります。 |

### その他の設定方法

`./coscli config init`を使用してインタラクティブに設定ファイルを作成する以外にも、COSCLIの設定ファイルを直接手動で編集することもできます。COSCLIの設定ファイルの形式は`yaml`となります。設定ファイルの例を次に示します。

```yaml
cos:
  base:
    secretid: XXXXXXXXXXXXXXX
    secretkey: XXXXXXXXXXXXXXXXX
    sessiontoken: ""
  buckets:
  - name: examplebucket1-1250000000
    alias: bucket1
    region: ap-shanghai
  - name: examplebucket2-1250000000
    alias: bucket2
    region: ap-guangzhou
  - name: examplebucket3-1250000000
    alias: bucket3
    region: ap-chengdu
```

>! COSCLIは、デフォルトで~/.cos.yamlから設定項目を読み込みます。ユーザーがカスタムの設定ファイルを使用する場合は、コマンドの後に-c(--config-path)オプションを使用してください。設定ファイルに保存されているsecretid/secretkey/sessiontokenはすべて暗号化後の文字列となっています。



### 複数バケットの設定

COSCLIは複数のバケットをサポートしていますが、初期設定時には1つのバケット情報のみを設定するよう要求します。その後、`./coscli config add`コマンドを使用すれば、バケット設定を追加することができます。

>? 設定ファイルのその他の操作については、[configコマンド](https://intl.cloud.tencent.com/document/product/436/43251)をご参照ください。
