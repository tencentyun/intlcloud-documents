## CSS課金

<span id="live_que1"></span>
### CSSにはどのような課金項目がありますか。支払う料金を知るにはどうすればよいですか。
CSSの課金対象項目には、基本料金と付加価値料金が含まれます。

- 基本料金：トラフィック/帯域幅料金は基本課金となります。すなわち、ユーザーをアクセラレーションオリジンサーバーに接続することによって生成される下りトラフィック/帯域幅の料金です。CSSコンテンツが視聴される限り、トラフィック/帯域幅の料金が発生すると捉えられます。
>?トラフィック課金または帯域幅課金から選択できます。価格の詳細については、 [Billing Details](https://intl.cloud.tencent.com/document/product/267/2818#traffic-and-bandwidth)，課金方法を切り替える方法については、[Billing Method Change](https://intl.cloud.tencent.com/document/product/267/30411)をご参照ください。
- 付加価値料金：トランスコーディング、レコーディング、スクリーンキャプチャ、ポルノ検出の料金で構成されます。これらの4つの機能はデフォルトで無効になっています。それらを有効にして使用すると、対応する料金が発生します。単価の詳細については、[Billing Details](https://intl.cloud.tencent.com/document/product/267/2818#lvb-transcoding)をご参照ください。

<span id="live_que2"></span>
### 支払い延滞しているかどうかはどのように分かりますか。
[CSS Console](https://console.cloud.tencent.com/live)にログインし、右上の【Fees】クリックして、料金の概要ページに入ります。利用可能な残高が0ドル未満の場合は、支払い延滞の状態となります。CSSなどのサービスに影響を与えないように、時間内に入金してください。

<span id="live_que3"></span>
### CSSの上りプッシュは課金されますか。
CSSの上りプッシュは課金されません。下りトラフィックに対してのみ課金されます。

<span id="live_que4"></span>
### 付加価値サービスはいつ計算されますか。
レコーディング、ウオーターマーク、スクリーンキャプチャ、ポルノ検出など、プッシュドメイン名に関連付られる付加価値サービスは、有効にしてプッシュすると、課金が開始されます。ドメイン名に関連付けられているトランスコーディングなどの付加価値サービスは、プル再生が開始された時点から課金が開始されます（すなわち、トランスコーディングテンプレートが作成されてドメイン名に関連付けられて、プル再生を開始しない場合、トランスコーディング料金は発生しません）。クラウドストリームミキシングは、ストリームミキシングタスクが開始された時点から課金されます。ウォーターマークまたはクラウドストリームミキシング機能を有効にした場合、標準トランスコーディング料金が発生する場合があります、解像度は出力されるライブストリームの解像度になります。



## トランスコーディング課金

<span id="tran_que1"></span>
### CSSトのトランスコーディングはどのように課金されますか。トランスコーディング料金の見積もり方法とは何ですか。
CSSトランスコーディングは、実際に使用されているトランスコーディングのコーデック方式、解像度、およびトランスコーディングの期間に基づいて課金されます。CSSストリームミキシングとウオーターマーク追加もトランスコーディングモジュールによって処理されるため、トランスコーディング料金が発生します。詳細については、[CSS Transcoding](https://intl.cloud.tencent.com/document/product/267/2818#lvb-transcoding)をご参照ください。
同じCSSストリームを同じビットレートで複数名で視聴される場合、1つのトランスコーディング料金のみが課金されます。

<span id="tran_que2"></span>
### CSSトランスコーディングを使用しませんでしたが、トランスコーディング課金書が発行されるのはなぜですか。
CSSストリーミングトランスコーディングには、CSSリアルタイムトランスコーディング、クラウドストリームミックス、およびウォーターマークが含まれます。ストリームミックスまたはウォーターマーク機能を使用すると、トランスコーディング料金も発生します。

<span id="tran_que3"></span>
### CSSストリームミックスには必ずトランスコーディング料金が発生しますか。
はい。トランスコーディング料金は、ストリームミックス後のCSSストリーム出力に基づいて課金されます。ストリームミックスタスクが正常に完了してから再生しない場合でも、トランスコーディングリソースが使用されるため、ストリームミックスのトランスコーディング料金は、通常トランスコーディングの再生時間による課金とは異なり、ストリームミックス期間によって課金されます。



## レコーディング課金
<span id="record_que1"></span>
### CSSレコーディングはどのように課金されますか 
CSSのレコーディング機能の課金は、当月の同時レコーディングのピークに基づいており、統計期間のレコーディングチンネル数の合計が同時チャンネル数のピークになります。1つのCSSストリームレコーディングは1種類のファイルで、1チャンネルとしてレコーディングされます。2つの形式（MP4とHLS）でレコーディングされる場合は、2チャンネルとしてレコーディングされます。

<span id="record_que2"></span>

### CSSレコーディングチャンネルのピーク数をどのように計算しますか。
1チャンネルのCSSストリーム（1つのストリームID）が1つのファイル形式でレコーディングされ、すなわち、1チャンネルのCSSレコーディングタスクとなります。現在のレコーディングチャンネル数は5分ごとにクエリーされ、当月のサンプルポイントの最大値がレコーディング課金のチャンネル数の月間ピーク値とします。
**課金例：**

<style>#ye{background:#ffe699;}#gr{background:#c6e0b4;}#br{background:#bdd7ee}</style>
<table id="rroad">
<tr><th rowspan=2 width="10%" style="text-align:center;">ストリームID</th>
<th rowspan=2 width="10%" style="text-align:center;"レコーディング<br>ファイル形式</th>
<th colspan=7 width="50%" style="text-align:center;">当月（01日～30日）</th>
</tr><tr>
<td style="text-align:center;">01日</td><td style="text-align:center;">02日</td><td style="text-align:center;">03日</td>
<td style="text-align:center;">……</td>
<td style="text-align:center;">28日</td><td style="text-align:center;">29日</td><td style="text-align:center;">30日</td>
</tr><tr>
<td rowspan=4 style="text-align:center;">A</td>
<td style="text-align:center;">HLS</td><td></td><td></td><td></td>
<td rowspan=13 style="text-align:center;">レコーディングしていない</td>
<td id="ye"></td><td id="ye"></td>
<td></td>
</tr><tr>
<td style="text-align:center;">MP4</td><td id="ye"></td><td id="ye"></td><td id="ye"></td><td id="ye"></td><td id="ye"></td><td id="ye"></td>
</tr><tr>
<td style="text-align:center;">FLV</td><td id="ye"></td><td id="ye"></td><td id="ye"></td><td id="ye"></td><td id="ye"></td><td></td>
</tr><tr>
<td style="text-align:center;">AAC</td><td id="ye"></td><td id="ye"></td><td id="ye"></td><td id="ye"></td><td id="ye"></td><td id="ye"></td>
</tr><tr>
<td rowspan=4 style="text-align:center;">B</td>
<td style="text-align:center;">HLS</td><td></td><td id="gr"></td><td id="gr"></td><td id="gr"></td><td></td><td></td>
</tr><tr>
<td style="text-align:center;">MP4</td><td id="gr"></td><td id="gr"></td><td></td><td id="gr"></td><td id="gr"></td><td></td>
</tr><tr>
<td style="text-align:center;">FLV</td><td></td><td id="gr"></td><td></td><td id="gr"></td><td></td><td id="gr"></td>
</tr><tr>
<td style="text-align:center;">AAC</td><td></td><td id="gr"></td><td></td><td id="gr"></td><td></td><td></td>
</tr><tr>
<td rowspan=4 style="text-align:center;">C</td>
<td style="text-align:center;">HLS</td><td id="br"></td><td></td><td id="br"></td><td id="br"></td><td></td><td></td>
</tr><tr>
<td style="text-align:center;">MP4</td><td></td><td></td><td id="br"></td><td id="br"></td><td id="br"></td><td id="br"></td>
</tr><tr>
<td style="text-align:center;">FLV</td><td></td><td></td><td></td><td id="br"></td><td></td><td></td>
</tr><tr>
<td style="text-align:center;">AAC</td><td></td><td></td><td></td><td></td><td></td><td id="br"></td>
</tr><tr>
<td colspan=2 style="text-align:center;">レコーディングチャンネル数</td>
<td style="text-align:center;">5</td><td style="text-align:center;">7</td><td style="text-align:center;">6</td><td style="text-align:center;">11</td><td style="text-align:center;">6</td><td style="text-align:center;">5</td>
</tr><tr>
<td colspan=2 style="text-align:center;">レコーディングチャンネル数のピーク</td><td colspan=7 style="text-align:center;">11</td>
</tr>
</table>

>? 
>-  黄色：ストリームID **A**でのレコーディングタスクを表します。
>-  緑色：ストリームID **B**でのレコーディングタスクを表します。
>-  青色：ストリームID **C**でのレコーディングタスクを表します。


