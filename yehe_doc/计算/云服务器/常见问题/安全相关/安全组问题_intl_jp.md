
### セキュリティグループにデフォルトで拒否ルールがあるのは、なぜですか？

セキュリティグループルールは上から下へと順番に有効になります。前に設定された許可ルールが有効になると、他のルールはデフォルトで拒否されます。すべてのポートをオープンにしている場合は、最後の拒否ルールは有効になりません。セキュリティ上の理由から、このデフォルト設定を提供しています。

### セキュリティグループの優先順位を調整するにはどうすればよいですか？

操作の詳細については、[セキュリティグループの優先順位の調整](https://intl.cloud.tencent.com/document/product/213/35375)をご参照ください。

### 誤ったセキュリティグループをインスタンスにバインドすると、インスタンスにどのような影響がありますか。この問題を解決するにはどうすればよいですか？

**潜在的リスク**

- SSH経由でLinuxインスタンスへのリモート接続、またはリモートデスクトップ経由でWindowsインスタンスへのリモート接続に失敗する場合があります。
- このセキュリティグループ内のCVMインスタンスのパブリックネットワークIPアドレスとプライベートネットワークIPアドレスへのリモートpingに失敗する場合があります。
- HTTP経由で当該セキュリティグループのインスタンスによって暴露されるWebサービスへのアクセスに失敗する場合があります。
- このセキュリティグループのインスタンスは、Internetサービスにアクセスできない場合があります。

**ソリューション**

- 前述のいずれかの状況が発生した場合、コンソールのセキュリティグループに移動して、セキュリティグループルールを変更できます。例えば、デフォルトのオールポートオーペンセキュリティグループのみをバインディングします。
- セキュリティグループルールの設定方法の詳細については、[セキュリティグループの概要](https://intl.cloud.tencent.com/document/product/213/12452)をご参照ください。

### セキュリティグループの方向およびポリシーとは何ですか？

セキュリティグループのポリシー方向はアウトバウンドとインバウンドに分けられています。アウトバウンド方向はCVMの送信トラフィックをフィルタリングし、インバウンド方向はCVMの受信トラフィックをフィルタリングします。
セキュリティグループポリシーは、トラフィックの**許可**と**拒否**に分けられています。

### セキュリティグループポリシーはどの順序で有効になりますか？

セキュリティグループポリシーは、トラフィックがセキュリティグループを通過するときに上から下へ順番に有効になります。トラフィックがポリシーに一致すると、ポリシーはすぐに有効になります。

### セキュリティグループによって拒否されたIPアドレスが引き続きCVMにアクセスできるのはなぜですか？

以下の原因が考えられます：
- CVMは複数のセキュリティグループにバインディングされており、特定のIPアドレスは別のセキュリティグループによって許可されています。
- 特定のIPアドレスは、審査済みのTencent Cloudパブリックサービスに属しています。

### セキュリティグループを使用する場合、iptablesは使えなくなりますか？

いいえ。セキュリティグループとiptablesは同時に使用できます。トラフィックは次の方向で2回フィルタリングされます。
- アウトバウンド方向：インスタンス内のプロセス > iptables > セキュリティグループ。
- インバウンド方向：セキュリティグループ > iptables > インスタンス内のプロセス。

### すべてのCVMが返されたにもかかわらず、セキュリティグループを削除できないのはなぜですか？

ごみ箱にまだCVMが存在するかどうかを確認します。セキュリティグループがごみ箱のCVMにバインディングされている場合、セキュリティグループを削除することはできません。

### セキュリティグループをクローンするときに、名前はターゲットリージョンのセキュリティグループの名前と同じでもいいですか？

いいえ。名前は、ターゲットリージョンの既存のセキュリティグループの名前とは異なる必要があります。

### セキュリティグループを異なるユーザー間でクローンできますか？

この機能は現在サポートされていません。

### クロスプロジェクトやクロスリージョンでのセキュリティグループのクローンをサポートするTencent Cloud APIはありますか？

現時点では、コンソールを利用するユーザーのために、MCサポートを提供していますが、直接のTencent Cloud APIのサポートはありません。Tencent Cloud APIを使用して、セキュリティグループルールのバッチインポートとエクスポートを行うことで、間接的にクロスプロジェクトやクロスリージョンでのセキュリティグループのクローンを実現できます。

### クロスプロジェクトやクロスリージョンでのセキュリティグループのクローンを作成すると、セキュリティグループによって管理されるCVMが一緒にコピーされますか？

いいえ。クロスリージョンでのセキュリティグループのクローンは、元のセキュリティグループのアウトバウンド・インバウンドルールのみがクローンされます。したがって、CVMをセキュリティグループに個別にバインドする必要があります。

### セキュリティグループとは何ですか？
セキュリティグループは、ステートフルパケットをフィルタリングする機能を備えた仮想ファイアウォールです。CVM、Cloud Load Balancer(CLB)、MySQLなどのインスタンスを設定するネットワークアクセス制御、インスタンスレベルのインバウンド・アウトバウンドトラフィック制御のために使用されます。ネットワークセキュリティに対する重要な隔離手段です。

各CVMインスタンスは、少なくとも1つのセキュリティグループにバインドされています。インスタンスを作成するときはセキュリティグループを指定する必要があります。同じセキュリティグループ内のCVMインスタンスは、ネットワーク上で相互接続できます。デフォルトでは、異なるセキュリティグループ内のCVMインスタンスは、プライベートネットワークで接続できません。詳細については、[セキュリティグループの概要](https://intl.cloud.tencent.com/document/product/213/12452)をご参照ください。

### CVMインスタンス作成時にセキュリティグループを選択する理由は何ですか？
CVMインスタンスを作成する前に、セキュリティグループを選択してアプリケーション環境のセキュリティドメインを分割してください。セキュリティグループルールに権限を付与し、合理的なネットワークセキュリティの分離が行われています。

### CVMインスタンスの作成前にセキュリティグループを作成していないとどうなりますか？
CVMインスタンスを作成前にセキュリティグループを作成していない場合は、セキュリティグループの新規作成を選択できます。
セキュリティグループの新規作成は、次のルールを提供します。実際のニーズに応じてIP/ポートをオープンしてください。
- ICMP：ICMPプロトコルをオープンし、パブリックネットワーク経由でサーバーへのpingを許可します。
- TCP：80：ポート80をオープンし、HTTP経由でWebサービスへのアクセスを許可します。
- TCP22：ポート22をオープンし、SSH経由でLinux CVMへのリモート接続を許可します。
- TCP：443：ポート443をオープンし、HTTPS経由でWebサービスへのアクセスを許可します。
- TCP：3389：ポート3389をオープンし、RDP経由でWindows CVMへのリモート接続を許可します。
- プライベートネットワークをオープンする：プライベートネットワークをオーポンし、さまざまなクラウドリソース（IPv4）間のプライベートネットワークアクセスを許可します。


### セキュリティグループはどのような状況でデフォルトのセキュリティグループルールを使用しますか。
デフォルトのセキュリティグループルールは、次の状況で使用されます。
- CVMインスタンスを作成するときに、**クイック構成**を選択してCVMを購入する場合、システムによってデフォルトのセキュリティグループが自動的に作成されます。セキュリティグループは、デフォルトのセキュリティルールを使用します（つまり、すべてのIPv4ルールのオープンが許可されます）。
セキュリティ上の理由から、Tencent Cloudは新しいセキュリティグループにCVMを関連付けることをお勧めします。その新しく関連付けられたセキュリティグループはサービスに必要なポートのみをオープンし、不必要なセキュリティリスクを極力回避します。
- CVMコンソールでセキュリティグループを作成するときは、セキュリティグループテンプレートを選択できます。現在「Windowsログイン」テンプレート、「Linuxログイン」テンプレート、「Ping」テンプレート、「HTTP(80)」テンプレート、「HTTPS(443)」テンプレートを提供しています。
