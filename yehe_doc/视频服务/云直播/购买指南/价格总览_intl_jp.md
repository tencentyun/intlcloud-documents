>? [CSS価格計算ツール](https://buy.cloud.tencent.com/price/css/calculator)によって、LVBおよびLEBの関連料金の見積を行うことができます。

CSSの課金項目には、基本サービス料金と付加価値サービス料金が含まれます。Tencent Cloudのその他製品と連携させて提供する付加価値機能には、拡張サービス料金が発生します。料金の構成は下図のとおりです。

![](https://qcloudimg.tencent-cloud.cn/raw/7970d2961c95cd19a4e7568f3ea60467.png)


- [基本サービス料金](#base)：ライブストリーミング（LVB、LEB）の使用後に発生するライブストリーミング消費料金。LVBとLEBでは、トラフィックまたは帯域幅ピーク値という2種類の課金方式を切り替えることができますが、ライブカメラストリーミングはトラフィック課金のみに対応しています。
- [付加価値サービス料金](#appreciation)：ライブストリーミングトランスコーディング、レコーディング、タイムシフト、スクリーンキャプチャ、ポルノ検出、プルリツイートなどの付加価値機能を使用した時の料金。これらの機能はデフォルトでは無効になっており、使用する場合のみ課金されます。
- [拡張サービス料金](#extensions)：他のTencent Cloud製品と連携させて提供する付加価値機能は、他のクラウド製品では、それぞれの課金ルールに従って、別途関連料金が課金されます。

[](id:base)
## 基本サービス料金

基本サービス料金は、ライブストリーミングサービスによって、LVBサービス料金、LEBサービス料金、ライブカメラストリーミング料金に分かれます。

<table>
<tr><th width="20%">課金項目</th><th width="60%">課金説明</th><th>支払い方法</th></tr>
<tr>
<td>LVBトラフィック<br>（デフォルト）</td>
<td>
<li/>LVBのプッシュストリームおよびプルストリームで発生するアップリンクおよびダウンリンクのトラフィック消費は、デフォルトではダウンリンクの再生料金のみかかります。
<li/>中国本土、中国本土以外の課金標準はそれぞれ異なります。
</td>
<td>
<li><a href="https://www.tencentcloud.com/document/product/267/52220#live_pag">前払いリソースパッケージ</a></li>
<li><a href="https://intl.cloud.tencent.com/document/product/267/2818">後払い-日次決済</a></li>
<li/>後払い-月次決済
</td>
</tr><tr>
<td>LVBの帯域幅ピーク値</td>
<td>
<li/>LVBのプッシュストリームおよびプルストリームで発生するアップリンクおよびダウンリンクの帯域幅ピーク値は、デフォルトではダウンリンクの再生料金のみかかります。
<li/>中国本土、中国本土以外の課金標準はそれぞれ異なります。
</td><td>
<li/><a href="https://intl.cloud.tencent.com/document/product/267/2818">後払い-日次決済</a>
<li/>後払い-月次決済
</td>
</tr><tr>
<td>LEBトラフィック<br>（デフォルト）</td>
<td>
<li/>LEBのプッシュストリームおよびプルストリームで発生するアップリンクおよびダウンリンクのトラフィック消費は、デフォルトではダウンリンクの再生料金のみかかります。
<li/>中国本土、中国本土以外の課金標準はそれぞれ異なります。
</td>
<td>
<li/><a href="https://www.tencentcloud.com/document/product/267/52220#live_pag">前払いリソースパッケージ</a>
<li/><a href="https://intl.cloud.tencent.com/document/product/267/39969">後払い-日次決済</a>
<li/>後払い-月次決済
</td>
</tr><tr>
<td>LEB帯域幅ピーク値</td>
<td>
<li/>LEBのプッシュストリームおよびプルストリームで発生するアップリンクおよびダウンリンクの帯域幅ピーク値は、デフォルトではダウンリンクの再生料金のみかかります。
<li/>中国本土、中国本土以外の課金標準はそれぞれ異なります。
</td>
<td>
<li/><a href="https://intl.cloud.tencent.com/document/product/267/39969">後払い-日次決済</a>
<li/>後払い-月次決済
</td>
</tr></table>

>! 
>- LEBは超低遅延リンクを採用しているため、トラフィック/帯域幅料金はLVBより若干高くなります。
>- CSSでは、毎月のニーズが高いユーザーに対して、より柔軟な月次決済方式を提供しています。 必要な場合は、Tencent Cloudのビジネスマネージャーに連絡して、課金方式の変更をサポートしてもらうことができます。
>- 課金方式を選択し直す必要がある場合は、[課金の変更](https://intl.cloud.tencent.com/document/product/267/30411)をご参照ください。  


[](id:appreciation)
## 付加価値サービス料金

<table>
<tr><th colspan=2 width="20%">課金項目</th><th width="60%">課金説明</th><th>支払い方法</th></tr>
<tr>
<td rowspan=3>ライブストリーミングトランスコーディング</td>
<td>標準トランスコーディング</td>
<td><ul style="margin:0">
<li/>ライブストリーミングの標準トランスコーディング機能を使用した時に課金されます。
<li/><a href="https://intl.cloud.tencent.com/document/product/267/31064">ライブストリーミングウォーターマーク</a>、<a href="https://intl.cloud.tencent.com/document/product/267/31071">標準トランスコーディング</a>、<a href="https://intl.cloud.tencent.com/document/product/267/37665">ライブミクスストリーミング</a>などの機能を使用した時は、標準トランスコーディングの費用が発生します。
<li/>発生した料金は<b>トランスコーディングの時間に応じて課金され</b>、CSSストリームを出力する画面サイズに対応する価格が料金の単価となります。
</ul></td>
<td>
<li><a href="https://www.tencentcloud.com/document/product/267/52220#standard_pag">前払いリソースパッケージ</a></li>
  <li><a href="https://intl.cloud.tencent.com/document/product/267/39604">後払い-日次決済</a></li></ul>
	<li/>後払い-月次決済
</td>
</tr><tr>
<td>高速高画質トランスコーディング</td>
<td><ul style="margin:0">
<li/>ライブストリーミングの高速高画質トランスコーディング機能を使用した時に課金されます。
<li/> <a href="https://intl.cloud.tencent.com/document/product/267/31071">高速高画質トランスコーディング</a>の機能を使用したときは、高速高画質トランスコーディングの料金が発生します。
<li/>発生した料金は<b>トランスコーディングの時間に応じて課金され</b>、CSSストリームを出力する画面サイズに対応する価格が料金の単価となります。
</ul><td>
<li><a href="https://www.tencentcloud.com/document/product/267/52220#topspeed_pag">前払いリソースパッケージ</a></li>
<li><a href="https://intl.cloud.tencent.com/document/product/267/39604">後払い-日次決済</a></li>
<li/>後払い-月次決済
</td>
</tr><tr>
<td>オーディオトランスコード</td>
<td>
<li/>ライブストリーミングのオーディオトランスコーディング機能を使用した時に課金されます。
<li></li><a href="https://intl.cloud.tencent.com/document/product/267/31071">オーディオトランスコード</a>、オーディオミクスストリーミングなどの機能を使用するときは、いずれもオーディオトランスコード料金が発生します。
<li/>発生した料金は、<b>オーディオトランスコードの時間に応じて課金されます</b>。
<td>
<li><a href="https://www.tencentcloud.com/document/product/267/52220#standard_pag">前払いリソースパッケージ</a></li>
<li><a href="https://intl.cloud.tencent.com/document/product/267/39604">後払い-日次決済</a></li>
<li/>後払い-月次決済
</td>
</tr><tr>
  <td colspan=2>ライブストリーミングのレコーディング</td>
  <td>
    <li>ライブストリーミングのレコーディングは、レコーディングテンプレートに従ってレコーディングファイルを生成し、VODに保存します。</li>
    <li>レコーディングで発生するサービス料金は<b>ライブストリーミングレコーディングのチャンネル数のピーク値に応じて課金されます</b>。</li>
  </td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/39605">後払い-月次決済</a></td>
</tr><tr>
<td colspan=2>ライブストリーミングのタイムシフト</td>
<td>ライブストリーミングのタイムシフトは、タイムシフトの合計時間に応じて課金されます。</td>
<td>
<a href="https://www.tencentcloud.com/document/product/267/47534">後払い-日次決済</a>
</tr><tr>
<td colspan=2>ライブストリーミングのスクリーンキャプチャ</td>
<td>
  <li>ライブストリーミングのスクリーンキャプチャは、テンプレートに従って定期的にライブストリーミングのスクリーンをキャプチャし、画像をCOSに保存します。</li>
  <li>スクリーンキャプチャで発生するサービス料金は、<b>スクリーンキャプチャの枚数に応じて課金されます</b>。毎月の最初の1,000枚は無料です。</li>
</td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/39606">後払い-月次決済</a></td>
</tr><tr>
  <td colspan=2>インテリジェントポルノ検出</td>
  <td>スクリーンキャプチャによるポルノ検出では、ポルノ検出とスクリーンキャプチャという2つの料金が発生します。
    <li>ポルノ検出で発生するサービス料金は、<b>ポルノ検出の枚数に応じて課金され</b>、毎月の最初の1,000枚は無料です。</li>
    <li>スクリーンキャプチャで発生するサービス料金は、<b>スクリーンキャプチャの枚数に応じて課金されます</b>。毎月の最初の1,000枚は無料です。</li>
</td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/39607">後払い-月次決済</a></td>
</tr>
<tr><td colspan=2>プル転送</td>
<td>タスクのプル転送はタスク時間に応じて料金が発生します。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/41059">後払い-日次決済</a>
</td>
</tr><tr>
<td colspan=2>サードパーティへのプル転送料金</td>
<td>現在のアカウントではないCSSプッシュアドレスはすべてサードパーティアドレスであり、サードパーティへのプル転送の帯域幅に応じた料金が発生します。</td>
<td>
<a href="https://intl.cloud.tencent.com/document/product/267/41059">後払い-月次決済</a>
</td>
</tr>
</table>

[](id:extensions)
## 拡張サービス料金

<table>
<tr><th width="20%">課金項目</th><th width="60%">課金説明</th><th>支払い方法</th></tr>
<tr>
<td>レコーディングの保存</td>
<td>ライブストリーミングのレコーディングファイルはVODに保存する必要があり、発生したサービス料金は<b>データの実際の保存時間とストレージ容量に応じて課金されます</b>。 また、別途のオン・デマンド保存料金が必要です。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/266/14666">VOD-従量課金</a></td>
</tr><tr>
<td>スクリーンキャプチャの保存</td>
<td>ライブストリーミングのスクリーンキャプチャとポルノ検出で生成されたスクリーンキャプチャファイルはCOSに保存する必要があり、発生したサービス料金は<strong>データの実際の保存時間と保存量に応じて課金されます</strong>。また、別途のCOS保存料金が必要です。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/32534">COS-従量課金</a></td>
</tr></table>