`./coscli --help`または`./coscli -h`コマンドによって、COSCLIがサポートする共通オプションを確認することができます。

## オプションの説明
COSCLIの共通オプションは次のとおりです。これらのオプションはツールのすべてのコマンド内で使用できます。

>!
>- ユーザーには[一時キーを使用](https://intl.cloud.tencent.com/document/product/436/14048)してSDKを呼び出し、一時権限承認方式によってSDK使用の安全性をさらに向上させることをお勧めします。一時キーを申請する際は、[最小権限の原則についてのガイド](https://intl.cloud.tencent.com/document/product/436/32972)に従い、ターゲットバケットまたはオブジェクト以外のリソースが漏洩しないようにしてください。
>- どうしてもパーマネントキーを使用したい場合は、[最小権限の原則についてのガイド](https://intl.cloud.tencent.com/document/product/436/32972)に従って、パーマネントキーの権限範囲を限定することをお勧めします。


|  オプション  | 説明 |
|  ----  | ----  |
|-h, --help|ヘルプ情報を出力します。ユーザーは-hまたは--helpコマンドによってツールのhelp情報および使用法を確認できます。ユーザーはさらに、各コマンドの後に（パラメータなしで）-hを入力することで、そのコマンドの具体的な使用法を確認することもできます。例えば、バケット作成コマンドの具体的な使用法を確認する場合は、`coscli mb -h`と入力します   |
|-c, --config-path|設定ファイルのパスです。COSCLIのデフォルトの設定ファイルパスは`~/.cos.yaml`です。ユーザーがカスタムの設定ファイルを使用することも可能です。コマンドの後に`-c`を使用すると設定ファイルを指定できます|
|-e, --endpoint   |  設定ファイルで事前にバケットのリージョンを設定するほか、COSCLIはコマンド内で`-e`によってバケットのendpointを指定することもできます。endpointは`cos.<region>.myqcloud.com`のような形式であり、このうち`<region>`は`ap-guangzhou`、`ap-beijing`などのようなバケットリージョンを表します。COSがサポートするリージョンのリストについては[リージョンとアクセスドメイン名](https://intl.cloud.tencent.com/document/product/436/6224)をご参照ください|
|-i, --sercret-id  |  COSにアクセスする際に使用するキーのSecretIdを指定します|
|-k, --sercret-key  |  COSにアクセスする際に使用するキーのSecretKeyを指定します |
|-t, --sesssion-token  |  ユーザーが一時キーを使用してCOSにアクセスする場合、`-t`によって一時キー内のtokenを指定することができます|
|-v, --version |   COSCLIのバージョンを表示します |

## 操作事例

### 事例1：バケットを切り替えてオブジェクトをアップロードする


COSCLIによって別のリージョンのバケットに切り替えたい場合、ユーザーは-eオプションによってそのバケットの所属するEndpointを指定することができます。

例えば、ローカルファイルtest.txtを成都リージョンのバケットexamplebucket-1250000000にアップロードする場合、成都が読み取るendpointは`cos.ap-chengdu.myqcloud.com`であり、コマンドは次のようになります。
```
./coscli cp test.txt cos://examplebucket-1250000000/test.txt -e cos.ap-chengdu.myqcloud.com
```

### 事例2：ユーザーアカウントを切り替えてファイルリストを確認する

ユーザーが別のアカウントのIDを使用したい場合も、-iおよび-kオプションによってユーザーキーのSecretIdとSecretKeyをそれぞれ指定することができます。

例えば、別のアカウントのIDを使用して、成都リージョンにあるバケットexamplebucket-1250000000のファイルリストをリストアップする場合、コマンドは次のようになります。

```
./coscli ls cos://examplebucket-1250000000 -e cos.ap-chengdu.myqcloud.com -i AKIDYv3vWrwkHXVDfqkNjoc9PP8anjOm**** -k 4rNbYF1XmmVw67rKWTBernUu66u****
```
