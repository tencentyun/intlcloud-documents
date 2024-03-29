Cloud Object Storage（COS） はリソースパックのセルフ返金機能をサポートしています。返金の手続きを行う前に、[返金ルール](#rule)をよくお読みください。

## 返金についての注意事項

<span id="rule"></span>

### 返金ルール

1. リソースパックを購入する際に使用したクーポンは払い戻しの対象となりません。クーポン以外の料金は、支払い方法（現金/ギフト）と支払い比率に応じて支払者のTencent Cloudアカウントに払い戻されます。返金の詳細については[注文管理ページ](https://console.cloud.tencent.com/expense/deal)でご確認ください。
2. セルフ返金が可能なCOSリソースパックは、同時に次の3つの条件を満たす必要があります。
 - 注文タイプ：「新規購入」または「支払い更新」であること。
 - 使用量：リソースパックに使用量が発生しておらず、未使用であること。
 - 有効期間：新規購入リソースパックの場合は有効期間内であること、支払い更新リソースパックの場合は有効化されていないこと。

>!
>- キャンペーンに参加して購入したリソースパックの払い戻しを希望する場合で、かつ返金ルールとキャンペーンルールが競合する場合は、キャンペーンルールに準じます。
>- 異常な、あるいは悪意ある返金申請の疑いがある場合、Tencent Cloudには返金を拒否する権利があります。
>- 指定の有効化時間が設定されているリソースパックについては、返金が可能かどうかの判断はコンソール上での操作に準じます。

### よくあるご質問

#### 1. リソースパックの注文タイプを確認するにはどうすればよいですか。
注文タイプは**料金 > 料金センター > 注文管理 > 前払い注文**で確認できます。製品カテゴリーで「COS」を選択します。[ここをクリックして確認](https://console.cloud.tencent.com/expense/deal)できます。


#### 2. リソースパックの使用量および有効期限を確認するにはどうすればよいですか。
**COSコンソール > リソースパック管理 > 購入リソースパック**でリソースパックの使用量と有効期限を確認することができます。[ここをクリックして確認](https://console.cloud.tencent.com/cos/package/buy)できます



### 返金ポータル

- 新規購入リソースパックの場合
セルフ返金の条件に当てはまる場合は、**COSコンソール > リソースパック管理**で返金手続きを行うことができます。操作ガイドについては[新規購入リソースパックの返金手続き](#new)をご参照ください。
- 支払い更新リソースパックの場合
セルフ返金の条件に当てはまる場合は、**料金センター > 支払い更新管理**で返金手続きを行うことができます。操作ガイドについては[支払い更新を行ったリソースパックの返金手続き](#renewal)をご参照ください。


### 返金額の計算方法

返金額 = 支払金額 -（使用した時間/総時間）× 注文割引前価格 × 適用割引率

>?
> - 使用した時間とは、注文の購入から返金までの時間を指します。使用した時間が1日に満たない場合は、1日として計算します。
> - 注文割引前価格は、仕様、購入時間、従量課金単価によって計算します。
> - 適用割引はリソースを使用した時間、お客様の割引率などの要素によって決まります。
> 

### セルフ返金の計算例

COSリソースパック購入ページで、「中国大陸共通、50GB、有効期間6か月」という仕様の標準ストレージ容量パックを1つ購入したとします。利用可能なクーポンはなく、現金支払額が3.46米ドルであったとします。購入当日に、リソースが未使用の状態で、かつセルフ返金の条件を満たしており、セルフ返金を行った場合、返金の計算方法に基づく分析は次のようになります。

- 注文割引前価格は50GB × 6か月 × 0.024米ドル/GB/月 = 7.2米ドルとなります。
- 使用した時間が1日に満たないため、1日として計算します。

返金額 = 3.46 -（1/180）× 7.2 = 3.42ドルとなります。


## セルフ返金の操作手順

### 新規購入リソースパックの返金手続き[](id:new)

1. [COSコンソール](https://console.cloud.tencent.com/cos5)にログインします。
2. 左側メニューバーの**リソースパック管理**をクリックし、リソースパック管理の**購入リソースパック**ページに進みます。
3. 返金を希望するリソースパックを見つけ、リソースパックの右側の**返金**をクリックします。
>!使用量の統計データはリアルタイムデータではありません（24時間の遅延あり）。当日に購入したリソースパックの、その日の使用量を確認することができるのは翌日になります。
>
4. 返金情報ページで、返金情報（リソースパックの情報、返金形式、返金額など）をよくご確認ください。
5. 情報に誤りがないことを確認した後、**返金を確認**をクリックして申請します。
 - セルフ返金申請を送信後、3～5分でシステムによって返金が完了し、クラウドリソースが破棄されます。
 - 返金注文は[注文管理](https://console.cloud.tencent.com/expense/deal)で確認できます。注文のステータスが「返金済み」に更新されると、その後は料金センターのページで料金を確認できるようになります。

### 支払い更新を行ったリソースパックの返金手続き[](id:renewal)

1. [Tencent Cloudコンソール](https://console.cloud.tencent.com)にログインします。
2. コンソールページ右上方の**料金 > 料金センター > 支払い更新管理**をクリックし、製品カテゴリーで「COS」を選択します。支払い更新のタイプで「手動支払い更新項目」または「自動支払い更新項目」を選択してフィルタリングし、返金を希望するリソースパックを見つけます。支払い更新リストの操作列で**その他 > 支払い更新キャンセル**をクリックします。

  - リソースパックが返金ルールに適合している場合は、セルフ返金が可能です。
  - 要件を満たしていない場合は返金できません。
  - 
>!使用量の統計データはリアルタイムデータではありません（24時間の遅延あり）。当日に購入したリソースパックの、その日の使用量を確認することができるのは翌日になります。
>

3. 返金情報ページで、返金情報（リソースパックの情報、返金形式、返金額など）をよくご確認ください。
4. 情報に誤りがないことを確認した後、**返金を確認**をクリックして申請します。
 - セルフ返金申請を送信後、3～5分でシステムによって返金が完了し、クラウドリソースが破棄されます。
 - 返金注文は[注文管理](https://console.cloud.tencent.com/expense/deal)で確認できます。注文のステータスが「返金済み」に更新されると、その後は料金センターのページで料金を確認できるようになります。
