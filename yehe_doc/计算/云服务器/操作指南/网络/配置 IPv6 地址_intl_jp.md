## 概要
このドキュメントでは、IPv6 CIDRを持つCloud Virtual Machine（CVM）を構築し、Elastic Network Interface（ENI）でIPv6を有効にして、IPv6のプライベートネットワークとパブリックネットワークの通信を実装する方法について説明します。


<dx-alert infotype="explain" title="">
現在、ElasticパブリックネットワークIPv6、IPv6 Cloud Load Balancer（CLB）、およびIPv6プライベートネットワークの有効化をサポートしているのは、広州、深センファイナンス、上海、上海ファイナンス、南京、北京、成都、香港、シンガポール、バージニアの各地域のみです。ご利用の際は、[チケットの提出](https://console.intl.cloud.tencent.com/workorder/category)に申し込んでください。
</dx-alert>




## 操作についての注意事項

1. Tencent Cloud製品を使用する前、[TencentCloudアカウントを登録する](https://intl.cloud.tencent.com/register?&s_url=https%3A%2F%2Fconsole.intl.cloud.tencent.com%2Fworkorder%2Fcategory)必要があります。
2. 現在、ElasticパブリックネットワークIPv6、IPv6 CLB、およびIPv6プライベートネットワークの有効化をサポートしている地域：
広州、深センファイナンス、上海、上海ファイナンス、南京、北京、成都、香港、シンガポール、バージニア。ご利用の際は、[チケットの提出](https://console.intl.cloud.tencent.com/workorder/category)に申し込んでください。
3. IPv6アドレスはGUAアドレスです。各VPCには1つの`/56`のIPv6 CIDRが割り当てられ、各サブネットには1つの`/64`のIPv6 CIDRが割り当てられ、各ENIには1つのIPv6アドレスが割り当てられます。
4. プライマリENIとセカンダリENIの両方が、IPv6アドレスの適用をサポートしています。CVMとENIとの関係の詳細については、[Elastic Network Interface](https://intl.cloud.tencent.com/zh/document/product/576)製品のドキュメントをご参照ください。
5. Cloud Physical Machine（CPM）2.0は、インスタンスの作成時にIPv6アドレスを設定することをサポートしていません。CPM2.0でこの機能を構成するには、CPM2.0インスタンスを作成した後、ENI IPv6コンソールに進んで有効にしてください。
## 操作手順


<dx-alert infotype="explain" title="">
IPv6はベータテスト中であるため、デフォルトでCVMインスタンスはIPv6アドレスを設定しません。CVMでIPv6機能を有効にするには、まず、手動で構成してください。
</dx-alert>



### 手順1：CVMの購入（オプション）



<dx-alert infotype="explain" title="">
すでにCVMを購入している場合は、この手順をスキップできます。
</dx-alert>


1. [Tencent Cloud 購入ページ](http://manage.qcloud.com/shoppingcart/shop.php?tab=cvm&_ga=1.87370846.770173325.1571651505)にログインします。
2. モデルを選択するときは、IPv6をサポートする地域とネットワークを選択してください。
3. ホストを設定するときは、IPv6をサポートするセキュリティグループを選択し、**無料のIPv6アドレス割り当て**にチェックを入れてください。
<dx-alert infotype="notice" title="">
選択したネットワークまたはセキュリティグループがIPv6をサポートしていない場合は、「IPv6プライベートネットワークの迅速な構築」を参照して、ニーズを満たすプライベートネットワークとセキュリティグループを作成してください。
</dx-alert>
4. 購入したCVM情報を確認し、支払いを完了させます。

