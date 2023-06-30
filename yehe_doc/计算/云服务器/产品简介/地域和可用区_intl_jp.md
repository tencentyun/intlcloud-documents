## リージョン

### 概要

- [リージョン](https://intl.cloud.tencent.com/document/product/213/6091)： リージョン（Region）とは物理的なデータセンターがある地理的区域のことです。Tencent Cloudは異なるリージョン間を完全に隔離し、リージョン間での最大限の安定性とフォールトトレランスを保証します。Tencent Cloud サービスを購入する場合は、アクセスの遅延を減らし、ダウンロード速度を向上させるために、エンドユーザーに最も近いリージョンを選択することをお勧めします。

次の表を参照するか、または[DescribeRegions API](https://intl.cloud.tencent.com/document/product/213/15708) を使用してリージョンの完全なリストを取得できます。

### 関連の特性

- 異なるリージョン間のネットワークは完全に分離されており、異なるリージョン間のクラウド製品は、**デフォルトではプライベートネットワークを介して通信できません**。
- 異なるリージョン間のクラウド製品は、[パブリックIP](https://intl.cloud.tencent.com/document/product/213/5224) を介して相互に通信できます。異なる VPC 内のクラウド製品は、 [CCN](https://www.tencentcloud.com/document/product/1003)を介して相互に通信できます。この通信方式はより高速で安定しています。
- [CLB](https://www.tencentcloud.com/document/product/214 ) は、現在、デフォルトで同一リージョンのトラフィック転送をサポートしています。[クロスリージョンバインディング](https://intl.cloud.tencent.com/document/product/214/38441) 機能を有効にすると、CLBインスタンスを別のリージョンのCVMインスタンスにバインドできます。

## アベイラビリティーゾーン

### 概要

アベイラビリティーゾーン（AZ）とは、Tencent Cloudが同一リージョン内で電源とネットワークが互いに独立している物理的なデータセンターです。ユーザーのビジネスのオンラインサービスの持続性を確保するため、アベイラビリティーゾーン間の障害を互いに隔離し（大規模な災害または大規模な電力設備の障害を除く）、障害の影響が拡散しないようにすることを目的としています。独立したアベイラビリティーゾーンでインスタンスを起動することにより、単一障害点の影響からアプリケーションを保護することができます。
[DescribeZones](https://www.tencentcloud.com/document/product/213/35071) API を使用して、アベイラビリティ ゾーンの完全なリストを取得できます。

### 関連の特性

同じVPC内のクラウド製品は、プライベートネットワークを介して相互接続されているため、異なるアベイラビリティーゾーンにある場合でも、[プライベートIPアドレス](https://intl.cloud.tencent.com/document/product/213/5225)を通じて直接アクセスすることができます。
<dx-alert infotype="explain" title="">
プライベートネットワークの相互接続とは、同じアカウントの下でのリソースの相互接続を指します。異なるアカウントのリソースはプライベートネットワーク上で完全に分離されます。
</dx-alert>


## 中国[](id:MainlandChina)			
<table class="table-striped">			
<tbody>			
	</tr>		
		<th>リージョン</th>	
		<th>アベイラビリティーゾーン</th>	
	</tr>		
	<tr>		
		<td rowspan="6">華南地区（広州）<br> ap-guangzhou</td>	
		<td>広州1区（売り切れ）<br> ap-guangzhou-1</td>	
	</tr>		
	<tr>		
		<td>広州2区（売り切れ）<br> ap-guangzhou-2</td>	
	</tr>		
	<tr>		
		<td>広州3区<br> ap-guangzhou-3</td>	
	</tr>		
	<tr>		
		<td>広州4区<br> ap-guangzhou-4</td>	
	</tr>		
	<tr>		
		<td>広州6区<br> ap-guangzhou-6</td>	
	</tr>		
	<tr>		
		<td>広州7区<br> ap-guangzhou-7</td>	
	</tr>		
	<tr>		
		<td rowspan="6">華東地区（上海）<br>ap-shanghai</td>	
		<td>上海1区（売り切れ）<br>ap-shanghai-1</td>	
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
 </tr>			
		<td>上海5区<br>ap-shanghai-5</td>	
	</tr>		
	 <tr>		
		<td>上海8区<br>ap-shanghai-8</td></tr>	
	</tr>		
	<tr>		
			<td rowspan="3">華東地区（南京）<br>ap-nanjing</td>
			<td>南京1区<br>ap-nanjing-1</td>
	</tr>		
	<tr>		
			<td>南京2区<br>ap-nanjing-2</td>
	</tr>		
	<tr>		
			<td>南京3区<br>ap-nanjing-3</td>
	</tr>		
	<tr>		
			<td rowspan="7">華北地区（北京）<br>ap-beijing</td>
			<td>北京1区（売り切れ）<br>ap-beijing-1</td>
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
		</tr>	
			<td>北京6区<br>ap-beijing-6</td>
	</tr>		
		</tr>	
			<td>北京7区<br>ap-beijing-7</td>
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
			<td rowspan="3">香港・マカオ・台湾リージョン（中国香港）<br>ap-hongkong</td>
			<td>中国香港1区（中国香港のノードは中国香港・中国マカオ・中国台湾地域をカバーできる）（売り切れ）<br>ap-hongkong-1</td></tr>
	</tr>		
	<tr>		
			<td>香港2区（中国香港のノードは香港・マカオ・台湾地域をカバーできる）<br>ap-hongkong-2</td>
	</tr>		
	<tr>		
			<td>中国香港3区（中国香港のノードは中国香港・中国マカオ・中国台湾地域をカバーできる）<br>ap-hongkong-3</td>
	</tr>		
</tbody>			
</table>			
			
<dx-alert infotype="explain" title="">			
済南、杭州、福州、武漢、長沙、石家庄リージョンは現在ベータ版テスト中です。ご利用をご希望の場合はビジネスマネージャーまでご連絡ください。			
</dx-alert>	


## その他の国および地域[](id:InternationalArea)
<table class="table-striped">
	<tbody>
	<tr>
			<th>リージョン</th>
			<th>アベイラビリティーゾーン</th>
		</tr>
		<tr>
			<td  rowspan="4">東南アジア（シンガポール）<br>ap-singapore</td>
			<td>シンガポール1区（シンガポールのノードは東南アジア地域をカバーできる）<br>ap-singapore-1</td>
		</tr>
		<tr>
			<td>シンガポール2区（シンガポールのノードは東南アジア地域をカバーできる）<br>ap-singapore-2</td>
		</tr>
		<tr>
			<td>シンガポール3区（シンガポールのノードは東南アジア地域をカバーできる）<br>ap-singapore-3</td>
		</tr>
   <tr>
			<td>シンガポール4区（シンガポールのノードは東南アジア地域をカバーできる）<br>ap-singapore-4</td>
		</tr>
		<tr>
			<td rowspan="2">東南アジア（ジャカルタ）<br>ap-jakarta</td>
			<td>ジャカルタ1区（ジャカルタのノードは東南アジア地域をカバーできる）<br>ap-jakarta-1</td>
		</tr>
		<tr>
			<td>ジャカルタ2区（ジャカルタのノードは東南アジア地域をカバーできる）<br>ap-jakarta-2</td>
		</tr>
		<tr>
			<td  rowspan="2">北東アジア（ソウル）<br>ap-seoul</td>
			<td>ソウル1区（ソウルのノードは北東アジア地域をカバーできる）<br>ap-seoul-1</td>
		</tr>
		<tr>
			<td>ソウル2区（ソウルのノードは北東アジア地域をカバーできる）<br>ap-seoul-2</td>
		</tr>
		<tr >
			<td rowspan="2">北東アジア（東京）<br>ap-tokyo</td>
			<td>東京１区（東京のノードは北東アジア地域をカバーできる）<br>ap-tokyo-1</td>
		</tr>
		 <tr>
			<td>東京2区（東京のノードは北東アジア地域をカバーできる<br>ap-tokyo-2</td>
		</tr>
       <tr>
			<td  rowspan="2">南アジア太平洋（ムンバイ）<br>ap-mumbai</td>
			<td>ムンバイ1区（ムンバイのノードは南アジア太平洋地域をカバーできる）<br>ap-mumbai-1</td>
		</tr>
       <tr>
			<td>ムンバイ2区（ムンバイのノードは南アジア太平洋地域をカバーできる）<br>ap-mumbai-2</td>
		</tr>
		<tr>
		  	<td rowspan="2">東南アジア（バンコク）<br>ap-bangkok </td>
				 <td>バンコク1区（バンコクのノードは東南アジア地域をカバーできる）<br>ap-bangkok-1</td>
		</tr>
		<tr>
			<td>バンコク2区（バンコクのノードは東南アジア地域をカバーできる）<br>ap-bangkok-2</td>
		</tr>
		<tr>
			<td>北アメリカ（トロント）<br>na-toronto</td>
			<td>トロント1区（トロントのノードは北アメリカをカバーできる）<br>na-toronto-1</td>
		</tr>
		<tr>
			<td>南アメリカ（サンパウロ）<br>sa-saopaulo</td>
			<td>サンパウロ1区（サンパウロのノードは南アメリカをカバーできる）<br>sa-saopaulo-1</td>
		</tr>
		<tr>
			<td rowspan="2">米国西部（シリコンバレー）<br>na-siliconvalley</td>
			<td>リコンバレー1区（シリコンバレーのノードは米国西部をカバーできる）<br>na-siliconvalley-1</td>
		</tr>
    <tr>
			<td>リコンバレー2区（シリコンバレーのノードは米国西部をカバーできる）<br>na-siliconvalley-2</td>
		</tr>
		<tr>
			<td rowspan="2">米国東部（バージニア）<br>na-ashburn</td>
			<td>バージニア1区 （バージニアのノードは米国東部をカバーできる）<br>na-ashburn-1</td>
		</tr>
		<tr>
			<td>バージニア2区 （バージニアのノードは米国東部をカバーできる）<br>na-ashburn-2</td>
		</tr>
		<tr>
			<td rowspan="2">ヨーロッパ地域（フランクフルト）<br>eu-frankfurt</td>
			<td>フランクフルト1区（フランクフルトのノードはヨーロッパ地域をカバーできる）<br>eu-frankfurt-1</td>
		</tr>
		<tr>
			<td>フランクフルト2区（フランクフルトのノードはヨーロッパ地域をカバーできる）<br>eu-frankfurt-2</td>
		</tr>
	</tbody>
</table>

## リージョンとアベイラビリティーゾーンを選択する方法

リージョンとアベイラビリティーゾーンを選択するときは、次の点を考慮してください。
- CVMインスタンスのリージョン、あなたおよびターゲットユーザーの地理的位置
アクセス遅延を最小限に抑え、アクセス速度を向上させるために、CVMインスタンスを購入する場合は、エンドユーザーに最も近いリージョンを選択することをお勧めします。
- CVMと他のクラウド製品との関係
他のクラウド製品を選択する場合は、可能な限りすべて同一リージョン、同一アベイラビリティーゾーンに配置して、各クラウド製品間でプライベートネットワークを介して相互に通信できるようにし、アクセスの遅延を減らし、アクセス速度を向上させることができます。
- 高可用性と災害復旧
VPCが1つしかない場合であっても、単一障害点を防止し、クロスアベイラビリティーゾーン災害復旧を可能にするために、ビジネスを異なるアベイラビリティ ゾーンにデプロイすることをお勧めします。
- 異なるアベイラビリティーゾーン間では、ネットワーク遅延が発生する可能性がありますので、実際のビジネス要件に応じて検討し、高可用性と低遅延の最適なバランスを見つけることをお勧めします。
- 他の国または地域のCVMインスタンスにアクセスする必要がある場合は、他の国または地域のCVMを選択することをお勧めします。[中国本土](#MainlandChina)のCVMインスタンスを使用して、[他の国や地域のサーバー](#InternationalArea)にアクセスする場合、ネットワーク遅延が大幅に増加する可能性がありますので、ご利用はお勧めしません。

## リソースの可用性
ここではTencent Cloudのどのリソースがグローバルなものか、どのリソースがリージョンは区別するがアベイラビリティーゾーンは区別しないのか、どのリソースがアベイラビリティーゾーンベースであるのかについてご説明します。

<table>
	<tr><th width="14%">リソース</th><th>リソース ID形式<br><リソースの略語>-8桁の数字と文字</th><th>タイプ</th><th>説明</th></tr>
	<tbody>
	<tr>
	  <td>ユーザーアカウント</td>
	  <td>制限なし</td>
	  <td>グローバルに一意のアカウント</td>
	  <td>ユーザーは同じアカウントを使用して、世界中のTencent Cloud リソースにアクセスできます。</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/213/6092">SSH キー</a> </td>
	  <td>skey-xxxxxxxx</td>
	  <td>グローバル</td>
	  <td>ユーザーはSSHキーを使用して、アカウント下の任意のリージョンのCVMをバインドできます。</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/213/4939">CVM インスタンス</a> </td>
	  <td>ins-xxxxxxxx</td>
	  <td>単一リージョンの単一のアベイラビリティーゾーンでのみ利用可能</td>
	  <td>ユーザーは特定のアベイラビリティーゾーンでのみCVMインスタンスを作成できます。</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/213/4941">カスタムイメージ</a> </td>
	  <td>img-xxxxxxxx</td>
	  <td>単一リージョンの複数のアベイラビリティーゾーンで利用可能</td>
	  <td>ユーザーはインスタンスのカスタムイメージを作成し、それを同一のリージョンの異なるアベイラビリティーゾーンで使用できます。他のリージョンで使用する際は、イメージコピー機能を使用してカスタムイメージを他のリージョンにコピーする必要があります。</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/213/5733">Elastic IP</a> </td>
	  <td>eip-xxxxxxxx</td>
	  <td>単一リージョンの複数のアベイラビリティーゾーンで利用可能</td>
	  <td>EIPはリージョン固有であり、同じリージョン内のインスタンスにのみ関連付けることができます。</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/213/12452">セキュリティグループ</a> </td>
	  <td>sg-xxxxxxxx</td>
	  <td>単一リージョンの複数のアベイラビリティーゾーンで利用可能</td>
	  <td>セキュリティグループは、同じリージョン内のインスタンスにのみ関連付けることができます。Tencent Cloud は、ユーザーに3つのデフォルトのセキュリティグループを自動的に作成します。</td>
	</tr>
	<tr>
	<td> <a href="https://www.tencentcloud.com/document/product/362">Cloud Block Storage</a> </td>
	  <td>disk-xxxxxxxx</td>
	  <td>単一リージョンの単一のアベイラビリティーゾーンでのみ利用可能</td>
	  <td>ユーザーは特定のアベイラビリティーゾーンでのみCBSを作成でき、それを同じアベイラビリティ ゾーン内のインスタンスに接続できます。</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/362/31638">スナップショット</a> </td>
	  <td>snap-xxxxxxxx</td>
	  <td>単一リージョンの複数のアベイラビリティーゾーンで利用可能</td>
	  <td>CBSのスナップショットを作成すると、ユーザーはこのリージョン下でこのスナップショットを使用して他の操作（クラウドディスクの作成など）を行うことができます。</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/214/524">Cloud Load Balancer</a> </td>
	  <td>clb-xxxxxxxx</td>
	  <td>単一リージョンの複数のアベイラビリティーゾーンで利用可能</td>
	  <td>CLBは単一リージョンの異なるアベイラビリティーゾーンのCVMにバインドしてトラフィックの転送を行うことができます。</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/215/535">Virtual Private Cloud</a> </td>
	  <td>vpc-xxxxxxxx</td>
	  <td>単一リージョンの複数のアベイラビリティーゾーンで利用可能</td>
	  <td>私VPCはあるリージョンで作成し、異なるアベイラビリティーゾーンで同じVPCに属するリソースを作成することができます。</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/215/535#.E5.AD.90.E7.BD.91">サブネット</a> </td>
	  <td>subnet-xxxxxxxx</td>
	  <td>単一リージョンの単一のアベイラビリティーゾーンでのみ利用可能</td>
	  <td>ユーザーは、異なるアベイラビリティーゾーン間でサブネットを作成することができません。</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/215/31810">ルートテーブル</a> </td>
	  <td>rtb-xxxxxxxx</td>
	  <td>単一リージョンの複数のアベイラビリティーゾーンで利用可能</td>
	  <td>ルートテーブルを作成するとき、ユーザーはVPCを指定する必要があります。</td>
	</tr>
	</tbody>
</table>


## 関連する操作

### インスタンスを他のアベイラビリティーゾーンに移行する

インスタンスを一度起動すると、別のアベイラビリティーゾーンに移行することはできません。 ただし、CVM インスタンスのカスタムイメージを作成し、そのイメージを使用して、別のアベイラビリティ ゾーンでインスタンスを起動または更新することができます。
1. 現在のインスタンスのカスタムイメージを作成します。詳細については、[カスタムイメージの作成](https://intl.cloud.tencent.com/document/product/213/4942)をご参照ください。
2. 現在のインスタンスのネットワーク環境が [Virtual Private Cloud](https://intl.cloud.tencent.com/document/product/213/5227) で、移行後に現在のプライベートIPアドレスを保持する必要がある場合は、まず現在のアベイラビリティーゾーンのサブネットを削除し、元のサブネットと同じIPアドレス範囲で新しいアベイラビリティーゾーンにサブネットを作成します。サブネットは、使用可能なインスタンスが含まれていない場合にのみ削除できることに注意してください。したがって、現在のサブネット内のすべてのインスタンスを新しいサブネットに移行する必要があります。
3. 作成したカスタムイメージを使用して、新しいアベイラビリティーゾーンに新しいインスタンスを作成します。ユーザーは、元のインスタンスと同じタイプと構成を選択することも、新しい構成を選択することもできます。詳細については、[インスタンスの作成](https://intl.cloud.tencent.com/document/product/213/4855)をご参照ください。
4. 元のインスタンスがすでにElastic IPアドレスに関連付けられている場合、古いインスタンスとの関連付けを解除してから、新しいインスタンスに関連付ける必要があります。詳細については、[EIP](https://intl.cloud.tencent.com/document/product/213/5733)をご参照ください。
5. （オプション）元のインスタンスが [従量課金制](https://intl.cloud.tencent.com/document/product/213/2180) の場合、元のインスタンスを廃棄することができます。詳細については、 [インスタンスの廃棄](https://intl.cloud.tencent.com/zh/document/product/213/4930) をご参照ください。

### イメージを他のリージョンにコピーする

ユーザーがインスタンスを起動したり、インスタンスを表示したりするなどの操作は、リージョン属性によって識別されます。起動する必要があるインスタンスのイメージがリージョンに存在しない場合は、イメージを目的のリージョンにコピーする必要があります。 詳細については、 [イメージのコピー](https://intl.cloud.tencent.com/document/product/213/4943)をご参照ください。

