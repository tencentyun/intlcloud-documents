## 概要
このドキュメントでは、スポットインスタンスの管理及び購入方法などをご説明させていただきます。現在、スポットインスタンスは下記の3種類の方法を通じて利用することができます。
- **CVMコンソール**：CVM購入ページでは、スポットインスタンスモードがサポートされています。
- **BatchComputeコンソール**：BatchComputeコンソールでジョブ送信およびコンピューティング環境作成時に、スポットインスタンスを選択できます。
**TencentCloud API**：スポットインスタンスパラメーターが [RunInstanceインターフェース](https://intl.cloud.tencent.com/document/product/213/33237)に追加されました。

## 操作手順
<dx-tabs>
::: CVMコンソール

1. [CVM購入ページ](https://buy.intl.cloud.tencent.com/cvm?regionId=1&projectId=-1)にログインします。
2. 下図に示すように、課金方法は**スポットインスタンス**を選択します。
![](https://qcloudimg.tencent-cloud.cn/raw/1c6720cefc4f56bc05d7ba7fc7c31347.png)
3.実際のニーズと画面の指示に従って、リージョン、アベイラビリティーゾーン、ネットワークタイプ、インスタンスなどの構成情報を選択します。
4. 購入するスポットインスタンスの情報と各構成アイテムの費用の詳細を確認します。
5. アクティブ化をクリックして支払いを行います。
支払いが完了した後、[CVM コンソール](https://console.cloud.tencent.com/cvm)にログインしてスポットインスタンスを確認できます。

:::
::: Batch Computeコンソール
### BatchCompute機能の説明
-  **非同期インターフェース**
ジョブの送信またはコンピューティング環境の作成、予想されるコンピューティング環境のインスタンス数を変更する場合、BatchComputeは非同期の形式でリクエストを処理します。つまり、在庫、価格などの理由で現在のリクエストを満たせない場合は、満たせるようになるまでスポットインスタンス型リソースを申請し続けます。
インスタンスをリリースしたい場合は、BatchComputeコンソールで予想されるコンピューティング環境のインスタンス数を調整する必要があります。CVMコンソールでインスタンスをリリースすると、BatchComputeコンソールは、予想されるインスタンス数に達するまでインスタンスを自動的に作成します。
- **クラスターモデル**
BatchComputeインスタンスのコンピューティング環境は、スポットインスタンスのバッチを1つのクラスターとして維持することをサポートします。スポットインスタンスの希望する数、構成、および最高指値を送信するだけで、コンピューティング環境は、予想される数量に達するまでスポットインスタンスを自動的かつ継続的に適用します。中断が発生した後も補充数量の申請が自動的に再開されます。
- **固定価格**
現段階では固定割引モデルを採用しており、パラメータを現在の市場価格以上の値に設定する必要があります。市場価格の詳細については、[スポットインスタンス](https://intl.cloud.tencent.com/document/product/213/17817)をご参照ください。

#### 使用手順
1.  [BatchComputeコンソール](https://console.cloud.tencent.com/batch/env)にログインします。
2. コンピューティング環境管理ページで任意のリージョン（例えば広州リージョンなど）を選択し、**新規作成**をクリックします。
コンピューティング環境の作成ページに進みます。
3. 下図に示すように、「課金タイプ」を**スポットインスタンス**に設定し、実際のニーズに応じて、必要なモデル、イメージ、名前、目標数量などの情報を選択します。
![](https://qcloudimg.tencent-cloud.cn/raw/95437ac5e26f3270c758fcc282042972.png)
4.**OK**をクリックして、作成を完了します。
作成が完了したら、[BatchCompute コンソール](https://console.cloud.tencent.com/batch/env) で新しいコンピューティング環境を確認できます。また、コンピューティング環境内のCVMインスタンスも同期的に作成されており、このコンピューティング環境の**アクティビティログ**と**インスタンスリスト**でインスタンスの作成の進行状況を確認できます。
:::
::: クラウド\sAPI
RunInstance インターフェースにおける[InstanceMarketOptionsRequest]((https://intl.cloud.tencent.com/document/api/213/15753?from_cn_redirect=1)) パラメータはスポットインスタンスの使用モード（有効または無効）を指定し、関連情報を構成できます。
**同期インターフェース**：現在、 RunInstanceが提供している同期リクエストインターフェースは一回限り使用できます。即ち、申請が失敗（在庫不足、請求価格が市場価格以下）した場合は直ちに失敗を戻し、引き続き申請をしません。
* **固定価格**：現段階では固定割引モデルを採用しており、パラメータを現在の市場価格以上の値に設定する必要があります。市場価格の詳細については、[スポットインスタンス](https://intl.cloud.tencent.com/document/product/213/17817)をご参照ください。

### サンプルシナリオの説明
顧客は広州三区における一つのインスタンスを保有しており、当該インスタンスの課金モードが時間単位で課金する入札モードです。詳細な内容は以下の通りです。
- 最高入札額：0.0923ドル/時間
- 入札リクエストモード：1 回限りのリクエスト
- イメージ ID：img-pmqg1cw7
- 選択するモデル：2C4G二世代標準型（S2.MEDIUM4）
- 購入数：1台

### リクエストパラメータ
```
https://cvm.tencentcloudapi.com/?Action=RunInstances
&Placement.Zone=ap-guangzhou-3
&InstanceChargeType=SPOTPAID
&InstanceMarketOptions.MarketType=spot
&InstanceMarketOptions.SpotOptions.MaxPrice=0.0923
&InstanceMarketOptions.SpotOptions.SpotInstanceType=one-time
&ImageId=img-pmqg1cw7
&InstanceType=S2.MEDIUM4
&InstanceCount=1
&<パブリックリクエストパラメータ>
```

### リターンパラメータ
```
{
  "Response":{
    "InstanceIdSet": [
      "ins-1vogaxgk"
    ],
    "RequestId": "3c140219-cfe9-470e-b241-907877d6fb03"
  }
}
```
:::
</dx-tabs>
