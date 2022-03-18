## Tencent Cloudアカウントの登録
MPSサービスを使用するには、[Tencent Cloudアカウントの登録](https://intl.cloud.tencent.com/document/product/378/17985)が必要です。

## MPSサービスを申請する
### 手順1：登録とログイン

Tencent Cloudの公式ウェブサイトにログインし、**クラウド製品**>**Video Service**>[**ビデオ処理**](https://console.cloud.tencent.com/mps)を選択して、MPSコンソールに進みます。

### 手順2：権限承認管理
MPSは、COSバケットにアップロードしたファイルに対して、ダウンロード、トランスコード、アップロードなどの読み書き操作を行う必要があるため、サービスのロールを作成し、MPSにCOSの関連する操作権限を与える必要があります。

[MPSコンソール](https://console.cloud.tencent.com/mps)に進み、権限承認を行っていない場合は、**Cloud Access Managementに進む**をクリックして、コンソール共通の権限管理ページに移動し、権限承認操作を行う必要があります。
![](https://qcloudimg.tencent-cloud.cn/raw/e001187c224f239c596ccc4343e03be7.png)

>!権限承認が完了していない場合、MPSコンソールで他の操作を行うことはできません。


## MPSサービスを使用する
MPSサービスを申請した後、コンソールで**クラウド製品**>**Video Service**>[**ビデオ処理**](https://console.cloud.tencent.com/mps)を選択すると、MPSサービスの使用を開始できます。

## MPSサービスの課金
MPSの現在サポートしている課金方式には**日次決済（後払い）**と**月次決済（後払い）**があります。詳細については[課金方式](https://intl.cloud.tencent.com/document/product/1041/33478)をご参照ください。

- **日次決済課金**：先に使用して料金は後払いの課金方式です。Tencent Cloudアカウントで、先に[チャージ](https://console.cloud.tencent.com/expense/recharge)する必要があります。システムは、毎日、前日の実際の使用量を集計して請求書のプッシュと料金の精算を行い、お客様のアカウントの残高から実際の消費により発生した金額を差し引きます。
- **月次決済課金**：先に使用して料金は後払いの課金方式です。Tencent Cloudアカウントで、先に[チャージ](https://console.cloud.tencent.com/expense/recharge)する必要があります。システムは月ごとに課金し、毎月1日に前月に発生した料金の精算を行い、請求書を発行して料金を差し引きます。
