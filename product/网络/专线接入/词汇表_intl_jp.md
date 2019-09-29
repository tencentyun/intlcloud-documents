### BGP ASN
BGPルーティング中の各自律システムには、一意の自律システム番号が割り当てられています。自律システム番号（ASN）は、インターネット割当番号公社（Internet Assigned Numbers Authority（略称はIANA）。この公社はインターネットIPアドレスの割り当ても担当します）により各地域インターネットレジストリ（RIR）に大口で割り当てられます。各地区のRIRは、さらにIANAが割り当てたASNのバッチ全体から1つのエンティティのために1つのASNを割り当てます。ASNが必要なエンティティはその所属地区センターが規定する手順に従って申請を行わなければならず、申請が承認されてからASNが割り当てられます。


### ピアツーピア接続
<a href="https://cloud.tencent.com/doc/product/215/5000" target="_blank">ピアツーピア接続</a>（peering connection）は異なるVPCにより構築された接続であり、アカウント間および地域間のVPCトラフィックの相互接続をサポートします。

### IPsec
IPsec（Internet Protocol Security）はインターネットセキュリティプロトコルとも呼ばれ、プロトコルパケットであり、IPプロトコルのパケットを暗号化および認証することによりIPプロトコルのネットワーク伝送プロトコルファミリー（相互に関連付けするプロトコルの集合）を保護します。
IPsecは、主に以下のプロトコルにより構成されます。
- **認証ヘッダー**：IPデータグラムに、コネクションレスデータ整合性、メッセージ認証および反射攻撃保護を提供します。
- **カプセル化セキュリティペイロードプロトコル**：機密性、データソース認証、コネクションレス整合性、反射攻撃保護および限られたトラフィックフロー機密性を提供します。
- **セキュリティ関連付け**：アルゴリズムとパケットを提供し、認証ヘッダー、カプセル化セキュリティペイロードプロトコルに必要なパラメータを提供します。


### ルーティングテーブル
<a href="https://cloud.tencent.com/doc/product/215/4954" target="_blank">ルーティングテーブル</a>（routing table）は一連のルーティングポリシーを含み、VPCにおける各サブネットのネットワークトラフィックの方向を定義するために使用されます。各サブネットには関連付けられたルーティングテーブルが1つだけあり、各ルーティングテーブルは1つのVPCにおける複数のサブネットと関連付けることができます。

### VPC
VPC（Virtual Private Cloud）はTencent Cloudで独立したネットワーク空間を構築し、ユーザーのデータセンターで実行される従来のネットワークと非常に似ていますが、Tencent CloudのVPC内でホスティングされるのはTencent Cloudにおけるサービスリソースであり、<a href="https://cloud.tencent.com/doc/product/213/495" target="_blank">CVM</a>、<a href="https://cloud.tencent.com/doc/product/214/524" target="_blank">CLB</a>、<a href="https://cloud.tencent.com/document/product/236" target="_blank">データベース</a>などのクラウドサービスリソースを含みます。ネットワークデバイスの購入や維持管理について全く気にする必要なく、ソフトウェアを介してIPアドレス範囲の区分、IPアドレス、ルーティングポリシーなどをカスタマイズします。<a href="https://cloud.tencent.com/doc/product/213/1941" target="_blank">EIP</a>、<a href="https://cloud.tencent.com/doc/product/215/4975" target="_blank">NATゲートウェイ</a>および<a href="https://cloud.tencent.com/doc/product/215/4972" target="_blank">パブリックネットワーク</a>などを介して柔軟にInternetにアクセスできるだけでなく、また<a href="https://cloud.tencent.com/doc/product/215/4956" target="_blank">VPN</a>/<a href="https://cloud.tencent.com/doc/product/215/4976" target="_blank">DC</a>を介してVPCをデータセンターと接続させることもできます。同時に、Tencent Cloud VPCの<a href="https://cloud.tencent.com/doc/product/215/5000" target="_blank">ピアツーピア接続</a>サービスにより、グローバルで同一のサーバーを利用し二地域三センターで災害復旧を手軽に実現することができます。また、Tencent CloudのVPCにおける<a href="https://cloud.tencent.com/doc/product/213/500" target="_blank">セキュリティグループ</a>と<a href="https://cloud.tencent.com/doc/product/215/5132" target="_blank">ネットワークACL</a>により、多次元、全方位にわたってユーザーのネットワークセキュリティニーズを満たすことができます。

### VLAN ID
VLAN（Virtual Local Area Network）は仮想LANとも呼ばれ、LANスイッチ技術に構築されたネットワーク管理技術です。スイッチは一般的に255個のVLANに区分されます。各VLANのIDは、1～4096の間の任意の数字にすることができます。IDの作用は異なるVLANを区分することであり、TAG UNTag member属性を設定して、このポートの下りリンクまたは上りリンクデータグラムにタグをつけることができます。


### 物理的専用回線
物理的専用回線はTencent Cloudとローカルデータセンターを接続する物理回線接続で、1つの物理的専用回線で複数の地域の専用回線ゲートウェイと専用回線チャネルを構築することができます。

### サブネット
<a href="https://cloud.tencent.com/doc/product/215/4927" target="_blank">サブネット</a>（Subnet）は、VPCのIPアドレス範囲に対する柔軟な区分で、様々なサブネット内でアプリケーションやサービスを配置し、Tencent CloudのVPCにおいて多層のWebアプリケーションを安全で柔軟にホスティングすることができます。

### DC
<a href="https://cloud.tencent.com/doc/product/215/4976" target="_blank">DC</a>（Direct Connect）はTencent Cloudとローカルデータセンターを高速接続する方法で、物理的専用回線を介して一度に複数の地域にあるTencent Cloudコンピューティングリソースに繋ぎ、柔軟で信頼性の高いハイブリッドクラウドの展開を実現することができます。DCは単一障害点のない2線式ホットバックアップ接続方式をサポートし、金融など高度なネットワーク相互接続要求を満たします。

### 専用チャネル
専用チャネルは物理的専用回線のネットワークリンク区分で、様々な専用回線ゲートウェイに接続される専用回線チャネルを作成し、ローカルデータセンターと複数のVPCの相互接続を実現することができます。

### 専用回線ゲートウェイ
専用回線ゲートウェイはVPCの専用回線トラフィックの入口で、複数の専用チャネルに接続して複数のローカルデータセンターと相互接続することができます。





