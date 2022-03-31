
各ユーザーに対して、Tencent CloudのTKEクラスターは地域ごとに固定したクォーターを割り当てています。

### TKE クォーター制限

ユーザーごとに購入できるTKEクォーターはデフォルトでは以下となります。より多くのクォーター項目が必要である場合、[クォーター申請チケット](https://console.cloud.tencent.com/workorder/category/create?level1_id=6&level2_id=350&level1_name=%E8%AE%A1%E7%AE%97%E4%B8%8E%E7%BD%91%E7%BB%9C&level2_name=%E5%AE%B9%E5%99%A8%E6%9C%8D%E5%8A%A1CCS) でクォーターを申請することができます。
>!2019年10月21日より、ユーザークラスターがサポートする5000未満の最大ノードクォーターは、すべて5000に調整されました。
>


<table>
	<tr>
	<th>クォーター項目</th>
	<th>デフォルト値</th>
	<th>参照可能なエントリ</th>
	<th>クォーター拡張可否</th>
	</tr>
	<tr>
	<td>単一地域配下のクラスター</td>
	<td>5</td>
	<td rowspan=5><a href="https://console.cloud.tencent.com/tke2">TKE 概要画面の右下側</a></td>
	<td rowspan=5>はい</td>
	</tr>
	<tr>
	<td>単一クラスター配下のノード</td>
	<td>5000</td>
	</tr>
	<tr>
	<td>単一地域配下のイメージネームスペース</td>
	<td>10</td>
	</tr>
	<tr>
	<td>単一地域配下のイメージリポジトリ</td>
	<td>500</td>
	</tr>
	<tr>
	<td>単一イメージ配下のイメージバージョン</td>
	<td>100</td>
	</tr>
</table>



### CVMクォーター制限

Tencent CloudのTKEによって生成されたCVMは、CVMの購入制限にかけられます。詳しくは、[CVM購入制約](https://intl.cloud.tencent.com/document/product/213/2664)をご参照ください。ユーザーごとに購入できるCVMクォーターはデフォルトでは以下のとおりとなります。より多くのクォーター項目が必要である場合、[クォーター申請チケット](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%20CVM&level3_id=156&radio_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%E8%B4%AD%E4%B9%B0%E9%85%8D%E9%A2%9D%E6%8F%90%E5%8D%87%E7%94%B3%E8%AF%B7&queue=1&scene_code=12701&step=2) でクォーターを申請することができます。

<table>
	<tr>
	<th>クォーター項目</th>
	<th>デフォルト値</th>
	<th>参照可能なエントリ</th>
	<th>クォーター拡張可否</th>
    </tr>
	<td>単一利用可能リージョン配下の従量制課金CVM</td>
	<td>30台または60台</td>
	<td><a href="https://console.cloud.tencent.com/cvm/overview">CVM 概要画面-各地域のリソース</a></td>
	<td>はい</td>
</table>




### クラスター設定制限
>?クラスター設定制限は、クラスターの規模を制限しており、現在変更不可です。
>

| 設定項目 | アドレス範囲 | 影響範囲 | 参照可能なエリート | 変更可否 |
| ----- | ----- | ---- | --------- | ---------- |
| VPC ネットワーク-サブネットワーク | カスタム設定 | 当該サブネットワークに追加できるノード数 |	[クラスターに対応するVPCサブネットワーク一覧-利用可能なIP数](https://console.cloud.tencent.com/vpc/subnet)	| <ul class="params"><li>変更不可</li><li>新規サブネットワーク利用可能</li></ul>|
| コンテナーのネットワークセグメント CIDR |	カスタム設定 |	<ul class="params"><li>クラスター内部の最大ノード数</li><li>クラスター内部の最大service数</li><li>ノードごとの最大Pod数</li></ul> |	クラスター基本情報画面-コンテナーのネットワークセグメント | 変更不可 |

<style>
	.params{margin-bottom:0px !important;}
</style>


### リソース制限の説明




2021年1月13日より、Tencent CloudのTKEシステムは、ノード数（nodeNum）が5以下（0 < nodeNum ≤ 5）、また、ノード数が5より大きいが20未満（5 < nodeNum < 20）のクラスターにおけるネームスペースに自動的に一連のリソースクォーターを適用します。これらのクォーターはリムーブ不可であり、クラスターにデプロイされたアプリケーションの潜在バグからクラスターパネルを保護し、その安定性を確保します。

これらのクォーターを確認する場合、以下のコマンドを実行します。
```
kubectl get resourcequota tke-default-quota -o yaml
```

指定されたネームスペースの`tke-default-quota`オブジェクトを確認する場合、`--namespace`オプションを使用し、ネームスペースを指定してください。

具体的なクォーター制限は以下の通りです：
                                  

<table>
<thead>
<tr>
<th align="left">クラスター規模</th>
<th align="left">クォーター制限</th>
</tr>
</thead>
<tbody>
<tr>
<td align="left">0 &lt; nodeNum &le; 5</td>
<td align="left">総数の制限 Pod：4000，configMap：3000，CustomResourceDefinition(CRD)：4000 </td>
</tr>
<tr>
<td>5 &lt; nodeNum &lt; 20</td>
<td>総数の制限 Pod：8000，configMap：6000，CustomResourceDefinition(CRD)：8000</td>
</tr>
<tr>
<td> 20 &le; nodeNum </td>
<td>制限なし</td>
</tr>
</tbody></table>






特殊な運用シーンでクォーターを調整する必要がある場合、[チケットの提出](https://console.cloud.tencent.com/workorder/category)で申請してください。


