CDNはお客様のために**帯域幅課金**と**トラフィック課金**の2種類の課金方式を提供しいます。いずれの方式も**後払いの日割り課金**であり、即ち当日の00:00:00 - 23:59:59 の合計消費量は翌日に課金されることです。

## 帯域幅課金
### 階層価格
CDNの帯域幅課金は階層到達モードを採用しています。階層価格は下記の通りです。
<table  style="width:494px">
	<thead>
		<tr>
			<th scope="col" style="width: 145px;">課金モード</th>
			<th scope="col" style="width: 154px;">帯域幅の階層</th>
			<th scope="col" style="width: 180px;">単価（ドル/Mbps/日）</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td colspan="1" rowspan="4" style="text-align: center; width: 145px;">帯域幅のピーク値</td>
			<td style="text-align: center; width: 154px;">0-500Mbps</td>
			<td style="text-align: center; width: 180px;">0.094</td>
		</tr>
		<tr>
			<td style="text-align: center; width: 154px;">500Mbps-5Gbps</td>
			<td style="text-align: center; width: 180px;">0.092</td>
		</tr>
		<tr>
			<td style="text-align: center; width: 154px;">5Gbps-50Gbps</td>
			<td style="text-align: center; width: 180px;">0.086</td>
		</tr>
		<tr>
			<td style="text-align: center; width: 154px;">50Gbps以上</td>
			<td style="text-align: center; width: 180px;">0.084となり、もしくはオフラインの相談により、契約価格に準じます</td>
		</tr>
	</tbody>
</table>


### 計算方式
仮に前日 CDN のピーク値である帯域幅がXとする場合は、階層な計算方式は下記の通りです。
1. X < 500 Mbpsの場合は、請求書の費用は X \* 0.094となります。
2. 500 Mbps <= X < 5000 Mbpsの場合は、請求書の費用は X \* 0.092となります。
3. 5000 Mbps <= X < 50000Mbpsの場合は、請求書の費用は X \* 0.086となります。
4. X >= 50000Mbpsの場合は、オフラインの契約締結につきご連絡ください。もっと多くの特恵方法を選択することができます。



## トラフィック課金
### 階層価格
CDNのトラフィック課金は月度ごとに階層累進決算となります。階層価格は下記の通りです。
<table  style="width:494px">
	<thead>
		<tr>
			<th scope="col" style="width:98px">課金モード</th>
			<th scope="col" style="width: 170px;">トラフィックの階層</th>
			<th scope="col" style="width: 189px;">単価（ドル/GB）</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td colspan="1" rowspan="5" style="text-align:center; width:98px">月間流量</td>
			<td style="text-align: center; width: 170px;">0GB-2TB</td>
			<td style="text-align: center; width: 189px;">0.037</td>
		</tr>
		<tr>
			<td style="text-align: center; width: 170px;">2TB-10TB</td>
			<td style="text-align: center; width: 189px;">0.035</td>
		</tr>
		<tr>
			<td style="text-align: center; width: 170px;">10TB-50TB</td>
			<td style="text-align: center; width: 189px;">0.032</td>
		</tr>
		<tr>
			<td style="text-align: center; width: 170px;">50TB-100TB</td>
			<td style="text-align: center; width: 189px;">0.026</td>
		</tr>
		<tr>
			<td style="text-align: center; width: 170px;">大于等于 100TB</td>
			<td style="text-align: center; width: 189px;">0.020となり、もしくはオフラインの相談により、契約価格に準じます</td>
		</tr>
	</tbody>
</table>


### 計算方式
トラフィック課金は帯域幅課金とは違い、月度ごとのトラフィックにより階層に累進します。計算例は下記の通りです。
+  1 月 1 日のトラフィックが3TBである場合は、下図の通りです。図中の灰色部分は実際の課金階層であり、緑色部分は1 月 1 日のトラフィックです。そのうち、 2TB は 0TB-2TB の課金段階、1TB は 2TB-10TB の課金階層となるため、 1 月 1 日の実際費用は2 \* 1000 \* 0.037 + 1 \* 1000 \* 0.035となります。
  ![](https://mc.qcloudimg.com/static/img/bfdae242f6cca57421a65e46a96b0c67/image.png)

+  1 月 2 日のトラフィックも 3TBである場合は、下図の通りです。トラフィックは月度ごとの累進で課金されるため、 1 月 2 日のトラフィックは全部 2TB-10TB の課金階層に該当されるため、 1 月 2 日の実際費用は3 \* 1000 \* 0.035となります。
  ![](https://mc.qcloudimg.com/static/img/f62d1056c1c2cab249cec62ad6e74ddc/image.png)

階層+  1 月 3 日のトラフィックが 7TB である場合は、下図の通りです。この場合は、3日的 7TB のうち、 4TB は 2TB-10TB の課金階層、3TB は 10TB-50TB の課金階層となるため、 1 月 3 日の実際費用は4 \* 1000 \* 0.035 + 3 \* 1000 \* 0.032となります。
  ![](https://mc.qcloudimg.com/static/img/954e2d483e31afd411f9a91ebd7f66c8/image.png)

これにより類推し、当月の毎日の費用を計算します。 2 月 1 日から課金開始になると、階層累計が新しく始まります（すべては0から始まる）。

## 大口お客様の課金に関する説明
お客様はTencent Cloudにおける月間消費金額が既に2万ドル以上となっている場合は、或いはその見込みがある場合は、お客様はビジネス相談により、もっと優遇的な価格や月間決算など、より柔軟的な課金方式を取得することが可能です。

+ **毎日ピーク帯域幅の月間平均値**：CDN は每日の帯域幅統計ポイントが288個であり、有効日ごとにピーク値の平均をとることにより課金帯域幅を取得してから、契約価格により費用を計算します。
> 計算例：
> お客様は 2017 年 2 月 1 日 から正式に課金され、契約価格がP ドル/Mbps/月です
> 有効日：消費量が1 Kbps以上の場合、有効日とします
> 仮に2月の14日間の消費量が1Kbps以上の場合は、この14日間の各日における288個の統計ポイントの最大値がMax_1、Max_2、Max_3... Max_14であり、課金帯域幅が Average(Max_1, Max_2, ..., Max_14)であると、2月の費用がAverage(Max_1, Max_2, ..., Max_14)  x  P  x  14 / 28となります

+ **月間 95 帯域幅**：CDNは每日の帯域幅統計ポイントが288個であり、当月の1日から、各有効日（消費量がある）のすべての統計ポイントを並べ替え、最大の5%の統計ポイントを取り除いた後に、残った最大の統計ポイントを課金帯域幅とし、契約価格により費用を計算します。
> 計算例：
> お客様は 2017 年 2 月 1 日から正式に課金され、契約価格がP ドル/Mbps/月です
> 有効日：消費量が 1 Kbps以上の場合、有効日とします
> 仮にお客様は2月には14日間の消費量が1Kbps以上の場合は、課金帯域幅がこの14日間のすべての統計ポイント（14 \* 288個）から、最大の5%のポイントを取り除いた後に、残った統計ポイント（ Max95，Max95）を課金帯域幅とし、2月の費用がMax95 x P x 14 / 28です

+ **月間トラフィック量**：月度の累計使用トラフィックです。契約価格により費用を計算します。

 [作業依頼書のサブミット](https://console.cloud.tencent.com/workorder/category/create?level1_id=83&level2_id=85&level1_name=%E5%AD%98%E5%82%A8%E4%B8%8ECDN&level2_name=%E5%86%85%E5%AE%B9%E5%88%86%E5%8F%91%E7%BD%91%E7%BB%9C%20%20CDN) で詳細をお問い合わせください。

## 課金モードの選択
CCDNはお客様のために**トラフィック課金**と**帯域幅課金**の2種類の課金方式を提供しいます。お客様はサービス状況に応じて適切な課金モードを選択することができます。また、帯域幅利用率を計算することにより適切な課金モードを選択することが可能です。帯域幅利用率の計算例は下記の通りです。
仮にお客様は昨日 00:00 - 24:00 の消費トラフィックが200GBとすると、曲線グラフが下記の通りです。この場合の消費トラフィックは図中の曲線の占めている面積です。
![](https://mc.qcloudimg.com/static/img/3ecfe86a031782ebeaf0b1f7595cc69f/image.png)
仮にお客様は昨日 00:00 - 24:00 の帯域幅のピーク値が40Mbpsである場合は、1日が86400秒であるため、1日のトラフィックが 40 \* 1000 \* 86400です。単位をGBに換算すれば432GBとなります。即ち図中の長方形の面積です。
![](https://mc.qcloudimg.com/static/img/b80d043b6e7f461d62fd2d87abf67005/image.png)
この場合の帯域幅利用率が200GB / 432GB * 100% = 46%です。

**選択方法：**
+ お客様の帯域幅利用率が50%以上である場合、サービスの曲線は穏やかであるため、帯域幅課金モードの採用をお勧めします。
+ お客様の帯域幅利用率が50%以下である場合、サービスの曲線は波動が大きいため、トラフィック課金モードの採用をお勧めします。
