## ライブストリーミングの課金に関する事項

[](id:live_que1)
### CSSにはどのような課金項目がありますか。支払うべき料金は、どうすればわかりますか。
CSSの課金項目には、基本サービス料金と付加価値サービス料金が含まれます。Tencent Cloudのその他製品と連携させて提供する付加価値機能には、拡張サービス料金が発生します。

- **基本サービス料金**：トラフィック/帯域幅は基本サービス料金です。これはすなわち、お客様とアクセラレーションオリジンサーバー間の接続を確立することによって発生するダウンストリーム料金で、お客様のライブストリーミングコンテンツがユーザーによって視聴されている限り、トラフィック/帯域幅の料金が発生すると考えて差し支えありません。
>?トラフィック課金と帯域幅課金のどちらかを選択してください。単価の詳細については、[トラフィック帯域幅課金](https://intl.cloud.tencent.com/document/product/267/2818)をご参照ください。切り替え方法については、[課金の切り替え](https://intl.cloud.tencent.com/document/product/267/30411)をご参照ください。
- **付加価値サービス料金**：トランスコード、レコーディング、スクリーンキャプチャ、ポルノ検出が含まれます。上記の4つの機能はデフォルトでは無効になっており、有効にして使用すると、対応する料金が発生します。詳細な単価については、[付加価値サービス料金](https://intl.cloud.tencent.com/document/product/267/2819)をご参照ください。
- **拡張サービス料金**：Tencent Cloudのその他製品と組み合わせて提供される付加価値機能については、その他のクラウド製品がそれぞれの課金ルールに従って個別に請求します。付加価値機能を使用すると、拡張サービス料金が発生します。詳細な単価については、[拡張サービス料金](https://intl.cloud.tencent.com/document/product/267/2819)をご参照ください。

[](id:live_que2)
### 支払いが延滞しているかどうか、どうすればわかりますか。
[Tencent Cloud CSSコンソール](https://console.cloud.tencent.com/live)にログインして、右上の【料金】をクリックすると、料金概要ページに進めます。利用可能な残高が0米ドル未満の場合、支払い延滞の状態です。CSSやその他のサービスに影響を与えないよう、速やかにチャージしてください。

[](id:live_que3)
### CSSのアップストリームプッシュは、どのように課金されますか。
CSSのアップストリームプッシュに料金はかからず、ダウンストリームトラフィックの料金だけがかかります。

[](id:live_que4)
### 付加価値サービス料金の計算はいつ開始されますか。
レコーディング、スクリーンキャプチャ、ポルノ検出、ウォーターマークなど、プッシュドメイン名に関する付加価値サービスについては、プッシュがオンになった時点から課金が開始されます。トランスコードなど再生ドメイン名に関する付加価値サービスは、プルストリームが開始された時点から課金が開始されます（トランスコードテンプレートが作成され関連付けられた時点のことです。プルストリームでない場合、トランスコード料金は発生しません）。クラウドミクスストリーミングはミクスストリーミングタスクが開始されると課金を開始します。ウォーターマークの追加またはクラウドミクスストリーミング機能をオンにすると、標準トランスコード料金が発生する場合があります。解像度は、お客様の出力するCSSストリームの解像度に左右されます。



## トランスコードの課金に関する事項

[](id:tran_que1)
### CSSトランスコードの料金はどのように課金しますか。トランスコード料金はどうやって見積もるのでしょうか。
CSSトランスコードは、実際のトランスコードのコーデック、解像度および対応する所要時間に応じて課金されます。ライブミクスストリーミングとウォーターマークの追加は、どちらもトランスコードモジュールによって処理されるため、トランスコード料金が発生します。詳細については、[CSSトランスコード課金](https://intl.cloud.tencent.com/document/product/267/39604)をご参照ください。
同じCSSストリーム、同じビットレートで複数の人が視聴している場合、1つのトランスコード料金のみが請求されます。

**例：**2021年1月1日にCSSトランスコードとウォーターマークサービスを利用する場合、そのうちライブストリーミングのストリームAのトランスコーディングがH.264_720P（所要時間1時間）で、ライブストリーミングのストリームBにウォーターマークを追加（所要時間30min、解像度480P）するとします。
その場合、2021年1月2日に支払うべきCSSトランスコード料金は、次のようになります。
0.0057（米ドル/分）× 60（分）+ 0.0028（米ドル/分）× 30（分）= 0.426 米ドル。

[](id:tran_que2)
### CSSトランスコードを使用しませんでしたが、トランスコード請求書が発行されるのはなぜですか。
CSSトランスコードには、ライブストリーミング・リアルタイムトランスコード、クラウドミクスストリーミングおよびウォーターマークの追加という3種類があります。クラウドミクスストリーミングまたはウォーターマークの追加機能を使用すると、トランスコード請求書も発行されます。

[](id:tran_que3)
### ライブミクスストリーミングには必ずトランスコード料金がかかりますか。
かかります。トランスコード料金は、ミクスストリーミング後の出力CSSストリームに応じて課金されます。ミクスストリーミングタスクが成功した後は、再生しなくてもトランスコードリソースを消費するため、ミクスストリーミングのトランスコード料金は、一般的なトランスコードの再生時間の課金とは異なり、ミクスストリーミングの所要時間に応じて課金されます。



## レコーディング課金に関する事項
[](id:record_que1)
### CSSのレコーディング料金は、どのように課金されますか。
CSSのレコーディング機能の課金は、その月の同時レコーディングのピーク値に基づいており、統計期間中のレコーディングチャネル数の合計が同時ピークチャネル数となります。1つのCSSストリームは、1つのファイル、1つのチャネルとしてレコーディングされます。2つの形式（MP4とHLS）でレコーディングする場合、2つのチャネルとしてレコーディングされます。

[](id:record_que2)
### CSSレコーディングのチャネルピーク数はどのように計算すればよいですか。
1チャネルのCSSストリーム（1つのストリームID）は1種類の形式のファイル、すなわち1チャネルのCSSレコーディングタスクをレコーディングします。現在のレコーディングタスク数は5分ごとにクエリーされ、その月のサンプリングポイントの最大値がレコーディング課金を行うときのチャネル数月間ピーク値となります。
**事例：**

<style>#ye{background:#ffe699;}#gr{background:#c6e0b4;}#br{background:#bdd7ee}</style>
<table id="rroad">
<tr><th rowspan=2 width="10%" style="text-align:center;">ストリームID</th>
<tr><th rowspan=2 width="10%" style="text-align:center;">レコーディング<br>ファイル形式</th>
<th colspan=7 width="50%" style="text-align:center;">当月（01日～30日）</th>
</tr><tr>
<td style="text-align:center;">01日</td><td style="text-align:center;">02日</td><td style="text-align:center;">03日</td>
<td style="text-align:center;">……</td>
<td style="text-align:center;">28日</td><td style="text-align:center;">29日</td><td style="text-align:center;">30日</td>
</tr><tr>
<td rowspan=4 style="text-align:center;">A</td>
<td style="text-align:center;">HLS</td><td></td><td></td><td></td>
<td rowspan=13 style="text-align:center;">レコーディング未実施</td>
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
<td colspan=2 style="text-align:center;">レコーディングチャネル数</td>
<td style="text-align:center;">5</td><td style="text-align:center;">7</td><td style="text-align:center;">6</td><td style="text-align:center;">11</td><td style="text-align:center;">6</td><td style="text-align:center;">5</td>
</tr><tr>
<td colspan=2 style="text-align:center;">レコーディングチャネル数ピーク値</td><td colspan=7 style="text-align:center;">11</td>
</tr>
</table>

>? 
>- 黄色：ストリームID**A**でのレコーディングタスクを表します。
>- 緑色：ストリームID**B**でのレコーディングタスクを表します。
>- 青色：ストリームID**C**でのレコーディングタスクを表します。




[](id:record_que3)
### CSSレコーディング機能を使用すると、10.5882米ドルが差し引かれるのはなぜですか。 
2つのライブストリーミングが同時にレコーディングされるか、または1つのライブストリームに対して2つのレコーディングファイル形式が有効になっている場合、2つのレコーディングチャネルが生成されます。レコーディングは、レコーディングチャネル数ピーク値（1チャネルの月額5.2941米ドル）に応じて課金されます。その月のCSSレコーディングのピーク値が2時間の場合、10.5882米ドルの料金が差し引かれます。具体的な課金の詳細については、[CSSレコーディング課金](https://intl.cloud.tencent.com/document/product/267/39605)をご参照ください。
料金センターの【請求書明細】>[【リソースID請求書】](https://console.cloud.tencent.com/expense/bill/summary)にアクセスして、CSSレコーディングの請求書の状況を確認することをお勧めします。操作バーの【請求書明細】をクリックして進むと、前月の実際のピークレコーディングチャネル数が確認できます。

