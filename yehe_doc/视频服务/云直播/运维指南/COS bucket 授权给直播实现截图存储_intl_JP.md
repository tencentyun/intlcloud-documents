ここでは、主にTencent CSSスクリーンキャプチャ、ポルノ検出データをCOSに保存し、バケット（COS Bucket）を介してCSSスクリーンキャプチャ、ポルノ検出データを保存する方法を紹介します。まずCOS Bucketを作成し、次にCOS Bucketを介してCSSを承認し、最後にCSSコンソールでCSSスクリーンキャプチャ、ポルノ検出を設定します。その後CSSスクリーンキャプチャ、ポルノ検証データを指定されたCOS Bucketに書き込むことができます（新規バージョンのコンソール機能）。
### COS Bucketの作成
1. COSコンソールにログインし、[【バケットリスト】](https://console.cloud.tencent.com/cos5/bucket)を選択します。
2. 【バケットの作成】をクリックし、ポップアップページに対応する情報を入力して、【OK】をクリックすれば、バケット COS Bucketが正常に作成されます。
![](https://main.qcloudimg.com/raw/423beefad19658e0cec8cdd28d6d25e1.png)
>!
> - Bucket nameはbuckettest123で、-1259222427は含まれません。  
> - 以上の情報はいずれも業務の実際の必要性に応じて設定できます。
3. 業務の必要性に応じてCOS bucketのCDNアクセラレーションを有効にすることができます。作成済みのバケット名または【設定管理】をクリックし、左側の【ドメイン名と伝送管理】>【デフォルトのCDNアクセラレーションドメイン名】をクリックします。【デフォルトのCDNアクセラレーションドメイン名】設定項目の【編集】をクリックし、現在のステータスを有効に設定した後、下部のオプションを設定します。具体的な設定方法については、[デフォルトのCDNアクセラレーションドメイン名の有効化](https://intl.cloud.tencent.com/document/product/436/31505)をご参照ください。設定完了後、【保存】をクリックすれば、CDNアクセラレーションが有効になります。
![](https://main.qcloudimg.com/raw/097144cf7c6d1df5923d406b0301f93e.png)

 

### CSSスクリーンキャプチャStorageを承認
1. Tencent Cloudスクリーンキャプチャ保存のデータ書き込み権限を有効にします。承認するルートアカウントID：3508645126。
	1. バケットの【[バケットリスト](https://console.cloud.tencent.com/cos5/bucket)】>【権限管理】>【バケットアクセス許可】にユーザーを追加し、ユーザータイプのルートアカウントを選択して、**ルートアカウントID：3508645126**を入力します。
	>! **認証を実行するために、アカウントIDにはルートアカウント（メインアカウントとも言います） ID：3508645126を入力する必要があります。（ルートアカウントID：3508645126はCSSサービスですので、3508645126を直接入力してください）**。
	![](https://main.qcloudimg.com/raw/37362cc7a0b945e79899e24f84f33dab.png)
	
	2. バケットアクセス許可の設定APIについては [PUT Bucket aclドキュメント](https://intl.cloud.tencent.com/document/product/436/7737)をご参照ください。
2. 承認済みのCOS Bucket情報を取得します。
	1. バケットの【基本設定】>【基本情報】でCOSの全情報を表示できます。アクセスドメイン名（オリジンサーバードメイン名）には bucket name、cos appid および bucket regionが含まれます。
	![](https://main.qcloudimg.com/raw/b84d288cf37b40ed548ca4a25863742a.png)
	 - bucket name: buckettest123
	 - cos appid: 1259200900
	 - bucket region: ap-chengdu
	2. 上記3つのフィールド情報を送信すると、システムCSSスクリーンキャプチャデータを承認されたCOS Bucketに保存します。
