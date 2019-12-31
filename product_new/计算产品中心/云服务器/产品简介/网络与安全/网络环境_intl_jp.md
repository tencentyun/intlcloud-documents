Tencent Cloudのネット環境は、[Virtual Private Cloud](https://cloud.tencent.com/product/vpc?idx=2)（VPC）と基幹ネットワークの二種類に分けられます。
2017年6月13日以降は、登録の新規アカウントは基幹ネットワークに対応していないため、次の原因をもって、VPCを使用することをおすすめします。

- 完備な機能：VPCは基幹ネットワークのすべての機能を揃えているほか、IPレンジのカスタマイズ、ルーティング、Direct Connect対応、VPN、NATなどの多様なネットワークサービスを提供します。
- マイグレーションのスムーズ性：業界においては、まだ徹底なスムーズなマイグレーションがありません（シャットダウンやプライベートIP変更などの操作が必要です）。業務のためにVPCを使用する必要がある場合、マイグレーションプロセスは業務に影響を与える可能性があります。

## VPCと基幹ネットワーク

### VPC

Tencent Cloud[VPC](https://cloud.tencent.com/document/product/215) は、ユーザーがTencent Cloudにおいてカスタマイズしたロジック的に隔離されているネットワークスペースです。同じ地域にあっても、異なるVPCの間はデフォルトで相互通信できません。ユーザーがデータセンターにおいて使用している従来のネットワークに類似し、Tencent Cloud VPCにホスティングされるのは、 [Cloud Virtual Machine](https://intl.cloud.tencent.com/document/product/213/495)、[Cloud Load Balancer](https://intl.cloud.tencent.com/document/product/214/524)、[クラウドデータベース](https://cloud.tencent.com/document/product/236) などのクラウドサービスを含む、ユーザーが保有しているTencent Cloudのサービスリソースです。ユーザーは、VPCの環境を完全に把握できます、構成とユースケースの詳細については、[VPC製品の概要](https://intl.cloud.tencent.com/document/product/215/535)をご参照ください。VPCは複雑なネットワークアーキテクチャを構築できるため、ネットワーク管理に慣れているユーザーに適しています。
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
| セキュリティ制御　| [セキュリティグループ](https://intl.intl.intl.cloud.tencent.com/document/product/213/12452)| [セキュリティグループ](https://intl.intl.intl.cloud.tencent.com/document/product/213/12452) と [ネットワークACL](https://intl.cloud.tencent.com/document/product/215/5132) |

## VPCと基幹ネットワーク間のリソース共有及びアクセス

Tencent Cloudにおける一部のクラウドソースと機能は両方のネット環境に対応し、異なるネットワークの間で共有、アクセスできます。

|**リソース**|**説明**|
|--|--|
|[イメージ](https://intl.cloud.tencent.com/document/product/213/4940)|イメージを使って、任意のネット環境においてCVMインスタンスを起動できます|
|[Elastic IP](https://intl.cloud.tencent.com/document/product/213/5733)|Elastic IPは、任意のネット環境におけるCVMインスタンスをバインドできます|
|インスタンス|基幹ネットワークのインスタンスとVPCのインスタンスは、 [パブリックIP](https://intl.cloud.tencent.com/document/product/213/5224) または [基幹ネットワークの相互接続](https://cloud.tencent.com/document/product/215/20083) で相互通信できます|
|[SSHキー](https://intl.cloud.tencent.com/document/product/213/6092)|SSHキーは、任意のネット環境におけるCVMインスタンスにロードできます|
|[セキュリティグループ](https://intl.intl.intl.cloud.tencent.com/document/product/213/12452)|セキュリティグループは、任意のネット環境におけるCVMインスタンスにバインドできます|

> [Cloud Load Balancer](https://cloud.tencent.com/document/product/214) は基幹ネットワークとVPCの間で共有できません。ネットワークの相互接続が構築されていても、Cloud Load BalancerをVPCのインスタンスと基幹ネットワークのインスタンスに同時にバインドすることはできません。

## 基幹ネットワークからVPCへのインスタンスのマイグレーション

基幹ネットワークのインスタンスをVirtual Private Cloudにマイグレーションするには、[VPCサービスの切り替え](https://cloud.tencent.com/document/product/213/20278)をご参照ください。
