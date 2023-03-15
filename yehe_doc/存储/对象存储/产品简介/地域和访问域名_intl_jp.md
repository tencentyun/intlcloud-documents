## 概要

**リージョン（Region）**とは、Tencent Cloudのホスティングデータセンターが分布する地域です。Cloud Object Storage（COS）のデータはこれらのリージョンのバケット内に保存されます。COSによって、データを複数のリージョンに保存することが可能になります。通常の場合、COSはお客様の業務に最も近いリージョンにバケットを作成することを推奨します。低遅延、低コストおよびコンプライアンスの要件を満たすことができるためです。

例えば、お客様の業務が華南地域に分布している場合は、広州リージョンでのバケット作成を選択することで、オブジェクトのアップロード、ダウンロードの速度をさらに向上させることができます。

**デフォルトドメイン名**とは、COSのデフォルトのバケットドメイン名であり、ユーザーのバケット作成時に、システムがバケット名およびリージョンに基づいて自動的に生成します。デフォルトドメイン名は、バケットの存在するリージョンによって異なります。[COSコンソール](https://console.cloud.tencent.com/cos5)に進み、バケットの**概要 > ドメイン名情報**で確認することができます。


>?
> - 過去のバージョンでサポートされるリージョンの情報については、過去のバージョンのリージョンリストをご参照ください。
> 


### 中国大陸リージョン

<table>
   <tr>
	 <th colspan=3><center>リージョン</center></th>
      <th>リージョン略称</th>
      <th>デフォルトドメイン名（アップロード/ダウンロード/管理 ）</th>
   </tr>
   <tr>
      <td rowspan=10>中国大陸</td>
      <td rowspan=7 nowrap="nowrap">パブリッククラウドリージョン</td>
      <td nowrap="nowrap">北京1区（販売終了）</td>
      <td>ap-beijing-1</td>
      <td>&lt;BucketName-APPID&gt;.cos.ap-beijing-1.myqcloud.com</td>
   </tr>
   <tr>
      <td>北京</td>
      <td>ap-beijing</td>
      <td>&lt;BucketName-APPID&gt;.cos.ap-beijing.myqcloud.com</td>
   </tr>
   <tr>
      <td>南京</td>
      <td>ap-nanjing</td>
      <td>&lt;BucketName-APPID&gt;.cos.ap-nanjing.myqcloud.com</td>
   </tr>
   <tr>
      <td>上海</td>
      <td>ap-shanghai</td>
      <td>&lt;BucketName-APPID&gt;.cos.ap-shanghai.myqcloud.com</td>
   </tr>
   <tr>
      <td>広州</td>
      <td>ap-guangzhou</td>
      <td>&lt;BucketName-APPID&gt;.cos.ap-guangzhou.myqcloud.com</td>
   </tr>
   <tr>
      <td>成都</td>
      <td>ap-chengdu</td>
      <td>&lt;BucketName-APPID&gt;.cos.ap-chengdu.myqcloud.com</td>
   </tr>
   <tr>
      <td>重慶</td>
      <td>ap-chongqing</td>
      <td>&lt;BucketName-APPID&gt;.cos.ap-chongqing.myqcloud.com</td>
   </tr>
</table>




### 中国香港および海外リージョン

<table>
   <tr>
	 <th colspan=3><center>リージョン</center></th>
      <th>リージョン略称</th>
      <th>デフォルトドメイン名（アップロード/ダウンロード/管理 ）</th>
   </tr>
   <tr>
      <td rowspan=7>アジア太平洋</td>
      <td rowspan=13 nowrap="nowrap">パブリッククラウドリージョン</td>
      <td>中国香港</td>
      <td>ap-hongkong</td>
      <td>&lt;BucketName-APPID&gt;.cos.ap-hongkong.myqcloud.com</td>
   </tr>
   <tr>
      <td>シンガポール</td>
      <td>ap-singapore</td>
      <td>&lt;BucketName-APPID&gt;.cos.ap-singapore.myqcloud.com</td>
   </tr>
   <tr>
      <td>ムンバイ</td>
      <td>ap-mumbai</td>
      <td>&lt;BucketName-APPID&gt;.cos.ap-mumbai.myqcloud.com</td>
   </tr>
   <tr>
      <td  nowrap="nowrap">ジャカルタ</td>
      <td>ap-jakarta</td>
      <td>&lt;BucketName-APPID&gt;.cos.ap-jakarta.myqcloud.com</td>
   </tr>
   <tr>
      <td>ソウル</td>
      <td>ap-seoul</td>
      <td>&lt;BucketName-APPID&gt;.cos.ap-seoul.myqcloud.com</td>
   </tr>
   <tr>
      <td>バンコク</td>
      <td>ap-bangkok</td>
      <td>&lt;BucketName-APPID&gt;.cos.ap-bangkok.myqcloud.com</td>
   </tr>
   <tr>
      <td>東京</td>
      <td>ap-tokyo</td>
      <td>&lt;BucketName-APPID&gt;.cos.ap-tokyo.myqcloud.com</td>
   </tr>
   <tr>
      <td rowspan=3>北アメリカ</td>
      <td nowrap="nowrap">シリコンバレー（アメリカ西部）</td>
      <td>na-siliconvalley</td>
      <td>&lt;BucketName-APPID&gt;.cos.na-siliconvalley.myqcloud.com</td>
   </tr>
   <tr>
      <td nowrap="nowrap">バージニア（アメリカ東部）</td>
      <td>na-ashburn</td>
      <td>&lt;BucketName-APPID&gt;.cos.na-ashburn.myqcloud.com</td>
   </tr>
   <tr>
      <td>トロント</td>
      <td>na-toronto</td>
      <td>&lt;BucketName-APPID&gt;.cos.na-toronto.myqcloud.com</td>
   </tr>
   <tr>
      <td rowspan=1>南アメリカ</td>
      <td>サンパウロ</td>
      <td>sa-saopaulo</td>
      <td>&lt;BucketName-APPID&gt;.cos.sa-saopaulo.myqcloud.com</td>
   </tr>
   <tr>
      <td rowspan=2>ヨーロッパ</td>
      <td>フランクフルト</td>
      <td>eu-frankfurt</td>
      <td>&lt;BucketName-APPID&gt;.cos.eu-frankfurt.myqcloud.com</td>
   </tr>
</table>



### グローバルアクセラレーションドメイン名

グローバルアクセラレーションドメイン名の形式は&lt;BucketName-APPID&gt;.cos.accelerate.myqcloud.comです。グローバルアクセラレーションドメイン名の説明と使用例については、[グローバルアクセラレーションの概要](https://intl.cloud.tencent.com/document/product/436/33409)をご参照ください。


### 事例

ルートアカウント（APPIDは1250000000）でCOSコンソールにログインし、バケット1個を作成し、そのバケットの所在リージョンは**広州**リージョン、バケット名は**examplebucket**であったとします。この場合、このバケットのデフォルトドメイン名は次のようになります。

```shell
examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com
```

>?
>
>- examplebucket-1250000000とは、このバケットが、APPIDが1250000000のユーザーのものであることを表します。APPIDはTencent Cloudアカウントの申請に成功すると取得できるアカウントであり、システムによって自動的に割り当てられ、固有かつ唯一のものです。[アカウント情報](https://console.cloud.tencent.com/developer)で確認することができます。
>- cos：Cloud Object Storage（COS）です。
>- ap-guangzhou：バケットリージョンの略称です。
>- myqcloud.com：Tencent Cloudドメイン名であり、固定の文字列です。

バケットの作成完了後、1個の画像ファイルpicture.jpgをこのバケットにアップロードした場合、画像picture.jpgのアクセスアドレスは次のようになります。

```shell
examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/picture.jpg
```

>? 画像のアクセス権限を**パブリック読み取り・プライベート書き込み**に設定している場合、画像のアクセスアドレスをブラウザにペーストして開くと、画像の詳細を確認することができます。
>



## プライベートネットワークおよびパブリックネットワークアクセス

同一リージョンのCloud Virtual Machine（CVM）上で、COSデフォルトドメイン名によってファイルにアクセスする場合、デフォルトではプライベートネットワークリンクを使用します。このとき、ファイルのアップロードとダウンロードの際にはいずれもプライベートネットワークトラフィックが発生し、トラフィック料金は発生しませんが、リクエスト回数に対しては課金されます。

Tencent Cloud COSのアクセスドメイン名にはインテリジェントDNS解決を使用しており、インターネットの様々なキャリア環境の下で、お客様のCOSアクセスにとって最適なリンクを検知および指定します。

Tencent Cloud内でCOSへのアクセス用のサービスをデプロイしている場合、同一リージョン内のアクセスに対しては自動的にプライベートネットワークアドレスが指定されます。リージョン間では現時点ではプライベートネットワークアクセスをサポートしておらず、デフォルトでパブリックネットワークアドレスに解決されます。リージョン間のプライベートネットワーク相互接続をご希望の場合は、[チケットを提出](https://console.cloud.tencent.com/workorder/category)してご連絡ください。

プライベートネットワークとパブリックネットワークの関連情報の詳細については、[リクエスト作成の概要](https://intl.cloud.tencent.com/document/product/436/30613)のドキュメントをご参照ください。

