## A

### セキュリティグループ

セキュリティグループ（Security Group）とは、フィルタリング機能を備えたステートフルな仮想ファイアウォールであり、単一または複数のCVMのネットワークアクセス制御を設定するために使用されます。同一リージョン内にある、同一のネットワークセキュリティ隔離手段を必要とするCVMインスタンスを同一のセキュリティグループに追加し、セキュリティグループのネットワークポリシーによってCVMのアウトバウンドおよびインバウンドトラフィックのセキュリティフィルタリングを行うことができます。

## C

### CLB

[CLB](#clb)をご参照ください

## D

### リージョン

リージョン（Region）とは、Tencent Cloudのホスティングデータセンターが分布する地域のことです。リージョンの下にはさまざまなアベイラビリティーゾーンがあります。
例えば、あるホスティングデータセンターのリージョンは北京、アベイラビリティーゾーンは北京1区のようになります。同一のリージョンにあるクラウドサービス製品はプライベートネットワークによって相互接続しています。異なるリージョンのクラウド製品間では、プライベートネットワークは接続されません。お客様の最寄りのリージョンを選択すると、アクセス遅延を低下させ、ダウンロード速度を向上させることができます。

## F
<span id="clb"></span>
### CLB

Cloud Load Balancer（CLB）はTencent Cloudがご提供する、安全で安定した、フレキシブルな拡張が可能なトラフィック分配サービスです。単一点障害の解消によってシステムの可用性を高めます。

### CLBリスナー

CLBリスナー（Load Balance Listener）は、リスニングポート、ロードバランシングポリシー、ヘルスチェック設定などの、リクエスト分配のルールを提供します。リクエストはCLBリスナーの設定に従ってバックエンドサーバー上に転送されます。1つのCLBインスタンスには1つ以上のリスナーを追加してください。

### CLBインスタンス

CLBインスタンス（Cloud Load Balancer Instance）とは実行されるCLBサービスのことです。CLBを使用するには、先にCLBインスタンスを作成する必要があります。

## H
<span id="RS"></span>
### バックエンドサーバー

バックエンドサーバー（Real Server，RS）は1組のCloud Virtual Machine（CVM）インスタンスであり、CLBが分配したリクエストを処理するために用いられます。

## R

### RS

[バックエンドサーバー](#RS)をご参照ください

## S
<span id="vpc"></span>
### VPC

Virtual Private Cloud（VPC）はTencent Cloudが構築する独立したネットワークスペースであり、データセンターで運用される従来型のネットワークと極めてよく似ていますが、Tencent Cloud VPCではお客様のTencent Cloud上でのサービスリソースをホスティングします。これには[CVM](https://intl.cloud.tencent.com/document/product/213)、[CLB](https://intl.cloud.tencent.com/document/product/214)、[CDB](https://intl.cloud.tencent.com/document/product/236)などのクラウドサービスリソースが含まれます。お客様はネットワークデバイスの購入や運用保守に煩わされることなく、ソフトウェアによってネットワークセグメントの区分、IPアドレス、ルーティングポリシーなどをカスタマイズできます。[Elastic IP](https://intl.cloud.tencent.com/document/product/213/16586) 、[NAT Gateway](https://intl.cloud.tencent.com/document/product/1015)、[パブリックゲートウェイ](https://intl.cloud.tencent.com/document/product/213/34835)などによってフレキシブルにInternetにアクセスできるだけでなく、[VPN](https://intl.cloud.tencent.com/document/product/215) / [ダイレクト接続](https://intl.cloud.tencent.com/document/product/216)によってVPCとお客様のデータセンターを接続することもできます。また、Tencent Cloud VPCの[Peering Connection](https://intl.cloud.tencent.com/document/product/553)サービスによって、均質なグローバルサービスおよび2リージョン3センターの障害復旧を手軽に実現できます。さらに、Tencent Cloud VPCのセキュリティグループと[ネットワークACL](https://intl.cloud.tencent.com/document/product/215/31850)が、お客様のネットワークセキュリティのニーズを、多元的かつ全方位的に満たします。

## V

### VIP

[仮想サービスアドレス](#vip)をご参照ください

### VPC

[VPC](#vpc)をご参照ください

## X
<span id="vip"></span>
### virtual IP

virtual IP（VIP）はシステムがCLBインスタンスに割り当てるサービスIPアドレスです。ユーザーはこのサービスアドレスを外部に公開するかどうかを選択でき、パブリックネットワークタイプとプライベートネットワークタイプのCLBインスタンスをそれぞれ作成できます。ドメイン名をパブリックVIPに解決することで、外部へのサービス提供を行うことができます。