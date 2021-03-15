>?  [お問い合わせ](https://intl.cloud.tencent.com/zh/contact-sales) いただければ、お客様のライブストリーミング関連費用をお見積りいたします。

CSSの課金項目には、基本サービス費用、付加価値サービス費用、拡張サービス費用が含まれます。費用の構成は次のとおりです

![](https://main.qcloudimg.com/raw/40b382f7218804c557fdb9e3ce47294c.png)

- [基本サービス費用](#base)：CSSの使用後に発生する、ライブストリーミングの消費料金。トラフィックまたは帯域幅ピーク値に応じた2つの課金方式をサポートし、切り替えることが可能です。
- [付加価値サービス費用](#appreciation)：CSSのトランスコーディング、レコーディング、スクリーンキャプチャ、ポルノ検出などの付加価値機能を使用した時の料金。これらの機能はデフォルトでは無効になっており、使用する場合のみ課金されます。
- [拡張サービス費用](#extensions)：他のTencent Cloud製品と連携させて提供する付加価値機能は、他のクラウド製品では、それぞれの課金ルールに従って、別途関連費用が課金されます。

<span id="base"></span>

## 基本サービス費用
<table>
<tr><th width="20%">課金項目</th><th width="60%">課金説明</th><th>支払い方法</th></tr>
<tr>
<td>CSSトラフィック（デフォルト）</td>
<td>課金方式が<b>トラフィック日次課金</b>の場合、CSSで発生した費用は<strong>トラフィックの消費量に応じて課金されます</strong>。</td>
<td><a href="https://intl.cloud.tencent.com/zh/document/product/267/2818#.E5.B8.A6.E5.AE.BD.E8.AE.A1.E8.B4.B9">後払い-日次課金</a></td>
</tr><tr>
<td>CSS帯域幅ピーク値</td>
<td>課金方式が<b>帯域幅日次課金</b>の場合、CSSで発生した費用は、<b>帯域幅ピーク値に応じて課金されます</b>。</td>
<td><a href="https://intl.cloud.tencent.com/zh/document/product/267/2818#.E5.B8.A6.E5.AE.BD.E8.AE.A1.E8.B4.B9">後払い-日次課金</a></td>
</tr></table>

>? 課金方式を選択し直す必要がある場合は、[課金の変更](https://intl.cloud.tencent.com/document/product/267/30411)をご参照ください。  

<span id="appreciation"></span>

## 付加価値サービス費用

<table>
<tr><th colspan=2 width="20%">課金項目</th><th width="60%">課金説明</th><th>支払い方法</th></tr>
<tr>
<td rowspan=3>CSSトランスコーディング</td>
<td>標準トランスコーディング</td>
<td><ul style="margin:0">
<li/>CSSの標準トランスコーディング機能を使用した時に課金されます。
<li/><a href="https://intl.cloud.tencent.com/document/product/267/31064">CSSウォーターマーク</a>、<a href="https://intl.cloud.tencent.com/document/product/267/31071">標準トランスコーディング</a>、<a href="https://intl.cloud.tencent.com/document/product/267/37665">ライブミクスストリーミング</a>などの機能を使用した時は、標準トランスコーディングの費用が発生します。
<li/>発生した費用は<b>トランスコーディングの時間に応じて課金され</b>、ライブストリーミングを出力する画面サイズに対応する価格が料金の単価となります。
</ul></td>
<td>
  <li><a href="https://intl.cloud.tencent.com/zh/document/product/267/2818#.E6.A0.87.E5.87.86.E8.BD.AC.E7.A0.81">後払い-日次課金</a></li></ul>
</td>
</tr><tr>
<td>高速高画質トランスコーディング</td>
<td><ul style="margin:0">
<li/>CSSの高速高画質トランスコーディング機能を使用した時に課金されます。
<li/> <a href="https://intl.cloud.tencent.com/document/product/267/31071">高速高画質トランスコーディング</a>の機能を使用した時は、高速高画質トランスコーディングの費用が発生します。
<li/>発生した費用は<b>トランスコーディングの時間に応じて課金され</b>、ライブストリーミングを出力する画面サイズに対応する価格が料金の単価となります。
</ul><td>
<li><a href="https://intl.cloud.tencent.com/zh/document/product/267/2818#.E6.9E.81.E9.80.9F.E9.AB.98.E6.B8.85.E8.BD.AC.E7.A0.81">後払い-日次課金</a></li></td>
</tr><tr>
<td>オーディオトランスコーディング</td>
<td>
<li/>CSSのオーディオトランスコーディング機能を使用した時に課金されます。
<li/><a href="https://intl.cloud.tencent.com/document/product/267/31071">オーディオトランスコーディング</a>、オーディオミクスストリーミング、オーディオ・ビデオ分離などの機能を使用した時は、オーディオトランスコーディングの費用が発生します。
<li/>発生した費用は、<b>オーディオトランスコーディングの時間に応じて課金されます</b>。
<td>
<li><a href="https://intl.cloud.tencent.com/zh/document/product/267/2818#.E9.9F.B3.E9.A2.91.E8.BD.AC.E7.A0.81">後払い-日次課金</a></li></td>
</tr><tr>
  <td colspan=2>CSSレコーディング</td>
  <td>
    <li>CSSレコーディングでは、レコーディングテンプレートに従ってレコーディングファイルを生成し、VODに保存します。</li>
    <li>レコーディングで発生するサービス料金は<b>CSSレコーディングのチャンネル数のピーク値に応じて課金されます</b>。</li>
  </td>
<td><a href="https://intl.cloud.tencent.com/zh/document/product/267/2818#.E7.9B.B4.E6.92.AD.E5.BD.95.E5.88.B6">後払い-月次課金</a></td>
</tr><tr>
<td colspan=2>CSSスクリーンキャプチャ</td>
<td>
  <li>CSSスクリーンキャプチャは、テンプレートに従って定期的にライブストリーミングのスクリーンをキャプチャし、画像をCOSに保存します。</li>
  <li>スクリーンキャプチャで発生するサービス料金は、<b>スクリーンキャプチャの枚数に応じて課金されます</b>。毎月の最初の1,000枚は無料です。</li>
</td>
<td><a href="https://intl.cloud.tencent.com/zh/document/product/267/2818#.E7.9B.B4.E6.92.AD.E6.88.AA.E5.9B.BE">後払い-月次課金</a></td>
</tr><tr>
  <td colspan=2>スクリーンキャプチャによるポルノ検出</td>
  <td>スクリーンキャプチャによるポルノ検出では、ポルノ検出とスクリーンキャプチャの2つの費用が発生します。
    <li>ポルノ検出で発生するサービス料金は、<b>ポルノ検出の枚数に応じて課金され</b>、毎月の最初の1,000枚は無料です。</li>
    <li>スクリーンキャプチャで発生するサービス料金は、<b>スクリーンキャプチャの枚数に応じて課金されます</b>。毎月の最初の1,000枚は無料です。</li>
</td>
<td><a href="https://intl.cloud.tencent.com/zh/document/product/267/2818#.E6.99.BA.E8.83.BD.E9.89.B4.E9.BB.84">後払い-月次課金</a></td>
</tr><tr>
</tr>
</table>
 

<span id="extensions"></span>

## 拡張サービス費用

<table>
<tr><th width="20%">課金項目</th><th width="60%">課金説明</th><th>支払い方法</th></tr>
<tr>
<td>レコーディングの保存</td>
<td>>CSSレコーディングのファイルはVODに保存する必要があり、発生したサービス料金は、<b>データの実際の保存時間とストレージ容量に応じて課金されます</b>。VOD保存料金が別途必要です。</td>
<td><a href="https://intl.cloud.tencent.com/zh/contact-sales">申請するには、営業部門にお問い合わせください。</a></td>
</tr><tr>
<td>スクリーンキャプチャの保存</td>
<td> CSSスクリーンキャプチャとポルノ検出で生成したスクリーンキャプチャのファイルはCOSに保存する必要があり、発生したサービス料金は、<strong>データの実際の保存時間とストレージ容量に応じて課金されます</strong>。COSの保存料金が別途必要です。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/32534">COS-従量課金</a></td>
</tr></table>
