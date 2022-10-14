Tencent Cloudでは、「[Virtual Private Cloud](https://intl.cloud.tencent.com/product/vpc?idx=2)（VPC）」と「Classic Network」の2つのネットワーク環境をご提供します。



## Virtual Private CloudとClassic Network

### VPC

Tencent Cloud[VPC](https://intl.cloud.tencent.com/document/product/215) は、Tencent Cloud上に定義した論理的に分離されたプライベート仮想ネットワーク空間です。同じリージョン内であっても異なるVPCはデフォルトでは相互に通信できません。データセンターで実行するレガシーネットワークと同様に、 [Cloud Virtual Machine](https://intl.cloud.tencent.com/document/product/213/495)、[Cloud Load Balancer](https://intl.cloud.tencent.com/document/product/214/524)、[TencentDB for MySQL](https://intl.cloud.tencent.com/document/product/236)  などのTencent Cloudリソースは、Tencent Cloud の VPC でホストされ、仮想ネットワーキング環境を完全に制御できます。構成とユースケースの詳細については、[VPC製品の概要](https://intl.cloud.tencent.com/document/product/215/535)をご参照ください。VPC は、より複雑なネットワーク アーキテクチャを構築するのに役立ち、ネットワーク管理に精通しているユーザーに適しています。
![](https://mc.qcloudimg.com/static/img/33f800da64d2b7c0e6c2f23f102e059a/image.png)

### Classic Network

Classic Networkは、すべてのTencent Cloudユーザー向けのパブリックネットワークリソースプールです。すべての Tencent Cloud リソースは、Tencent Cloud によって集中管理されます。

### Virtual Private CloudとClassic Networkの機能比較

| **機能**| **Classic Network**| **VPC** |
|---------|---------|---------|
| テナントに関連付ける | テナントに関連付ける| GRE カプセル化に基づく論理的に分離されたネットワーク |
| ネットワークのカスタマイズ | 未対応| 対応|
| ルーティングのカスタマイズ | 未対応| 対応|
| カスタム IP | 未対応| 対応|
| 相互接続ルール |同じリージョン内の同じテナントは、相互接続されています| クロスリージョン、クロスアカウントでの相互接続がサポートされています|
| セキュリティ制御　| [セキュリティグループ](https://intl.cloud.tencent.com/document/product/213/12452)| [セキュリティグループ](https://intl.cloud.tencent.com/document/product/213/12452) と [ネットワークACL](https://intl.cloud.tencent.com/document/product/215/5132) |

## Virtual Private CloudとClassic Network間のリソースの共有とアクセス

一部のTencent Cloud リソースと機能は、Virtual Private CloudとClassic Networkの両方をサポートし、2 つの異なるネットワーク経由で共有またはアクセスできます。

|**リソース**|**説明**|
|--|--|
|[イメージ](https://intl.cloud.tencent.com/document/product/213/4940)|イメージを使用してあらゆるネットワーク環境で CVM インスタンスを起動できます|
|[Elastic IP](https://intl.cloud.tencent.com/document/product/213/5733)|EIPは、あらゆるネットワーク環境でCVMインスタンスに関連付けることができます|
|インスタンス|Virtual Private CloudとClassic Network内のインスタンスは、 [パブリックIP](https://intl.cloud.tencent.com/document/product/213/5224) または[ClassicLink](https://intl.cloud.tencent.com/document/product/215/31807) を介して相互に通信できます|
|[SSHキー](https://intl.cloud.tencent.com/document/product/213/6092)|SSH キーは、あらゆるネットワーク環境での CVM インスタンスの読み込みをサポートします|
|[セキュリティグループ](https://intl.cloud.tencent.com/document/product/213/12452)|セキュリティ グループは、あらゆるネットワーク環境下でCVMインスタンスに関連付けることができます|

> [Cloud Load Balancer](https://intl.cloud.tencent.com/document/product/214) はClassic NetworkとVPCの間で共有できません。
ネットワーク間の相互接続が構築されていても、Cloud Load BalancerをVirtual Private CloudとClassic Network内のインスタンスに同時に関連付けることはできません。

## Classic Network内のインスタンスを VPCに移行する
 [VPC への切り替え](https://intl.cloud.tencent.com/document/product/213/20278)を参照して、Classic Network内のインスタンスを VPC に移行してください。

