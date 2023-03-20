ここでは主に、スタンドアローン、クラスターおよびTencent Cloud EMRクラスター（現時点ではGooseFSをサポートするバージョンは統合していません）におけるGooseFSのデプロイ、設定および実行を標準化する方法についてご説明します。

## デプロイ環境要件

### ハードウェア環境

現在GooseFSは主流のx86/x64アーキテクチャのLinux/MacOS実行環境をサポートしています（**注意：MacOS M1プロセッサのサポートは未検証です**）。詳細な実行ノード構成は次のとおりです。

#### Masterノード

- **CPU**：動作クロック周波数1GHz以上とします。Masterが大量の処理を必要とすることを考慮し、本番環境ではマルチコアアーキテクチャプロセッサを使用することをお勧めします。
- **物理メモリ**：1GB以上とします。本番環境では8GB以上の物理メモリ構成を使用することをお勧めします。
- **ディスク**：20GB以上とします。本番環境ではハイパフォーマンスなNVME SSDディスクをメタデータキャッシュディスクとすることをお勧めします（RocksDBモード）。

#### Workerノード

- **CPU**：動作クロック周波数1GHz以上とします。Workerノードでも大量の同時実行リクエストを処理する必要があることを考慮し、同様に本番環境ではマルチコアアーキテクチャプロセッサを使用することをお勧めします。
- **物理メモリ**：2GB以上とします。本番環境ではパフォーマンス要件に応じて適切な物理メモリ構成を選択することをお勧めします。例えば、本番環境で大量のデータブロックをWorkerノードのメモリ内にキャッシュする必要がある場合、またはMEM + SSD/HDDの混合ストレージを使用している場合は、実際にメモリにキャッシュする可能性のあるデータ量に応じて物理メモリを配備する必要があります。どのキャッシュモードを使用する場合でも、本番環境ではWorkerノードに16GB以上の物理メモリを配備することをお勧めします。
- **ディスク**：20GB以上のSSD/HDDディスクとします。実際の本番環境でプリフェッチキャッシュを行う必要があるデータ量のサイズに基づいて、各Workerノードに設定する必要があるディスク容量を推計することをお勧めします。また、より良いパフォーマンスを体験するためには、NVMEインターフェースを備えたSSDディスクをWorkerノードのデータディスクとすることをお勧めします。

### ソフトウェア環境

- Red Hat Enterprise Linux 5.5+、Ubuntu Linux 12.04 LTS+（バッチデプロイを使用しない場合はサポート可）、CentOS 7.4+およびTLinux 2.x（Tencent Linux 2.x）、IntelベースのアーキテクチャのMacOS 10.8.3以上のバージョン。Tencent Cloud CVMのユーザーにはCentOS 7.4、Tencent（TLinux 2.x）またはTencentOS Server 2.4バージョンのOSの使用を推奨します。
- OpenJDK 1.8/Oracle JDK 1.8。JDK 1.9以上のバージョンのサポートは未検証ですのでご注意ください。
- SSHツールセット（SSHおよびSCPツールを含む）、Expect Shellツール（バッチデプロイを使用する場合に必要）およびYumパッケージ管理ツールをサポートしています。

### クラスターネットワーク環境

- Master/Workerノード間はパブリックネットワークまたはプライベートネットワークで相互接続します。バッチデプロイを使用する場合は、Masterがパブリックネットワークのソフトウェアソースに正常にアクセスできるようにするか、またはパッケージ管理システムのプライベートネットワークソフトウェアソースを正確に設定する必要があります。
- クラスターはパブリックネットワークまたはプライベートネットワーク経由でCOSバケットまたはCHDFSファイルシステムにアクセスできるようにします。

### セキュリティグループとユーザー権限の要件

通常、GooseFSではユーザーが専用のLinuxアカウントを使用してGooseFSのデプロイと実行を行うことを推奨しています。例えば、自作のクラスターおよびEMR環境では統一してhadoopユーザーを使用し、GooseFSのデプロイと実行を行うことなどが可能です。バッチデプロイでは、以下のユーザー機能および権限を補足する必要があります。

- rootに切り替える、またはsudo権限を使用する機能を備えること
- アカウントにディレクトリの読み取り、書き込み、インストールの権限をデプロイし実行すること
- Masterノードがクラスター内の全WorkerノードにSSHログインできる権限を備えること
- クラスター内の対応するノードのロールは以下の対応するポートを許可する必要があります。Master（9200および9201）、Worker（9203および9204）、Job Master(9205、9206、9207)、Job Worker（9208、9209、9210）、Proxy（9211）、LogServer（9212）。

## スタンドアローンモードでのデプロイと実行（疑似分散型アーキテクチャ）

疑似分散型アーキテクチャデプロイは主にGooseFSの体験とデバッグに適しています。初級ユーザーは自身のLinuxまたはMacシステムのホスト上でGooseFSのクイック体験およびデバッグを行うことができます。

### デプロイ

1. 初めに[GooseFSのバイナリーディストリビューションパッケージをダウンロード](https://downloads.tencentgoosefs.cn/goosefs/1.4.0/release/goosefs-1.4.0-bin.tar.gz)します。
2. ディストリビューションパッケージをダウンロードして解凍し、GooseFSのディレクトリに進み、次の操作を実行します。
- conf/goosefs-site.properties.templateをコピーしてconf/goosefs-site.properties設定ファイルを作成します。
```bash
 $ cp conf/goosefs-site.properties.template conf/goosefs-site.properties
```
- conf/goosefs-site.properties設定ファイル内で`goosefs.master.hostname`を`localhost`に設定します。
- conf/goosefs-site.properties設定ファイル内で`goosefs.master.mount.table.root.ufs`をローカルファイルシステム内のディレクトリ（例：/tmpまたは/data/goosefsなど）に設定します。

localhostのパスワードなしでのSSHログインを設定しておくことをお勧めします。これを行わなければ、フォーマット化および起動などの操作の際にlocalhostのログインパスワードを入力する必要があります。

### 実行

次のコマンドを実行すると、RamFSファイルシステムのマウントが完了します。

```bash
$ ./bin/goosefs-mount.sh SudoMount
```

同様に、上記のコマンドを実行せず、GooseFSクラスターの起動時に直接マウントすることもできます。

```bash
$ ./bin/goosefs-start.sh local SudoMount
```

起動後、`jps`コマンドを使用すると、疑似分散型モードでGooseFSの全プロセスを表示することができます。

```bash
$ jps
35990 Jps
35832 GooseFSSecondaryMaster
35736 GooseFSMaster
35881 GooseFSWorker
35834 GooseFSJobMaster
35883 GooseFSJobWorker
35885 GooseFSProxy
```

その後、`goosefs`コマンドラインを使用し、namespace、fileSystem、job、tableの各操作を実行できます。例えば、あるローカルファイルをGooseFSにアップロードし、現在のGooseFS内のルートディレクトリ下のファイルおよびディレクトリをリストアップするなどです。

```bash
$ goosefs fs copyFromLocal test.txt /
Copied file:///Users/goosefs/test.txt to /

$ goosefs fs ls /
-rw-r--r--  goosefs         staff                        0       PERSISTED 04-28-2021 04:00:35:156 100% /test.txt

```

GooseFSのコマンドラインは、GooseFSの管理とアクセスを行うすべてのコマンドラインインターフェースをユーザーに提供しています。それにはネームスペース（namespace）、テーブル（table）、ジョブ（job）および一般的なファイルシステム（fs）操作などが含まれます。具体的には公式ドキュメントをご参照いただくか、または`goosefs -h`コマンドラインパラメータを使用して詳細なヘルプ情報を取得することが可能です。

## クラスターモードでのデプロイと実行

クラスターデプロイと実行は主にユーザーが自作したIDCクラスターの本番環境、またはGooseFSを統合していないTencent Cloud EMRの本番環境向けのものです。具体的にはStandaloneアーキテクチャデプロイと高可用性（HA）アーキテクチャデプロイがあります。

GooseFSは`scripts`ディレクトリ下でパスワードなしSSHログインの一括設定およびGooseFSの一括インストールとデプロイを行うスクリプトツールを提供し、ユーザーがGooseFSの大規模クラスターのインストールとデプロイを便利でスピーディーに行えるようにしています。ユーザーは前章で述べたデプロイ環境要件のバッチデプロイ条件をご自身でチェックし、バッチデプロイが実行可能かどうかを柔軟に選択することができます。

### バッチデプロイツールの紹介

GooseFSは`scripts`ディレクトリ下でパスワードなしSSHログインの一括設定およびGooseFSのバッチデプロイとインストールを行うスクリプトツールを提供し、ユーザーが実行条件を満たす前提で、次の手順に従ってバッチデプロイタスクを完了できるようにしています。
- GooseFS解凍ディレクトリ、`cd ${GOOSEFS_HOME}`に進みます。
- `conf/masters`および`conf/workers`内のホスト名またはIPアドレスを設定します。
- その後`scripts`ディレクトリに進み、`commons.sh`というスクリプトファイルの`SCRIPT_EXEC_USER`および`SCRIPT_EXEC_PASSWORD`を正しく入力します。再び`root`アカウントに切り替えるか、または`sudo`権限で`config_ssh.sh`を実行し、クラスター全体のパスワードなしログイン設定を完了します。
- パスワードなしログイン設定の完了後、`validate_env.sh`ツールを実行してクラスター全体の設定状態をチェックすることができます。
- 設定ファイルディレクトリのソフトリンク、`ln -s conf ~/.goosefs`を作成します。
- 最後に`goosefs copy .`および`goosefs copy ~/.goosefs`を実行し、goosefsのバイナリーパッケージおよび設定ファイルを全ノードに配信します。

デプロイ全体のフローがすべて完了した後、`./bin/goosefs-start.sh all SudoMount`を実行してクラスター全体を起動し実行することができます。デフォルト設定では、すべての実行ログは`${GOOSEFS_HOME}/logs`に記録されます。

### Standaloneアーキテクチャデプロイ

StandaloneアーキテクチャはシングルMasterノード、マルチWorkerノードのクラスターデプロイアーキテクチャを採用しています。具体的には下記の手順を参照してデプロイおよび実行することができます。

1. [GooseFSのバイナリーディストリビューションパッケージをダウンロード](https://downloads.tencentgoosefs.cn/goosefs/1.4.0/release/goosefs-1.4.0-bin.tar.gz)します。
2. `tar zxvf goosefs-x.x.x-bin.tar.gz`コマンドを使用して、インストールパスの後に解凍します。バッチデプロイツールの紹介を参照してクラスターのバッチデプロイを設定および実行することができます。もしくは下記の詳細な手動デプロイフローを引き続き参照することも可能です。

（1）`conf`ディレクトリ下から`template`ファイルをコピーして設定ファイルを作成します。
```bash
$ cp conf/goosefs-site.properties.template conf/goosefs-site.properties
```
（2）`goosefs-site.properties`設定ファイル内で次の設定を指定します。
```properties
goosefs.master.hostname=<MASTER_HOSTNAME>
goosefs.master.mount.table.root.ufs=<STORAGE_URI>
```
このうち、`goosefs.master.hostname`はmasterノードのhostnameまたはipとして設定します。`goosefs.master.mount.table.root.ufs`はGooseFSルートディレクトリがマウントする基盤ファイルシステム（UFS）のパスURIを指定します。注意：このURIは必ずMasterおよびWorkerノードのどちらからもアクセス可能でなければならないため、ローカルディレクトリはサポートしていません。

例えば、あるCOSパスをGooseFSのルートパス：goosefs.master.mount.table.root.ufs=cosn://bucket-1250000000/goosefs/にマウントすることができます。

`masters`設定ファイルでシングルMasterノードのhostnameまたはipを指定します。例えば次のようになります。

```plaintext
# The multi-master Zookeeper HA mode requires that all the masters can access
# the same journal through a shared medium (e.g. HDFS or NFS).
# localhost
cvm1.compute-1.myqcloud.com
```

`workers`設定ファイルで全Workerノードのhostまたはipを指定します。例えば次のようになります。

```plaintext
# An GooseFS Worker will be started on each of the machines listed below.
# localhost
cvm2.compute-2.myqcloud.com
cvm3.compute-3.myqcloud.com
```

すべての設定が完了してから`./bin/goosefs copyDir conf/`を実行すると、全ノードに設定を同期することができます。

最後に`./bin/goosefs-start.sh all`を実行すると、GooseFSクラスターを起動できます。


### 高可用性アーキテクチャのデプロイ

シングルMasterノードのStandaloneアーキテクチャでは単一点障害の問題が発生しやすいため、実際の本番環境ではマルチMasterノードをデプロイして可用性の高いシステムアーキテクチャを得ることをお勧めします。複数のMasterノードのうち1つだけがリーダー（Leader）ノードとして外部にサービスを提供し、その他のスタンバイ（Standby）ノードは共有ログであるジャーナル（Journal）を同期することでリーダーノードと同一のファイルシステムの状態を維持します。リーダーノードに障害が発生してダウンすると、現在のスタンバイノードの中から1つが自動的に選択され、リーダーノードに代わって外部へのサービス提供を行います。こうすることでシステムの単一点障害を解消し、全体的な高可用性アーキテクチャを実現することができます。

現在GooseFSはRaftログとZookeeperという2種類の方式をベースにしてリーダーノードとスタンバイノードの状態の強整合性を実現しています。この2つのデプロイ方式について以下でそれぞれご説明します。

#### Raftの埋め込みログに基づく高可用性デプロイ設定

初めに設定テンプレートに従って設定ファイルを作成します。

```bash
$ cp conf/goosefs-site.properties.template conf/goosefs-site.properties
```

```properties
goosefs.master.mount.table.root.ufs=<STORAGE_URI>
goosefs.master.embedded.journal.addresses=<EMBBEDDED_JOURNAL_ADDRESS>
```

上記の設定選択項目の説明は次のとおりです。
-  `goosefs.master.mount.table.root.ufs`はGooseFSルートディレクトリにマウントする基盤ストレージURIとして設定します。
-  `goosefs.master.embedded.journal.addresses`はすべてのスタンバイノードの`ip:embedded_journal_port`または`host:embedded_journal_port`として設定します。このうち、embedded_journal_portはデフォルトでは9202です。例えば、192.168.1.1:9202,192.168.1.2:9202,192.168.1.3:9202のようになります。

Raftの埋め込みログに基づくデプロイ方法は[copycat](https://github.com/atomix/copycat)のLeader選出メカニズムに依存します。このため、RaftのHAデプロイアーキテクチャはZookeeperと相互に併用することはできません。

すべての設定が完了した後、同様に以下のコマンドを使用してすべての設定を同期します。

```bash
$ ./bin/goosefs copyDir conf/
```

最後にフォーマット化を完了すると、GooseFSクラスターの起動が可能になります。

```bash
$ ./bin/goosefs format
```

```bash
$ ./bin/goosefs-start.sh all
```
権限が不足していると表示された場合は、次の方法での再起動をお試しください。
```bash
$ ./bin/goosefs-stop.sh all
$ ./bin/goosefs-start.sh all SudoMount
```

次のコマンドを使用すると、現在のリーダー（Leader）ノードを確認できます。

```bash
$ ./bin/goosefs fs leader
```

次のコマンドを使用してクラスターの状態を確認することもできます。

```bash
$ ./bin/goosefs fsadmin report
```

#### Zookeeperのジャーナルに基づくデプロイ設定

Zookeeperサービスを設定してGooseFSの高可用性アーキテクチャを構築するには、次の条件を満たしている必要があります。
 - Zookeeperクラスター、GooseFS MasterはZookeeperを使用してLeaderを選出し、GooseFSのクライアントとWorkerノードはZookeeperによってリーダーMasterノードを照会していること。
 - 高可用性、強整合性の共有ストレージシステムで、なおかつすべてのGooseFSのMasterノードがアクセス可能であること。リーダーMasterノードはこのストレージシステムにログを書き込み、スタンバイ（Standby）ノードは常に共有ストレージシステムからログを読み取り、リプレイを行うことでリーダーノードの状態との整合性を維持します。通常、この共有ストレージシステムはHDFSまたはCOSに設定することを推奨します。例えば、`hdfs://10.0.0.1:9000/goosefs/journal`または`cosn://bucket-1250000000/journal`のようになります。

設定は次のとおりです。

```properties
goosefs.zookeeper.enabled=true
goosefs.zookeeper.address=<ZOOKEEPER_ADDRESSS>
goosefs.master.journal.type=UFS
goosefs.master.journal.folder=<JOURNAL_URI>
```

ZKモードの`JOURNAL_URI`は必ず共有ストレージシステムのURIでなければならない点に注意が必要です。その後、`./bin/goosefs copyDir conf/`を使用して、設定をクラスター内の全ノードに同期配信します。最後にクラスター`./bin/goosefs-start.sh all`を起動すれば完了です。


## GooseFSのプロセスリスト

`goosefs-start.sh all`スクリプトを実行してGooseFSを起動後、クラスターには次のプロセスが含まれます。

| プロセス             | 説明                                |
| ---------------- | ----------------------------------- |
| GooseFSMaster    | デフォルトのRPCポートは9200、Webポートは9201 |
| GooseFSWorker    | デフォルトのRPCポートは9203、Webポートは9204 |
| GooseFSJobMaster | デフォルトのRPCポートは9205、Webポートは9206 |
| GooseFSProxy     | デフォルトのWebポートは9211                 |
| GooseFSJobWorker | デフォルトのRPCポートは9208、Webポートは9210 |

