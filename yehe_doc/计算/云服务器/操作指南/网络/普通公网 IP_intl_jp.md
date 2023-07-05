## 概要
このドキュメントでは、一般的なパブリックIPアドレスを使用する方法についてご紹介いたします。 一般的なパブリックIPはCloud Virtual Machineの購入時にのみ割り当てられます。CVMとの関連付けを解除することはできません。 購入時に割り当てられていない場合は、取得することができません。
<dx-alert infotype="explain" title="">
- 従来のアカウントタイプでは、CVMからEIPの関連付けを解除すると、各アカウントは一般的なパブリックIPアドレスを1日あたり10回無料で再割り当てできます。
- 現在、一般的なパブリックIPアドレスは、General BGP IPのみサポートしています。
</dx-alert>





## 操作ガイド


次の一般的なパブリックIP機能を使用することができます。

<table>
  <tr>
	<th width="17%">機能タイプ</th>
	<th>操作シナリオ</th>
	<th width="20%">関連ドキュメント</th>	
  </tr>
  <tr>
	<td>パブリックIPアドレスの復元</td>
	<td>誤操作によってパブリックIPアドレス（Elastic IPと一般的なパブリックIPを含む）をリリースまたは返却した場合は、パブリックIPコンソールで復元でき、復元後のパブリックIPはElastic IPとなります。</td>
	<td>
	  -
	</td>
  </tr>
  <tr>
	<td>一般的なパブリックIPをEIPに変換</td>
	<td>CVMの一般的なパブリックIPをElastic IPに変換すると、変換後のElastic IPはいつでもCVMと関連付けおよび関連付け解除できるため、パブリックIPの柔軟な管理をさらに手軽に実現できます。</td>
	<td>
	  -</a>
	</td>
  </tr>
  <tr>
	<td>パブリックIPの変更</td>
	<td>CVMの一般的なパブリックIPを変更し、変更後、元のパブリックIPはリリースされます。</td>
	<td>
	  <ul style="margin:0px">
	 <a href="https://intl.cloud.tencent.com/document/product/213/16642">CVMコンソールにおけるパブリックIPの変更</a>
		</li>
	  </ul>
	</td>
  </tr>
  <tr>
	<td>ネットワーク帯域幅の調整</td>
  <td>必要に応じて、帯域幅または課金モデルを変更できます。変更が完了した時点ですぐに反映されます。</td>
	<td>
	  <a href="https://intl.cloud.tencent.com/document/product/213/15517">ネットワーク設定の調整</a>
	</td>
  </tr>
</table>

