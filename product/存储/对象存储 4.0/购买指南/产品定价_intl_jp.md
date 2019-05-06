本文では、COSの従量制課金による定価を紹介します。COSの課金方式や課金アイテムなどの情報については、[COS課金説明](https://cloud.tencent.com/document/product/436/16871)を参照してください。。

実際のケースによってCOS課金も了解できます。[課金インスタンス](https://cloud.tencent.com/document/product/436/6241)を参照してください。

## 従量制課金による定価

従量制課金の場合、ユーザーは自分で使用量を試算できます。**[COS価格計算機](https://buy.cloud.tencent.com/price/cos/calculator)**を利用して詳細な購入価格を計算します。 

## 従量制課金による定価

<table>
   <tr>
      <th rowspan="3" width="75px">利用地域</th>
      <th rowspan="3">ストレージタイプ</th>
	<th colspan="6"><center>課金アイテム</center></th>
   </tr>
   <tr>
      <th rowspan="2">ストレージ容量の料金（USD/GB/Month）</th>
      <th rowspan="2" width="150px">読取/書込の料金<br>（UDS/万回）</th>
      <th rowspan="2">データ検索料金（USD/GB）</th>
      <th colspan="3">トラフィック料金（USD/GB）</th>
   </tr>
   <tr>
      <th>パブリックネットワーク下りトラフィック</th>
      <th>CDNプルトラフィック</th>
      <th>地域間コピートラフィック</th>
   </tr>
   <tr>
      <td rowspan="3">成都、重慶</td>
      <td>スタンダートストレージ</td>
      <td>0.02</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.1</td>
      <td rowspan="2">0.02</td>
      <td rowspan="2">0.05</td>
   </tr>
   <tr>
      <td>低頻度ストレージ</td>
      <td>0.014</td>
      <td>0.01</td>
      <td>0.002</td>
   </tr>
   <tr>
      <td>CAS</td>
      <td>0.0045</td>
      <td>0.0147（回復してから要求できます）</td>
      <td width="150px">Quick to retrieve:0.03<br>Standard to retrieve:0.01<br>Batch to retrieve:0.0025</td>
      <td>0.1（回復してから対応できます）</td>
      <td>対応しません</td>
      <td>対応しません</td>
   </tr>
   <tr>
      <td rowspan="3">中国本土の別の都市</td>
      <td>スタンダートストレージ</td>
      <td>0.024</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.1</td>
      <td rowspan="2">0.02</td>
      <td rowspan="2">0.05</td>
   </tr>
   <tr>
      <td>低頻度ストレージ</td>
      <td>0.018</td>
      <td>0.01</td>
      <td>0.002</td>
   </tr>
   <tr>
      <td>CAS</td>
      <td>0.005</td>
      <td>0.0147（回復してから要求できます）</td>
      <td width="150px">Quick to retrieve:0.03<br>Standard to retrieve:0.01<br>Batch to retrieve:0.0025</td>
      <td>0.1（回復してから対応できます）</td>
      <td>対応しません</td>
      <td>対応しません</td>
   </tr>
   <tr>
      <td rowspan="2">香港</td>
      <td>スタンダートストレージ</td>
      <td>0.022</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.08</td>
      <td rowspan="2">0.08</td>
      <td rowspan="2">0.08</td>
   </tr>
   <tr>
      <td>低頻度ストレージ</td>
      <td>0.016</td>
      <td>0.01</td>
      <td>0.002</td>
   </tr>
   <tr>
      <td rowspan="3">シンガポール</td>
      <td>スタンダートストレージ</td>
      <td>0.022</td>
      <td>0.003</td>
      <td>0</td>
      <td rowspan="2">0.072</td>
      <td rowspan="2">0.072</td>
      <td rowspan="2">0.072</td>
   </tr>
   <tr>
      <td>低頻度ストレージ</td>
      <td>0.016</td>
      <td>0.015</td>
      <td>0.003</td>
   </tr>
	 	    <tr>
      <td>CAS</td>
      <td>0.005</td>
      <td>0.0147（回復してから要求できます）</td>
      <td width="150px">Quick to retrieve:0.036<br>Standard to retrieve:0.012<br>Batch to retrieve:0.003</td>
      <td>0.072（回復してから対応できます）</td>
      <td>対応しません</td>
      <td>対応しません</td>
   </tr>
   <tr>
      <td rowspan="2">フランクフルト</td>
      <td>スタンダートストレージ</td>
      <td>0.02</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
   </tr>
   <tr>
      <td>低頻度ストレージ</td>
      <td>0.014</td>
      <td>0.01</td>
      <td>0.002</td>
   </tr>
   <tr>
      <td rowspan="2">トロント</td>
      <td>スタンダートストレージ</td>
      <td>0.02</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
   </tr>
   <tr>
      <td>低頻度ストレージ</td>
      <td>0.014</td>
      <td>0.01</td>
      <td>0.002</td>
   </tr>
   <tr>
      <td rowspan="2">ムンバイ</td>
      <td>スタンダートストレージ</td>
      <td>0.024</td>
      <td>0.003</td>
      <td>0</td>
      <td rowspan="2">0.1</td>
      <td rowspan="2">0.1</td>
      <td rowspan="2">0.1</td>
   </tr>
   <tr>
      <td>低頻度ストレージ</td>
      <td>0.018</td>
      <td>0.015</td>
      <td>0.003</td>
   </tr>
   <tr>
      <td rowspan="2">ソール</td>
      <td>スタンダートストレージ</td>
      <td>0.024</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.12</td>
      <td rowspan="2">0.12</td>
      <td rowspan="2">0.12</td>
   </tr>
   <tr>
      <td>低頻度ストレージ</td>
      <td>0.018</td>
      <td>0.01</td>
      <td>0.002</td>
   </tr>
   <tr>
      <td rowspan="2">シリコンバレー</td>
      <td>スタンダートストレージ</td>
      <td>0.024</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
   </tr>
   <tr>
      <td>低頻度ストレージ</td>
      <td>0.018</td>
      <td>0.01</td>
      <td>0.002</td>
   </tr>
   <tr>
      <td rowspan="2">バージニア</td>
      <td>スタンダートストレージ</td>
      <td>0.02</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
   </tr>
   <tr>
      <td>低頻度ストレージ</td>
      <td>0.014</td>
      <td>0.01</td>
      <td>0.002</td>
   </tr>
   <tr>
      <td rowspan="2">バンコック</td>
      <td>スタンダートストレージ</td>
      <td>0.024</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.12</td>
      <td rowspan="2">0.12</td>
      <td rowspan="2">0.12</td>
   </tr>
   <tr>
      <td>低頻度ストレージ</td>
      <td>0.018</td>
      <td>0.01</td>
      <td>0.003</td>
   </tr>
   <tr>
      <td rowspan="2">モスクワ</td>
      <td>スタンダートストレージ</td>
      <td>0.024</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
   </tr>
   <tr>
      <td>低頻度ストレージ</td>
      <td>0.018</td>
      <td>0.01</td>
      <td>0.002</td>
   </tr>
   <tr>
      <td rowspan="2">東京</td>
      <td>スタンダートストレージ</td>
      <td>0.02</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
   </tr>
   <tr>
      <td>低頻度ストレージ</td>
      <td>0.014</td>
      <td>0.01</td>
      <td>0.002</td>
   </tr>
</table>


