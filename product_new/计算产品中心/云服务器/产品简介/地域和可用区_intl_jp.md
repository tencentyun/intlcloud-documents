## リージョン

### 概要

リージョンとは、物理的なデータセンターの地理的地域です。Tencent Cloudは異なるリージョン間で完全に隔離されて、それぞれのリージョン間で最大限の安定性とフォールトトレランスが確保されます。アクセスのレイテンシーを低減し、ダウンロード速度を向上するためには、顧客に最も近いリージョンを選定することをお勧めします。

以下の表をご確認いただくか、APIインターフェース[リージョン一覧照会](http://intl.cloud.tencent.com/document/product/213/9456)から完全なリージョン一覧をご確認いただけます。

### 関連特徴

- 異なるリージョン間のネットワークは完全に隔離されており、異なるリージョン間のクラウド製品は、**デフォルトではプライベートネットワークを介して通信できません**。
- 異なるリージョン間でクラウド製品は、[パブリックIPアドレス](http://intl.cloud.tencent.com/document/product/213/5224)を介してインターネットにアクセスできます。Virtual Private Cloud上のクラウド製品は、Tencent Cloudが提供する[Peering Connection](http://intl.cloud.tencent.com/document/product/215/5000) を介してTencent Cloud高速インターネット通信経由で、 インターネットアクセスよりも安定した高速な相互接続を実現できます。
- [Cloud Load Balancer](https://intl.cloud.tencent.com/document/product/214 ) 現在、デフォルトでは、同一リージョンのトラフィック転送をサポートし、対象リージョンのCVMをバインディングします。[クロスリージョンバインディング](http://intl.cloud.tencent.com/document/product/214/12014) 機能をアクティブにすると、Cloud Load BalancerがCVMをクロスリージョンでバインディングできるようになります。

## アベイラビリティーゾーン

### 概要

アベイラビリティーゾーンとは、Tencent Cloudが同じリージョン内で電源とネットワークが独立した物理的なデータセンターです。ユーザーのサービスをオンラインで継続させるために、アベイラビリティーゾーン間の障害を互いに隔離させ(大きな災害または電力システム障害の場合を除く)、障害が広がらないようにすることは目的です。独立したアベイラビリティーゾーン内のインスタンスを起動することにより、ユーザーは単一障害点の影響からアプリケーションを保護できます。
APIインターフェース[アベイラビリティーゾーン一覧照会](http://intl.cloud.tencent.com/document/product/213/9455) を介して、完全なアベイラビリティーゾーン一覧を確認できます。

### 関連特徴

クラウド製品は同じリージョン内の異なるアベイラビリティーゾーンに存在しますが、同じVPCのクラウド製品間でプライベートネットワークを介して相互運用できるため、[プライベートIPアドレス](http://intl.cloud.tencent.com/document/product/213/5225)を直接使用してアクセスすることができます。
> プライベートネットワーク相互運用とは、同じアカウントのリソースは资源運用できますが、異なるアカウントのリソースは、プライベートネットワークで完全に隔離されていることです。

<span id="MainlandChina"></span>
## 中国
<table class="table-striped">
<tbody>
	<tr>
		<th>リージョン</th>
		<th>アベイラビリティーゾーン</th>
	</tr>
	<tr>
		<td rowspan="4">華南地区(広州)<br> ap-guangzhou</td>
		<td>広州1区(売り切れ)<br> ap-guangzhou-1</td>
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
		<td rowspan="4">華東地区(上海)<br>ap-shanghai</td>
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
	<tr>
			<td rowspan="4">華北地区(北京)<br>ap-beijing</td>
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
		<td rowspan="2">西南地区(成都)<br>ap-chengdu</td>
		<td>成都1区<br>ap-chengdu-1</td>
	</tr>
	<tr>
			<td>成都2区<br>ap-chengdu-2</td>
	</tr>    
	<tr>
			<td >西南地区(重慶)<br>ap-chongqing</td>
			<td>重慶1区<br>ap-chongqing-1</td>
	</tr>
	<tr>
			<td rowspan="2">香港・マカオ・台湾リージョン(中国香港)<br>ap-hongkong</td>
			<td>香港1区(中国香港ノードは香港・マカオ・台湾地域をカバーできる)<br>ap-hongkong-1</td>
	</tr>
	<tr>
			<td>香港2区(中国香港ノードは香港・マカオ・台湾地域をカバーできる)<br>ap-hongkong-2</td>
	</tr>
</tbody>
</table>	

<span id="InternationalArea"></span>

## その他の国と地域	
<table class="table-striped">
	<tbody>
	<tr>
			<th>リージョン</th>
			<th>アベイラビリティーゾーン</th>
		</tr>
		<tr>
			<td>東南アジアパシフィック(シンガポール)<br>ap-singapore</td>
			<td>シンガポール1区(シンガポールノードは東南アジアパシフィック地域をカバーできる)<br>ap-singapore-1</td>
		</tr>
		<tr>
			<td >北東アジアパシフィック(ソウル)<br>ap-seoul</td>
			<td>ソウル1区(ソウルノードは北東アジアパシフィック地域をカバーできる)<br>ap-seoul-1</td>
		</tr>
		<tr>
			<td >北東アジアパシフィック(東京)<br>ap-tokyo</td>
			<td>東京１区(東京ノードは北東アジアパシフィック地域をカバーできる)<br>ap-tokyo-1</td>
		</tr>
       <tr>
			<td  rowspan="2">南アジアパシフィック(ムンバイ)<br>ap-mumbai</td>
			<td>ムンバイ1区(ムンバイノードは南アジアパシフィック地域をカバーできる)<br>ap-mumbai-1</td>
		</tr>
       <tr>
			<td>ムンバイ2区(ムンバイノードは南アジアパシフィック地域をカバーできる)<br>ap-mumbai-2</td>
		</tr>
		<tr>
		  	<td >東南アジア(バンコク)<br>ap-bangkok </td>
				 <td >バンコク1区  (バンコクノードは東南アジアパシフィック地域をカバーできる)<br>ap-bangkok-1</td>
		<tr>
			<td>北米地域(トロント)<br>na-toronto</td>
			<td>トロント1区(トロントノードは北米地域をカバーできる)<br>na-toronto-1</td>
		</tr>
		<tr>
			<td rowspan="2">米国西部(シリコンバレー)<br>na-siliconvalley</td>
			<td>リコンバレー1区(シリコンバレーノードは米国西部をカバーできる)<br>na-siliconvalley-1</td>
		</tr>
    <tr>
			<td>リコンバレー2区(シリコンバレーノードは米国西部をカバーできる)<br>na-siliconvalley-2</td>
		</tr>
		<tr>
			<td rowspan="2">米国東部(バージニア)<br>na-ashburn</td>
			<td>バージニア1区 (バージニアノードは米国東部をカバーできる)<br>na-ashburn-1</td>
		</tr>
		<tr>
			<td>バージニア2区 (バージニアノードは米国東部をカバーできる)<br>na-ashburn-2</td>
		</tr>
		<tr>
			<td>欧州リージョン(フランクフルト)<br>eu-frankfurt</td>
			<td>フランクフル1区(フランクフルトノードは欧州地域をカバーできる)<br>eu-frankfurt-1</td>
		</tr>
		<td >欧州リージョン(モスクワ)<br>eu-moscow</td>
		<td>モスクワ1区(モスクワノードアベイラビリティーゾーンは欧州地域をカバーできる)<br>eu-moscow-1</td>
		</tr>
	</tbody>
</table>

## リージョンとアベイラビリティーゾーンの選定方法

リージョンとアベイラビリティーゾーンを選択する際に、以下の要因を考慮する必要があります。
- CVMの所在地、ユーザーおよびターゲットユーザーの地理的な場所。
アクセスのレイテンシーを低減し、アクセス速度を向上するためには、CVMを購入する際に、顧客に最も近いリージョンを選定することをお勧めします。
- CVMと他のクラウド製品との関係。
他のクラウド製品を選定する際に、各クラウド製品がプライベートネットワークを介して通信できるように、なるべく同じリージョンの同じアベイラビリティーゾーンにすることをお勧めします。その場合、アクセスのレイテンシが低減され、アクセス速度が向上されます。
-サービスの高可用性と災害復帰の考慮事項。
VPCが1つしかないユースケースでも、アベイラビリティーゾーン間の障害隔離を確保し、クロスアベイラビリティーの災害復帰を実現するために、サービスを少なくとも異なるアベイラビリティーゾーンにデプロイすることをお勧めします。
-異なるアベイラビリティーゾーン間でネットワーク通信のディレーが発生する可能性がありますので、実際のサービス要件に応じて検討し、高可用性と低レイテンシとの最適なバランスを取る必要があります。
- 他の国や地域のホストにアクセスする必要がある場合は、他の国や地域のCVMを選択してアクセスすることをお勧めします。[中国](#MainlandChina)でCVMを作成して、[他の国・地域のホスト](#InternationalArea)にアクセスする場合、アクセスのディレーが高くなるため、ご利用はお勧めしません。

## リソース場所の説明
ここでは、Tencent Cloudにおいて、どのリソースがグローバル的なものであるか、どのリソースがリージョンによって異なり、アベイラビリティーゾーンに依存しないものであるか、どのリソースがアベイラビリティーゾーンに基づくものであるかを説明します。

<table>
	<tr><th>リソース</th><th>リソース ID形式<br><リソースの略語>-8桁の数字と文字</th><th>種類</th><th>説明</th></tr>
	<tbody>
	<tr>
	  <td>ユーザーアカウント</td>
	  <td>制限なし</td>
	  <td>グローバルに一意</td>
	  <td>ユーザーは同じアカウントで、Tencent Cloudのグローバルリソースにアクセスできます。</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/213/6092">SSHキー</a> </td>
	  <td>skey-xxxxxxxx</td>
	  <td>すべてのリージョンで利用可能</td>
	  <td>ユーザーはSSHキーを使用して、アカウントに対応する任意のリージョンのCVMをバインディングできます。</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/213/4939">CVMインスタンス</a> </td>
	  <td>ins-xxxxxxxx</td>
	  <td>単一リージョンの単一アベイラビリティーゾーンでのみ利用可能</td>
	  <td>ユーザーは特定のアベイラビリティーゾーンでのみCVMインスタンスを作成できます。</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/213/4941#custom-images">カスタマイズイメージ</a> </td>
	  <td>img-xxxxxxxx</td>
	  <td>単一リージョンの複数のアベイラビリティーゾーンで利用可能</td>
	  <td>ユーザーはインスタンスのカスタマイズイメージを作成でき、また、同じリージョンの異なるアベイラビリティーゾーンで使用できます。他のリージョンで使用する場合は、イメージのコピー機能を利用して、カスタマイズイメージを他のリージョンにコピーしてください。</td>
	</tr>
	<tr>
	<td> <a href="http://intl.cloud.tencent.com/document/product/213/5733">Elastic IP</a> </td>
	  <td>eip-xxxxxxxx</td>
	  <td>単一リージョンの複数のアベイラビリティーゾーンで利用可能</td>
	  <td>Elastic IPアドレスは特定のリージョンで作成され、同じリージョンのインスタンスにのみ関連付けられます。</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/213/12452">セキュリティグループ</a> </td>
	  <td>sg-xxxxxxxx</td>
	  <td>単一リージョンの複数のアベイラビリティーゾーンで利用可能</td>
	  <td>セキュリティグループは、特定のリージョンで作成され、同じリージョン内のインスタンスにのみ関連付けられます。Tencent Cloudは、ユーザーに3つのデフォルトセキュリティグループを自動的に作成します。</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/362">Cloud Block Storage</a> </td>
	  <td>disk-xxxxxxxx</td>
	  <td>単一リージョンの単一アベイラビリティーゾーンでのみ利用可能</td>
	  <td>ユーザーは、特定のアベイラビリティーゾーンでのみCloud Block Storageを作成でき、また、同じアベイラビリティーゾーンのインスタンスにマウントできます。</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/362/2345">スナップショット</a> </td>
	  <td>snap-xxxxxxxx</td>
	  <td>単一リージョンの複数のアベイラビリティーゾーンで利用可能</td>
	  <td>特定のCloud Block Storageにスナップショットを作成してから、ユーザーは対象リージョンで作成されたスナップショットを使用して、他の操作(Cloud Block Storageの作成など)を行うことができます。</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/214/524">Cloud Load Balancer</a> </td>
	  <td>clb-xxxxxxxx</td>
	  <td>単一リージョンの複数のアベイラビリティーゾーンで利用可能</td>
	  <td>Cloud Load Balancerは、単一リージョン内の異なるアベイラビリティーゾーンのCVMをバインディングして、トラフィックを転送することができます。</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/215/535">Virtual Private Cloud</a> </td>
	  <td>vpc-xxxxxxxx</td>
	  <td>単一リージョンの複数のアベイラビリティーゾーンで利用可能</td>
	  <td>Virtual Private Cloudは特定のリージョンに作成され、異なるアベイラビリティーゾーンで同じVirtual Private Cloudに属するリソースを作成できます。</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/215/535">サブネット</a> </td>
	  <td>subnet-xxxxxxxx</td>
	  <td>単一リージョンの単一アベイラビリティーゾーンでのみ利用可能</td>
	  <td>ユーザーは、アベイラビリティーゾーンを跨ってサブネットを作成することができません。</td>
	</tr>
	<tr>
	<td> <a href="https://intl.cloud.tencent.com/document/product/215/4954">ルートテーブル</a> </td>
	  <td>rtb-xxxxxxxx</td>
	  <td>単一リージョンの複数のアベイラビリティーゾーンで利用可能</td>
	  <td>ユーザーは、ルートテーブルを作成するときに特定のVirtual Private Cloudを指定する必要があるため、Virtual Private Cloudの場所属性に従います。</td>
	</tr>
	</tbody>
</table>


## 関連操作

### インスタンスを他のアベイラビリティーゾーンに移行させる

すでに起動されたインスタンスは、対象アベイラビリティーゾーンを変更できませんが、ユーザーは他の方法でインスタンスを他のアベイラビリティーゾーンに移行させることができます。移行は、元のインスタンスからカスタマイズイメージを作成し、カスタマイズイメージを使用して新しいアベイラビリティーゾーンでインスタンスを起動し、新しいインスタンスの構成を更新する手順になります。
1. 現在のインスタンスのカスタマイズイメージを作成します。詳細については、[カスタマイズイメージの作成](http://intl.cloud.tencent.com/document/product/213/4942)を参照してください。
2. 現在のインスタンスのネットワーク環境が[Virtual Private Cloud](http://intl.cloud.tencent.com/document/product/213/5227)であり、また、移行後に現在のプライベートIPアドレスを保持する必要がある場合、ユーザーは現在のアベイラビリティ
3. ーゾーン内のサブネットを作成してから、新しいアベイラビリティーゾーンで元のサブネットと同じIPアドレス範囲でサブネットを作成できます。使用可能なインスタンスを含まないサブネットのみが削除可能であることに注意してください。そのため、現在のサブネット内のすべてのインスタンスを新しいサブネットに移行させる必要があります。
3. 上記手順で作成されたカスタマイズイメージを使用して、新しいアベイラビリティーゾーンで新しいインスタンスを作成します。ユーザーは、元のインスタンスと同じインスタンスタイプの構成を選択するか、新しいインスタンスタイプと構成を選択できます。詳細については、[インスタンスの購入と起動](http://intl.cloud.tencent.com/document/product/213/4855)を参照してください。
4. 元のインスタンスがすでにElastic IPアドレスに関連付けられている場合、古いインスタンスとの関連付けを解除してから、新しいインスタンスに関連付ける必要があります。詳細については、[Elastic IP](http://intl.cloud.tencent.com/document/product/213/5733)を参照してください。
5. (オプション)元のインスタンスが[従量課金](http://intl.cloud.tencent.com/document/product/213/2180)タイプの場合、元のインスタンスを廃棄することができます。詳細については、[Destruction Instances](http://intl.cloud.tencent.com/document/product/213/4930)を参照してください。

### イメージを他のリージョンにコピーする

インスタンスの起動と表示などのユーザー操作はすべて、リージョン属性に依存します。起動するインスタンスのイメージが対象リージョンに存在しない場合、イメージを対象リージョンにコピーする必要があります。詳細については、[イメージのコピー](http://intl.cloud.tencent.com/document/product/213/4943)を参照してください。
