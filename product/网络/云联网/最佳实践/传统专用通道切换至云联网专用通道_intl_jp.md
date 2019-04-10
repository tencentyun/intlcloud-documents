## 一般的な事例
ユーザローカルIDCは物理的専用回線を介し従来の専用チャネルを使用してクラウドに接続し、トポグラフィは以下のとおりです。
![](https://main.qcloudimg.com/raw/e11798e61637bc0a8d73aa60464fe0b2.png)

### VPCルーティングテーブル構成の確認
1. [Tencent Cloudコンソール](https://console.cloud.tencent.com)にログインし、【クラウド製品】>【クラウドコンピューティングとネットワーク】>【VPC】を選択し、VPCコンソールに進みます。
2. 左側のディレクトリの【ルーティングテーブル】をクリックして、「VPCのある地域」を選択し、「VPC」を選択し、「ルーティングテーブルID」をクリックします。このドキュメントは「北京」、「Default-VPC（172.21.0.0/16）」、「rtb-2kanpxjb」を例とします。
![](https://main.qcloudimg.com/raw/289f0d1e4568da441ac506843e35df68.png)
3. 進むと、VPCルーティングテーブル構成の詳細が下図のとおり確認できます。
![](https://main.qcloudimg.com/raw/3fa9826a367155c001eff718440da810.png)

### 専用チャネル構成の確認
1. [Tencent Cloudコンソール](https://console.cloud.tencent.com)にログインし、[DCコンソール](https://console.cloud.tencent.com/dc/dcConn)に進みます。
2. 左側のディレクトリの【専用チャネル】をクリックし、「専用チャネルID」をクリックし、詳細ページに進みます。このドキュメントでは「dcx-4xls4yx2」を例とします。
![](https://main.qcloudimg.com/raw/4d924207e0dffa832ea6822e02a3a5e6.png)
4. 【高度な構成】をクリックすると、専用チャネルの高度な構成を確認できます。
![](https://main.qcloudimg.com/raw/d1c0b3a1a10fc28631e73eb41cb6d27b.png)

以上の情報をまとめると、VPCのターゲットIPアドレス範囲192.168.0.0/24へのトラフィックは、VPCルーティングテーブルポリシーに基づきDCゲートウェイdcg-019f9l0qのパス方向を選択して送信します。

## 切り替えステップ
1. CCN DCゲートウェイを作成します。
 1. [Tencent Cloudコンソール](https://console.cloud.tencent.com)にログインし、【クラウド製品】>【クラウドコンピューティングとネットワーク】>【VPC】を選択し、VPCコンソールに進みます。
 2. 左側のディレクトリの[DCゲートウェイ](https://console.cloud.tencent.com/vpc/dcGw?rid=8)をクリックし、【新規作成】をクリックし、DCゲートウェイの名称を入力し、ネットワークが「CCN」を選択して関連付けます。このドキュメントでは「dcg-dx8kvqto」を例とします。
![](https://main.qcloudimg.com/raw/3a5f479742998239283cf23fd64ee268.png)
 3. 【OK】ボタンをクリックします。

 >!CCN DCゲートウェイを作成する地域は、物理的専用回線のDCポイントと同じ地域でなければなりません。
2. CCN専用チャネルを作成します。
 1. [Tencent Cloudコンソール](https://console.cloud.tencent.com)にログインし、[DCコンソール](https://console.cloud.tencent.com/dc/dcConn/create)に進みます。
 2. 左側のディレクトリの【専用チャネル】をクリックし、【新規作成】をクリックします。
![](https://main.qcloudimg.com/raw/aece2f4003c62d5fb3fbde0548477b90.png)
 3. 専用チャネルの新規作成に進み、「基本構成」ページで名称を入力し、「専用回線のタイプ」、「物理的専用回線」、「ネットワークへの接続」、「DCゲートウェイ」のパラメータを選択します。このドキュメントでは「test」を例とします。
![](https://main.qcloudimg.com/raw/bd097cdd58f42eaa8d6daff2a9be84b3.png)
>?
>- 物理的専用回線は元のもの、すなわちIDがdc-dqggvxadの物理的専用回線を使用します。
>- アクセスネットワークはCCNを選択します。
>- DCゲートウェイはステップ1で作成したCCN DCゲートウェイ、すなわち名称がdcg-dx8kvqtoのCCN DCゲートウェイを選択します。
 4. 【次へ】をクリックし、高度な構成に進み、「VLAN ID」を入力します。このドキュメントでは「501」を例とします。
![](https://main.qcloudimg.com/raw/f6bb1944403b288fd48e67d924958e7c.png)
>!VLAN IDの名称は、新しいIDでなければなりません。
 5. 【次へ】をクリックし、IDCデバイスの構成に進み、【提出】をクリックします。
3. CCN DCゲートウェイにユーザのIDCのIPアドレス範囲を追加します。
 1. [DCゲートウェイコンソール](https://console.cloud.tencent.com/vpc/dcGw?rid=8)にログインし、ステップ1で作成したCCN DCゲートウェイID（名称は「テスト用DCゲートウェイ」）を選択し、「dcg-dx8kvqto」詳細ページに進み、【IDCのIPアドレス範囲】をクリックし、【追加】をクリックします。
![](https://main.qcloudimg.com/raw/fe57c56980c4a8775705a4bcbb76b80d.png)
 2. 追加ページに進み、IDCのIPアドレス範囲を入力し、【保存】をクリックします。このドキュメントでは「192.168.0.0/24」を例とします。
![](https://main.qcloudimg.com/raw/1e97fe05d1ea75fe965cb3be73a00f27.png)
 3. 保存が完了すると、追加されたIDCのIPアドレス範囲を見ることができます。
![](https://main.qcloudimg.com/raw/91ee51c43216435bb57aba406d37ef44.png)
>?
>- IDCのIPアドレス範囲の静的な追加を選択することも、IDCのIPアドレス範囲の自動学習を選択することもできます。
>- 現在、IDCのIPアドレス範囲を自動学習する時に1分間遅延されるため、ニーズを満たすことができない場合、まず静的方式を選択して追加してください。
4. CCNインスタンスを作成します。
 1. [CCNコンソール](https://console.cloud.tencent.com/vpc/ccn)にログインし、【新規作成】をクリックし、CCNインスタンス名を入力し、インスタンスのVPCを関連付け、【作成】をクリックします。このドキュメントでは「ccn-msg8kju5」、「vpc-gu64ju2u」を例とします。
![](https://main.qcloudimg.com/raw/08fd52950a6285af04fb4a585470e39a.png)
 2. CCNの作成が完了後、CCNリストページでインスタンスIDをクリックしてCCNインスタンス詳細に進みます。このドキュメントでは「ccn-msg8kju5」を例とします。
![](https://main.qcloudimg.com/raw/be26e13c848bab9c8b1333bd16df6276.png)
 3. 【ルーティングテーブル】をクリックします。
![](https://main.qcloudimg.com/raw/1408028fc2f22d61a5513bb94ee6a464.png)

 >?従来の専用チャネルVPCがIDCにリリースするのはCIDRの大規模なIPアドレス範囲であり、VPCがCCNにリリースするのはVPCのサブネットです。
5. IDCをVPCに向けたトラフィックパスに切り替えます。
 1. 「テスト用CCN（ccn-msg8kju5）」ページで【インスタンスの関連付け】をクリックし、【インスタンスの新規作成】をクリックします。このドキュメントでは、以下の図に示すとおり、「DCゲートウェイ」、「北京」、「dcg-dx8kvqto」を例とします。
![](https://main.qcloudimg.com/raw/c6db304e2186c2f18e7ea2c0e1454446.png)
 2. 【提出】をクリックすると、IDがdcg-dx8kvqtoのインスタンスのCCNへの関連付けが完了します。
![](https://main.qcloudimg.com/raw/90495973efd23bcf585869b1ab2a94b6.png)
 3. 【ルーティングテーブル】をクリックすると、CCNのルーティングテーブルが以下のとおりになります。
![](https://main.qcloudimg.com/raw/9a8f62a335c1463df026c7d0ddbdad3f.png)
>?
>- 専用チャネルは静的ルーティングであり、IDCのVPCへ向けたトラフィックをCCNチャネルパスに切り替えたい場合、ユーザのCPEルーティングを新しいサブAPIのCCNチャネルに方向づけるするだけでよいです。
>- 専用チャネルがいずれもBGPルーティングである場合、クラウドの接続デバイスの古いチャネルがIDCに送信するのはCIDR大規模なIPアドレス範囲であり、新しいCCNチャネルがIDCに送信するのはサブネット明細ルーティングです。**ルーティングマスクの最長一致原則に基づき、IDCのVPCに向けたトラフィックは自動的にCNN専用チャネルに切り替えられます。**
>- CCN中のVPCまたはDCゲートウェイルーティングを無効または有効にすることもでき、それによりIDCのVPCに向けたトラフィックパスを制御することができます。
6. VPCをIDCに向けたトラフィックパスに切り替えます。
 1. IDがrtb-2kanpxjbのルーティングテーブルをクリックして、[VPCルーティングテーブルポリシーの変化](https://console.cloud.tencent.com/vpc/route?rid=8)を確認します。VPCはCCNルーティングテーブルを自動学習する能力を有しており、後で加わった等価ルーティングはデフォルトで有効化されません。VPCのIDCに向けたトラフィックパスは依然として古い専用チャネルを選択します。
![](https://main.qcloudimg.com/raw/369984d65c6ddf72cc874ee29ec96ace.png)
 2. 古いDCゲートウェイのルーティングポリシーを無効にし、次のホップがCCNのルーティングポリシーを有効化する必要があります。
![](https://main.qcloudimg.com/raw/c26b3b21f26e35df00c7123ab6eafe64.png)
操作が完了後、VPCのIDCに向けたトラフィックパスは既にCCN専用チャネルに切り替えられています。

 >!無効化と再有効化の過程において、VPCのIDCに向けたトラフィックは中断されます。ビジネスのセキュリティのため、ビジネスを中断することができる時間帯を選択して操作する必要があります。

スムーズに切り替える必要がある場合、方法とステップは以下のとおりです。
 a. IDCルーティングは2つの明細ルーティングに分割され、192.168.0.0/24は192.168.0.0/25と192.168.0.128/25に分割されます。
 b. VPCルーティングテーブルは2つの明細ルーティングポリシーを追加します。
![](https://main.qcloudimg.com/raw/cd9b09904fd356d91d30d3aca7d1a28d.png)
 c. VPCのIDCに向けたトラフィックは、25ビットのマスクの詳細ルーティングポリシーを選択します。この時、ターゲットIPアドレス範囲192.168.0.0/24の次のホップがDCゲートウェイのルーティングポリシーは既に失効しており、このルーティングポリシーを無効にする、または削除することができます。
 d. VPCルーティングテーブルは次のホップがCCNターゲットIPアドレス範囲192.168.0.0/24のルーティングポリシーを有効化します。この時、VPCのIDCに向けたトラフィックパスは、引き続き古いDCゲートウェイの明細ルーティングポリシーを選択します。
![](https://main.qcloudimg.com/raw/8c72c7b05cd9829417038acfbc8ab980.png)
 e. VPCルーティングテーブルは明細ルーティングのルーティングポリシーを1つずつ無効にし、または削除し、VPCのIDCに向けたトラフィックも1つずつCCNチャネルに切り替えられます。
![](https://main.qcloudimg.com/raw/54b0dea5e4f29ae7acbc2918887ddc3c.png)

7. チャネルとDCゲートウェイを削除します。
以上のステップにより切り替えが完了しますが、まず一定の時間内に観察することをお勧めします。ネットワークが安定後、古いチャネルと古いDCゲートウェイを削除することができます。
