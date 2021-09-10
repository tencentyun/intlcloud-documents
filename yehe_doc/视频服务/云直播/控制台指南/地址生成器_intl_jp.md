ここでは、主にTencent CSSスクリーンキャプチャ、ポルノ検出データをCOSに保存し、バケット（COS Bucket）を介してCSSスクリーンキャプチャ、ポルノ検出データを保存する方法を紹介します。まずCOS Bucketを作成し、次にCOS Bucketを介してCSSを承認し、最後にCSSコンソールでCSSスクリーンキャプチャ、ポルノ検出を設定します。その後CSSスクリーンキャプチャ、ポルノ検証データを指定されたCOS Bucketに書き込むことができます（新規バージョンのコンソール機能）。

### COS Bucketの作成
1. COSコンソールにログインし、[【CSSツールボックス】](https://console.cloud.tencent.com/cos5/bucket)を選択します。
2. 【バケットの作成】をクリックし、ポップアップページに対応する情報を入力して、【OK】をクリックすれば、バケット COS Bucketが正常に作成されます。
![](https://main.qcloudimg.com/raw/422f9ca892a0a9a46cc411712fbb1c06.png)
>!
>- Bucket nameはtestで、 `-125****577`は含まれません。  
>- 以上の情報はいずれも業務の実際の必要性に応じて設定できます。
3. 業務の必要性に応じてCOS bucketのCDNアクセラレーションを有効にすることができます。作成済みのバケット名または【設定管理】をクリックし、左側の【ドメイン名と伝送管理】>【デフォルトのCDNアクセラレーションドメイン名】をクリックします。【デフォルトのCDNアクセラレーションドメイン名】設定項目の【編集】をクリックし、現在のステータスを有効に設定した後、下部のオプションを設定します。具体的な設定方法については、[デフォルトのCDNアクセラレーションドメイン名の有効化](https://intl.cloud.tencent.com/document/product/436/31505)をご参照ください。設定完了後、【保存】をクリックすれば、CDNアクセラレーションが有効になります。
![](https://main.qcloudimg.com/raw/96538f69d6de9e987f206aa8b26bfa5d.png)

 

### CSSスクリーンキャプチャStorageを承認

1. Tencent Cloudスクリーンキャプチャ保存のデータ書き込み権限を有効にします。承認するルートアカウントID：`-125****577`。
   1. バケットの【[バケットリスト](https://console.cloud.tencent.com/cos5/bucket)】で承認するバケットを選択し、右側の【設定管理】をクリックしてバケットリスト設定管理インターフェースに入ります。【権限管理】>【[バケットアクセス許可](https://console.cloud.tencent.com/cos5/bucket/setting?type=aclconfig&anchorType=accessPermission&bucketName=text-1258968577&projectId=&path=%252F&region=ap-guangzhou)】を選択してユーザーを追加し、ユーザータイプでルートアカウントを選択して、<b>ルートアカウント ID：`-125****577`</b>を入力します。【保存】をクリックします。
![](https://main.qcloudimg.com/raw/76b93786e2d54c9166fcf0ed63b12d97.png)
![](https://main.qcloudimg.com/raw/b00fcba492552d1a7105132d1f69e714.png)
または【承認管理】をクリックして承認管理インターフェースに入り、承認が必要なバケットにチェックを入れ、【パブリック権限】と【ユーザー権限】ボタンを開いてユーザーを追加します。ユーザータイプでルートアカウントを選択し、<b>ルートアカウント ID：`-125****577`</b>を入力します。【保存】ならびに【OK】をクリックします。
![](https://main.qcloudimg.com/raw/b00fcba492552d1a7105132d1f69e714.png)
![](https://main.qcloudimg.com/raw/75667a8ec647a60700ce6ff5557c0f46.png)
>! <b>認証を実行するために、アカウントIDにはルートアカウント（メインアカウントとも言います） ID：`125****577` を入力する必要があります。（ルートアカウントID：`125****577` はCSSサービスAPPIDなので、 `125****577` を直接入力してください）</b>。

   2. バケットアクセス許可の設定APIについては [PUT Bucket aclドキュメント](https://intl.cloud.tencent.com/document/product/436/7737)をご参照ください。
2. 承認済みのCOS Bucket情報を取得します。
   1. バケットの【[概要](https://console.cloud.tencent.com/cos5/bucket/setting?type=bucketoverview&bucketName=text-1258968577&projectId=&path=%252F&region=ap-guangzhou)】でCOSのすべての情報を確認できます。アクセスドメイン名（オリジンサーバードメイン名）はbucket name、cos appid、bucket regionを含みます。
![](https://main.qcloudimg.com/raw/d533e4b8c386454085d1e8604503d892.png)
    - bucket name: `test`
    - cos appid: `125****577`
    - bucket region: `ap-nanjing`

   2. 上記3つのフィールド情報を送信すると、システムはCSSスクリーンキャプチャデータを承認されたCOS Bucketに保存します。
