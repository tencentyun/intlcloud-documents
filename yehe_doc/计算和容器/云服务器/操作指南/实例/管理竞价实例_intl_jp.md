## 概要
このドキュメントは、ビッドインスタンスの管理及び購入する方法について説明させていただきます。現在、下記の3種類の利用方法があります。
- **CVMコンソール**：CVM購入ページはビッドインスタンスモードに対応しています。
- **BatchComputeコンソール**：BatchComputeは作業提出及びコンピューティング環境作成時にビッドインスタンスを選択することに対応しています。
**TencentCloud API**：[RunInstance インターフェース](https://intl.cloud.tencent.com/zh/document/product/213/33237) はビッドインスタンスの関連パラメータを追加しています。


## 操作手順
<dx-tabs>
::: CVMコンソール

1. [CVM購入ページ](https://buy.intl.cloud.tencent.com/cvm?regionId=1&projectId=-1)にログインします。
2. 下図に示すように、モデル選択時に、課金モデルで**スポットインスタンス**を選択します。
![](https://qcloudimg.tencent-cloud.cn/raw/1c6720cefc4f56bc05d7ba7fc7c31347.png)
3.実際の要件とページの指示に従って、リージョン、アベイラビリティーゾーン、ネットワーク、インスタンスなどの構成情報を設定します。
4. 購入したビッドインスタンスの情報を確認し、各コンフィギュレーションの費用明細を把握します。
5. **アクティブ化**をクリックし、支払いを完了します。
支払った後に、 [CVMコンソール](https://console.cloud.tencent.com/cvm) に入り、ビッドインスタンスを確認することができます。

:::
::: Batch Computeコンソール
### Batch Computeの特性についての説明
-  **非同期インターフェース**
ジョブの提出またはコンピューティング環境の作成、予想されるコンピューティング環境の数を変更する場合、Batch Computeは非同期の形式でリクエストを処理します。つまり、在庫、価格などの理由で現在のリクエストを満たせない場合は、満たせるようになるまでスポットインスタンス型リソースを申請し続けます。
インスタンスをリリースしたい場合は、BatchComputeコンソールでコンピューティング環境のインスタンス数を調整する必要があります。CVMコンソールでリリースする場合は、BatchComputeは期待する数を満たすまでに自動的に作成します。
- **クラスターモデル**
Batch Computeのコンピューティング環境はクラスターモデルによる一群のスポットインスタンスのメンテナンスをサポートしています。必要な数量、設定および最高指値を提出するだけで、コンピューティング環境が予定の数量を満たすまで、自動的に申請を開始し続けます。中断が発生した後も補充数量の申請が自動的に再開されます。
- **固定価格**
現段階では固定割引モデルを採用しており、パラメータを現在の市場価格以上に設定する必要があります。市場価格の詳細については、[現在のスポットインスタンスがサポートするリージョンとインスタンスタイプおよび仕様](https://intl.cloud.tencent.com/document/product/213/17817)をご参照ください。

#### 使用手順
1.  [BatchComputeコンソール](https://console.cloud.tencent.com/batch/env)にログインします。
2. コンピューティング環境管理ページで任意のリージョン（例えば広州リージョンなど）を選択し、**新規作成**をクリックします。
コンピューティング環境の新規作成ページに入ります。
3. 下図に示すように、コンピューティング環境新規作成ページで「課金タイプ」を**スポットインスタンス**に設定し、実際のニーズに応じて、必要なモデル、イメージ、名称、希望する数量などの情報を選択します。
![](https://qcloudimg.tencent-cloud.cn/raw/95437ac5e26f3270c758fcc282042972.png)
4.**確定**をクリックして、作成を完了します。
作成が完了したら、[Batch Computeコンソール](https://console.cloud.tencent.com/batch/env)で作成したコンピューティング環境を確認できます。また、コンピューティング環境内のCVMも同時に作成中である場合は、そのコンピューティング環境の**イベントログ**と**インスタンスリスト**を介して作成状況を確認できます。
:::
::: クラウド\sAPI
RunInstance インターフェースにおける [InstanceMarketOptionsRequest](https://intl.cloud.tencent.com/zh/document/api/213/15753?from_cn_redirect=1) パラメータはビッドインスタンスモードを指定し、関連情報をコンフィギュレーションすることができます。
**同期インターフェース**：現在、 RunInstanceが提供している同期リクエストインターフェースは一回限り使用できます。即ち、申請が失敗（在庫不足、請求価格が市場価格以下）した場合は直ちに失敗を戻し、引き続き申請をしません。
* **固定価格**：現在の段階では固定割引モードを採用しています。顧客はパラメータを現在の市場価格以上に設定しなければなりません。市場価格の詳細情報は [現在ビッドインスタンスの対応しているリージョン及びインスタンスタイプ・仕様](https://intl.cloud.tencent.com/document/product/213/17817)をご参照ください。

### シナリオ事例の説明
顧客は広州三区における一つのインスタンスを保有しており、当該インスタンスの課金モードが時間ごとに課金する後払いのビッドモードとします。具体的なビッドモードのコンフィギュレーション情報は下記の通りです。
- 最高ビッド：0.0923ドル/時間
- ビッドリクエストモード：一回限りのリクエスト
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
