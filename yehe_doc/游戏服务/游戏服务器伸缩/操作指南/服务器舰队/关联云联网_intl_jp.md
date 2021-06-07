
## 操作シナリオ

このドキュメントでは、主にCloud Connect Networkを複数のプライベートネットワーク相互接続サービスに関連付け、各リージョンのクラウド上、クラウド下の複数の相互接続を実現する方法について説明しています。

## 操作手順

### サーバーフリート作成時のCloud Connect Networkの関連付け

1. [GSEコンソール](https://console.cloud.tencent.com/gse/asset)にログインし、左側メニューの【サーバーフリート】をクリックして、フリートリストの画面に入ります。
2. 【新規作成】をクリックし、サーバーフリートを作成します。
<img src="https://main.qcloudimg.com/raw/594df872d7941bfcedbc278997a948f2.png" style="width: 95%;"/>
3. サーバーフリート新規作成画面で、Cloud Connect Networkの関連付けにチェックを入れます。
<img src="https://main.qcloudimg.com/raw/6c9766a2666326922d832889f5cadd18.png" style="width: 75%;"/>
4.アカウントIDおよびCloud Connect Network IDを入力し、関連付け操作を行います。<br>
<img src="https://main.qcloudimg.com/raw/919fcf3bfa194d02ab6f177bb40c74d0.png" style="width: 75%;"/>

>?
> 1. サーバーフリート作成過程でCloud Connect Networkを関連付けるには、20分以内に申請に同意してください。そうでなければ作成は失敗します。
> 2. Cloud Connect Networkへのインスタンス追加で発生するネットワーク相互接続料金は、Cloud Connect Networkが所在するアカウントが負担します。  
> 3. このCloud Connect Network内のインスタンスの所属リージョンは、現時点では異なるリージョン間の相互接続サービスをサポートしていません。必要な場合はサービス担当者に連絡してください。 
>




### サーバーフリート作成完了後のCloud Connect Networkの関連付け

1. [GSEコンソール](https://console.cloud.tencent.com/gse/asset)にログインし、左側メニューの【サーバーフリート】をクリックして、フリートリストの画面に入ります。
2. [サーバーフリートの作成](https://intl.cloud.tencent.com/document/product/1055/36675)を完了します。
3. 【ID】をクリックして、Cloud Connect Networkの関連付けが必要なフリート詳細画面に入ります。
![](https://main.qcloudimg.com/raw/634314877af8cbf321bbb1f7bd65bd73.png)
4. サーバーフリート詳細画面で、右側の【今すぐ関連付ける】をクリックすれば、関連付け操作を実行できます。
![](https://main.qcloudimg.com/raw/636460d9d57e6a043a175197c46226b1.png)
5. アカウントIDおよびCloud Connect Network IDを入力し、関連付け操作を行います。
<img src="https://main.qcloudimg.com/raw/a4a77b4aff6b433fd7375da4c0e67697.png" style="width: 70%;"/>

> ? 
> 1. サーバーフリート作成完成後のCloud Connect Networkは、相手方が7日の内に申請に同意することが必要です。7日後の申請は期限切れになります。  
> 2. Cloud Connect Networkへのインスタンス追加で発生するネットワーク相互接続料金は、Cloud Connect Networkが所在するアカウントが負担します。  
> 3. このCloud Connect Network内のインスタンスの所属リージョンは、現時点では異なるリージョン間の相互接続サービスをサポートしていません。必要な場合はサービス担当者に連絡してください。  
