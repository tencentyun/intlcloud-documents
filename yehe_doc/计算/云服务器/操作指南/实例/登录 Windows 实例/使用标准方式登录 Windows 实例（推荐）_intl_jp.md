## 概要
ここでは、標準ログイン方式(WebRDP)を使用してWindowsインスタンスにログインする方法についてご説明します。 

<dx-alert infotype="explain" title="">
この方式はローカルマシンのOSを区別せず、コンソールからWindowsインスタンスへの直接ログインをサポートしています。
</dx-alert>



## 前提条件[](id:Prerequisites)
- Windowsインスタンスにリモートログインするには、インスタンスの管理者アカウントとパスワードを取得する必要があります。
 - ログインパスワードを設定済みの場合は、そのパスワードを使用してログインしてください。パスワードを忘れた場合は、[インスタンスのパスワードのリセット方法](https://intl.cloud.tencent.com/document/product/213/16566)してください。
 - インスタンス作成時に、システムによるパスワードのランダム発行を選択した場合は、[サイト内メール](https://console.cloud.tencent.com/message)にアクセスして初期パスワードを取得してください。
- CVMインスタンスはパブリックIPがすでに購入され、インスタンスに関連付けられたセキュリティグループの中で、送信元がWebShellのプロキシIPとなるリモートログインポート（デフォルトは3389）を開放しています。
 - クイック設定で CVMインスタンスを購入した場合、ポートはデフォルトで開かれます。
 - カスタム設定経由でCVMインスタンスを購入した場合は、[セキュリティグループの応用例](https://intl.cloud.tencent.com/document/product/213/32369)を参照して、ポートを手動で開くことができます。
- インスタンスのパブリックネットワーク帯域幅が 5Mbit/s 以上であることを確認してください。そうでない場合、リモートデスクトップの応答が遅くなる可能性があります。ネットワーク帯域幅の調整が必要な場合は、[ネットワーク構成の変更](https://intl.cloud.tencent.com/document/product/213/15517)をご参照ください。


## 操作手順

1. [CVMコンソール](https://console.cloud.tencent.com/cvm/index)にログインします。
2. インスタンスの管理画面で、実際に使用されているビューモードに従って操作します。
<dx-tabs>
::: リストビュー
下図のように、ログインする Windows CVMインスタンスを選択し、右側にあるログインをクリックします。
![](https://qcloudimg.tencent-cloud.cn/raw/bad0e4e6670096461c7e9498d5d47654.png)

:::
::: タブビュー
下図のように、ログインするWindows CVM インスタンスのタブを選択し、ログインをクリックします。
![](https://qcloudimg.tencent-cloud.cn/raw/2cdbf7a52ed228109fd1bc55a6ed1d6c.png)

:::
</dx-tabs>
3. 開いた「標準ログイン | Windowsインスタンス」ウィンドウに、実際の状況に応じてログイン情報を入力します。
 - **ポート**：デフォルトは3389です。必要に応じて入力してください。
 - **ユーザー名**：Windowsインスタンスのデフォルトのユーザー名は`Administrator`です。必要に応じて入力してください。
 - **パスワード**：[前提条件](#Prerequisites)のステップで取得したログインパスワードを入力します。
5. **ログイン**をクリックすると、Windowsインスタンスにログインできます。
ここでは、OSがWindows Server 2016 Data center Edition 64ビット英語版であるCVMを例とします。ログインに成功すると以下のような画面が表示されます。
![](https://main.qcloudimg.com/raw/60abc6a9f51ae33ea95aa11edc53e009.jpg)


## 関連ドキュメント
- [インスタンスのパスワードのリセット方法](https://intl.cloud.tencent.com/document/product/213/16566)
- [ネットワーク設定の調整](https://intl.cloud.tencent.com/document/product/213/15517)
