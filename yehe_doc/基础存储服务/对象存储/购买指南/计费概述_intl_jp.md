ここでは主に、Cloud Object Storage(COS)の課金方式、課金項目、課金周期、製品価格などの情報について紹介しており、COSの課金システムを理解するうえで役立ちます。

## 課金方式

COSの課金方式は従量課金です。説明は次のとおりです。

| 課金方式                                                     | 説明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| 従量課金（後払い） | 先に使って後で支払う、COSのデフォルトの課金方式です。各課金項目の実際の使用量は、日単位で計測、決済、引き落とし、請求書発行が行われ、[全リージョン](https://intl.cloud.tencent.com/document/product/436/6224)でサポートされています。詳細については、[従量課金（後払い）](https://intl.cloud.tencent.com/document/product/436/32534)をご参照ください。 |




## 課金項目

下図のように、COSの課金項目にはストレージ容量料金、リクエスト料金、データ取得料金、トラフィック料金、管理機能料金が含まれます。その他の説明については、[課金項目](https://intl.cloud.tencent.com/document/product/436/33776)をご参照ください。


![](https://qcloudimg.tencent-cloud.cn/raw/f122045a434978ab26cb7c276723fc9d.png)





## 課金周期

COSの各課金項目の課金周期および課金順序の説明は次のとおりです。

> ?
>2022年9月1日より、COSのストレージ容量、リクエストおよびデータ取得といった課金項目は、日次決済されることになりました。詳細については、[COSストレージ容量、リクエストおよびデータ取得の日次決済に関するお知らせ](https://intl.cloud.tencent.com/document/product/436/47593)をご参照ください。

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
      <td rowspan=4>前日に発生した料金が毎日決済され、請求書が出力されます</td>
      <td>無料利用枠 >従量課金。無料利用枠に対応していない場合は従量課金となります</td>
   </tr>
   <tr>
      <td rowspan=3>リクエスト料金</td>
      <td colspan=1>読み書きリクエスト料金</td>
      <td rowspan=3>日</td>
      <td>従量課金</td>
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
      <td rowspan=2>日</td>
      <td rowspan=2>前日に発生した料金が毎日決済され、請求書が出力されます</td>
      <td rowspan=2>従量課金</td>
   </tr>
   <tr>
      <td colspan=1>アーカイブデータ取得料金</td>
   </tr>
   <tr>
      <td colspan=1>ディープアーカイブデータ取得料金</td>
      <td>日</td>
      <td>前日に発生した料金が毎日決済され、請求書が出力されます</td>
      <td>従量課金</td>
   </tr>
   <tr>
      <td colspan=2>トラフィック料金</td>
      <td>日</td>
      <td>前日に発生した料金が毎日決済され、請求書が出力されます</td>
      <td>従量課金</td>
   </tr>
   <tr>
      <td rowspan=4>管理機能料金</td>
      <td colspan=1>リスト機能料金</td>
      <td>日</td>
      <td>前日に発生した料金が毎日決済され、請求書が出力されます</td>
      <td>従量課金</td>
   </tr>
   <tr>
      <td colspan=1>検索機能料金</td>
      <td>日</td>
      <td>前日に発生した料金が毎日決済され、請求書が出力されます</td>
      <td>従量課金</td>
   </tr>
   <tr>
      <td colspan=1>バッチ処理料金</td>
      <td>日</td>
      <td>前日に発生した料金が毎日決済され、請求書が出力されます</td>
      <td>従量課金</td>
   </tr>
   <tr>
      <td colspan=1>オブジェクトタグ料金</td>
      <td>日</td>
      <td>前日に発生した料金が毎日決済され、請求書が出力されます</td>
      <td>従量課金</td>
   </tr>
</table>


## 製品料金

COSの課金項目については、[製品価格](https://buy.intl.cloud.tencent.com/price/cos?lang=en&pg=)をご参照ください。


## 関連リンク


1. COSの料金の詳細な計算およびケースごとの課金の詳細については、[課金の例](https://intl.cloud.tencent.com/document/product/436/6241)をご参照ください。
2. COSの支払延滞によるサービス停止ポリシー（データの保存および破棄までの期間、ならびに関連の課金説明）については、COSの[支払い延滞の説明](https://intl.cloud.tencent.com/document/product/436/10044)をご参照ください。
3. 課金周期について：[課金モデルと請求書統計周期](https://www.tencentcloud.com/document/product/555/7430?lang=en&pg=)をご参照ください。
4. COSの課金に関するご質問について：[よくあるご質問](https://intl.cloud.tencent.com/document/product/436/32532)をご参照いただくか、テクニカルサポートまで[お問い合わせ](https://www.tencentcloud.com/contact-us)ください。

