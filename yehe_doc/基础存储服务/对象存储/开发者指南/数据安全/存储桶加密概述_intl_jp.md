## 概要

バケット暗号化はバケットに対する設定の1つであり、バケット暗号化を設定することで、新たにバケットにアップロードされたすべてのオブジェクトに対し、デフォルトで、指定された暗号化方式で暗号化を行うことができます。

現在はSSE-COS暗号化をサポートしています。これはCloud Object Storage（COS）ホストキーを使用したサーバー側の暗号化です。

サーバー側の暗号化に関するその他の情報については、[サーバー側の暗号化の概要](https://intl.cloud.tencent.com/document/product/436/18145)をご参照ください。

## 使用方法

#### COSコンソールの使用

COSコンソールを使用してバケットの暗号化を設定することができます。詳細については、[バケット暗号化の設定](https://intl.cloud.tencent.com/document/product/436/33455)のコンソールガイドドキュメントをご参照ください。

#### REST APIの使用
次のAPIによってバケットの暗号化を設定できます。

- [PUT Bucket encryption](https://intl.cloud.tencent.com/document/product/436/33459) 
- [GET Bucket encryption](https://intl.cloud.tencent.com/document/product/436/33460) 
- [DELETE Bucket encryption](https://intl.cloud.tencent.com/document/product/436/33461) 

## 注意事項

#### 暗号化されたバケットへのオブジェクトのアップロード

バケット暗号化機能を設定したいバケットについては、次の数点に注意が必要です。

- バケット暗号化では、バケット内にすでに存在するオブジェクトに対する暗号化操作は行いません。
- バケット暗号化を設定した後、このバケットにアップロードされるオブジェクトは次のようになります。
  - PUTリクエストに暗号化情報が含まれていない場合、アップロードされるオブジェクトはバケットの暗号化設定によって暗号化されます。
  - PUTリクエストに暗号化情報が含まれている場合、アップロードされるオブジェクトはPUTリクエスト内の暗号化情報によって暗号化されます。
- バケット暗号化を設定した後、このバケットに送信されるリストレポートは次のようになります。
  - リスト自体に暗号化が設定されていない場合、送信されるリストはバケットの暗号化設定によって暗号化されます。
  - リスト自体に暗号化が設定されている場合、送信されるリストはリストの暗号化設定によって暗号化されます。
- バケット暗号化を設定した後、このバケットにback-to-originされるデータは、デフォルトでバケットの暗号化設定によって暗号化されます。

#### クロスリージョンレプリケーションルールが設定されているバケットに対する暗号化

クロスリージョンレプリケーションルールが設定されているターゲットバケットに対し、さらにバケット暗号化を設定する場合は、次の数点に注意が必要です。

- ソースバケット内のオブジェクトが暗号化されていない場合、ターゲットバケット内のレプリカオブジェクトに対してはデフォルトで暗号化が設定されます。
- ソースバケット内のオブジェクトが暗号化されている場合、ターゲットバケット内のレプリカオブジェクトはソースバケットの暗号化を継承するため、バケット暗号化設定は実行されません。


