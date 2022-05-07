## 概要
ここでは、Windowsシステムのローカルコンピュータでのリモートデスクトップを介したWindowsインスタンスへのログイン方法について説明します。

## サポートされるシステム

Windows

## 前提条件[](id:Preconditions)

- Windowsインスタンスにリモートログインするには、インスタンスの管理者アカウント番号と対応するパスワードを獲得する必要があります。
 - システムのデフォルトパスワードを使用してインスタンスにログインする場合は、[サイト内メール](https://console.cloud.tencent.com/message)にアクセスしてパスワードを取得してください。
 - パスワードを忘れた場合は、[インスタンスのパスワードをリセット](https://intl.cloud.tencent.com/document/product/213/16566)してください。
- CVMインスタンスはパブリックネットワークIPを購入済みであり、このインスタンスはCVMインスタンスの3389ポート（クイック設定で購入したCVMインスタンスの場合、デフォルトでアクティブになっています）をアクティブしました。

## 操作手順


<dx-alert infotype="explain" title="">
以下、Windows7OSを例に取って、操作手順を説明します。
</dx-alert>

1. 下図に示すように、ローカルのWindowsコンピュータで、<img src="https://main.qcloudimg.com/raw/370daffec54024ee262d1e5dbcd4bde2.png" style="margin: -5px 0px;width: 35px;">をクリックし、**プログラムとファイルの検索**に**mstsc**と入力し、**Enter**を押して、リモートデスクトップ接続ダイアログボックスを開きます。
![](https://main.qcloudimg.com/raw/d8a4b0f70f876f6c0edc6e995a02c37d.png)
2. 「コンピュータ」の後にWindowsサーバーのパブリックIPを入力し、**接続**をクリックします。 [パブリックIPアドレスの取得](https://intl.cloud.tencent.com/document/product/213/17940)を参考にサーバーのパブリックIPを取得できます。
3. 下図に示すように、ポップアップした 「Windowsセキュリティ」ウィンドウに、インスタンスの管理者アカウントとパスワードを入力します。
<dx-alert infotype="explain" title="">
 - 「このリモート接続を信頼しますか。」 というダイアログボックスがポップアップした場合は、「今後、このコンピュータに接続するかどうかの質問を表示しない」にチェックを入れ、**接続**をクリックします。
 - Windows CVMインスタンスのデフォルトの管理者アカウントは`Administrator`で、パスワードは[前提条件](#Preconditions)を参考に取得できます。
</dx-alert>
<img src="https://main.qcloudimg.com/raw/5d3d89e3ec4616a367b80ba377a3f541.png"/>
4. **確定**をクリックすると、Windowsインスタンスにログインできます。

