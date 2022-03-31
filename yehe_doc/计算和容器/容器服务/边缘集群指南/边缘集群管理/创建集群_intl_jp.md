>?現在のページインターフェースは古いAPIであり、今後メンテナンスが終了する可能性があります。テンセントクバネティスエンジンAPI 3.0インターフェース定義がより規範化され、アクセス遅延が大幅に減少しているため、[テンセントクバネティスエンジンAPI 3.0](https://intl.cloud.tencent.com/zh/document/product/457/32029)をお勧めします。
>

## インターフェースの説明
本インターフェース（CreateCluster）はクラスターの作成に使用されます。

インターフェースのリクエストドメイン名：
```
ccs.api.qcloud.com
```

* クラスターを作成する際には、クラスターのノード（CVM）の数量および構成を指定してください。
* クラスターのすべてのノードは一般のクラウドストレージです。
* 1つのアカウントには5つのクラスターまで作成できます。[チケットを送信](https://console.cloud.tencent.com/workorder/category/create?level1_id=6&level2_id=350&level1_name=%E8%AE%A1%E7%AE%97%E4%B8%8E%E7%BD%91%E7%BB%9C&level2_name=%E5%AE%B9%E5%99%A8%E6%9C%8D%E5%8A%A1CCS)して割り当て量を追加できます。
* 一つのクラスターのノード数は最大20個までです。[チケットを送信](https://console.cloud.tencent.com/workorder/category/create?level1_id=6&level2_id=350&level1_name=%E8%AE%A1%E7%AE%97%E4%B8%8E%E7%BD%91%E7%BB%9C&level2_name=%E5%AE%B9%E5%99%A8%E6%9C%8D%E5%8A%A1CCS) して割り当て量を追加できます。また[CVMインスタンス購入制限](https://cloud.tencent.com/doc/product/213/CVM%E5%AE%9E%E4%BE%8B%E8%B4%AD%E4%B9%B0%E9%99%90%E5%88%B6)ドキュメントに記載されている最大数量制限を満たさなければなりません。
* CPUおよびメモリの**割り当て量制限**の詳細については、[CVMインスタンス設定](https://cloud.tencent.com/doc/product/213/CVM%E5%AE%9E%E4%BE%8B%E9%85%8D%E7%BD%AE)をご参照ください。
* 帯域幅を変更する場合は、ノードが正常に作成されたら、インターフェース [UpdateInstanceBandwidthHour](https://cloud.tencent.com/doc/api/229/1345)を使用して変更してください。**パブリックネットワーク帯域幅が指定されていない場合は、デフォルトで0**です。
* サポートされているノードタイプ **（各アベイラビリティーゾーンで購入する機種が異なる）**の詳細については、[CVMインスタンス設定](https://cloud.tencent.com/doc/product/213/CVM%E5%AE%9E%E4%BE%8B%E9%85%8D%E7%BD%AE)をご参照ください。


##　入力パラメータ
次のリクエストパラメーターリストにはインターフェースリクエストパラメーターだけが記載され、他のパラメーターについては[共通リクエストパラメーター](https://cloud.tencent.com/document/product/457/9463)をご参照ください。

| パラメータ名称       | 説明                                       | タイプ     | 必須項目   | 
|---------|---------|---------|---------|
| clusterName|クラスター名称| String|はい| 
| clusterDesc| クラスタの説明|String|いいえ| 
| clusterCIDR| クラスターコンテナおよびサービスIPの割り当てに使用されるCIDRはVPC CIDRまたは同じVPCの他のクラスターCIDRと競合してはいけません。|String|はい| 
| ignoreClusterCIDRConflict | ClusterCIDR競合エラーを無視するかどうか。デフォルトでは0<br>0：競合を無視しない（エラーを返す）<br>1：競合を無視する（引き続き作成する）|Int|いいえ| 
| zoneId| アベイラビリティーゾーンです。[アベイラビリティーゾーン照会](/doc/api/213/9455)インターフェースから返したZoneフィールドを入力してください| String|はい|
| goodsNum|購入ノード数量です。最大100です。|Int|はい| 
| cpu| CPUのコア数。具体的な制限については上記をご参照ください。 |Int|はい|  
| mem|  メモリのサイズ( GB )です。具体的な制限については上記をご参照ください。 |Int|はい| 
| osName| システム名。centos7.2x86_64またはubuntu16.04.1 LTSx86_64。クラスターにおけるすべてのノードではこのシステムを使用します。拡張ノードも自動的にこのシステムを使用します。|String| はい| 
| instanceType| 詳細については[CVMインスタンス設定](https://cloud.tencent.com/doc/product/213/CVM%E5%AE%9E%E4%BE%8B%E9%85%8D%E7%BD%AE)をご参照ください。デフォルト値：S1.SMALL1|String|いいえ| 
| cvmType| ノードのタイプ。デフォルトでは従量課金です。<br>PayByHour：従量課金  <br>PayByMonth：年額/月額<br>|String|いいえ| 
| renewFlag|年額/月額の自動更新フラグ。数値範囲：<br><li>NOTIFY_AND_AUTO_RENEW：有効期限切れを通知して自動更新する<br><li>NOTIFY_AND_MANUAL_RENEW：有効期限切れを通知するが自動更新しない<br><li>DISABLE_NOTIFY_AND_MANUAL_RENEW：有効期限切れ通知と自動更新はしない<br><br>デフォルト数値：NOTIFY_AND_AUTO_RENEW。このパラメーターはNOTIFY_AND_AUTO_RENEWと指定され、アカウントの残高が十分ある場合は、インスタンスの有効期限が切れた後に毎月自動更新されます。[InstanceChargePrepaid](https://cloud.tencent.com/document/api/213/9451#instancechargeprepaid)をご参照ください。|String|いいえ|
| bandwidthType|帯域幅のタイプ<br>年額/月額のCVM：PayByMonth：帯域幅の使用時間に応じた課金。PayByTraffic：従量課金<br> 従量課金のCVM：PayByHour：帯域幅の使用時間に応じた課金。PayByTraffic：従量課金<br>ネットワーク課金モードの違いについては[ネットワーク帯域幅の購入](/doc/product/213/509)をご参照ください。|  String|はい|
| bandwidth| パブリック帯域幅(Mbps)。従量課金の場合は、パブリック帯域幅のピーク値とします。|Int| はい| 
| wanIp| パブリックIPを有効化するかどうか<br>0：有効化しない<br>1：有効化<br>bandwidthが0以上の場合は、有効にするかどうか自由に選択できます。デフォルトではパブリックIPを有効にします。bandwidthは0の場合は、パブリックIPを割り当てません。| Int| いいえ|
| vpcId| プライベートID。[プライベートネットワークリスト照合](/doc/api/215/1372)インターフェースから返したunVpcId (プライベートネットワークの統一ID)フィールドを入力してください。| String| はい|
| subnetId| サブネットID。[サブネットリスト照合](/doc/api/215/1371)インターフェースから返したunSubnetId(サブネットの統一ID)フィールドを入力してください。|String|  はい| 
| isVpcGateway| パブリックゲートウェイかどうか。パブリックゲートウェイはパブリックIPおよびプライベートネットワークでなければ、正常に使用できません。<br>0：パブリックゲートウェイではない<br>1：パブリックゲートウェイ|Int|はい|  
| rootSize|システムディスクのサイズ。Linux システム調整範囲は20～50GBで、調整単位は1| Int| はい| 
|rootType|システムディスクのタイプ。システムディスクのタイプに関する制限については[CVMインスタンス設定](https://cloud.tencent.com/doc/product/213/2177)をご参照ください。数値範囲：<br><li>LOCAL_BASIC：ローカルディスク<br><li>LOCAL_SSD：ローカルSSDディスク<br><li>CLOUD_BASIC：一般ディスク<br><li>CLOUD_SSD：SSDディスク<br><br>デフォルト数値：CLOUD_BASIC。|String|いいえ|
| storageSize| データディスクのサイズ（GB）。容量単位は10です。0：データディスクが不要。ディスクの最大値については[ディスク製品概要](/doc/product/213/498)をご参照ください。|Int| はい| 
|storageType|データディスクのタイプ。データディスクのタイプ制限については[CVMインスタンス設定](https://cloud.tencent.com/doc/product/213/2177)をご参照ください。数値範囲：<br><li>LOCAL_BASIC：ローカルディスク<br><li>LOCAL_SSD：ローカルSSDディスク<br><li>CLOUD_BASIC：一般ディスク<br><li>CLOUD_PREMIUM：高性能ディスク<br><li>CLOUD_SSD：SSDディスク<br><br>デフォルト数値：CLOUD_BASIC。<br>|String|いいえ|
| password| ノードパスワード。未設定の場合はランダムで生成して、サイト内メッセージで送信されます。ノードパスワードは、[ a - z，A - Z ]、[ 0 - 9 ]  和  [ ( )  & # 96；~ ! @ # $ % ^ & * - + = & #124； { }  [ ] ： ； ' < > ，. ?  /  ]の特殊記号からどれか2種類を組み合わせて8～16文字にしなければなりません|String| いいえ| 
| keyId| [キー](/doc/product/213/503) ID。キーを関連つけるとキーを使用してノードにログインできます。keyIdはインターフェース[キー照合](/doc/api/229/%E6%9F%A5%E8%AF%A2%E5%AF%86%E9%92%A5) により取得できます。キーとパスワードは同時に指定できません。またWindows OSはキーの指定をサポートしません。| String| いいえ|
| period|年額/月額ノード時間（単位：月）。cvmTypeはPayByMonthである場合は、このパラメーターを入力します。 | Int| いいえ| 
| sgId|  セキュリティグループID。デフォルトではセキュリティグループをバインディングしません。[セキュリティグループリスト照合](/doc/api/213/1232)インターフェースから返したsgIdフィールドを入力してください。|String|いいえ| 
| masterSubnetId|  クラスターMasterは一つのVPCサブネットの IPを使用します。このパラメーターはMasterで使用するIPのサブネットを使用します。このサブネットはクラスターと同じVPC内に存在する必要があります。|String|いいえ| 
|userScript|base64でエンコードされたユーザースクリプト。このスクリプトはk8sコンポーネントが動作後に実行します。ユーザーがスクリプトの再入可能と再試行ロジックを保証しなければなりません。スクリプトと生成するログファイルをノードの/data/ccs_userscript/パスで確認できます。|String| いいえ| 

##　出力パラメータ
 
| パラメータ名 | 記述               | タイプ          |
|---------|---------|---------|
| code | 共通エラーコード。0は成功、他の値は失敗を意味します。詳細については[ エラー戻り結果](/doc/api/457/9469)をご参照ください。|Int | 
| codeDesc | サービス側のエラーコード。成功するとSuccessを返します。エラーが発生した場合はサービスエラーの原因を返します。|String |
| message | インターフェースに関連するモジュールエラーメッセージの説明。詳細については[エラー戻り結果](/doc/api/457/9469)をご参照ください。|String | 
| requestId|タスクID |Int |
| clusterId|クラスターID |Int |

## 事例
###　入力
```
  https://domain/v2/index.php?Action=CreateCluster
  &cvmType=PayByHour
  &period=1
  &zoneId=xxxx
  &cpu=1
  &mem=2
  &osName=centos7.2x86_64
  &bandwidthType=PayByTraffic
  &bandwidth=1&wanIp=1
  &vpcId=vpc-xxxxx
  &subnetId=subnet-hadbzxag
  &isVpcGateway=0
  &storageType=CLOUD_PREMIUM
  &storageSize=50
  &rootType=CLOUD_PREMIUM
  &rootSize=50
  &mountTarget=/var/lib/docker
  &dockerGraphPath=/var/lib/docker
  &goodsNum=1
  &sgId=sg-fxdfnvua
  &securityService=0
  &monitorService=1
  &clusterDesc=tete
  &clusterCIDR=xxx.xxx.xxx.xxx/xx
  &ignoreClusterCIDRConflict=0
  &projectId=0
  &asEnabled=0
  &unschedulable=0
  &clusterName=xxxxx
  &clusterVersion=1.8.13
  &instanceType=S3.SMALL2
  &password=xxxxx
  &instanceName=xxxx
  &その他の共通パラメーター
```
###　出力
```
{
    "data":{
        "code":0,
        "message":"",
        "codeDesc":"Success",
        "data":{
            "requestId":xxxx,
            "clusterId":"cls-xxxxxx"
        }
    },
    "message":"",
    "code":0
}
```
