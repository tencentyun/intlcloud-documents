>? [CSS価格計算機](https://buy.cloud.tencent.com/pricing/css/calculator) でライブストリーミング関連費用の見積もりができます。

CSSの課金項目には、基本サービス費用、付加価値サービス費用、拡張サービス費用が含まれます。費用の構成は次のとおりです

![](https://main.qcloudimg.com/raw/446418a33f13dc82bc9d26b7b6e96b89.png)


- [基本サービス費用](#base)：CSSの使用後に発生する、ライブストリーミングの消費料金。トラフィックまたは帯域幅ピーク値に応じた2つの課金方式をサポートし、切り替えることが可能です。
- [付加価値サービス費用](#appreciation)：CSSのトランスコーディング、レコーディング、スクリーンキャプチャ、ポルノ検出などの付加価値機能を使用した時の料金。これらの機能はデフォルトでは無効になっており、使用する場合のみ課金されます。
- [拡張サービス費用](#extensions)：他のTencent Cloud製品と連携させて提供する付加価値機能は、他のクラウド製品では、それぞれの課金ルールに従って、別途関連費用が課金されます。

<span id="base"></span>

## 基本サービス費用
<table>
<tr><th width="20%">課金項目</th><th width="60%">課金の説明</th><th>支払い方法</th></tr>
<tr>
<td>LVBトラフィック<br>（デフォルト）</td>
<td>
<li/>LVB視聴により発生する下り方向のトラフィック消費は、日次決済の後払いで課金されます。
<li/>中国内地（大陸）、中国香港・マカオ・台湾、海外の高速化課金標準はそれぞれ異なります。
</td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/2818?lang=en&pg=#bill-by-traffic">後払い-日次決済</a></td>
</tr><tr>
<td>LVB帯域幅ピーク値</td>
<td>
<li/>LVB視聴により発生する下り方向の帯域幅ピーク値は、日次決済の後払いで課金されます。
<li/>中国内地（大陸）、中国香港・マカオ・台湾、海外の高速化課金標準はそれぞれ異なります。
</td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/2818?lang=en&pg=#bill-by-bandwidth">後払い-日次決済</a></td>
</tr></table>

>! 新たに課金方法の選択を行う場合は、 [課金の変更](https://intl.cloud.tencent.com/document/product/267/30411)を参照してください。  


<span id="appreciation"></span>

## 付加価値サービス費用

<table>
<tr><th colspan=2 width="20%">課金項目</th><th width="60%">課金の説明</th><th>支払い方法</th></tr>
<tr>
<td rowspan=3>CSSトランスコード</td>
<td>標準トランスコーディング</td>
<td><ul style="margin:0">
<li>CSSの標準トランスコーディング機能を使用した時に課金されます。
<li> <a href="https://intl.cloud.tencent.com/document/product/267/31064">CSSウォーターマーク</a>、<a href="https://intl.cloud.tencent.com/document/product/267/31071#C_trans">標準トランスコーディング</a>、<a href="https://intl.cloud.tencent.com/document/product/267/37665">ライブミクスストリーミング</a> 等の機能を使用した時に、標準トランスコーディング料金がそれぞれ発生します。
<li>発生した費用は<b>トランスコーディングの時間に応じて課金され</b>、ライブストリーミングを出力する画面サイズに対応する価格が料金の単価となります。
</ul></td>
<td>
  <li><a href="https://intl.cloud.tencent.com/document/product/267/39604#n_trans">後払い-日次決済</a></li></ul>
</td>
</tr><tr>
<td>高速高画質トランスコーディング</td>
<td><ul style="margin:0">
<li>CSSの高速高画質トランスコーディング機能を使用した時に課金されます。
<li> <a href="https://intl.cloud.tencent.com/document/product/267/31071#creating-top-speed-codec-transcoding-template">高速高画質トランスコーディング</a> 機能を使用した時に、高速高画質トランスコーディング料金が発生します。
<li>発生した費用は<b>トランスコーディングの時間に応じて課金され</b>、ライブストリーミングを出力する画面サイズに対応する価格が料金の単価となります。
</ul><td>
<li><a href="https://intl.cloud.tencent.com/document/product/267/39604#s_trans">後払い-日次決済</a></li></td>
</tr><tr>
<td>オーディオトランスコーディング</td>
<td>
<li/>CSSのオーディオトランスコーディング機能を使用した時に課金されます。
<li/> <a href="https://intl.cloud.tencent.com/document/product/267/31071#creating-pure-audio-transcoding-template">オーディオトランスコーディング</a>、オーディオミクスストリーミング、オーディオビデオ分離等の機能を使用した時に、オーディオトランスコーディング料金がそれぞれ発生します。
<li/>発生した費用は<b>オーディオトランスコーディングの時間に応じて課金されます</b>。
<td>
<li><a href="https://intl.cloud.tencent.com/document/product/267/39604#a_trans">後払い-日次決済</a></li></td>
</tr><tr>
  <td colspan=2>CSSレコーディング</td>
  <td>
    <li>CSSレコーディングでは、レコーディングテンプレートに従ってレコーディングファイルを生成し、VODに保存します。</li>
    <li>レコーディングで発生するサービス料金は<b>CSSレコーディングのチャンネル数のピーク値に応じて課金されます</b>。</li>
  </td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/39605">後払い-月次決済</a></td>
</tr><tr>
<td colspan=2>CSSスクリーンキャプチャ</td>
<td>
  <li>CSSスクリーンキャプチャは、テンプレートに従って定期的にライブストリーミングのスクリーンをキャプチャし、画像をCOSに保存します。</li>
  <li>スクリーンキャプチャで発生するサービス料金は、<b>スクリーンキャプチャの枚数に応じて課金され</b>、毎月の最初の1,000枚は無料です。</li>
</td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/39606">後払い-月次決済</a></td>
</tr><tr>
  <td colspan=2>インテリジェントなポルノ検出</td>
  <td>スクリーンキャプチャによるポルノ検出では、ポルノ検出とスクリーンキャプチャの2つの費用が発生します。
    <li>ポルノ検出で発生するサービス料金は、<b>ポルノ検出の枚数に応じて課金され</b>、毎月の最初の1,000枚は無料です。</li>
    <li>スクリーンキャプチャで発生するサービス料金は、<b>スクリーンキャプチャの枚数に応じて課金され</b>、毎月の最初の1,000枚は無料です。</li>
</td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/39607">後払い-月次決済</a></td>
</tr><tr>
</tr>
</table>
 


<span id="extensions"></span>

## 拡張サービス費用

<table>
<tr><th width="20%">課金項目</th><th width="60%">課金の説明</th><th>支払い方法</th></tr>
<tr>
<td>レコーディングのストレージ</td>
<td>CSSレコーディングのファイルはVODに保存する必要があり、発生したサービス料金は、<b>データの実際の保存時間とストレージ容量に応じて課金されます</b>。VOD保存料金が別途必要です。</td>
<td><a href="https://intl.cloud.tencent.com/contact-sales">ビジネスマネージャーに連絡して申請</a></td>
</tr><tr>
<td>スクリーンキャプチャストレージ</td>
<td>CSSスクリーンキャプチャとポルノ検出で生成したスクリーンキャプチャのファイルはCOSに保存する必要があり、発生したサービス料金は、<strong>データの実際の保存時間とストレージ容量に応じて課金されます</strong>。COSの保存料金が別途必要です。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/32534">COS-従量課金</a></td>
</tr></table>
