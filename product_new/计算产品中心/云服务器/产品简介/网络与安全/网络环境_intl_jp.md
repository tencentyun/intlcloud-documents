Tencent Cloudのネット環境は、[Virtual Private Cloud](https://intl.cloud.tencent.com/product/vpc?idx=2)（VPC）と基幹ネットワークの二種類に分けられます。



## VPCと基幹ネットワーク

### VPC

Tencent Cloud[VPC](https://intl.cloud.tencent.com/document/product/215) は、ユーザーがTencent Cloudにおいてカスタマイズしたロジック的に隔離されているネットワークスペースです。同じ地域にあっても、異なるVPCの間はデフォルトで相互通信できません。ユーザーがデータセンターにおいて使用している従来のネットワークに類似し、Tencent Cloud VPCにホスティングされるのは、 [Cloud Virtual Machine](https://intl.cloud.tencent.com/document/product/213/495)、[Cloud Load Balancer](https://intl.cloud.tencent.com/document/product/214/524)、[クラウドデータベース](https://intl.cloud.tencent.com/document/product/236) などのクラウドサービスを含む、ユーザーが保有しているTencent Cloudのサービスリソースです。ユーザーは、VPCの環境を完全に把握できます、構成とユースケースの詳細については、[VPC製品の概要](https://intl.cloud.tencent.com/document/product/215/535)をご参照ください。VPCは複雑なネットワークアーキテクチャを構築できるため、ネットワーク管理に慣れているユーザーに適しています。
![](https://mc.qcloudimg.com/static/img/33f800da64d2b7c0e6c2f23f102e059a/image.png)

### 基幹ネットワーク

基幹ネットワークは、Tencent Cloudにおけるすべてのユーザーのパブリックネットワークリソースプールです。クラウドにおけるユーザーリソースはすべてTencent Cloudによって統一的に管理されるため、その管理は手軽かつ迅速です。

### 機能の区別

| **機能**| **基幹ネットワーク**| **VPC** |
|---------|---------|---------|
| テナント関連付け | テナント関連付け| GREに基づいてカプセル化したロジック的に隔離されたネットワークです |
| ネットワークのカスタマイズ | 未対応| 対応|
| ルーティングのカスタマイズ | 未対応| 対応|
| IPのカスタマイズ | 未対応| 対応|
| 相互接続ルール |同一テナント、同一地域で相互接続します| クロスリージョン、クロスアカウントの相互接続に対応しています |
| セキュリティ制御　| [セキュリティグループ](https://intl.cloud.tencent.com/document/product/213/12452)| [セキュリティグループ](https://intl.cloud.tencent.com/document/product/213/12452) と [ネットワークACL](https://intl.cloud.tencent.com/document/product/215/5132) |

## VPCと基幹ネットワーク間のリソース共有及びアクセス

Tencent Cloudにおける一部のクラウドソースと機能は両方のネット環境に対応し、異なるネットワークの間で共有、アクセスできます。

|**リソース**|**説明**|
|--|--|
|[イメージ](https://intl.cloud.tencent.com/document/product/213/4940)|イメージを使って、任意のネット環境においてCVMインスタンスを起動できます|
|[Elastic IP](https://intl.cloud.tencent.com/document/product/213/5733)|Elastic IPは、任意のネット環境におけるCVMインスタンスをバインドできます|
|インスタンス|基幹ネットワークのインスタンスとVPCのインスタンスは、 [パブリックIP](https://intl.cloud.tencent.com/document/product/213/5224) または 基幹ネットワークの相互接続 で相互通信できます|
|[SSHキー](https://intl.cloud.tencent.com/document/product/213/6092)|SSHキーは、任意のネット環境におけるCVMインスタンスにロードできます|
|[セキュリティグループ](https://intl.cloud.tencent.com/document/product/213/12452)|セキュリティグループは、任意のネット環境におけるCVMインスタンスにバインドできます|

> [Cloud Load Balancer](https://intl.cloud.tencent.com/document/product/214) は基幹ネットワークとVPCの間で共有できません。ネットワークの相互接続が構築されていても、Cloud Load BalancerをVPCのインスタンスと基幹ネットワークのインスタンスに同時にバインドすることはできません。

## 基幹ネットワークからVPCへのインスタンスのマイグレーション
 1. 基幹ネットワークのCVMインスタンスでは、[カスタムイメージを作成します](/doc/product/213/4942) 。
 2. （オプション）基幹ネットワークのCVMインスタンスのデータディスクで、[スナップショットを作成します](/doc/product/362/5755) 。
 3. [VPCとサブネットを作成します](/doc/product/215/4927#.E5.88.9B.E5.BB.BA.E7.A7.81.E6.9C.89.E7.BD.91.E7.BB.9C.E3.80.81.E5.88.9D.E5.A7.8B.E5.8C.96.E5.AD.90.E7.BD.91.E5.92.8C.E8.B7.AF.E7.94.B1.E8.A1.A8) 。
 4. VPC内で、[CVMインスタンスを購入して起動します](/doc/product/213/4855) 。


