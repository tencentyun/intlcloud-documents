Tencent Cloudでは公式サイト購入およびAPI購入という2種類のCLB購入方法を提供しています。ここではその2種類の購入方法をご紹介します。

## [公式サイト購入](id:Official-Purchase)
すべてのユーザーは[Tencent Cloud公式サイト](https://buy.cloud.tencent.com/lb)からCLBをご購入いただけます。Tencent Cloudアカウントには標準アカウントタイプと従来型アカウントタイプがあり、2020年6月17日0時以降に登録したアカウントはすべて標準アカウントタイプとなります。この時点より前に登録したユーザーはコンソールでアカウントタイプを確認してください。具体的な操作については、[アカウントタイプの判断](https://intl.cloud.tencent.com/document/product/684/15246)をご参照ください。

1. Tencent Cloudの[CLB購入ページ](https://buy.cloud.tencent.com/lb)にログインします。
2. 必要に応じて次のCLB関連設定を選択します。
<dx-accordion>
::: 標準アカウントタイプ
<table>
<thead>
<tr>
<th width="18%">パラメータ</th>
<th width="82%">説明</th>
</tr>
</thead>
<tbody>
<tr>
<td><span style="font-weight:bold">課金モデル</span></td>
<td>
従量課金モデルをサポートしています。
</td>
</tr>
<tr>
<td><span style="font-weight:bold">リージョン</span></td>
<td>
所属リージョンを選択します。CLBのサポートリージョンの詳細については、<a href="https://intl.cloud.tencent.com/document/product/214/33792">リージョンリスト</a>をご参照ください。
</td>
</tr>
<tr>
<td><span style="font-weight:bold">インスタンスタイプ</span></td>
<td>
CLBインスタンスタイプのみサポートしています。
</td>
</tr>
<tr>
<td><span style="font-weight:bold">ネットワークタイプ</span></td>
<td>ネットワークタイプにはパブリックネットワークとプライベートネットワークの2種類があります。詳細については、<a href="https://intl.cloud.tencent.com/document/product/214/13629#network-type">ネットワークタイプ</a>をご参照ください。
	<ul>
	<li>パブリックネットワーク：CLBを使用してパブリックネットワークからのリクエストを振り分けます。</li>
	<li>プライベートネットワーク：CLBを使用してTencent Cloudプライベートネットワークからのリクエストを振り分けます。プライベートネットワークは、次の<strong>Elastic IP</strong>、<strong>IPバージョン</strong>、<strong>キャリアタイプ</strong>、<strong>インスタンス仕様</strong>、<strong>ネットワーク課金モデル</strong>、<strong>帯域幅上限</strong>をサポートしておらず、これらの設定項目はデフォルトで非表示になっています。</li>
	</ul>
	ネットワークタイプのサポート状況は課金モデルによって異なります。
	<ul>
	<li>従量課金モデルでは、パブリックネットワークとプライベートネットワークの両方のネットワークタイプをサポートしています。</li>
	</ul>
</td>
</tr>
<tr>
<td><span style="font-weight:bold">IPバージョン</span></td>
<td>
CLBのIPバージョンはIPv4、IPv6またはIPv6 NAT64から選択できます。IPv6バージョンのサポートは従量課金モデルのみとなります。その他の制限の状況については<a href="https://intl.cloud.tencent.com/document/product/214/13629#IP-type">IPバージョン</a>をご参照ください。
</td>
</tr>
<tr>
<td><span style="font-weight:bold">所属ネットワーク</span></td>
<td>
CLBがサポートする所属ネットワークは基幹ネットワークとVPCです。
	<ul>
	<li>基幹ネットワークとはTencent Cloud上のすべてのユーザーのための公共のネットワークリソースプールです。すべてのCVMのプライベートIPアドレスはTencent Cloudが一元的に割り当てており、ネットワークセグメントの区分、IPアドレスをカスタマイズすることはできません。</li>
	<li>VPCとは、ユーザーがTencent Cloud上に構築した、論理的に隔離されているネットワークスペースです。VPC内では、ユーザーはネットワークセグメントの区分、IPアドレスおよびルーティングポリシーを自由に定義できます。</li>
	</ul>
	両者を比較すると、VPCは基幹ネットワークに比べて、ネットワークのカスタム設定が求められるシーンにより適しています。また基幹ネットワーク製品全体が2022年12月31日に正式にサービス終了を予定しているため、VPCを選択することをお勧めします。
</td>
</tr>
<tr>
<td><span style="font-weight:bold">キャリアタイプ</span></td>
<td>
キャリアタイプには、BGP、チャイナモバイル、チャイナテレコム、チャイナユニコムがあります。
	<ul>
	<li>従量課金モデルでは、上記の4種類の選択をサポートしています。
現在は広州、上海、南京、済南、杭州、福州、北京、石家庄、武漢、長沙、成都、重慶リージョンのみで静的単一IP回線タイプをサポートしています。その他のリージョンのサポート状況はコンソールページでご確認ください。体験をご希望の場合はビジネスマネージャーにご連絡の上、お申し込みください。承認後、購入ページでチャイナモバイル、チャイナユニコムまたはチャイナテレコムのキャリアタイプを選択できるようになります。
	</li>
	</ul>
</td>
</tr>
<tr>
<td><span style="font-weight:bold">マスター/スレーブアベイラビリティーゾーン</span></td>
<td>マスターアベイラビリティーゾーンとは現在トラフィックを担っているアベイラビリティーゾーンです。スレーブアベイラビリティーゾーンはマスターアベイラビリティーゾーンが使用できない場合に使用します。現在は広州、上海、南京、北京、中国香港、ソウルリージョンのIPv4バージョンのCLBのみマスター/スレーブアベイラビリティーゾーンをサポートしています。
</td>
</tr>
<tr>
<td><span style="font-weight:bold">インスタンス仕様</span></td>
<td>共有インスタンスをサポートしています。
	<ul>
	<li>共有インスタンスでは複数のインスタンスがリソースを共有し、単一のインスタンスについては担保可能なパフォーマンス指標を提供しません。デフォルトではすべてのインスタンスが共有インスタンスとなります。</li>
	</ul>
</td>
</tr>
<tr>
<td><span style="font-weight:bold">ネットワーク課金モデル</span></td>
<td>ネットワーク課金モデルには、帯域幅課金（月額帯域幅）、帯域幅課金（時間単位帯域幅）、トラフィック課金、共有帯域幅パッケージがあります。
	<ul>
	<li>従量課金のインスタンス課金モデルでは、帯域幅課金（時間単位帯域幅）、使用トラフィック課金という2種類のネットワーク課金モデルをサポートしています。</li>
	</ul>
</td>
</tr>
<tr>
<td><span style="font-weight:bold">帯域幅上限</span></td>
<td>1～1024Mbpsです。
</td>
</tr>
<tr>
<td><span style="font-weight:bold">所属プロジェクト</span></td>
<td>所属プロジェクトを選択します。
</td>
</tr>
<tr>
<td><span style="font-weight:bold">タグ</span></td>
<td>タグキーとタグ値を選択するか、もしくはタグの新規作成を選択することもできます。詳細については、<a href="https://intl.cloud.tencent.com/document/product/651/41575">タグの作成</a>をご参照ください。
</td>
</tr>
<tr>
<td><span style="font-weight:bold">インスタンス名</span></td>
<td>60文字まで入力でき、アルファベット、数字、中国語、「-」、「_」、「.」を使用できます。入力しない場合はデフォルトで自動生成されます。
</td>
</tr>
</tbody></table>
:::
::: 従来型アカウントタイプ

<table>
<thead>
<tr>
<th width="18%">パラメータ</th>
<th width="82%">説明</th>
</tr>
</thead>
<tbody>
<tr>
<td><span style="font-weight:bold">課金モデル</span></td>
<td>
従量課金モデルのみサポートしています。
</td>
</tr>
<tr>
<td><span style="font-weight:bold">リージョン</span></td>
<td>
所属リージョンを選択します。CLBのサポートリージョンの詳細については、<a href="https://intl.cloud.tencent.com/document/product/214/33792">リージョンリスト</a>をご参照ください。
</td>
</tr>
<tr>
<td><span style="font-weight:bold">インスタンスタイプ</span></td>
<td>
CLBインスタンスタイプのみサポートしています。
</td>
</tr>
<tr>
<td><span style="font-weight:bold">ネットワークタイプ</span></td>
<td>ネットワークタイプにはパブリックネットワークとプライベートネットワークの2種類があります。詳細については、<a href="https://intl.cloud.tencent.com/document/product/214/13629#network-type">ネットワークタイプ</a>をご参照ください。
	<ul>
	<li>パブリックネットワーク：CLBを使用してパブリックネットワークからのリクエストを振り分けます。</li>
	<li>プライベートネットワーク：CLBを使用してTencent Cloudプライベートネットワークからのリクエストを振り分けます。プライベートネットワークは、次の<strong>IPバージョン</strong>、<strong>キャリアタイプ</strong>、<strong>インスタンス仕様</strong>をサポートしておらず、これらの設定項目はデフォルトで非表示になっています。</li>
	</ul>
</td>
</tr>
<tr>
<td><span style="font-weight:bold">IPバージョン</span></td>
<td>
CLBのIPバージョンはIPv4、IPv6またはIPv6 NAT64から選択できます。使用制限の詳細については<a href="https://intl.cloud.tencent.com/document/product/214/13629#IP-type">IPバージョン</a>をご参照ください。
</td>
</tr>
<tr>
<td><span style="font-weight:bold">所属ネットワーク</span></td>
<td>
CLBがサポートする所属ネットワークは基幹ネットワークとVPCです。
	<ul>
	<li>基幹ネットワークとはTencent Cloud上のすべてのユーザーのための公共のネットワークリソースプールです。すべてのCVMのプライベートIPアドレスはTencent Cloudが一元的に割り当てており、ネットワークセグメントの区分、IPアドレスをカスタマイズすることはできません。</li>
	<li>VPCとは、ユーザーがTencent Cloud上に構築した、論理的に隔離されているネットワークスペースです。VPC内では、ユーザーはネットワークセグメントの区分、IPアドレスおよびルーティングポリシーを自由に定義できます。</li>
	</ul>
	両者を比較すると、VPCは基幹ネットワークに比べて、ネットワークのカスタム設定が求められるシーンにより適しています。また基幹ネットワーク製品全体が2022年12月31日に正式にサービス終了を予定しているため、VPCを選択することをお勧めします。
</td>
</tr>
<tr>
<td><span style="font-weight:bold">キャリアタイプ</span></td>
<td>
キャリアタイプには、BGP、チャイナモバイル、チャイナテレコム、チャイナユニコムがあります。<br/>
現在は広州、上海、南京、済南、杭州、福州、北京、石家庄、武漢、長沙、成都、重慶リージョンのみで静的単一IP回線タイプをサポートしています。その他のリージョンのサポート状況はコンソールページでご確認ください。体験をご希望の場合はビジネスマネージャーにご連絡の上、お申し込みください。承認後、購入ページでチャイナモバイル、チャイナユニコムまたはチャイナテレコムのキャリアタイプを選択できるようになります。
</td>
</tr>
<tr>
<td><span style="font-weight:bold">インスタンス仕様</span></td>
<td>共有インスタンスをサポートしています。
	<ul>
	<li>共有インスタンスでは複数のインスタンスがリソースを共有し、単一のインスタンスについては担保可能なパフォーマンス指標を提供しません。デフォルトではすべてのインスタンスが共有インスタンスとなります。</li>
	</ul>
</td>
</tr>
<tr>
<td><span style="font-weight:bold">所属プロジェクト</span></td>
<td>所属プロジェクトを選択します。
</td>
</tr>
<tr>
<td><span style="font-weight:bold">タグ</span></td>
<td>タグキーとタグ値を選択するか、もしくはタグの新規作成を選択することもできます。詳細については、<a href="https://intl.cloud.tencent.com/document/product/651/41575">タグの作成</a>をご参照ください。
</td>
</tr>
<tr>
<td><span style="font-weight:bold">インスタンス名</span></td>
<td>60文字まで入力でき、アルファベット、数字、中国語、「-」、「_」、「.」を使用できます。入力しない場合はデフォルトで自動生成されます。
</td>
</tr>
</tbody></table>
:::
</dx-accordion>

4. 上記の設定が完了した後、購入数と料金をご確認の上、**今すぐ購入**をクリックします。
 -  従量課金モデル：ポップアップした「確認」ダイアログボックスで**OK**をクリックします。
5. 購入に成功すると、CLBサービスがすぐにアクティブになり、CLBの設定を行って使用することができます。

### [共有インスタンスの購入方法](id:Shared-CLB-Instance)
1. Tencent Cloudの[CLB購入ページ](https://buy.cloud.tencent.com/lb)にログインします。
2. 上記の[公式サイト購入](#Official-Purchase)の操作手順を参照し、必要に応じて共有CLBインスタンスの関連設定を選択し、「インスタンス仕様」で**共有タイプ**を選択します。
![]()
3. 引き続き、上記の[公式サイト購入](id:Official-Purchase)の操作手順を参照し、その後の操作を完了します。

### [ロードバランサキャパシティユニット（LCU）タイプインスタンスの購入方法](id:LCU-CLB-Instance)
1. Tencent Cloudの[CLB購入ページ](https://buy.cloud.tencent.com/lb)にログインします。
2. 上記の[公式サイト購入](#Official-Purchase)の操作手順を参照し、必要に応じてLCUタイプのCLBインスタンスの関連設定を選択し、「インスタンス仕様」で**LCUタイプ**を選択します。

3. 引き続き、上記の[公式サイト購入](id:Official-Purchase)の操作手順を参照し、その後の操作を完了します。


## [API購入](id:Official-Purchase)
APIによるCLBの購入を希望するユーザーは、[CLB API - CLBインスタンスの購入](https://intl.cloud.tencent.com/document/product/214/33841)をご参照ください。

## 後続の操作
- CLBにリスナーを作成したい場合は、[CLBリスナー](https://intl.cloud.tencent.com/document/product/214/6151)をご参照ください。
- CLBのリスナーにバックエンドサービスをバインドしたい場合は、[バックエンドサーバー](https://intl.cloud.tencent.com/document/product/214/32388)をご参照ください。

## 関連ドキュメント
[製品属性の選択](https://intl.cloud.tencent.com/document/product/214/13629)
