## 概要

CloudBerry Explorer はCloud Object Storage（COS）を管理するために使用されるクライアントツールです。 CloudBerry ExplorerによってCOSをWindowsなどのOSにマウントすることができ、ユーザーのCOSファイルへのアクセス、移動および管理を容易にします。


## サポートしているシステム

Windows、macOSシステムをサポートしています。

## ダウンロードアドレス

[CloudBerry 公式ダウンロード](https://www.cloudberrylab.com/download-thanks.aspx?prod=cbes3free&src=ms)に進みます。

## インストールと設定

>! 以下の設定手順はCloudBerry Explorer Windows v6.3バージョンを例としています。その他のバージョンでは設定手順に若干の違いがあるため、適宜調整してください。
>

1. インストールパッケージをダブルクリックし、表示に従ってインストールを完了させます。
2. ツールを開き、S3 Compatibleを選択してダブルクリックします。
3. ポップアップウィンドウ内で以下の情報を設定し、Test Connectionをクリックして、接続に成功したことが表示されれば完了です。
![](https://qcloudimg.tencent-cloud.cn/raw/c7c351ac3c8fbabcf635ae7699fb3dba.png)
設定項目の説明は次のとおりです。
 - Display name：カスタムユーザー名を入力します。
 - Service point：形式が`cos.<Region>.myqcloud.com`で、例えば成都リージョンのバケットにアクセスする場合は、`cos.ap-chengdu.myqcloud.com`と入力します。適用するリージョンの略称（region）については、[リージョンとアクセスドメイン名](https://intl.cloud.tencent.com/document/product/436/6224)をご参照ください。
 - Access key：アクセスキー情報SecretIdを入力し、[Tencent Cloud APIキー](https://console.cloud.tencent.com/capi) に進んで作成と取得を行うことができます。
 - Secret key：アクセスキー情報Secretkeyを入力し、 [Tencent Cloud APIキー](https://console.cloud.tencent.com/capi) に進んで作成と取得を行うことができます。
4. アカウント情報の追加が完了したら、Source内で以前設定したユーザー名を選択すると、そのユーザー名の下のバケットリストを確認することができ、これは設定が完了したことを意味します。
![](https://qcloudimg.tencent-cloud.cn/raw/5b001159dea9eada859a06014d1cbdfd.png)

## COSファイルの管理

### バケットリストの照会

Source内で以前設定したユーザー名を選択すると、そのユーザー名下のバケットリストを確認することができます。

>! Service pointに設定されたリージョンに対応するバケットのみ確認できます。その他のリージョンのバケットを確認したい場合は、**File > Edit Accounts**をクリックして、ユーザー名を選択し、Service pointパラメータをその他のリージョンに修正すれば完了です。
>

### バケットの作成

画像内のアイコンをクリックし、ポップアップウィンドウ内に完全なバケット名を入力します。例えばexamplebucket-1250000000です。入力情報に誤りがなければ、**OK**をクリックすると作成が完了します。
バケットの命名ルールについては、 [バケット命名ルール](https://intl.cloud.tencent.com/document/product/436/13312)をご参照ください。
![](https://qcloudimg.tencent-cloud.cn/raw/9192916f402017e27f8b233ac2c72c9e.png)

### バケットの削除

バケットリスト内で削除する必要があるバケットを選択し、 **Delete**を右クリックすると削除することができます。


### オブジェクトのアップロード

バケットリスト内でオブジェクトのアップロードを行う必要があるバケットまたはパスを選択し、その後ローカルコンピュータでアップロードする必要があるオブジェクトを選択し，其それを左側のウィンドウ内にドラッグすれば、アップロード操作が完了します。
![](https://qcloudimg.tencent-cloud.cn/raw/92aea7e39697ab46bb29f430bc58206a.png)

### オブジェクトのダウンロード

左側のウィンドウ内でダウンロードする必要があるオブジェクトを選択し、次にオブジェクトを右側のローカルコンピュータのフォルダ内にドラッグすれば、ダウンロード操作が完了します。
![](https://qcloudimg.tencent-cloud.cn/raw/1ed1432256fd44ac2f9739f6fda263b1.png)

### オブジェクトのコピー

ツールの右側のウィンドウで、オブジェクトがコピーされた後のターゲットパスを選択し、その後左側のウィンドウ内でコピーする必要があるオブジェクトを選択し、**Copy**を右クリックし、ポップアップウィンドウの情報を確認すると、オブジェクトのコピー操作が完了します。
![](https://qcloudimg.tencent-cloud.cn/raw/5d1801cd20fe1885ee6e16ddec1139c5.png)

### オブジェクトのリネーム

バケット内でリネームが必要なオブジェクトを探し、 **Rename**を右クリックして、新しい名称を入力すれば完了です。


### オブジェクトの削除

バケット内で削除が必要なオブジェクトを選択し、 **Delete**を右クリックすれば、オブジェクトの削除が完了します。

### オブジェクトの移動

ツールの右側のウィンドウで，オブジェクトが移動された後のターゲットパスを選択し、その後左側のウィンドウ内で移動する必要があるオブジェクトを選択し、**Move**を右クリックし、ポップアップウィンドウの情報を確認すれば、オブジェクトの移動操作が完了します。
![](https://qcloudimg.tencent-cloud.cn/raw/5b4f20a2f400bf24f70dde5b93ed8053.png)


### その他の機能

以上の機能以外に、CloudBerry Explorerはさらに他の機能をサポートしています。例えばオブジェクトのACLの設定、オブジェクトのメタデータの確認、Headersのカスタマイズ、オブジェクトのURLの取得などです。ユーザーは実際のニーズに応じて操作を行うことができます。


