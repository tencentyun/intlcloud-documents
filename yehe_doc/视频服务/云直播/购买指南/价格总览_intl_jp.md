LVBの課金項目には、基本サービス料金、付加価値サービス料金、拡張サービス料金が含まれます。料金の構成は次のとおりです。

![img](https://main.qcloudimg.com/raw/67a295effc191c4f710d9e2622fa1b01.png)

- [基本サービス料金]（＃base）：LVBを使用した後に生成されるライブブロードキャストの消費料金。トラフィックまたはピーク帯域幅の2つの課金方式を切り替えることができます。
- [付加価値サービス料金](#appreciation)：LVBのトランスコーディング、レコーディング、スクリーンキャプチャ、ポルノ検出などの付加価値機能を使用します。これらの機能はデフォルトで無効になっており、使用される場合にのみ課金されます。
- [拡張サービス料金](#extensions)：他のTencent Cloud製品が提供する付加価値機能と連携して提供される付加価値機能は、他のクラウド製品でそれぞれの課金ルールに従って関連料金を別途課金されます。


## 基本サービス料金
<table>
<tr><th width="20%">課金項目</th><th width="60%">課金の説明</th><th>支払い方法</th></tr>
<tr>
<td>LVBトラフィック（デフォルト）</td>
<td>課金方式が<b>日次トラフィック課金</b>の場合、LVBに発生する料金は<strong>消費されたトラフィック応じて課金されます</strong>。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/2818#traffic-and-bandwidth">後払い-日次課金</a></td>
</tr><tr>
<td>LVB帯域幅のピーク値</td>
<td>課金方式が<b>日次帯域幅課金</b>の場合、LVBに発生する料金は<b>ピーク帯域幅に応じて課金されます</b>。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/2818#traffic-and-bandwidth">後払い-日次課金</a></td>
</tr></table>


>? 課金方式を再選択する必要がある場合は、[Billing Method Change](https://intl.cloud.tencent.com/document/product/267/30411)をご参照ください。  



## 付加価値サービス料金

<table>
<tr><th colspan=2 width="20%">課金項目</th><th width="60%">課金の説明</th><th>支払い方法</th></tr>
<tr>
<td rowspan=2>LVBトランスコーディング</td>
<td>LVBトランスコーディング</td>
<td>
	 <li>ライブブロードキャスト再生における標準的なトランスコーディングシーンでの使用をサポートします。</li>
	<li> <a href="https://intl.cloud.tencent.com/document/product/267/31064">ウォーターマーク追加</a>または<a href="https://intl.cloud.tencent.com/document/product/267/37665">クラウドミックス</a>機能を有効にすると、標準トランスコーディング料金が発生する場合があります。解像度は、出力されるLVBストリームの解像度に準じます。</li>
	<li>トランスコーディングに発生するサービス料金は、<b>トランスコーディングの時間に応じて課金されます</b>。</li>
</td>
<td>
	<a href="https://intl.cloud.tencent.com/document/product/267/2818#lvb-transcoding">後払い-日次課金</a>
</td>
</tr><tr>
<td>超高速HDトランスコーディング</td>
<td>
	<li>ライブブロードキャスト再生における超高速HDトランスコーディングシーンでの使用をサポートします。</li>
	<li> <a href="https://intl.cloud.tencent.com/document/product/267/31064">ウォーターマーク追加</a>または<a href="https://intl.cloud.tencent.com/document/product/267/37665">クラウドミックス</a>機能を有効にすると、標準トランスコーディング料金が発生する場合があります。解像度は、出力されるLVBストリームの解像度に準じます。</li>
	<li>トランスコーディングに発生するサービス料金は、<b>トランスコーディングの時間に応じて課金されます</b>。</li></td>
<td>
<a href="https://intl.cloud.tencent.com/document/product/267/2818#top-speed-codec-transcoding">後払いの日次課金</a></td>
</tr><tr>
	<td colspan=2>グローバルアクセラレーション</td>
	<td>
		<li>ユーザーとグローバルアクセラレーションオリジンサーバーを接続することによって生成される下りトラフィックと帯域幅。</li>
		<li>トラフィックによる課金と帯域幅による課金の2つの課金方式が用意されています</b>。</li>
	</td>
<td><ahref="https：//intl.cloud.tencent.com/document/product/267/2818#global-acceleration">後払い-日次課金</a></td>
</tr>
    <tr>
	<td colspan=2>ライブブロードキャストレコーディング</td>
	<td>
		<li>LVBレコーディングは、レコーディングテンプレートに従ってレコーディングファイルを生成し、VODに保存します。</li>
		<li>レコーディングに発生するサービス料金は、<b>LVBレコーディングの並列チャンネルのピーク数に応じて課金されます</b>。</li>
	</td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/2818#lvb-recording">後払い-月次課金</a></td>
</tr><tr>
<td colspan=2>LVBスクリーンキャプチャ</td>
<td>
	<li>LVBスクリーンキャプチャは、テンプレートに従って一定の期間でライブブロードキャストのスクリーンをキャプチャし、画像はCOSに保存されます。</li>
	<li>スクリーンキャプチャのサービス料金は<b>スクリーンキャプチャの枚数に応じて課金されます</b>、毎月の最初の1,000枚は無料です。</li>
</td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/2818#lvb-screencapturing">後払い-月次課金</a></td>
</tr><tr>
	<td colspan=2>スクリーンキャプチャポルノ検出</td>
	<td>スクリーンキャプチャのポルノ検出は、ポルノ検出とスクリーンキャプチャの両方に料金が発生します。
		<li>ポルノ検出に発生するサービス料金は、<b>ポルノ検出評の枚数に応じて課金されます</b>、毎月の最初の1,000枚は無料です。</li>
		<li>スクリーンキャプチャのサービス料金は<b>スクリーンキャプチャの枚数に応じて課金されます</b>、毎月の最初の1,000枚は無料です。</li>
</td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/2818#intelligent-porn-detection">後払い-日次課金</a></td>
</tr><tr>
</tr><tr>
</tr>
</table>




## 拡張サービス料金

<table>
<tr><th width="20%">課金項目</th><th width="60%">課金の説明</th><th>支払い方法</th></tr>
<tr>
<td>レコーディングの保存</td>
<td>LVBレコーディングファイルはVODに保存する必要があり、発生したサービス料金は<b>データの実際の保存時間とストレージ容量に応じて課金されます</b>。 また、別途のオン・デマンド保存料金が必要です。</td>
<td><a href="https://intl.cloud.tencent.com/contact-sales">申請するには業務担当者にお問い合わせください</a></td>
</tr><tr>
<td>スクリーンキャプチャの保存</td>
<td>LVBスクリーンキャプチャとポルノ検出で生成されたスクリーンキャプチャファイルはCOSに保存する必要があり、発生したサービス料金は<strong>データの実際の保存時間とストレージ容量に応じて課金されます</strong>。 また、別途のCOS保存料金が必要です。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/32534">COS-従量課金</a></td>
</tr></table>