## 機能の説明
ドメイン名がContent Delivery Network（CDN）に接続されると、すべてのユーザー側のリソース要求がCDNノードにスケジュールされて応答します。 ノードがリソースをキャッシュしている場合は、コンテンツを直接返します。 CDNノードがリソースをキャッシュしていない場合、要求をドメイン名設定のオリジンサーバーにパススルーして、必要なリソースを取得します。

CDNノードはほとんどのユーザー要求に応答するため、顧客はユーザーからのアクセス状況を分析するために、CDNサービスは時間単位のアクセスログを提供しますので、最近30日のアクセスログをダウンロードすることができます。

> 現時点では、ノードアクセスログのみが提供されていますが、back to originログは提供されていません。

## ユースケース
### アクセス行動分析
お客様はアクセスログをダウンロードすることにより、ニーズに応じて、人気のあるリソース分析、アクティブユーザー分析などを行います。

### サービス品質の監視
アクセスログをダウンロードすることにより、CDNノード全体のサービス状況を把握し、平均応答時間や平均ダウンロード速度などの指標を計算することができます。

## 操作ガイド
### 利用方法
 [CDNコンソール](https://console.cloud.tencent.com/cdn)にログインし、左側のメニューで【Log Service】をクリックします。ドメイン名と時間を選択して、アクセスログをクエリできます。 複数のログパッケージを選択し、ローカルにバッチダウンロードできます。
![](https://mc.qcloudimg.com/static/img/043e70b6829ce67d6af125b51736b249/1.png)

>
- アクセスログはデフォルトでは時間ごとに分割され、毎日24個のログファイルが生成されますが、ある時間にドメイン名がリクエストされていない場合、この時間範囲ではログパケットが生成されません。
- 同一ドメイン名の海外アクセスログは中国国内のアクセスログとは別にパッケージ化されており、ログデータパッケージの命名形式は「時間-ドメイン名-加速エリア」です。
- アクセスログは各CDN加速ノードから収集されるため、遅延には違いがあります。一般的には、ログパッケージは約30分の遅延でクエリおよびダウンロードできます。ログパッケージは継続的に追加され、2〜3時間後に安定になります。
- ドメイン名の履歴アクセスログでは、ログパッケージが30日以内にのみ保持されます。 次のガイドラインに従って、SCF関数を使用してログパッケージをCloud Object Storage に転送し、永続的に保存することができます。

### ログフィールドの説明
ログに対応するフィールドの順序（左から右へ）と意味は次の通りです。
<table style="width:660px;">
<thead>
</tr>
<th align="left" style="width:100px;font-weight:700">順序</th>
<th align="left" style="width:560px;font-weight:700">ログ内容 </th>
</tr>
</thead>
<tbody><tr>
<td>1</td>
<td>リクエスト時間</td>
</tr>
</tbody>
<tbody><tr>
<td>2</td>
<td>クライアントIP</td>
</tr>
</tbody>
<tbody><tr>
<td>3</td>
<td>ドメイン名</td>
</tr>
</tbody>
<tbody><tr>
<td>4</td>
<td>リクエストパス</td>
</tr>
</tbody>
<tbody><tr>
<td>5</td>
<td>今回のアクセスのバイト数のサイズにはファイル自身のサイズとリクエストheaderのサイズが含まれます</td>
</tr>
</tbody>
<tbody><tr>
<td>6</td>
<td>国内のログは省番号を表し、海外のログは地域番号を表します（マッピングテーブルについては以下をご参照ください）</td>
</tr>
</tbody>
<tbody><tr>
<td>7</td>
<td>国内のログはキャリア番号を表し、海外のログは -1に統一されています（マッピングテーブルについては以下をご参照ください）</td>
</tr>
</tbody>
<tbody><tr>
<td>8</td>
<td>HTTPステータスコード</td>
</tr>
</tbody>
<tbody><tr>
<td>9</td>
<td>Referer 情報</td>
</tr>
</tbody>
<tbody><tr>
<td>10</td>
<td>応答時間（ミリ秒）、リクエストを受信した後、ノードがすべてのパケットに応答してクライアントに戻るまでにかかる時間を指します</td>
</tr>
</tbody>
</tbody>
<tbody><tr>
<td>11</td>
<td>User-Agent 情報</td>
</tr>
</tbody>
</tbody>
<tbody><tr>
<td>12</td>
<td>Range パラメータ</td>
</tr>
</tbody>
</tbody>
<tbody><tr>
<td>13</td>
<td>HTTP Method</td>
</tr>
</tbody>
</tbody>
<tbody><tr>
<td>14</td>
<td>HTTPプロトコルロゴ</td>
</tr>
</tbody>
</tbody>
<tbody><tr>
<td>15</td>
<td>キャッシュHIT/MISS、CDNエッジノードのヒットと親ノードのヒットはHITとしてマークされます</td>
</tr>
</tbody></table>

### 地域 / キャリアのマッピングテーブル

#### 省のマッピング
<table style="width:660px;">
<thead>
</tr>
<th align="left" style="width:100px;font-weight:700">地域ID</th>
<th align="left" style="width:120px;font-weight:700">地域</th>
<th align="left" style="width:100px;font-weight:700">地域ID</th>
<th align="left" style="width:120px;font-weight:700">地域</th>
<th align="left" style="width:100px;font-weight:700">地域ID</th>
<th align="left" style="width:120px;font-weight:700">地域</th>
</tr>
</thead>
<tbody><tr>
<td>22</td>
<td>北京</td>
<td>86</td>
<td>内モンゴル</td>
<td>146</td>
<td>山西</td>
</tr>
</tr>
<td>1069</td>
<td>河北</td>
<td>1177</td>
<td>天津</td>
<td>119</td>
<td>寧夏</td>
</tr>
</tr>
<td>152</td>
<td>陝西</td>
<td>1208</td>
<td>甘粛</td>
<td>1467</td>
<td>青海</td>
</tr>
</tr>
<td>1468</td>
<td>新疆</td>
<td>145</td>
<td>黒竜江</td>
<td>1445</td>
<td>吉林</td>
</tr>
</tr>
<td>1464</td>
<td>遼寧</td>
<td>2</td>
<td>福建</td>
<td>120</td>
<td>江蘇</td>
</tr>
</tr>
<td>121</td>
<td>安徽</td>
<td>122</td>
<td>山東</td>
<td>1050</td>
<td>上海</td>
</tr>
</tr>
<td>1442</td>
<td>浙江</td>
<td>182</td>
<td>河南</td>
<td>1135</td>
<td>湖北</td>
</tr>
</tr>
<td>1465</td>
<td>江西</td>
<td>1466</td>
<td>湖南</td>
<td>118</td>
<td>貴州</td>
</tr>
</tr>
<td>153</td>
<td>雲南</td>
<td>1051</td>
<td>重慶</td>
<td>1068</td>
<td>四川</td>
</tr>
</tr>
<td>1155</td>
<td>チベット</td>
<td>4</td>
<td>広東</td>
<td>173</td>
<td>広西</td>
</tr>
</tr>
<td>1441</td>
<td>海南</td>
<td>0</td>
<td>その他</td>
<td>1</td>
<td>中国香港・中国マカオ・中国台湾</td>
</tr>
</tr>
<td>-1</td>
<td>海外</td>
<td>-</td>
<td>-</td>
<td>-</td>
<td>-</td>
</tr>
</tbody></table>


#### キャリアのマッピング
<table  style="width:494px">
<thead>
</tr>
<th align="left" style="width:100px;font-weight:700">キャリア ID</th>
<th align="left" style="width:120px;font-weight:700">キャリア </th>
<th align="left" style="width:100px;font-weight:700">キャリア  ID</th>
<th align="left" style="width:120px;font-weight:700">キャリア</th>
<th align="left" style="width:100px;font-weight:700">キャリアID</th>
<th align="left" style="width:120px;font-weight:700">キャリア</th>
</tr>
</thead>
<tbody><tr>
<td>2</td>
<td>チャイナテレコム</td>
<td>26</td>
<td>チャイナユニコム</td>
<td>38</td>
<td>教育サイト</td>
</tr>
</tbody>
<tbody><tr>
<td>43</td>
<td>長城ブロードバンド</td>
<td>1046</td>
<td>チャイナモバイル</td>
<td>3947</td>
<td>中国鉄通</td>
</tr>
</tbody>
<tbody><tr>
<td>-1</td>
<td>海外キャリア</td>
<td>0</td>
<td>その他のキャリア</td>
<td>-</td>
<td>-</td>
</tr>
</tbody>
</table>


#### 海外地域マッピング
<table  style="width:494px">
<thead>
</tr>
<th align="left" style="width:100px;font-weight:700">地域 ID</th>
<th align="left" style="width:170px;font-weight:700">地域</th>
<th align="left" style="width:100px;font-weight:700">地域 ID</th>
<th align="left" style="width:120px;font-weight:700">地域</th>
<th align="left" style="width:100px;font-weight:700">地域 ID</th>
<th align="left" style="width:120px;font-weight:700">地域</th>
</tr>
</thead>
<tbody><tr>
<td>2000000001</td>
<td>アジア太平洋地域1（サービスエリア）</td>
<td>765</td>
<td>スロバキア</td>
<td>1613</td>
<td>アンゴラ</td>
</tr>
</tr>
<td>2000000002</td>
<td>アジア太平洋地域2（サービスエリア）</td>
<td>766</td>
<td>セルビア</td>
<td>1617</td>
<td>コートジボワール</td>
</tr>
</tr>
<td>2000000003</td>
<td>アジア太平洋地域3(サービスエリア）</td>
<td>770</td>
<td>フィンランド</td>
<td>1620</td>
<td>スーダン</td>
</tr>
</tr>
<td>2000000004</td>
<td>中東(サービスエリア)</td>
<td>773</td>
<td>ベルギー</td>
<td>1681</td>
<td>モーリシャス</td>
</tr>
</tr>
<td>2000000005</td>
<td>北米(サービスエリア)</td>
<td>809</td>
<td>ブルガリア</td>
<td>1693</td>
<td>モロッコ</td>
</tr>
</tr>
<td>2000000006</td>
<td>ヨーロッパ(サービスエリア)</td>
<td>811</td>
<td>スロベニア</td>
<td>1695</td>
<td>アルジェリア</td>
</tr>
</tr>
<td>2000000007</td>
<td>南アメリカ(サービスエリア)</td>
<td>812</td>
<td>モルドバ</td>
<td>1698</td>
<td>ギニア</td>
</tr>
<tr>
<td>2000000008</td>
<td>アフリカ（サービスエリア)</td>
<td>813</td>
<td>マケドニア</td>
<td>1730</td>
<td>セネガル</td>
</tr>
</tr>
<td>-20</td>
<td>アジア(クライアント領域)</td>
<td>824</td>
<td>エストニア</td>
<td>1864</td>
<td>チュニジア</td>
</tr>
</tr>
<td>-21</td>
<td> 南アメリカ大陸(クライアント領域)</td>
<td>835</td>
<td>クロアチア</td>
<td>1909</td>
<td>ウルグアイ</td>
</tr>
</tr>
<td>-22</td>
<td>北アメリカ大陸(クライアント領域)</td>
<td>837</td>
<td>ポーランド</td>
<td>1916</td>
<td>グリーンランド</td>
</tr>
</tr>
<td>-23</td>
<td>ヨーロッパ(クライアント領域)</td>
<td>852</td>
<td>ラトビア</td>
<td>2026</td>
<td>中国台湾</td>
</tr>
</tr>
<td>-24</td>
<td>アフリカ(クライアント領域)</td>
<td>857</td>
<td>ヨルダン</td>
<td>2083</td>
<td>ミャンマー</td>
</tr>
</tr>
<td>-25</td>
<td>オセアニア(クライアント領域)</td>
<td>884</td>
<td>キルギスタン</td>
<td>2087</td>
<td>ブルネイ</td>
</tr>
</tr>
<td>35</td>
<td>ネパール</td>
<td>896</td>
<td>アイルランド</td>
<td>2094</td>
<td>スリランカ</td>
</tr>
</tr>
<td>57</td>
<td>タイ</td>
<td>901</td>
<td>リビア</td>
<td>2150</td>
<td>パナマ</td>
</tr>
</tr>
<td>73</td>
<td>インド</td>
<td>904</td>
<td>アルメニア</td>
<td>2175</td>
<td>コロンビア</td>
</tr>
</tr>
<td>144</td>
<td>ベトナム</td>
<td>921</td>
<td>イエメン/td>
<td>2273</td>
<td>モナコ</td>
</tr>
</tr>
<td>192</td>
<td>フランス</td>
<td>926</td>
<td>ベラルーシ</td>
<td>2343</td>
<td>アンドラ</td>
</tr>
</tr>
<td>207</td>
<td>イギリス</td>
<td>971</td>
<td>ルクセンブルク</td>
<td>2421</td>
<td>トルクメニスタン</td>
</tr>
</tr>
<td>208</td>
<td>スウェーデン</td>
<td>1036</td>
<td>ニュージーランド</td>
<td>2435</td>
<td>ラオス</td>
</tr>
</tr>
<td>209</td>
<td>ドイツ</td>
<td>1044</td>
<td>日本</td>
<td>2488</td>
<td>東ティモール</td>
</tr>
</tr>
<td>213</td>
<td>イタリア</td>
<td>1066</td>
<td>パキスタン</td>
<td>2490</td>
<td>トンガ</td>
</tr>
</tr>
<td>214</td>
<td>スペイン</td>
<td>1070</td>
<td>マルタ</td>
<td>2588</td>
<td>フィリピン</td>
</tr>
</tr>
<td>386</td>
<td>アラブ首長国連邦</td>
<td>1091</td>
<td>バハマ</td>
<td>2609</td>
<td>ベネズエラ</td>
</tr>
</tr>
<td>391</td>
<td>イスラエル</td>
<td>1129</td>
<td>アルゼンチン</td>
<td>2612</td>
<td>ボリビア</td>
</tr>
</tr>
<td>397</td>
<td>ウクライナ</td>
<td>1134</td>
<td>バングラデシュ</td>
<td>2613</td>
<td>ブラジル</td>
</tr>
</tr>
<td>398</td>
<td>ロシア</td>
<td>1158</td>
<td>カンボジア</td>
<td>2623</td>
<td>コスタリカ</td>
</tr>
</tr>
<td>417</td>
<td>カザフスタン</td>
<td>1159</td>
<td>中国マカオ</td>
<td>2626</td>
<td>メキシコ</td>
</tr>
</tr>
<td>428</td>
<td>ポルトガル</td>
<td>1176</td>
<td>シンガポール</td>
<td>2639</td>
<td>ホンジュラス</td>
</tr>
</tr>
<td>443</td>
<td>ギリシャ</td>
<td>1179</td>
<td>モルディブ</td>
<td>2645</td>
<td>エルサルバドル</td>
</tr>
</tr>
<td>471</td>
<td>サウジアラビア</td>
<td>1180</td>
<td>アフガニスタン</td>
<td>2647</td>
<td>パラグアイ</td>
</tr>
</tr>
<td>529</td>
<td>デンマーク</td>
<td>1185</td>
<td>フィジー</td>
<td>2661</td>
<td>ペルー</td>
</tr>
</tr>
<td>565</td>
<td>イラン</td>
<td>1186</td>
<td>モンゴル</td>
<td>2728</td>
<td>ニカラグア</td>
</tr>
</tr>
<td>578</td>
<td>ノルウェー</td>
<td>1195</td>
<td>インドネシア</td>
<td>2734</td>
<td>エクアドル</td>
</tr>
</tr>
<td>669</td>
<td>アメリカ</td>
<td>1200</td>
<td>中国香港</td>
<td>2768</td>
<td>グアテマラ</td>
</tr>
</tr>
<td>692</td>
<td>シリア</td>
<td>1233</td>
<td>カタール</td>
<td>2999</td>
<td>アルバ</td>
</tr>
</tr>
<td>704</td>
<td>キプロス</td>
<td>1255</td>
<td>アイスランド</td>
<td>3058</td>
<td>エチオピア</td>
</tr>
</tr>
<td>706</td>
<td>チェコ</td>
<td>1289</td>
<td>アルバニア</td>
<td>3144</td>
<td>ボスニア</td>
</tr>
</tr>
<td>707</td>
<td>スイス/td>
<td>1353</td>
<td>ウズベキスタン</td>
<td>3216</td>
<td>ドミニカ</td>
</tr>
</tr>
<td>708</td>
<td>イラク</td>
<td>1407</td>
<td>サンマリノ</td>
<td>3379</td>
<td>韓国</td>
</tr>
</tr>
<td>714</td>
<td>オランダ</td>
<td>1416</td>
<td>クウェート</td>
<td>3701</td>
<td>マレーシア</td>
</tr>
</tr>
<td>717</td>
<td>ルーマニア</td>
<td>1417</td>
<td>モンテネグロ</td>
<td>3839</td>
<td>カナダ</td>
</tr>
</tr>
<td>721</td>
<td>レバノン</td>
<td>1493</td>
<td>タジキスタン</td>
<td>4450</td>
<td>オーストラリア</td>
</tr>
</tr>
<td>725</td>
<td>ハンガリー</td>
<td>1501</td>
<td>バーレーン</td>
<td>4460</td>
<td>中国大陸</td>
</tr>
</tr>
<td>726</td>
<td>ジョージア</td>
<td>1543</td>
<td>チリ</td>
<td>-15</td>
<td>アジアその他</td>
</tr>
</tr>
<td>731</td>
<td>アゼルバイジャン</td>
<td>1559</td>
<td>南アフリカ</td>
<td>-14</td>
<td>南アメリカ大陸その他</td>
</tr>
</tr>
<td>734</td>
<td>オーストリア</td>
<td>1567</td>
<td>エジプト</td>
<td>-13</td>
<td> 北アメリカ大陸その他</td>
</tr>
</tr>
<td>736</td>
<td>パレスチナ</td>
<td>1590</td>
<td>ケニア</td>
<td>-12</td>
<td>ヨーロッパその他</td>
</tr>
</tr>
<td>737</td>
<td>トルコ</td>
<td>1592</td>
<td>ナイジェリア</td>
<td>-11</td>
<td>アフリカその他</td>
</tr>
</tr>
<td>759</td>
<td>リトアニア</td>
<td>1598</td>
<td>タンザニア</td>
<td>-10</td>
<td>オセアニアその他</td>
</tr>
</tr>
<td>763</td>
<td>オマーン</td>
<td>1611</td>
<td>マダガスカル</td>
<td>-2</td>
<td>海外その他</td>
</tr>
</tbody></table>


#### 海外キャリアマッピング
<table  style="width:494px">
<thead>
</tr>
<th align="left" style="width:100px;font-weight:700">キャリアID</th>
<th align="left" style="width:120px;font-weight:700">キャリア</th>
</tr>
</thead>
<tbody><tr>
<td>-1</td>
<td>海外キャリア</td>
</tr>
</tbody>
<table>

### 注意事項
アクセスログの5番目のフィールドに記録されたバイト数に基づいて、計算されたトラフィック/帯域幅データは、CDN課金トラフィック/帯域幅データと一致しません。その理由は次のとおりです。
- アクセスログにはアプリケーション層のデータのみが記録されており、実際のネットワーク転送では、生成されるネットワークトラフィックは純粋なアプリケーション層のトラフィックよりも5％〜15％多くなります。トラフィックは2つの部分で構成されています。
	-TCP/IPパケットヘッダの消費：TCP/IPプロトコルに基づくHTTPリクエストでは、各パケットのサイズは最大1500バイトであり、TCPとIPプロトコルの40バイトのパケットヘッダが含まれます。パケットヘッダ部分にトラフィックが生成しますが、アプリケーション層にカウントされません。この部分のオーバーヘッドは約3%です。
	-TCP再送信：通常のネットワーク転送中、送信されるネットワークパケットは3%～10%ぐらいがインターネットによって廃棄されます。サーバーは廃棄された部分を再送信しますが、アプリケーション層はこの部分にかかったトラフィックをカウントできません。比率は約3%～7%です。
業界標準では、課金用トラフィックは、一般的にアプリケーション層がカウントしたトラフィックに上記のオーバーヘッドを加えます。Tencent Cloud CDNは10%を取りますので、モニタリングトラフィックがログコンピューティングトラフィックの110%程度となります。

## 利用事例

### 中国国内アクセスログの例
![](https://mc.qcloudimg.com/static/img/a3ef1ea051dc277872ec10a7135872df/logs.png)

### 海外アクセスログの例
![](https://main.qcloudimg.com/raw/b0612a5204abdbdc6a4364ad02972900.png)
