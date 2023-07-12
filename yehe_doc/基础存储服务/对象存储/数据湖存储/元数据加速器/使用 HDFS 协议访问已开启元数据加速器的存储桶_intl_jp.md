## メタデータアクセラレーターの概要

メタデータアクセラレーターはTencent Cloud COS（Cloud Object Storage）サービス向けにハイパフォーマンスなファイルシステム機能をご提供します。メタデータアクセラレーターの基盤にはCloud HDFSの優れたメタデータ管理機能を採用し、ユーザーがファイルシステムのセマンティクスによってCOSサービスにアクセスできるようサポートします。システム設計指標は100GBの帯域幅、10万レベルのQPSおよびミリ秒レベルの遅延を実現可能です。バケットでメタデータアクセラレーターを有効にすることで、ビッグデータ、ハイパフォーマンスコンピューティング、機械学習、AIなどのシーンに幅広く応用できます。メタデータアクセラレーターの詳細な説明に関しては、[メタデータアクセラレーター](https://intl.cloud.tencent.com/document/product/436/43305)をご参照ください。

## HDFSプロトコルを使用したアクセスのメリット

これまでのCOSをベースにしたビッグデータアクセスには主にHadoop-COSツールが使用されてきました。Hadoop-COSツールの内部ではHCFSインターフェースをCOSのRestfulインターフェースに適用することで、COS上のデータへのアクセスを可能にしています。COSとファイルシステムではメタデータの構成方法に違いがあるため、メタデータの操作性能にも差異があり、ビッグデータの分析性能に影響しています。メタデータアクセラレーターを有効にしたBucketは、HCFSプロトコルとの間に完全な互換性を有し、ネイティブのHDFSインターフェースを使用して直接アクセスできます。HDFSプロトコルをオブジェクトのプロトコルに変換するコストが不要なだけでなく、高効率なディレクトリのアトミックRename、ファイルのAtime、Mtime更新、高効率なディレクトリのDU統計、Posix ACL権限サポートなどの、ネイティブHDFSのいくつかの機能もご提供可能です。

<span id="1"></span>

## バケットの作成とHDFSプロトコルの設定

1. [COSバケットの作成](https://intl.cloud.tencent.com/document/product/436/13309)を行い、メタデータアクセラレーターを有効化します。
バケットの作成完了後、バケットの**ファイルリスト**のページに進み、このページでファイルのアップロードおよびダウンロード操作を行うことができます。
2. 左側のメニューバーで、**パフォーマンス設定 > メタデータアクセラレーション機能**をクリックすると、メタデータアクセラレーション機能が有効になっていることを確認できます。
**メタデータアクセラレーションを有効にしたい**バケットを初めて作成した場合は、表示に従って対応する**権限承認**操作を行う必要があります。クリックして権限承認を完了すると、HDFSプロトコルが自動的に有効化され、デフォルトのバケットマウントポイント情報を見ることができるようになります。

>?対応するHDFSファイルシステムが見つからないと表示される場合は、[チケットを提出](https://console.cloud.tencent.com/workorder/category)をクリックしてお問い合わせいただければ、サポートを受けることができます。
>
3. HDFS権限設定バーで、**権限設定の追加**をクリックします。


4. VPCネットワーク名の列でコンピューティングクラスターのあるVPCネットワークアドレスを選択し、ノードのIPアドレス列に、VPCネットワークセグメント下で許可したいIPアドレスまたはIPセグメントを入力します。アクセスのタイプは読み取り/書き込みまたは読み取り専用を選択し、設定完了後に**保存**をクリックします。
>? **HDFSの権限設定**とネイティブのCOS権限システムとの間には違いがあります。HDFSプロトコルを使用してアクセスする際は、ネイティブHDFSと同じ権限を取得するのに便利なため、HDFS権限設定によってVPC内のマシンを指定してCOSバケットにアクセスすることをお勧めします。

## コンピューティングクラスターを設定してCOSにアクセス

### 環境の依存

|     依存項目         | chdfs-hadoop-plugin                               | COSN（hadoop-cos）                                | cos_api-bundle                                               |
| ------------ | ------------------------------------------------- | ------------------------------------------------- | ------------------------------------------------------------ |
| 必要なバージョン     | ≥ バージョン2.7                                         | ≥ バージョン8.1.5                                       | COSNのバージョンに対応します。[COSN github releases](https://github.com/tencentyun/hadoop-cos/releases)をご確認ください |
| オープンソースダウンロードアドレス | [Githubアドレス](https://github.com/tencentyun/chdfs-hadoop-plugin)   | [Githubアドレス](https://github.com/tencentyun/hadoop-cos/releases) | [Githubアドレス](https://github.com/tencentyun/hadoop-cos/releases)            |

### Tencent Cloud EMR環境

[Tencent Cloud EMR環境](https://console.cloud.tencent.com/emr) COSがすでにシームレスに統合されているため、次の手順を行うだけで完了します。

1. EMRマシンを見つけ、このマシン上で次のコマンドを実行します。EMR環境下で必要なサービスのフォルダにあるパッケージのバージョンが環境依存要件に適合するかどうかをチェックします。
```plaintext
find / -name "chdfs*" 
find / -name "temrfs_hadoop*" 
```
![](https://qcloudimg.tencent-cloud.cn/raw/cb73bf879c1b7c0aa3304392c6845c2d.png)
![](https://qcloudimg.tencent-cloud.cn/raw/654573077995cb16701af9635d7db351.png)


検索結果の2つのjarパッケージのバージョンが上記の環境依存の要件に適合していることを確認します。

2. chdfs-hadoop-pluginバージョンのパッケージを更新する必要がある場合は、次の手順を実行し、更新します。

   jarパッケージのスクリプトファイルをダウンロードして更新します。ダウンロードアドレスは次のとおりです。

   - [update_cos_jar.sh](https://hadoop-jar-beijing-1259378398.cos.ap-beijing.myqcloud.com/hadoop_plugin_network/2.7/update_cos_jar.sh)
   - [update_cos_jar_common.sh](https://hadoop-jar-beijing-1259378398.cos.ap-beijing.myqcloud.com/hadoop_plugin_network/2.7/update_cos_jar_common.sh)

   2つのスクリプトをサーバーの/rootディレクトリ下に置き、update_cos_jar.shに実行権限を追加し、次のコマンドを実行します。
```
sh update_cos_jar.sh  https://hadoop-jar-beijing-1259378398.cos.ap-beijing.myqcloud.com/hadoop_plugin_network/2.7  
```
パラメータを対応するリージョンのバケットのものに置き換えます。例えば広州リージョンの場合は、`https://hadoop-jar-guangzhou-1259378398.cos.ap-guangzhou.myqcloud.com/hadoop_plugin_network/2.7`に置き換えます。
各EMRノード上で上記の手順を実行します。これを、マシン上のjarパッケージの置き換えがすべて完了するまで行います。

3. hadoop-cosパッケージまたはcos_api-bundleバージョンのパッケージを更新する必要がある場合は、次の手順を実行し、更新します。
 - /usr/local/service/hadoop/share/hadoop/common/lib/hadoop-temrfs-1.0.5.jarをtemrfs_hadoop_plugin_network-1.1.jarに置き換えます。
 - core-site.xmlに次の設定項目を追加します。
    -  emr.temrfs.download.md5=822c4378e0366a5cc26c23c88b604b11
    -  emr.temrfs.download.version=2.7.5-8.1.5-1.0.6 （2.7.5をご自身のhadoopのバージョンに置き換え、8.1.5を必要なhadoop-cosパッケージのバージョンに置き換えます。ただし、バージョンは8.1.5より低くてはなりません。cos_api-bundleバージョンは自動的に適用されます）
    -  emr.temrfs.download.region=sh
    -  emr.temrfs.tmp.cache.dir=/data/emr/hdfs/tmp/temrfs 
 - core-site.xmlで設定fs.cosn.impl=com.qcloud.emr.fs.TemrfsHadoopFileSystemAdapterを変更します。

4. [EMRコンソール](https://console.cloud.tencent.com/emr)でcore-site.xmlを設定し、設定項目`fs.cosn.bucket.region`、`fs.cosn.trsf.fs.ofs.bucket.region`を追加します。このパラメータは、`ap-shanghai`のようなバケットの所在COSリージョンを指定するために用いられます。
>!`fs.cosn.bucket.region`と`fs.cosn.trsf.fs.ofs.bucket.region`は必ず設定する必要があります。このパラメータは、`ap-shanghai`のようなバケットの所在COSリージョンを指定するために用いられます。
>
5. Yarn、Hive、Presto、Impalaなどの常駐サービスを再起動します。


###  自作Hadoop/CDHなどの環境

1. [自作環境](https://docs.cloudera.com/csp/2.0.1/deployment/topics/csp-install-cdh.html)では、環境依存の中の、バージョン要件に適合する3つのjarパッケージをダウンロードする必要があります。
2. ダウンロード後、上記の3つのインストールパッケージをHadoopクラスターの各サーバーの`classpath`パスに正しく配置します。例えば、 `/usr/local/service/hadoop/share/hadoop/common/lib/`となります（実際の状況に応じて配置してください。コンポーネントによって配置位置が異なる可能性があります）。
3. hadoop-env.shファイルを変更します。`$HADOOP_HOME/etc/hadoop`ディレクトリに移動し、hadoop-env.shファイルを編集して、以下の内容を追加し、cosn関連のjarパッケージをHadoop環境変数に追加します。
   ```shell
   for f in $HADOOP_HOME/share/hadoop/tools/lib/*.jar; do
     if [ "$HADOOP_CLASSPATH" ]; then
       export HADOOP_CLASSPATH=$HADOOP_CLASSPATH:$f
     else
       export HADOOP_CLASSPATH=$f
     fi
   done
   ```
4. コンピューティングクラスターに`core-site.xml`を設定し、次の設定を追加します。

   ```xml
   <!--cosnの実装クラス-->
   <property>
           <name>fs.cosn.impl</name>
           <value>org.apache.hadoop.fs.CosFileSystem</value>
   </property>
   
   <!--ユーザーバケットのリージョン情報です。形式はap-guangzhou-->のようになります    
   <property>
           <name>fs.cosn.bucket.region</name>
           <value>ap-guangzhou</value>
   </property>
   
   <!--ユーザーバケットのリージョン情報です。形式はap-guangzhou-->のようになります    
   <property>
           <name>fs.cosn.trsf.fs.ofs.bucket.region</name>
           <value>ap-guangzhou</value>
   </property>
   
   <!--SecretIdおよびSecretKeyの取得方法の設定-->
   <property>
           <name>fs.cosn.credentials.provider</name>
           <value>org.apache.hadoop.fs.auth.SimpleCredentialProvider</value>
   </property>
   
   <!--アカウントのAPIキー情報です。[CAMコンソール](https://console.cloud.tencent.com/capi)にログインすると、Tencent Cloud APIキーを確認することができます。-->
   <property>
           <name>fs.cosn.userinfo.secretId</name>
           <value>XXXXXXXXXXXXXXXXXXXXXXXX</value>
   </property>
   
   <!--アカウントのAPIキー情報です。[CAMコンソール](https://console.cloud.tencent.com/capi)にログインすると、Tencent Cloud APIキーを確認することができます。-->
   <property>
           <name>fs.cosn.userinfo.secretKey</name>
           <value>XXXXXXXXXXXXXXXXXXXXXXXX</value>
   </property>
   
   <!--アカウントのappidの設定-->
   <property>
           <name>fs.cosn.trsf.fs.ofs.user.appid</name>
           <value>125XXXXXX</value>
   </property>
   
   <!--プロセス実行中に生成される一時ファイル保存用のローカル一時ディレクトリ-->     
   <property>
           <name>fs.cosn.trsf.fs.ofs.tmp.cache.dir</name>
           <value>/tmp</value>
   </property>
   ```

5. Yarn、Hive、Presto、Impalaなどの常駐サービスを再起動します。

### 環境の検証

環境設定がすべて完了した後、次の操作によって検証を行うことができます。

- 下図のように、クライアントでHadoopコマンドラインを使用して、マウントが成功したかどうかを確認します。
![](https://qcloudimg.tencent-cloud.cn/raw/3dbfa5004cf6a3b9183fae20cfaa4e49.png)
- [COSコンソール](https://console.cloud.tencent.com/cos)にログインしてバケットファイルリストを確認し、ファイルとディレクトリが一致しているかどうかを確認します。

## Ranger権限設定

HDFSプロトコルは、デフォルトではネイティブPOSIX ACL方式を採用して認証を行います。Ranger認証を使用したい場合は、次のフローを参照して設定を行うことができます。

### EMR環境

1. EMR環境にはCOSRangerサービスが統合されています。EMRクラスターの購入時にCOSRangerサービスにチェックを入れます。
2. HDFSプロトコルの**HDFS認証モード**で**Ranger認証モード**を選択し、Rangerに対応するアドレス情報を設定します。
 - core-site.xmlに設定項目fs.cosn.credentials.providerを追加し、org.apache.hadoop.fs.auth.RangerCredentialsProviderに設定します。
 - Rangerに関するご質問がありましたら、[Rangerの概要説明](https://intl.cloud.tencent.com/document/product/436/39144)をご参照ください。

### 自作Hadoop/CDHなどの環境

1. Rangerサービスを設定し、RangerサービスによってHDFSプロトコルでCOSにアクセスすることができます。詳細については、[COS Ranger権限システムソリューション](https://intl.cloud.tencent.com/document/product/436/39144)のドキュメントをご参照ください。
2. HDFSプロトコルの**HDFS認証モード**で**Ranger認証モード**を選択し、Rangerに対応するアドレス情報を設定します。
 - core-site.xmlに設定項目fs.cosn.credentials.providerを追加し、org.apache.hadoop.fs.auth.RangerCredentialsProviderに設定します。


## その他

ビッグデータのシーンでは、次の手順を参照して、メタデータアクセラレーション機能を有効にしたバケットにHDFSプロトコルを使用してアクセスすることができます。

1. [バケットの作成とHDFSプロトコルの設定](#1) で示したように、`core-stie.xml`でHDFSプロトコルに関連するマウントポイントの情報を設定します。
2. Hive、MR、Sparkなどのコンポーネントによってバケットにアクセスします。[コンピューティングクラスターにおけるCOSバケットのマウント](https://intl.cloud.tencent.com/document/product/436/46199)をご参照ください。
3. デフォルトでは、ネイティブ`POSIX ACL`方式を採用して認証を行います。`Ranger認証`を使用したい場合は、 [COS Ranger権限システムソリューション](https://intl.cloud.tencent.com/document/product/436/39144)をご参照ください。

