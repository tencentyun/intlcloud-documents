## Tencent Cloudアカウントの登録
メディア処理サービスを使用するには、[Tencent Cloudアカウントの登録](https://intl.cloud.tencent.com/document/product/378/17985)が必要です。

## メディア処理サービスの申請
### ステップ1：登録とログイン
Tencent Cloudの公式ウェブサイトにログインし、**クラウド製品** > **Video Service**>[**メディア処理**](https://console.cloud.tencent.com/mps)を選択して、メディア処理コンソールに進みます。

### ステップ2：権限承認管理
メディア処理は、COSバケットにアップロードしたファイルに対して、ダウンロード、トランスコード、アップロードなどの読み書き操作を行う必要があるため、サービスのロールを作成し、メディア処理にCOSの関連する操作権限を与える必要があります。
[メディア処理コンソール](https://console.cloud.tencent.com/mps)に進み、権限承認を行っていない場合は、**Cloud Access Managementに進む**をクリックして、コンソール共通の権限管理ページに移動し、権限承認操作を行う必要があります。
![](https://qcloudimg.tencent-cloud.cn/raw/b5cf2f61dfd652dbd4af57abe13b06d3.png)
>!権限承認が完了していない場合、メディア処理コンソールで他の操作を行うことはできません。

## メディア処理サービスを使用する
メディア処理サービスを申請した後、コンソールで**クラウド製品** > **Video Service**>[**メディア処理**](https://console.cloud.tencent.com/mps)を選択すると、メディア処理サービスの使用を開始できます。

## メディア処理サービスの課金
メディア処理が現在サポートする課金方式には[**従量課金**](https://intl.cloud.tencent.com/document/product/1041/33478)および [**前払いリソースパック**](https://intl.cloud.tencent.com/document/product/1041/48810)があります。
- **従量課金-日次決済**：先に使用して料金は後払いの課金方式です。Tencent Cloudアカウントで、先に[チャージ](https://console.cloud.tencent.com/expense/recharge)する必要があります。システムは、毎日、前日の実際の使用量を集計して請求書のプッシュと料金の精算を行い、お客様のアカウントの残高から実際の消費により発生した金額を差し引きます。
- **従量課金-月次決済**：先に使用して料金は後払いの課金方式です。Tencent Cloudアカウントで、先に[チャージ](https://console.cloud.tencent.com/expense/recharge)する必要があります。システムは月ごとに課金し、毎月1日に前月に発生した料金の精算を行い、請求書を発行して料金を差し引きます。
-  **前払いリソースパック**：パッケージで販売するメディア処理のリソースパックです。先に [リソースパックを購入](https://buy.cloud.tencent.com/mps)してから、リソースを使用する必要があります。毎日消費されるメディア処理のリソースは、リソースパック内であれば非課金です。超過部分については、日次決済の課金方式に基づき課金されます。詳細については、[リソースパック](https://intl.cloud.tencent.com/document/product/1041/48810)をご参照ください。
