
## 概要

このドキュメントでは、主にCloud Connect Networkを複数のプライベートネットワーク相互接続サービスに関連付け、各リージョンのクラウド上、クラウド下の複数の相互接続を実現する方法について説明しています。

## 前提条件
[アセット](https://intl.cloud.tencent.com/document/product/1055/36674)または[イメージリソース](https://intl.cloud.tencent.com/document/product/1055/39061)を作成済み。

## 操作手順

### サーバーフリートの作成時

1. [GSEコンソール](https://console.cloud.tencent.com/gse/asset)にログインし、左側メニューの**サーバーフリート**をクリックして、フリートリストの画面に入ります。
2. **新規作成**をクリックし、サーバーフリートを作成します。
<img src="https://camo.githubusercontent.com/02155cd8e3264bae81e2936d80c5a421bbde29c0340f690a24b1f859f8bedaf0/68747470733a2f2f6d61696e2e71636c6f7564696d672e636f6d2f7261772f35393464663837326437393431626663656462633237383939376139343866322e706e67" style="width: 95%;"/>
3. サーバーフリートの「Cloud Connect Networkの関連付け」画面の**はい**にチェックを入れます。
<dx-alert infotype="explain" title="">
 - 同一アカウントのVPCに対してCloud Connect Networkの自動チェックを行いたい場合は、チェックを入れた後に [サービス権限の承認](#test51) をし、以下の操作を行います。
 - 自動承認が必要ない場合は、ポップアップされた「VPC承認の自動チェック」中の**取消**または「X」をクリックし、ポップアップを閉じて、引き続き以下の操作を行います。
</dx-alert>


![](https://camo.githubusercontent.com/d01cc445038fa547acb626b29ca43a9766629b00e284397111976373e7ab4395/68747470733a2f2f6d61696e2e71636c6f7564696d672e636f6d2f7261772f36633937363661323636363332363932326438333238383966356361646431382e706e67)
4.アカウントIDおよびCloud Connect Network IDを入力し、関連付け操作を行います。
![](https://camo.githubusercontent.com/a30c3ed1cf7dda51ec46c1ee93a558a328e0773aa4d48e685964551063f52e53/68747470733a2f2f6d61696e2e71636c6f7564696d672e636f6d2f7261772f39313966636633626661313934643032616236663137376262343063373464302e706e67)
<dx-alert infotype="explain" title="">
- サーバーフリート作成過程でCloud Connect Networkを関連付けるには、20分以内に申請に同意してください。そうでなければ作成は失敗します。
- Cloud Connect Networkへのインスタンス追加で発生するネットワーク相互接続料金は、Cloud Connect Networkが所在するアカウントが負担します。  
- このCloud Connect Network内のインスタンスの所属リージョンは、現時点では異なるリージョン間の相互接続サービスをサポートしていません。必要な場合はサービス担当者に連絡してください。 
</dx-alert>

 

### [サーバーフリート作成完了後](id:test21)

1. [GSEコンソール](https://console.cloud.tencent.com/gse/asset)にログインし、左側メニューの**サーバーフリート**をクリックして、フリートリストの画面に入ります。
2. [サーバーフリートの作成](https://intl.cloud.tencent.com/document/product/1055/36675)を完了します。
3. **ID**をクリックして、Cloud Connect Networkの関連付けが必要なフリート詳細画面に入ります。
![](https://camo.githubusercontent.com/3bc6a3b373b8dab13e24bb09a8d80b5a0e7579a6dcd56e3c2d346364b17b1351/68747470733a2f2f6d61696e2e71636c6f7564696d672e636f6d2f7261772f36333433313438373761663863626633323162626231663762643635626437332e706e67)
4. サーバーフリート詳細画面で、右側の**今すぐ関連付ける**をクリックすれば、関連付け操作を実行できます。
<dx-alert infotype="explain" title="">
- 同一アカウントのVPCに対してCloud Connect Networkの自動チェックを行いたい場合は、チェックを入れた後に [サービス権限の承認](#test51) をし、以下の操作を行います。
- 自動承認が必要ない場合は、ポップアップされた「VPC承認の自動チェック」中の**取消**または「X」をクリックし、ポップアップを閉じて、引き続き以下の操作を行います。
</dx-alert>



![](https://camo.githubusercontent.com/cd203d79081eeb9400dfa0420edfafbe3850f776d8d3671e9f793d8a8bd67783/68747470733a2f2f6d61696e2e71636c6f7564696d672e636f6d2f7261772f36333634363064396435376536613034336131373531393763343632323662312e706e67)
5. アカウントIDおよびCloud Connect Network IDを入力し、関連付け操作を行います。
<img src="https://camo.githubusercontent.com/d71628bf784f991f4d683f53951fd34dd0eaf5aa31e886e0dab1971c4353121d/68747470733a2f2f6d61696e2e71636c6f7564696d672e636f6d2f7261772f61346137376234616666366234333366643733373564613463306536373639372e706e67" alt="" class="zoom-img-hover" style="
    width: 65%;
">
<dx-alert infotype="explain" title="">
- サーバーフリート作成完成後のCloud Connect Networkの関連付けは、相手方が7日の内に申請に同意することが必要です。7日後の申請は期限切れになります。  
- Cloud Connect Networkへのインスタンス追加で発生するネットワーク相互接続料金は、Cloud Connect Networkが所在するアカウントが負担します。  
- このCloud Connect Network内のインスタンスの所属リージョンは、現時点では異なるリージョン間の相互接続サービスをサポートしていません。必要な場合はサービス担当者に連絡してください。  
</dx-alert>






### フリートのコピー時

1. [GSEコンソール](https://console.cloud.tencent.com/gse/asset)にログインし、左側メニューの**サーバーフリート**をクリックして、フリートリストの画面に入ります。
2. [サーバーフリートの作成](https://intl.cloud.tencent.com/document/product/1055/36675)を完了します。
3. **コピー**をクリックし、フリートのコピー画面に入ります。
![](https://qcloudimg.tencent-cloud.cn/raw/cb8288e39fc8067ba254712671042492.png)
4. 「基本情報」画面の**クリックして開く**をクリックし、フリート詳細画面を開きます。
5. フリート詳細画面の「Cloud Connect Networkの関連付け」中の**はい**にチェックを入れます。
<dx-alert infotype="explain" title="">
- 同一アカウントのVPCに対してCloud Connect Networkの自動チェックを行いたい場合は、チェックを入れた後に [サービス権限の承認](#test51) をし、以下の操作を行います。
- 自動承認が必要ない場合は、ポップアップされた「VPC承認の自動チェック」中の**取消**または「X」をクリックし、ポップアップを閉じて、引き続き以下の操作を行います。
</dx-alert>

![](https://qcloudimg.tencent-cloud.cn/raw/76a17da70c59d8bac78e668c3823445a.png)
6. アカウントIDおよびCloud Connect Network IDを入力し、関連付け操作を行います。
![](https://qcloudimg.tencent-cloud.cn/raw/9e763574c405f714e255020f5284398e.png)
7. 関連付けるタイミングにチェックを入れます。
 - フリート作成時に関連付けを申請する場合、相手側のアカウントを20分以内にチェックする必要があります。そうでない場合、サーバーフリートの作成に失敗します。
 - フリート作成の完了後に関連付けを申請し、相手側アカウントが7日以内に申請に同意する必要があります。




## [サービス権限の承認](id:test51)

GSEにサービス権限を付与し、同一アカウントのVPCに対してCloud Connect Networkの自動チェックを行わせることができます。具体的な操作手順は次のとおりです。
1. ポップアップされた「VPC承認の自動チェック」中の**Cloud Access Managementに進む**をクリックし、CAMコンソールに入ります。
<img src="https://qcloudimg.tencent-cloud.cn/raw/2a85c9164001aeb4b345b48c28331fd4.png" alt="" class="zoom-img-hover" style="
    width: 70%;
">
2. ロール管理画面で**権限承認に同意**をクリックし、サービス権限の承認を完了します。
<img src="https://qcloudimg.tencent-cloud.cn/raw/f44c110c8866ddd2b14bbfd23730e422.png" alt="" class="zoom-img-hover" style="
    width: 70%;
">

このほか、サブアカウントで「VPC承認の自動チェック」を行いたい場合は、まずルートアカウントでサービス権限の承認を行ってから、以下の権限構文でサブアカウントに権限を付与します。
<dx-codeblock>
:::  Java
{
	"version": "2.0", 
	"statement": [
		{
				"effect": "allow",
				"action": [
						"cam:ListAttachedRolePolicies",
						"cam:GetRole"
				],
				"resource": "*"
		}
	]
}
:::
</dx-codeblock>



