## メタデータアクセラレーターの概要

メタデータアクセラレーターはTencent Cloud COS（Cloud Object Storage）サービス向けにハイパフォーマンスなファイルシステム機能をご提供します。メタデータアクセラレーターの基盤にはCloud HDFSの優れたメタデータ管理機能を採用し、ユーザーがファイルシステムのセマンティクスによってCOSサービスにアクセスできるようサポートします。システム設計指標は帯域幅2.4Gb/s、10万レベルのQPSおよびミリ秒レベルの遅延を実現可能です。バケットでメタデータアクセラレーターを有効にすることで、ビッグデータ、ハイパフォーマンスコンピューティング、機械学習、AIなどのシーンに幅広く応用できます。メタデータアクセラレーターの詳細な説明に関しては、[メタデータアクセラレーター](https://intl.cloud.tencent.com/document/product/436/43305)をご参照ください。

## HDFSプロトコルを使用したアクセスのメリット

これまでのCOSをベースにしたビッグデータアクセスには主にHadoop-COSツールが使用されてきました。Hadoop-COSツールの内部ではHCFSインターフェースをCOSのRestfulインターフェースに適用することで、COS上のデータへのアクセスを可能にしています。COSとファイルシステムではメタデータの構成方法に違いがあるため、メタデータの操作性能にも差異があり、ビッグデータの分析性能に影響しています。メタデータアクセラレーターを有効にしたBucketは、HCFSプロトコルとの間に完全な互換性を有し、ネイティブのHDFSインターフェースを使用して直接アクセスできます。HDFSプロトコルをオブジェクトのプロトコルに変換するコストが不要なだけでなく、高効率なディレクトリのアトミックRename、ファイルのAtime、Mtime更新、高効率なディレクトリのDU統計、Posix ACL権限サポートなどの、ネイティブHDFSのいくつかの機能もご提供可能です。

<span id="1"></span>
## バケットの作成とHDFSプロトコルの設定

1. COSバケットを作成し、メタデータアクセラレーターを有効にします。

バケットの作成完了後、バケットの**ファイルリスト**のページに進み、このページでファイルのアップロードおよびダウンロード操作を行うことができます。
2. 左側のメニューバーで、**パフォーマンス設定 > メタデータアクセラレーション機能**をクリックすると、メタデータアクセラレーション機能が有効になっていることを確認できます。
**メタデータアクセラレーションを有効にしたい**バケットを初めて作成した場合は、表示に従って対応する**権限承認**操作を行う必要があります。クリックして権限承認を完了すると、HDFSプロトコルが自動的に有効化され、デフォルトのバケットマウントポイント情報を見ることができるようになります。
>?対応するHDFSファイルシステムが見つからないと表示される場合は、[チケットを提出](https://console.cloud.tencent.com/workorder/category)をクリックしてお問い合わせいただければ、サポートを受けることができます。
>
3. HDFS権限設定バーで、**権限設定の追加**をクリックします。

4. VPCネットワーク名の列でコンピューティングクラスターのあるVPCネットワークアドレスを選択し、ノードのIPアドレス列に、VPCネットワークセグメント下で許可したいIPアドレスまたはIPセグメントを入力します。アクセスのタイプは読み取り/書き込みまたは読み取り専用を選択し、設定完了後に**保存**をクリックします。
>? HDFSの権限設定とネイティブのCOS権限システムとの間には違いがあります。HDFSプロトコルを使用してアクセスする際は、ネイティブHDFSと同じ権限を取得するのに便利なため、HDFS権限設定によってVPC内のマシンを指定してCOSバケットにアクセスすることをお勧めします。


## コンピューティングクラスターを設定してCOSにアクセス

### Tencent Cloud EMR環境

Tencent Cloud EMR環境にはすでにCOSがシームレスに統合されていますので、次のいくつかの手順を実行するだけです。
1. EMRマシンを見つけ、このマシン上で次のコマンドを実行します。EMR環境下のHDFSプロトコルのクライアントパッケージのバージョンをチェックし、クライアントjarパッケージが、2.7およびそれ以降のバージョンであることを確認します。
```
find / -name "chdfs*"
```
検索結果のchdfsパッケージのバージョンのサフィックスが2.7あるいはそれ以降であることを確認します。
2. クライアントバージョンのパッケージを更新する必要がある場合は、次の手順を実行し、更新します。
 1. jarパッケージのスクリプトファイルをダウンロードして更新します。ダウンロードアドレスは次のとおりです。
    - [update_cos_jar.sh](https://hadoop-jar-beijing-1259378398.cos.ap-beijing.myqcloud.com/hadoop_plugin_network/2.7/update_cos_jar.sh)
    - [update_cos_jar_common.sh](https://hadoop-jar-beijing-1259378398.cos.ap-beijing.myqcloud.com/hadoop_plugin_network/2.7/update_cos_jar_common.sh)
 2. 2つのスクリプトをサーバーの/rootディレクトリ下に置き、update_cos_jar.shに実行権限を追加し、次のコマンドを実行します。
```
sh update_cos_jar.sh  https://hadoop-jar-beijing-1259378398.cos.ap-beijing.myqcloud.com/hadoop_plugin_network/2.7  
```
パラメータを対応するリージョンのバケットのものに置き換えます。例えば広州リージョンの場合は、`https://hadoop-jar-guangzhou-1259378398.cos.ap-guangzhou.myqcloud.com/hadoop_plugin_network/2.7`に置き換えます。
各EMRノード上で上記の手順を実行します。これを、マシン上のjarパッケージの置き換えがすべて完了するまで行います。
3. EMRコンソールでcore-site.xmlを設定し、設定項目`fs.ofs.bucket.region`を追加します。このパラメータは、`ap-shanghai`のようなバケットの所在COSリージョンを指定するために用いられます。
>!`fs.ofs.bucket.region`は必ず設定する必要があります。このパラメータは、`ap-shanghai`のようなバケットの所在COSリージョンを指定するために用いられます。
>
4. Yarn、Hive、Presto、Impalaなどの常駐サービスを再起動します。


### 自作Hadoop/CDHなどの環境
1. HDFSプロトコルアクセスの[クライアントインストールパッケージ](https://github.com/tencentyun/chdfs-hadoop-plugin/tree/master/jar)をダウンロードします。インストールパッケージが、2.7およびそれ以降のバージョンであることを確認してください。
2. ダウンロード後、インストールパッケージをHadoopクラスターの各サーバーの`classpath`パスに正しく配置します。例えば、 `/usr/local/service/hadoop/share/hadoop/common/lib/`となります（実際の状況に応じて配置してください。コンポーネントによって配置位置が異なる可能性があります）。
2. コンピューティングクラスターに`core-site.xml`を設定します。具体的な設定ガイドについては[CHDFSのマウント](https://intl.cloud.tencent.com/document/product/1106/41965)をご参照ください。
3. Yarn、Hive、Presto、Impalaなどの常駐サービスを再起動します。

>!`fs.ofs.bucket.region`は必ず設定する必要があります。このパラメータは、`ap-shanghai`のようなバケットの所在COSリージョンを指定するために用いられます。
>

### 環境の検証

環境設定がすべて完了した後、次の操作によって検証を行うことができます。
- 下図のように、クライアントでHadoopコマンドラインを使用して、マウントが成功したかどうかを確認します。
![](https://qcloudimg.tencent-cloud.cn/raw/90264cdfe35753b95d48db5ab6675629.png)
- [COSコンソール](https://console.cloud.tencent.com/cos)にログインしてバケットファイルリストを確認し、ファイルとディレクトリが一致しているかどうかを明らかにすることができます。


## Ranger権限設定

HDFSプロトコルは、デフォルトではネイティブPOSIX ACL方式を採用して認証を行います。Ranger認証を使用したい場合は、次のフローを参照して設定を行うことができます。

### EMR環境

1. EMR環境にはCOSRangerサービスが統合されています。EMRクラスターの購入時にCOSRangerサービスにチェックを入れます。
2. HDFSプロトコルのHDFS認証モードでRanger認証モードを選択し、Rangerに対応するアドレス情報を設定します。
 - CHDFSの場合は、core-site.xmlに設定項目fs.ofs.ranger.enable.flagを追加し、trueに設定します。
 - COSNの場合は、core-site.xmlに設定項目fs.cosn.credentials.providerを追加し、org.apache.hadoop.fs.auth.RangerCredentialsProviderと設定します。
 - Rangerに関するご質問がありましたら、[CHDFSに関するよくあるご質問](https://intl.cloud.tencent.com/document/product/1106/41958)をご参照ください。

### 自作Hadoop/CDHなどの環境

1. Rangerサービスを設定し、RangerサービスによってHDFSプロトコルでCOSにアクセスすることができます。詳細については、[CHDFS Ranger権限システムソリューション](https://intl.cloud.tencent.com/document/product/1106/41973)のドキュメントをご参照ください。
2. HDFSプロトコルのHDFS認証モードでRanger認証モードを選択し、Rangerに対応するアドレス情報を設定します。
 - CHDFSの場合は、core-site.xmlに設定項目fs.ofs.ranger.enable.flagを追加し、trueに設定します。
 - COSNの場合は、core-site.xmlに設定項目fs.cosn.credentials.providerを追加し、org.apache.hadoop.fs.auth.RangerCredentialsProviderと設定します。
 - Rangerに関するご質問がありましたら、[CHDFSに関するよくあるご質問](https://intl.cloud.tencent.com/document/product/1106/41958)をご参照ください。

## その他

ビッグデータのシーンでは、次の手順を参照して、メタデータアクセラレーション機能を有効にしたバケットにHDFSプロトコルを使用してアクセスすることができます。

1. [バケットの作成とHDFSプロトコルの設定](#1) で示したように、`core-stie.xml`でHDFSプロトコルに関連するマウントポイントの情報を設定します。
2. Hive、MR、Sparkなどのコンポーネントによってバケットにアクセスします。[コンピューティングクラスターにおけるCOSバケットのマウント](https://intl.cloud.tencent.com/document/product/436/46199)をご参照ください。
3. デフォルトでは、ネイティブ`POSIX ACL`方式を採用して認証を行います。`Ranger認証`を使用したい場合は、 [Rangerの関連原理およびアクセスの実践](https://intl.cloud.tencent.com/document/product/1106/41973)をご参照ください。



