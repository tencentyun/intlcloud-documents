Tencent Cloudデータベースを委託管理するデータセンターは全世界の多くの場所に分散されています。これらの位置ノードをリージョン（Region）と呼び、各リージョンは複数のアベイラビリティーゾーン（Zone）から構成されています。
各リージョン（Region）は1つの独立した地理的ゾーンです。各リージョン（Region）は相互に隔絶された多くの場所に位置し、アベイラビリティーゾーン（Zone）と呼びます。各アベイラビリティーゾーンはみな独立していますが、同一リージョンのアベイラビリティーゾーンはディレイタイムが少ない内部ネットワークのリンクで接続されています。Tencent Cloudは、ユーザーが様々な場所にクラウドリソースを分配することをサポートし、1か所の故障によってサービスが使えなくならないよう、ユーザーがシステム設計をする際はリソースを異なるアベイラビリティーゾーンに配置することをお勧めします。

リージョン名、アベイラビリティーゾーン名は、データセンターの担当範囲で最も直接的に訴えるものなので、わかりやすいものになっています。命名のルールは次のとおりです。
- リージョンの命名は【担当範囲＋データセンターのある都市】で構成され、前半部はそのデータセンターの担当範囲を、後半はそのデータセンターの所在都市、または近隣都市を示しています。
- アベイラビリティーゾーンの命名は【都市+コード】で構成されています。


## リージョン
Tencent Cloudは他のリージョンとは完全に隔絶しているので、異なるリージョン間における最大の安定性と耐障害性を保証します。アクセス遅延を縮小し、ダウンロードを速くするために、最もお近くのリージョンを選択することをお勧めします。ユーザーのインスタンスの起動、表示などの動作はすべてリージョン属性を区別します。
クラウド製品の内部ネットワークの注意事項：
- アベイラビリティーゾーンが異なっても同リージョンのクラウドソース間では内部ネットワークによって相互接続しており、直接[内部ネットワークIP](https://intl.cloud.tencent.com/document/product/213/5225)を利用してアクセスできます。
- リージョンが異なるクラウド製品では**デフォルトで内部ネットワークによる通信ができません**。
 - CVMのデフォルトではクロスリージョンでの相互アクセスはできなくなっており、デフォルトではクロスリージョンでのクラウドデータベースMemcachedへのアクセスはできません。
 - Cloud Load Balancer（CLB）がサーバーにバインドされているとき、同じリージョンにバインドされているCVMだけ選択できます。
- 異なるリージョン間のクラウドリソースは[パブリックIP](https://intl.cloud.tencent.com/document/product/213/5224)によってInternetアクセスします。VPCにあるクラウドサービスもTencent Cloudが提供する[対等接続](https://console.cloud.tencent.com/vpc/conn)によるTencent Cloud高速インターネット通信経由で、Internetアクセスよりもさらに安定した高速インターネットが行えます。
- [Cloud Load Balancer（CLB）](https://intl.cloud.tencent.com/document/product/214)はクロスリージョンのトラフィック転送をサポートしません。

上記の内部ネットワーク接続は、すべて同一アカウントでのリソース接続のことを指し、アカウントが異なるリソース内部ネットワークは完全に隔絶されます。


## アベイラビリティーゾーン
アベイラビリティーゾーン（Zone）とは、Tencent Cloudの、同一リージョン内で電力とネットワークが独立している物理的データセンターを指します。アベイラビリティーゾーン間での障害を相互に隔絶し（大規模災害または大型電力施設の故障は除く）、ユーザーのオンラインタスクを継続するために、障害を拡散させないことが目的です。独立したアベイラビリティーゾーンのインスタンスを起動させることで、ユーザーのアプリケーションプログラムが1つの障害箇所の影響を受けないようにします。
ユーザーがインスタンスを起動するときは、指定のリージョン下の任意のアベイラビリティーゾーンを選択できます。ユーザーがアプリケーションシステムを高信頼性に設計するとき（あるインスタンスに障害が発生してもサービスをそのまま利用可）、クロスリージョンでのデプロイプラン（例：[CLB](https://intl.cloud.tencent.com/document/product/214)、[EIP](https://intl.cloud.tencent.com/document/product/213/5733) 等）を使用でき、これによって別のアベイラビリティーゾーンのインスタンスに代わりに関連リクエストを処理させることができます。

## リージョンとアベイラビリティーのリスト
リージョン（Region）とアベイラビリティーゾーン（Zone）構成：

### 中国
<table class="table-striped">
<tbody>
	<tr>
		<th>リージョン</th>
		<th>アベイラビリティーゾーン</th>
	</tr>
	<tr>
		<td rowspan="4">華南地区（広州）<br> ap-guangzhou</td>
		<td>広州1区（売り切れ）<br> ap-guangzhou-1</td>
	</tr>	
	<tr>
		<td>広州2区<br> ap-guangzhou-2</td>
	</tr>
	<tr>
		<td>広州3区<br> ap-guangzhou-3</td>
	</tr>
	<tr>
		<td>広州4区<br> ap-guangzhou-4</td>
	</tr>
	<tr>
		<td rowspan="4">華東地区（上海）<br>ap-shanghai</td>
		<td>上海1区<br>ap-shanghai-1</td>
	</tr>
	<tr>
		<td>上海2区<br>ap-shanghai-2</td>
	</tr>
	<tr>
		<td>上海3区<br>ap-shanghai-3</td>
	</tr>
	<tr>
		<td>上海4区<br>ap-shanghai-4</td>
	</tr>
			<td rowspan="2">華東地区（南京）<br>ap-nanjing</td>
		<td>南京1区<br>ap-nanjing-1</td>
	</tr>
	<tr>
		<td>南京2区<br>ap-nanjing-2</td>
	</tr>
	<tr>
			<td rowspan="5">華北地区（北京）<br>ap-beijing</td>
			<td>北京1区<br>ap-beijing-1</td>
	</tr>
	<tr>
			<td>北京2区<br>ap-beijing-2</td>
	</tr>
	<tr>
			<td>北京3区<br>ap-beijing-3</td>
	</tr>
	<tr>
			<td>北京4区<br>ap-beijing-4</td>
	</tr>
		<tr>
			<td>北京5区<br>ap-beijing-5</td>
	</tr> 
	<tr>
		<td rowspan="2">西南地区（成都）<br>ap-chengdu</td>
		<td>成都1区<br>ap-chengdu-1</td>
	</tr>
	<tr>
			<td>成都2区<br>ap-chengdu-2</td>
	</tr>    
	<tr>
			<td >西南地区（重慶）<br>ap-chongqing</td>
			<td>重慶1区<br>ap-chongqing-1</td>
	</tr>
	<tr>
			<td rowspan="2">香港、マカオ、台湾地区（中国香港）<br>ap-hongkong</td>
			<td>中国香港1区（中国香港ノードは香港、マカオ、台湾地区をカバー）<br>ap-hongkong-1</td>
	</tr>
	<tr>
			<td>中国香港2区（中国香港ノードは香港、マカオ、台湾地区をカバー）<br>ap-hongkong-2</td>
	</tr>
</tbody>
</table>	

<span id="InternationalArea"></span>

### その他の国と地域
<table class="table-striped">
	<tbody>
	<tr>
			<th>リージョン</th>
			<th>アベイラビリティーゾーン</th>
		</tr>
		<tr>
			<td>アジア太平洋東南部（シンガポール）<br>ap-singapore</td>
			<td>シンガポール1区（シンガポールノードはアジア太平洋東南地区をカバー）<br>ap-singapore-1</td>
		</tr>
				<tr>
		  	<td >アジア太平洋東南部（バンコク）<br>ap-bangkok </td>
				 <td >バンコク1区（バンコクノードはアジア太平洋東南地区をカバー）<br>ap-bangkok-1</td>
		       <tr>
			<td  rowspan="2">アジア太平洋南部（ムンバイ）<br>ap-mumbai</td>
			<td>ムンバイ1区（ムンバイノードはアジア太平洋南部地区をカバー）<br>ap-mumbai-1</td>
		</tr>
       <tr>
			<td>ムンバイ2区（ムンバイノードはアジア太平洋南部地区をカバー）<br>ap-mumbai-2</td>
		</tr>		
		<tr>
			<td >アジア太平洋東北部（ソウル）<br>ap-seoul</td>
			<td>ソウル1区（ソウルノードはアジア太平洋東北部をカバー）<br>ap-seoul-1</td>
		</tr>
		<tr>
			<td >アジア太平洋東北部（東京）<br>ap-tokyo</td>
			<td>東京1区（東京ノードはアジア太平洋東北部をカバー）<br>ap-tokyo-1</td>
		</tr>
				<tr>
			<td rowspan="2">米国西部（シリコンバレー）<br>na-siliconvalley</td>
			<td>シリコンバレー1区（シリコンバレーノードは米国西部地区をカバー）<br>na-siliconvalley-1</td>
		</tr>
    <tr>
			<td>シリコンバレー2区（シリコンバレーノードは米国西部地区をカバー）<br>na-siliconvalley-2</td>
		</tr>
				<tr>
			<td rowspan="2">米国東部（バージニア）<br>na-ashburn</td>
			<td>バージニア1区（バージニアノードは米国東部地区をカバー）<br>na-ashburn-1</td>
		</tr>
		<tr>
			<td>バージニア2区（バージニアノードは米国東部地区をカバー）<br>na-ashburn-2</td>
		</tr>
		<tr>
			<td>北米地区（トロント）<br>na-toronto</td>
			<td>トロント1区（トロントノードは北米地区をカバー）<br>na-toronto-1</td>
		</tr>
		<tr>
			<td>欧州地区（フランクフルト）<br>eu-frankfurt</td>
			<td>フランクフルト1区（フランクフルトノードは欧州地区をカバー）<br>eu-frankfurt-1</td>
		</tr>
		<td >欧州地区（モスクワ）<br>eu-moscow</td>
		<td>モスクワ1区（モスクワノードは欧州地区をカバー）<br>eu-moscow-1</td>
		</tr>
	</tbody>
</table>


## リージョンとアベイラビリティーゾーンはどのように選択しますか。
CVMを購入する際には、アクセス遅延を縮小し、ダウンロードを速くするために、最もお近くのリージョンを選択することをお勧めします。
