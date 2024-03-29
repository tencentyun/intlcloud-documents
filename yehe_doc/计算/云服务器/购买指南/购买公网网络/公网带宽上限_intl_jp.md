このドキュメントでは、CVMインスタンスのアウトバウンドおよびインバウンドの帯域幅上限、さまざまな課金モデルでのピーク帯域幅の違いについてご説明します。

## アウトバウンド帯域幅上限（ダウンストリーム帯域幅）

設定したパブリックネットワーク帯域幅の上限は、デフォルトでアウトバウンド帯域幅の上限、つまりCVMインスタンスから発信する帯域幅を示します。パブリックネットワーク帯域幅の上限はネットワークの課金モデルによって異なります。具体的な情報は以下のとおりです：
- 次のルールは、2020年2月24日00:00以降に作成されたインスタンスに適用されます。
<table>
<tbody><tr><th rowspan="2" style="width: 20%;">ネットワーク課金モデル</th><th colspan="2">インスタンス</th><th rowspan="2" style="width:35%">帯域幅設定範囲（Mbps）</th></tr>
<tr><th style="width: 20%;">インスタンス課金モデル</th><th style="width: 25%;">インスタンス構成</th></tr>
<tr><td>トラフィック課金</td><td>従量課金インスタンス</td><td>ALL</td><td>0 - 100</td></tr>
<tr><td>帯域幅課金</td><td>従量課金インスタンス</td><td>ALL</td><td>0 - 100</td></tr
<tr><td>共有帯域幅パッケージ</td><td colspan="2">ALL</td><td>0 - 2000</td></tr>
</tbody></table>

- 次のルールは、2020年2月24日00:00より前に作成されたインスタンスに適用されます。
<table>
<tbody><tr><th rowspan="2" style="width: 20%;">ネットワーク課金モデル</th><th colspan="2">インスタンス</th><th rowspan="2" style="width:35%">帯域幅設定範囲（Mbps）</th></tr>
<tr><th style="width: 20;">インスタンス課金モデル</th><th style="width: 25%;">インスタンス構成</th></tr>
<tr><td>トラフィック課金</td><td>従量課金インスタンス</td><td>ALL</td><td>0 - 100</td></tr>
<tr><td>帯域幅課金</td><td>従量課金インスタンス</td><td>ALL</td><td>0 - 100</td></tr>
<tr><td>共有帯域幅パッケージ</td><td colspan="2">ALL</td><td>0 - 1000</td></tr>
</tbody></table>



## インバウンド帯域幅上限（アップストリーム帯域幅）

- パブリックネットワークのインバウンド帯域幅は、CVMインスタンスに着信する帯域幅を示します。
- 利用したトラフィック量に応じて課金されるパブリックIP：
 - ユーザーが購入した帯域幅が10Mbps以下の場合、Tencent Cloudは10 Mbpsのパブリックネットワークのインバウンド帯域幅を割り当てます。
 - ユーザーが購入した帯域幅が10Mbpsを超える場合、Tencent Cloudは購入した帯域幅に等しいパブリックネットワークのインバウンド帯域幅を割り当てます。
- 共有帯域幅パッケージに応じて課金されるパブリックIP：
Tencent Cloudは、購入した帯域幅に等しいパブリックネットワークのインバウンド帯域幅を割り当てます。

## ピーク帯域幅
ピーク帯域幅は、「トラフィック課金」と「帯域幅課金」の両方に適用されますが、両者の意味合いは異なります。2つの料金プランの違いが一目でわかるように一覧にまとめました：

<table>
       <tbody><tr>
			 <th width="17%">課金モデル</th>
			 <th>ピーク帯域幅の違い</th>
			 <th>説明</th>
       </tr>
			 <tr>
			 <td>トラフィック課金</td>
			 <td>ピーク帯域幅は、コミットされた帯域幅ではなく、最大帯域幅と見なされるだけです。リソースの競合が発生した場合、ピーク帯域幅が制限される場合があります。</td> 
			 <td>実行中のすべての従量課金インスタンス (CVM、EIP、Elastic IPv6 ) のピーク帯域幅の合計は、1つのリージョン内で5Gbpsを超えることはできません。アプリケーションが帯域幅保証またはそれ以上の帯域幅を必要とする場合は、固定帯域幅に応じて課金されるパブリックネットワーク帯域幅を購入してください。</td> 
			 </tr>
       <tr>          
            <td>帯域幅課金<br/>（月額帯域幅および時間単位帯域幅を含む）</td>
            <td>ピーク帯域幅はコミットされた帯域幅と見なされます。リソースの競合が発生した場合、ピーク帯域幅は保証され、制限を受けません。</td>
						<td>固定帯域幅（月額帯域幅および時間単位帯域幅を含む）に応じて課金される実行中のすべてのインスタンス (CVM、EIP）のピーク帯域幅の合計は、1つのリージョン内で50Gbpsを超えることはできません。より多くの帯域幅が必要な場合は、営業担当者にお問い合わせください。

</td> 
            </tr> 
</tbody></table>


## 関連ドキュメント
[パブリックネットワーク帯域幅の調整](https://intl.cloud.tencent.com/document/product/213/15517)
