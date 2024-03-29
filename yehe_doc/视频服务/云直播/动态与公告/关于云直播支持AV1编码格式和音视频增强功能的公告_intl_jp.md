Tencent Cloud CSSは**2022年6月1日0時**より、AV1コーデック形式のサポートを開放し、オーディオビデオエンハンスメント機能のサポートを追加します。同時にAV1コーデック形式およびオーディオビデオエンハンスメント機能について、日次決済の公表価格を新たに追加します。

価格にかかわる課金項目には、CSSの標準トランスコーディング、高速高画質トランスコーディングおよびオーディオビデオエンハンスメントが含まれます。

## 追加機能の説明

### AV1コーデック形式

AV1はオープンかつロイヤリティフリーのビデオコーデック形式であり、ネットワーク経由でのストリーミング伝送に特化して設計されています。AV1はAlliance for Open Media（AOMedia）によって開発されました。その使用には次のようなメリットがあります。
- 1Mbps〜2Mbpsの速度で1080P（解像度1920\*1080）のFHDオーディオおよびビデオを伝送できます。
- H.264コーデック形式と比べて圧縮率を40%以上高めることができ、同一の画質視聴体験では、40%以上のCDN配信コストを低減することができます。
- H.265コーデック形式と比べて、ブラウザでの再生をより良好にサポートするエコシステムです。現在、AV1デコードは（Chrome）を含む75%以上のブラウザでサポートされています。
- AV1とライブイベントストリーミング（WebRTC）技術はいずれもGoogleに由来するため、相乗効果があります。Tencent Cloud[ライブイベントストリーミング](https://intl.cloud.tencent.com/document/product/267/42141)をAV1のクラウドトランスコード機能と組み合わせることで、超低遅延、より高解像度の画質、CDNコストのさらなる削減が実現できます。

### オーディオビデオエンハンスメント
画質修正および画質エンハンスメントという2つのモジュールにAIアルゴリズムを組み合わせることで、超解像度、インテリジェントフレーム補間、HDR、ビデオノイズ除去、輪郭修正、オーディオエンハンスメントなどの機能をご提供できます。ライブストリーミングビデオ品質の向上などのケースに適用可能です。

## 追加機能使用ガイド

### AV1コーデック形式

CSSトランスコードテンプレートを設定する際、**コーデック**を「AV1」に設定するだけでOKです。具体的には[CSSトランスコード設定説明](https://intl.cloud.tencent.com/document/product/267/31071)をご参照ください。

### オーディオビデオエンハンスメント
必要がありましたら担当者またはサービスチームにご連絡の上、単独でアクティブ化するようご依頼ください。

## 追加機能料金説明
CSS付加価値サービス[CSSトランスコード（ウォーターマーク、ミクスストリーミング）](https://intl.cloud.tencent.com/document/product/267/39604) の料金に関する説明および注意事項は、ソースドキュメントをご参照ください。

### 標準トランスコーディング
<table>
<tr>
<th >コーデック</th>
<th >解像度</th>
<th >価格（米ドル/分）</th>
<th >備考（ライブストリーミング画面の幅と高さによって区別され、絶対値の大きい方が、長辺と定義付けられます）</th>
</tr>
<tr>
<td rowspan="5"><b>AV1</td>
<td>480P</td>
<td>0.0282</td>
<td>長辺 ≦ 640、かつ短辺 ≦ 480</td>
</tr>
<tr>
<td>720P</td>
<td>0.0550</td>
<td>長辺 ≦ 1280、かつ短辺 ≦ 720</td>
</tr>
<tr>
<td>1080P</td>
<td>0.1098</td>
<td>長辺 ≦ 1936、かつ短辺 ≤ 1088</td>
</tr>
<tr>
<td>2K</td>
<td>0.2366</td>
<td>長辺 ≦ 2560、かつ短辺 ≦ 1440</td>
</tr>
<tr>
<td>4K</td>
<td>0.4732</td>
<td>長辺 ＞ 2560、または短辺 ＞ 1440</td>
</tr>
</table>

### 高速高画質トランスコーディング
<table>
<tr>
<th >コーデック</th>
<th >解像度</th>
<th >価格（米ドル/分）</th>
<th >備考（ライブストリーミング画面の幅と高さによって区別され、絶対値の大きい方が、長辺と定義付けられます）</th>
</tr>
<tr>
<td rowspan="5"><b>AV1</td>
<td>480P</td>
<td>0.0698</td>
<td>長辺 ≦ 640、かつ短辺 ≦ 480</td>
</tr>
<tr>
<td>720P</td>
<td>0.1330</td>
<td>長辺 ≦ 1280、かつ短辺 ≦ 720</td>
</tr>
<tr>
<td>1080P</td>
<td>0.2658</td>
<td>長辺 ≦ 1936、かつ短辺 ≤ 1088</td>
</tr>
<tr>
<td>2K</td>
<td>0.5318</td>
<td>長辺 ≦ 2560、かつ短辺 ≦ 1440</td>
</tr>
<tr>
<td>4K</td>
<td>1.0634</td>
<td>長辺 ＞ 2560、または短辺 ＞ 1440</td>
</tr>
</table>


### オーディオビデオエンハンスメント
<table>
<tr>
<th >コーデック</th>
<th >解像度</th>
<th >価格（米ドル/分）</th>
<th >備考（ライブストリーミング画面の幅と高さによって区別され、絶対値の大きい方が、長辺と定義付けられます）</th>
</tr>
<tr>
<td rowspan="5"><b>H.264</td>
<td>480P</td>
<td>0.1278</td>
<td>長辺 ≦ 640、かつ短辺 ≦ 480</td>
</tr>
<tr>
<td>720P</td>
<td>0.2545</td>
<td>長辺 ≦ 1280、かつ短辺 ≦ 720</td>
</tr>
<tr>
<td>1080P</td>
<td>0.5088</td>
<td>長辺 ≦ 1936、かつ短辺 ≤ 1088</td>
</tr>
<tr>
<td>2K</td>
<td>1.0175</td>
<td>長辺 ≦ 2560、かつ短辺 ≦ 1440</td>
</tr>
<tr>
<td>4K</td>
<td>2.0350</td>
<td>長辺 ＞ 2560、または短辺 ＞ 1440</td>
</tr>
<tr>
<td rowspan="5"><b>H.265</td>
<td>480P</td>
<td>0.1510</td>
<td>長辺 ≦ 640、かつ短辺 ≦ 480</td>
</tr>
<tr>
<td>720P</td>
<td>0.2988</td>
<td>長辺 ≦ 1280、かつ短辺 ≦ 720</td>
</tr>
<tr>
<td>1080P</td>
<td>0.5973</td>
<td>長辺 ≦ 1936、かつ短辺 ≤ 1088</td>
</tr>
<tr>
<td>2K</td>
<td>1.1947</td>
<td>長辺 ≦ 2560、かつ短辺 ≦ 1440</td>
</tr>
<tr>
<td>4K</td>
<td>2.3893</td>
<td>長辺 ＞ 2560、または短辺 ＞ 1440</td>
</tr>
<tr>
<td rowspan="5"><b>AV1</td>
<td>480P</td>
<td>0.1860</td>
<td>長辺 ≦ 640、かつ短辺 ≦ 480</td>
</tr>
<tr>
<td>720P</td>
<td>0.3652</td>
<td>長辺 ≦ 1280、かつ短辺 ≦ 720</td>
</tr>
<tr>
<td>1080P</td>
<td>0.7302</td>
<td>長辺 ≦ 1936、かつ短辺 ≤ 1088</td>
</tr>
<tr>
<td>2K</td>
<td>1.4604</td>
<td>長辺 ≦ 2560、かつ短辺 ≦ 1440</td>
</tr>
<tr>
<td>4K</td>
<td>2.9207</td>
<td>長辺 ＞ 2560、または短辺 ＞ 1440</td>
</tr>
</table>

>? ライブストリーミングの業務量が大量にあり、日次決済の課金方法ではお客様のニーズを満たせない場合、お客様の課金方法と価格をTencent Cloudの担当者と協議して設定することができます。[チケットを提出](https://console.cloud.tencent.com/workorder/category) して詳細をお問い合わせください。


ご不明な点がございましたら、お気軽に[お問い合わせ](https://console.cloud.tencent.com/workorder/category)ください。ユーザーの皆様方には、Tencent CloudのCloud Streaming Services(CSS)製品に対する格別のお引き立てとご愛顧を賜り、心より御礼申し上げます。


2022-05-27
Tencent Cloud CSSチーム
