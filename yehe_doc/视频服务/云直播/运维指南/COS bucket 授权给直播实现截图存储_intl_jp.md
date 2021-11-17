ここでは、主にTencent CSSスクリーンキャプチャ、ポルノ検出データをCOSに保存し、バケット（COS Bucket）を介してCSSスクリーンキャプチャ、ポルノ検出データを保存する方法を紹介します。まずCOS Bucketを作成し、次にCOS Bucketを介してCSSを承認し、最後にCSSコンソールでCSSスクリーンキャプチャ、ポルノ検出を設定します。その後CSSスクリーンキャプチャ、ポルノ検証データを指定されたCOS Bucketに書き込むことができます（新規バージョンのコンソール機能）。

### COS Bucketの作成
1. COSコンソールにログインし、[**バケットリスト**](https://console.cloud.tencent.com/cos5/bucket)を選択します。
2. **バケットの作成**をクリックし、ポップアップされたページに基本情報とアクセス許可の設定を入力し、**次へ**をクリックします。
![](https://qcloudimg.tencent-cloud.cn/raw/a447693216193809de86e422149f5a25.png)
3.必要に応じて高度なオプション設定を選択し、完了後に**次へ**をクリックします。
![](https://qcloudimg.tencent-cloud.cn/raw/29fe705f2b98c29bc7ae913e39fc99d0.png)
4. 設定情報を確認し、**作成**をクリックすれば、COS Bucketの作成が完了します。
![](https://qcloudimg.tencent-cloud.cn/raw/fb2c3a34e7502234600b93cfff7900b6.png)

>!
>- Bucket nameはtestで、 `-130****592`は含まれません。  
>- 以上の情報はいずれも業務の実際の必要性に応じて設定できます。

5. 業務の必要性に応じてCOS bucketのCDNアクセラレーションを有効にすることができます。作成済みのバケット名または**設定管理**をクリックし、左側の**ドメイン名と伝送管理**>**デフォルトのCDNアクセラレーションドメイン名**をクリックします。**デフォルトのCDNアクセラレーションドメイン名**設定項目の**編集**をクリックし、現在のステータスを有効に設定した後、下部のオプションを設定します。具体的な設定方法については、[デフォルトのCDNアクセラレーションドメイン名の有効化](https://intl.cloud.tencent.com/document/product/436/31505)をご参照ください。設定完了後、**保存**をクリックすれば、CDNアクセラレーションが有効になります。
![](https://qcloudimg.tencent-cloud.cn/raw/dc7a8ff49c0832d2322d03a0714d2f76.png)


### CSSのスクリーンキャプチャ保存を承認

1. Tencent Cloudスクリーンキャプチャ保存のデータ書き込み権限を有効にします。承認するルートアカウントID：`3508645126`。
   1. バケットの**[バケットリスト](https://console.cloud.tencent.com/cos5/bucket)**で承認するバケットを選択し、右側の**設定管理**をクリックしてバケットリスト設定管理インターフェースに入ります。**権限管理**>**[バケットアクセス許可](https://console.cloud.tencent.com/cos5/bucket/setting?type=aclconfig&anchorType=accessPermission&bucketName=text-1258968577&projectId=&path=%252F&region=ap-guangzhou)**を選択してユーザーを追加し、ユーザータイプでルートアカウントを選択して、**ルートアカウントID：`3508645126`</b>**を入力します。**保存**をクリックします。
![](https://qcloudimg.tencent-cloud.cn/raw/f31e4a9251f1c959954b958b284bfb44.png)
![](https://qcloudimg.tencent-cloud.cn/raw/8c8b4331c37cfb3f07169eb8726017df.png)
または**承認管理**をクリックして承認管理インターフェースに入り、承認が必要なバケットにチェックを入れ、**パブリック権限**と**ユーザー権限**ボタンを開いてユーザーを追加します。ユーザータイプでルートアカウントを選択し、**ルートアカウントID：`3508645126`**を入力します。**保存**ならびに**OK**をクリックします。
![](https://qcloudimg.tencent-cloud.cn/raw/3af1130fae59890e7658d4681aadf844.png)
![](https://qcloudimg.tencent-cloud.cn/raw/0025f6d26a3cf83f7e213c32e7f7eddf.png)
>! **認証を実行するために、アカウントIDにはルートアカウント（メインアカウントとも言います） ID：`3508645126`を入力する必要があります。（ルートアカウントID：`3508645126`はCSSサービスAPPIDですので、`3508645126`を直接入力してください）**。

   2. バケットアクセス許可の設定APIについては [PUT Bucket aclドキュメント](https://intl.cloud.tencent.com/document/product/436/7737)をご参照ください。
2. 承認済みのCOS Bucket情報を取得します。
   1. バケットの**[概要](https://console.cloud.tencent.com/cos5/bucket/setting?type=bucketoverview&bucketName=text-1258968577&projectId=&path=%252F&region=ap-guangzhou)**でCOSのすべての情報を確認できます。アクセスドメイン名（オリジンサーバードメイン名）はbucket name、cos appid、bucket regionを含みます。
![](https://qcloudimg.tencent-cloud.cn/raw/2b1fa50e6551966b3a7fe946f59d6260.png)
    - bucket name: `test`
    - cos appid: `130****592`
    - bucket region: `eu-moscow`
   2. 上記3つのフィールド情報を送信すると、システムはCSSスクリーンキャプチャデータを承認されたCOS Bucketに保存します。
