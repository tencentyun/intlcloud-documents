### TencentDB for MySQLインスタンスにはどうやって接続しますか。
MySQLインスタンスの接続方法は次のとおりです。
- **プライベートネットワーク接続**：CVMを使用してクラウドデータベースのプライベートネットワークアドレスに直接接続します。この接続方法はプライベートネットワークの高速ネットワークを使用しますので、低レイテンシーです。
CVMとデータベースが同一アカウントであり、かつ同一の[VPC](https://intl.cloud.tencent.com/document/product/215/535)内（同一リージョンであることを保障するため）、または同一の基本ネットワーク内にある必要があります。 
- **パブリックネットワーク接続**：プライベートネットワークを介して接続できない時は、パブリックネットワークアドレス経由でTencentDB for MySQLに接続することができます。パブリックネットワークアドレスは手動で有効にする必要があります。[MySQLコンソール](https://console.cloud.tencent.com/cdb)のインスタンス詳細ページで確認でき、不要な場合は無効にすることもできます。

詳細については、[MySQLインスタンスの接続](https://intl.cloud.tencent.com/document/product/236/37788)をご参照ください。

### TencentDB for MySQLの接続に失敗しました。どのように処理すればいいですか。
#### CVM、ローカルコンピュータからのMySQLの接続に失敗
1. チェックツールによる原因診断
TencentDB for MySQLコンソールでは[クイック接続チェックツール](https://intl.cloud.tencent.com/document/product/236/40333)を提供し、接続不能の原因を判断できるようにしています。プロンプトにしたがって修正した後、インスタンスに再接続します。
2. 原因のセルフ診断
クイック接続チェックツールでトラブルの原因を特定できない場合は、[本ドキュメントで紹介する失敗の原因によって、失敗の原因を自主的に識別・特定する](https://intl.cloud.tencent.com/document/product/236/40333)ことも可能です。

#### データベース管理（DMC）プラットフォームからのMySQLの接続に失敗
1. ログインアカウントのホストの制限の中で、当該リージョンのDMCサーバーのすべてのIPに権限がすでに付与されていることを確認します。権限付与については、[アクセス権限を付与するホストアドレスの修正](https://intl.cloud.tencent.com/document/product/236/31903)をご参照ください。また直接%を使用し、すべてのIPを通過させ、セキュリティグループによってのみデータベースのアクセス元を制限することもできます。
2. IPへの権限付与が確認された場合、アカウントのパスワードエラーの可能性がありますので、正しいパスワードを再度入力してください。[パスワードの再設定](https://intl.cloud.tencent.com/document/product/236/31901)または[権限がニーズを満たす臨時アカウントの作成](https://intl.cloud.tencent.com/document/product/236/31900)を行うこともできます。

より詳しい紹介については、[インスタンスに接続できない場合](https://intl.cloud.tencent.com/document/product/236/40333)をご参照ください。

### プライベート/パブリックネットワークアドレスをどうやって確認しますか。
[MySQLコンソール](https://console.cloud.tencent.com/cdb)にログインし、インスタンスリストでインスタンスIDをクリックして、インスタンス詳細ページに入り、確認します。

### パブリックネットワークアドレスをどうやって有効化しますか。
[MySQLコンソール](https://console.cloud.tencent.com/cdb)にログインし、インスタンスリストの中のインスタンスIDをクリックして、インスタンス詳細ページに入り、「パブリックネットワークアドレス」のところを開きます。

### パブリックネットワーク接続が遅い場合は、どうすればいいですか。
プライベートネットワークを使用して接続することをお勧めします。この接続方法ならばプライベートネットワークの高速ネットワークを使用しますので、低レイテンシーです。プライベートネットワークの接続については、[MySQLインスタンスの接続](https://intl.cloud.tencent.com/document/product/236/37788)をご参照ください。

### プライベートネットワークを使用して、自分のCVMとTencentDB for MySQLを直接接続することは可能ですか。
1. プライベートネットワークを使用して接続するには、次の条件を満たす必要があります。
CVMとデータベースが同一[VPC](https://intl.cloud.tencent.com/document/product/215/535) 内（同一リージョンを保障）、または同一基本ネットワーク内にある必要があります。 
2. 同一VPCまたは同一基本ネットワーク内という条件を満たしているかの判断方法は次となります。
 - CVMのネットワークから、[コンソール](https://console.cloud.tencent.com/cvm/instance)のインスタンスリストまたは詳細ページが確認できること。
 - TencentDB for MySQLのネットワークから、[コンソール](https://console.cloud.tencent.com/cdb)のインスタンスリストまたは詳細ページが確認できること。
詳細については、[ネットワークタイプ/VPCの判断方法](https://intl.cloud.tencent.com/document/product/236/40333#wllxvpdff)をご参照ください。


### 自分のCVMとTencentDB for MySQLを、プライベートネットワーク経由で接続できません。どうすればいいですか。
まず[クイック接続チェックツール](https://intl.cloud.tencent.com/document/product/236/31927)を使って原因調査を行い、チェックレポートの表示に従い、[接続できない場合によくあるケース](https://intl.cloud.tencent.com/document/product/236/40333#wfljcjwt)で対応するソリューションを検索してください。

### 自分のCVMとTencentDB for MySQLのリージョンが同じでない場合（例：CVMが広州、MySQLが上海）、プライベートネットワーク経由で直接アクセスできますか。
プライベートネットワーク経由で直接アクセスすることはできません。対処方法については、[リージョンが異なる場合](https://intl.cloud.tencent.com/document/product/236/40333#dywt)をご参照ください。

### 自分のCVMとTencentDB for MySQLが同一リージョンの異なるアベイラビリティーゾーンにある場合（例：CVMが上海2区、MySQLが上海1区）、プライベートネットワークを使用して接続できますか。
CVMとTencentDB for MySQLが同一リージョンでも、必ずしも同一VPCとはなりません。VPCが異なる可能性があります。
- VPCが同じでアベイラビリティーゾーンが異なる場合は、プライベートネットワークを使用して相互接続することができます。
- 同一VPCではない場合（例：クラウドデータベースがVPC1とVPC2である場合）は、プライベートネットワーク経由で相互接続することはできません。対処方法については、[VPCが異なる場合](https://intl.cloud.tencent.com/document/product/236/40333#cmvbt)をご参照ください。

### アカウントが異なるCVMとTencentDB for MySQLとは、プライベートネットワーク経由で直接接続できますか。
プライベートネットワーク経由で直接接続することはできませんが、[CCN](https://intl.cloud.tencent.com/document/product/1003)を使用してクロスアカウントのプライベートネットワーク接続を実現することができます。

### [telnetを使用してクラウドデータベースのネットワークポート接続が正常であることを検証した後、CVM上でコマンドラインを使ってクラウドデータベースにログインしたときに、関連するエラーが出ました。どのように対処すればいいですか。](id:sytyzysjk)
- 「ERROR 1045(28000):Access denied for user...」 のプロンプトが出現した時は、入力したクラウドデータベースアカウント、パスワードが正しいかどうかを確認してください。パスワードを忘れた場合は、[パスワードの再設定](https://intl.cloud.tencent.com/document/product/236/31901)をご参照ください。正しい情報を再度入力した後もこのエラーが発生する場合は、ご自身のインスタンスが接続IPを制限していないかを、[MySQLコンソール](https://console.cloud.tencent.com/cdb)のインスタンス管理ページの【データベース管理】>【アカウント管理】で確認してください。

- 「ERROR 1040(00000):Too many connections」のプロンプトが出現した時は、クラウドデータベースインスタンスの現在の最大接続数が制限を超えていることを意味します。一般的な原因と対処方法は次のとおりです。
i. sleepスレッド数が非常に多い場合は、コンソールでwait_timeoutおよびinteractive_timeoutのパラメータ値を下げることをお勧めします。
ii. スロークエリーの堆積。long_query_timeのパラメータ値はデフォルトで10sです。1s - 2sに変更し、スロークエリーのログを観察することをお勧めします。
iii. sleepスレッド数が非常に少なく、スロークエリーの堆積もない場合は、コンソールで、max_connectionsのパラメータ値を大きくすることをお勧めします。
- 「ERROR 2003 (HY000): Can't connect to MySQL server...」のプロンプトが出現した時は、入力したクラウドデータベースのIP、ポート情報が正しいかどうか確認してください。正しい情報を再度入力してもこのエラーが発生する場合は、このインスタンスのコンソールのセキュリティグループポリシーを確認し、そのCVMにこのデータベースに接続する権限があるかどうかを確認します。[クラウドデータベースセキュリティグループ](https://intl.cloud.tencent.com/document/product/236/14470)をご参照ください。
- データ移行時に接続性テストに合格しない場合は、表示されたマイグレーションプロキシIPについて、セキュリティポリシーを通過させているかを確認してください。
- ユーザーがinit_connectパラメータを設定している場合。例：mysql>set global init_connect='insert into db_monitor.accesslog(thread_id,log_time,localname,matchname) values(connection_id(),now(),user(),current_user())';
これによって、super権限以外の各ユーザーの接続がトリガーされ、データベースに接続するたびにdb_monitor.accesslogテーブルに1件のレコードが挿入されます。一度db_monitor.accesslogテーブルにトランザクションを実行していないイベントや関連するロック待ちがあると、insert into db_monitor.accesslogテーブルの操作がいずれも引っかかって止まり、さらにsuper権限以外のユーザーのすべての接続も滞留して、クラウドデータベースの正常な使用に影響を及ぼします。init_connectパラメータは、慎重に設定するようにしてください。

