## 操作シナリオ 
MPSは、COSバケットにアップロードしたファイルに対して、ダウンロード、トランスコード、アップロードなどの読み書き操作を行う必要があるため、サービスのロールを作成し、MPSにCOSの関連する操作権限を与える必要があります。

## 操作手順
1. [MPSコンソール](https://console.cloud.tencent.com/mps)に進み、左側ナビゲーションバーの[**Cloud Monitor** > **権限承認管理**](https://console.cloud.tencent.com/mps/auth)をクリックして、**権限承認管理**ページに進みます。権限を承認していない場合は、**Cloud Access Managementに進む**をクリックして、コンソール共通の権限管理ページに移動し、権限承認操作を行う必要があります。MPS権限の承認に同意すると、サービスプリセットのロールが作成され、MPSに関連する権限が承認されます。
![](https://qcloudimg.tencent-cloud.cn/raw/7eede4a6eb36a65a4d26b49f4e7b59af.png)
>! 権限承認が完了していない場合、MPSコンソールで他の操作を行うことはできません。
2. 権限の承認後、**権限承認管理**ページに戻ると、権限承認が完了したことが表示されます。**権限承認の取消**をクリックすると、**CAM**に移動し、[サービスロール](https://intl.cloud.tencent.com/document/product/598/19388)が削除され、MPSのCOSに対する操作権限を解除することができます。
![](https://qcloudimg.tencent-cloud.cn/raw/a4972ed47afa9acc4b8e1ca3bd5035b7.png)