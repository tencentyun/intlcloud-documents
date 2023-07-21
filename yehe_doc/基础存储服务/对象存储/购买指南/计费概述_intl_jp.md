ここでは主に、Cloud Object Storage(COS)の課金方式、課金項目、課金周期、製品価格などの情報について紹介しており、COSの課金システムを理解するうえで役立ちます。

## 課金方式

COSは従量課金（後払い）とリソースパック（前払い）の2種類の課金方式をサポートしています。詳細は次のとおりです。

| 課金方式                                                     | 説明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| 従量課金（後払い） | 先に使って後で支払う、COSのデフォルトの課金方式です。各課金項目の実際の使用量は、日単位で計測、決済、引き落とし、請求書発行が行われ、[全リージョン](https://intl.cloud.tencent.com/document/product/436/6224)でサポートされています。詳細については、[従量課金（後払い）](https://intl.cloud.tencent.com/document/product/436/32534)をご参照ください。 |
| リソースパック（前払い） | COSは課金項目ごとにお得なリソースパックを販売しており、こちらは先に購入して後で使う方式になります。決済の際、システムは優先してリソースパックから使用量を差し引き、リソースパックを超過した部分については従量課金方式となります。リソースパックはパブリッククラウドリージョンのみの適用となり、金融クラウドリージョンには適用されません。その他の詳細については、[リソースパック（前払い）](https://www.tencentcloud.com/document/product/436/54353)をご参照ください。 |



## 課金項目

COSの課金項目は[ストレージ容量料金](https://intl.cloud.tencent.com/document/product/436/40099)、[リクエスト料金](https://intl.cloud.tencent.com/document/product/436/40100)、[データ取得料金](https://intl.cloud.tencent.com/document/product/436/40097)、[トラフィック料金](https://intl.cloud.tencent.com/document/product/436/33776)、[管理機能料金](https://intl.cloud.tencent.com/document/product/436/40098)で構成されます。詳細は下図のとおりです。



![](https://qcloudimg.tencent-cloud.cn/raw/f122045a434978ab26cb7c276723fc9d.png)


## 課金周期

COSの各課金項目の課金周期および課金順序の説明は次のとおりです。

> ?
>- COSリソースパックの使用期限および充当の説明に関しては、[リソースパック（前払い）](https://www.tencentcloud.com/document/product/436/54353)をご参照ください。
>- 2022年9月1日より、COSのストレージ容量、リクエストおよびデータ取得といった課金項目は日次決済となっています。詳細については、[COSストレージ容量、リクエストおよびデータ取得の日次決済に関するお知らせ](https://intl.cloud.tencent.com/document/product/436/47593)をご参照ください。

<table>
   <tr>
      <th colspan=2>課金項目</td>
      <th>課金周期</td>
      <th>課金周期説明</td>
      <th>課金順序</td>
   </tr>
   <tr>
      <td colspan=2>ストレージ容量料金</td>
      <td>日</td>
      <td rowspan=1>前日に発生した料金が毎日決済され、請求書が出力されます</td>
      <td>無料利用枠 > リソースパック > 従量課金。対応する無料利用枠およびリソースパックがない場合は従量課金となります</td>
   </tr>
   <tr>
      <td rowspan=3>リクエスト料金</td>
      <td colspan=1>読み書きリクエスト料金</td>
      <td rowspan=3>日</td>
      <td rowspan=3>前日に発生した料金が毎日決済され、請求書が出力されます</td>
      <td>リソースパック > 従量課金</td>
   </tr>
   <tr>
      <td colspan=1>ディープアーカイブ取得リクエスト料金</td>
      <td>従量課金</td>
   </tr>
   <tr>
      <td colspan=1>INTELLIGENT_TIERINGオブジェクト監視料金</td>
      <td>従量課金</td>
   </tr>
   <tr>
      <td rowspan=3>データ取得料金</td>
      <td colspan=1>低頻度データ取得料金</td>
      <td rowspan=3>日</td>
      <td rowspan=3>前日に発生した料金が毎日決済され、請求書が出力されます</td>
      <td rowspan=3>従量課金</td>
   </tr>
   <tr>
      <td colspan=1>アーカイブデータ取得料金</td>
   </tr>
   <tr>
      <td colspan=1>ディープアーカイブデータ取得料金</td>
   </tr>
   <tr>
      <td colspan=2>トラフィック料金</td>
      <td>日</td>
      <td>前日に発生した料金が毎日決済され、請求書が出力されます</td>
      <td>リソースパック > 従量課金</td>
   </tr>
   <tr>
      <td rowspan=4>管理機能料金</td>
      <td colspan=1>リスト機能料金</td>
      <td rowspan=4>日</td>
      <td rowspan=4>前日に発生した料金が毎日決済され、請求書が出力されます</td>
      <td rowspan=4>従量課金</td>
   </tr>
   <tr>
      <td colspan=1>検索機能料金</td>
   </tr>
   <tr>
      <td colspan=1>バッチ処理料金</td>
   </tr>
   <tr>
      <td colspan=1>オブジェクトタグ料金</td>
   </tr>
</table>


## 製品料金

COSの課金項目の価格については、[製品価格](https://buy.intl.cloud.tencent.com/price/cos?lang=en&pg=)をご参照ください。詳細は次のとおりです。
- 従量課金価格：パブリッククラウド価格はパブリッククラウドリージョンに適用され、金融クラウド価格は金融クラウドリージョンに適用されます。詳細については、[製品価格](https://buy.intl.cloud.tencent.com/price/cos?lang=en&pg=)をご参照ください。
- リソースパック価格：パブリッククラウドリソースパック価格は中国大陸共通リージョン、中国香港および海外共通リージョンに適用されます。詳細については、[製品価格](https://buy.intl.cloud.tencent.com/price/cos?lang=en&pg=)または[リソースパックの購入](https://buy.intl.cloud.tencent.com/price/cos?lang=en&pg=)をご参照ください。


## 価格計算ツール

ご自身の業務ニーズに応じて課金項目ごとの使用量を見積もることができます。[価格計算ツール](https://buy.intl.cloud.tencent.com/price/cos?lang=en&pg=)で計算し、見積もりリストをエクスポートします。

## 関連リンク


1. COSの料金の詳細な計算およびケースごとの課金の詳細については、[課金の例]https://intl.cloud.tencent.com/document/product/436/6241)をご参照ください。
2. COSの支払延滞によるサービス停止ポリシー（データの保存および破棄までの期間、ならびに関連の課金説明）については、「COSの[お支払い遅れについて](https://intl.cloud.tencent.com/document/product/436/10044)」をご参照ください。
3. リソースパックの使用について：リソースパックの購入時の注意事項をご存じであるとの前提の下で、リソースパック購入ページでの購入が可能です。[COSリソースパックご購入時の注意事項](https://www.tencentcloud.com/document/product/436/54353)をご参照ください。
4. 課金周期について：[課金モデルと請求書統計周期](https://www.tencentcloud.com/document/product/555/7430?lang=en&pg=)をご参照ください。
5. COSの課金に関するご質問について：[よくあるご質問](https://intl.cloud.tencent.com/document/product/436/32532)をご参照いただくか、テクニカルサポートまで[お問い合わせ](https://www.tencentcloud.com/contact-us)ください。

