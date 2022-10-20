## CAMで権限承認が可能なCLBのリソースタイプ
| リソースタイプ | 承認ポリシーにおけるリソースの記述メソッド |
| :-------- | -------------- |
| CLBインスタンス |  ` qcs::clb:$region::clb/$loadbalancerid`  |
| CLBバックエンドサーバー |   `qcs::cvm:$region:$account:instance/$cvminstanceid` |

そのうち：
- `$region`はすべて、あるregionのIDとしなければなりません。空にすることができます。
- `$account`はすべて、リソース所有者のAccountIdとするか、または「\*」としなければなりません。
- `$loadbalancerid`はすべて、あるloadbalancerのIDとするか、または「\*」としなければなりません。

以下同様とします。

## CAMでCLBの権限承認を行うことができるインターフェース
CAMではCLBリソースに対し、次のActionの権限承認を行うことができます。
### インスタンス関連

| API操作 | リソース記述 | インターフェース説明 |
| :-------- | :--------| :------ |
| DescribeLoadBalancers	|  CLBインスタンスリストの照会を行います | `*`はインターフェースに対してのみ認証を行います |
| CreateLoadBalancer	|  CLBを購入します | `qcs:$projectid:clb:$region:$account:clb/*` |
| DeleteLoadBalancers	|  CLBを削除します | `qcs::clb:$region:$account:clb/$loadbalancerid` |
| ModifyLoadBalancerAttributes	|  CLBの属性情報を変更します | `qcs::clb:$region:$account:clb/$loadbalancerid` |
| ModifyForwardLBName	|  CLBの名前を変更します | `qcs::clb:$region:$account:clb/$loadbalancerid` |

### リスナー関連

| API操作 | リソース記述 | インターフェース説明 |
| :-------- | :---------| :------ |
|DeleteLoadBalancerListeners	|CLBリスナーを削除します| `qcs::clb:$region:$account:clb/$loadbalancerid`  |
|DescribeLoadBalancerListeners	|CLBリスナーリストを取得します|	`qcs::clb:$region:$account:clb/$loadbalancerid`  |
|ModifyLoadBalancerListener	|CLBリスナーの属性を変更します|	`qcs::clb:$region:$account:clb/$loadbalancerid` |
|CreateLoadBalancerListeners	|CLBリスナーを作成します|	`qcs::clb:$region:$account:clb/$loadbalancerid` |
|DeleteForwardLBListener	|CLBリスナーを削除します（レイヤー4およびレイヤー7）|	`qcs::clb:$region:$account:clb/$loadbalancerid`  |
|ModifyForwardLBSeventhListener	|CLBレイヤー7リスナーの属性を変更します|	`qcs::clb:$region:$account:clb/$loadbalancerid`  |
|ModifyForwardLBFourthListener	|CLBレイヤー4リスナーの属性を変更します|	`qcs::clb:$region:$account:clb/$loadbalancerid`  |
|DescribeForwardLBListeners	|CLBリスナーリストの照会を行います|	`qcs::clb:$region:$account:clb/$loadbalancerid` |
|CreateForwardLBSeventhLayerListeners	|レイヤー7CLBリスナーを作成します|	`qcs::clb:$region:$account:clb/$loadbalancerid` |
|CreateForwardLBFourthLayerListeners	|レイヤー4CLBリスナーを作成します	|`qcs::clb:$region:$account:clb/$loadbalancerid` |

### CLBドメイン名 + URL関連

| API操作 | リソース記述 | インターフェース説明 |
| :-------- | --------| :------ |
|ModifyForwardLBRulesDomain|	CLBリスナー転送ルールのドメイン名を変更します  |	`qcs::clb:$region:$account:clb/$loadbalancerid`  |
|CreateForwardLBListenerRules|	CLBリスナー転送ルールを作成します|	`qcs::clb:$region:$account:clb/$loadbalancerid`  |
|DeleteForwardLBListenerRules	|レイヤー7CLBリスナーのルールを削除します|	`qcs::clb:$region:$account:clb/$loadbalancerid` |
|DeleteRewrite	|CLB転送ルール間のリダイレクト関係を削除します|	`qcs::clb:$region:$account:clb/$loadbalancerid` |
|ManualRewrite	|CLB転送ルールのリダイレクト関係を手動で追加します| `qcs::clb:$region:$account:clb/$loadbalancerid`  |
|AutoRewrite	|CLB転送ルールのリダイレクト関係を自動生成します|`qcs::clb:$region:$account:clb/$loadbalancerid`  |

### バックエンドサーバー関連

| API操作 | リソース記述 | インターフェース説明 |
| :-------- | :--------| :------ |
|ModifyLoadBalancerBackends	| CLBバックエンドサーバーの重みを変更します|	`qcs::clb:$region:$account:clb/$loadbalancerid` |
|DescribeLoadBalancerBackends	| CLBにバインドしたバックエンドサーバーのリストを取得します|	`qcs::clb:$region:$account:clb/$loadbalancerid`  |
|DeregisterInstancesFromLoadBalancer |	バックエンドサーバーのバインドを解除します|	`qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::cvm:$region:$account:instance/$cvminstanceid`|
|RegisterInstancesWithLoadBalancer	| バックエンドサーバーをCLBにバインドします|	`qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::cvm:$region:$account:instance/$cvminstanceid`|
|DescribeLBHealthStatus	| CLBヘルスステータスの照会を行います|	`qcs::clb:$region:$account:clb/$loadbalancerid`  |
|ModifyForwardFourthBackendsPort	| レイヤー4リスナーの転送ルール上のCVMのポートを変更します|	`qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::cvm:$region:$account:instance/$cvminstanceid` |
|ModifyForwardFourthBackendsWeight	|レイヤー4リスナーの転送ルール上のCVMの重みを変更します|`qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::cvm:$region:$account:instance/$cvminstanceid` |
|RegisterInstancesWithForwardLBSeventhListener	| CVMをCLBレイヤー7リスナーの転送ルール上にバインドします|	`qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::cvm:$region:$account:instance/$cvminstanceid` |
|RegisterInstancesWithForwardLBFourthListener| CVMをCLBレイヤー4リスナーの転送ルール上にバインドします|	`qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::cvm:$region:$account:instance/$cvminstanceid` |
|DeregisterInstancesFromForwardLBFourthListener	|CLBレイヤー4リスナーの転送ルール上のCVMのバインドを解除します|	`qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::cvm:$region:$account:instance/$cvminstanceid` |
|DeregisterInstancesFromForwardLB	| CLBレイヤー7リスナーの転送ルール上のCVMのバインドを解除します|	`qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::cvm:$region:$account:instance/$cvminstanceid` |
|ModifyForwardSeventhBackends	| レイヤー7リスナーの転送ルール上のCVMの重みを変更します|	`qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::cvm:$region:$account:instance/$cvminstanceid`|
|ModifyForwardSeventhBackendsPort	| レイヤー7リスナーの転送ルール上のCVMのポートを変更します|`qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::cvm:$region:$account:instance/$cvminstanceid`|
|DescribeForwardLBBackends |	CLBのCVMリストの照会を行います|	`qcs::clb:$region:$account:clb/$loadbalancerid` `qcs::cvm:$region:$account:instance/*`|
|DescribeForwardLBHealthStatus	|CLBのヘルスチェックステータスの照会を行います|	`qcs::clb:$region:$account:clb/*`  |
|ModifyLoadBalancerRulesProbe	| CLBリスナーの転送ルールのヘルスチェックおよび転送パスを変更します|	`qcs::clb:$region:$account:clb/$loadbalancerid` |


