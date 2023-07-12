## 背景

ビッグデータユーザーがストレージ・コンピューティング分離を使用した後、Cloud HDFS(CHDFS)でデータをホストします。CHDFSは、HDFSに類する権限システム制御を提供します。Hadoop RangerはHDFS権限に基づいて、ユーザーグループの権限設定や特定のプレフィックスの権限設定など、よりきめ細かい権限制御を提供します。また同時にHadoop Rangerは、ワンストップの権限システムソリューションとして、ストレージ側の権限の管理と制御をサポートするだけでなく、YARNやHiveなどのコンポーネントの権限制御もサポートします。お客様の利便性を維持するため、お客様がRangerを使用してCHDFS権限を制御する際に便利なCHDFSのRangerアクセスソリューションを提供しています。


## メリット

- Hadoop権限の習慣と互換性のある細粒度の権限制御。
- ユーザーは、ビッグデータコンポーネントとクラウドホスティングストレージを統合管理する権限を持っています。

## ソリューションアーキテクチャ

![](https://main.qcloudimg.com/raw/ccbe75fb92788fce02b02cf0ce63de1c.png)

Hadoop権限システムでは、認証はKerberosによって提供され、権限付与と認証はRangerが担当します。これをベースとして、以下のコンポーネントを提供し、CHDFSのRanger権限スキームをサポートします。

- CHDFS-Ranger-Plugin：Rangerサーバー用のサービス定義プラグインを提供します。Ranger側のCHDFSサービスの説明が提供され、このプラグインがデプロイされると、ユーザーはRangerの制御ページで対応するアクセス許可ポリシーを入力できるようになります。
- COSRangerService：このサービスは、Rangerのクライアントを統合し、Rangerサーバーから権限ポリシーを定期的に同期し、お客様の認証リクエストを受信した後、ローカルで権限チェックを行います。同時に、HadoopでのDelegationTokenの発行や更新などのインターフェースを提供します。すべてのインターフェースは、Hadoop IPCを介して定義されます。
- CosRangerClient：COSNプラグインはそれを動的にロードし、権限チェックのリクエストをCosRangerServiceに転送します。

## デプロイ環境

- Hadoop環境。
- ZooKeeper、Ranger、Kerberosサービス（認証の必要がある場合は、デプロイします）。

>? 以上のサービスは成熟したオープンソースコンポーネントであるため、お客様はご自身でインストールすることができます。
>

## コンポーネントのデプロイ

<dx-tabs>
::: CHDFS-Ranger-Pluginのデプロイ
CHDFS-Ranger-Pluginは、Ranger Adminコンソールにおけるサービスの種類を拡張します。ユーザーはRangerコンソールで、CHDFSに関連する操作権限を設定することができます。

#### コードアドレス

[Github](https://github.com/tencentyun/cos-ranger-service)のranger-pluginディレクトリから取得できます。

#### バージョン

V1.2およびそれ以降のバージョン。

#### デプロイ手順

1. Rangerのサービス定義ディレクトリの下にCOSディレクトリを新規作成します（注意：ディレクトリの権限には、少なくともxとrの権限が必要です）。
 1. Tencent CloudのEMR環境の場合、パスはranger/ews/webapp/WEB-INF/classes/ranger-pluginsです。
 2. セルフビルドのhadoop環境では、rangerディレクトリ下のfind hdfsなどの方法によって、rangerサービスに接続されているコンポーネントを探し、ranger-pluginsディレクトリの場所を見つけることができます。
![](https://main.qcloudimg.com/raw/679f61339b8c3864a84b3b757dd84815.png)
2. CHDFSディレクトリ下にcos-chdfs-ranger-plugin-xxx.jarを配置します（注意：jarパッケージには少なくともr個の権限があります）。
3. Rangerサービスを再起動します。
4. RangerにCHDFS Serviceを登録します。次のコマンドを参照できます。
<dx-codeblock>
::: plaintext
##サービスを発行するには、Ranger管理者アカウントのパスワードとRangerサービスのアドレスを渡す必要があります。
##Tencent Cloud EMRクラスターの場合、管理者ユーザーはrootであり、パスワードはemrクラスターの構築時に設定されたrootパスワードです。rangerサービスのIPは、EMRのmasterノードのIPに置き換えられます。
adminUser=root
adminPasswd=xxxxxx
rangerServerAddr=10.0.0.1:6080
curl -v -u${adminUser}:${adminPasswd} -X POST -H "Accept:application/json" -H "Content-Type:application/json" -d @./chdfs-ranger.json http://${rangerServerAddr}/service/plugins/definitions
##定義されたサービスを削除する場合は、作成されたばかりのサービスが渡され、サービスIDが返されます
serviceId=102
curl -v -u${adminUser}:${adminPasswd} -X DELETE -H "Accept:application/json" -H "Content-Type:application/json" http://${rangerServerAddr}/service/plugins/definitions/${serviceId}
:::
</dx-codeblock>
5. 次に示すように、サービスの作成に成功すると、RangerコンソールにCHDFSサービスが表示されます。
![](https://main.qcloudimg.com/raw/163aac38c68931f51ab34c221ea3cef1.png)
6. CHDFSサービス側の【+】をクリックして、新しいサービスインスタンスを定義します。サービスインスタンス名は、`chdfs`や`chdfs_test`などにカスタマイズできます。サービスの設定は次のとおりです。
![](https://main.qcloudimg.com/raw/255869b8c485a93427585d21476ec001.png)
そのうちpolicy.grantrevoke.auth.usersは、COSRangerServiceサービスを後で起動するためのユーザー名を設定する必要があります。通常はhadoopに設定することをお勧めします。その後のCOSRangerServiceは、このユーザー名で起動できます。
7. 次に示すように、新しく発行されたCHDFSサービスインスタンスをクリックして、policyを追加します。
![](https://main.qcloudimg.com/raw/f0d76ecf787eec3340f7d923e65b9b48.png)
8. ジャンプインターフェースで、以下のパラメータを設定します。具体的な手順は次のとおりです。
![](https://main.qcloudimg.com/raw/317e1b5cb39abae6904552cb1ebade58.png)
 - **MountPoint**: マウントポイントの名前。形式はf4mxxxxxx-yyyyなどのスタイルで、[CHDFSコンソール](https://console.cloud.tencent.com/chdfs/filesystem)にログインして確認することができます。
 - **path**: CHDFSパス。CHDFSパスは、必ず`/`で始まる必要があることにご注意ください。
    - include：設定された権限がpath自体またはpath以外の他のパスに適用されることを示します。
    - recursive：権限がpathだけでなく、path下のサブメンバー（つまり、再帰的なサブメンバー）にも適用できることを示します。通常、pathがディレクトリに設定されている場合に用いられます。
 - **user/group**：ユーザー名とユーザーグループ。ここでは「OR」関係です。ユーザー名またはユーザーグループがそれらのうちいずれかを満たす場合、対応する操作権限を有することができます。
 - **Permissions**:
    -  Read：読み取り操作。オブジェクトのダウンロード、オブジェクトメタデータの照会など、Cloud Object StorageでのGET、HEADといった操作に対応します。
    -  Write：書き込み操作。オブジェクトのアップロードなど、COS内のPUTといった変更操作に対応します。
    -  Delete：削除操作。COS内のObjectの削除に対応します。HadoopのRename操作の場合、元のパスに対する削除操作権限と、新しいパスに対する書き込み操作権限が必要です。
    -  List：トラバース権限。COS内のList Objectに対応します。

:::
::: COS-Ranger-Serviceのデプロイ
COS-Ranger-Serviceは、権限システム全体のコアであり、rangerクライアントの統合、ranger client認証リクエストの受信、token発行・更新のリクエストや一時キー発行リクエストを担当します。同時に、センシティブ情報（Tencent Cloudのキー情報）が配置されているエリアでもあり、通常は踏み台サーバーにデプロイされ、クラスター管理者のみが操作や設定の確認などを行うことができます。

COS-Ranger-Serviceは、1つの本番データベースと1つ以上のスタンバイによるHAデプロイをサポートし、DelegationTokenのステータスはHDFSに永続化されます。ZKを介してロックを取得することにより、Leaderの身分を決定します。Leaderの身分を取得するサービスは、COS Ranger Clientがルーティング・アドレッシングを実行できるように、アドレスをZKに書き込みます。

#### コードアドレス

[Github](https://github.com/tencentyun/cos-ranger-service)のcos-ranger-serverディレクトリ下から取得できます。

#### バージョン

V1.2およびそれ以降のバージョン。

#### デプロイ手順

1. COS Ranger Serviceサービスコードをクラスター内の複数のマシンにコピーします。本番環境は、少なくとも2台のマシン（1台は本番データベースでもう1台はスタンバイ）にすることをお勧めします。センシティブ情報が含まれるため、踏み台サーバーまたは厳格に制御されているマシンにすることをお勧めします。
2. cos-ranger.xmlファイルの関連設定を変更します。そのうち変更が必要な設定項目を、以下に示します。設定項目の説明については、ファイル内のコメントをご参照ください。
 -  qcloud.object.storage.rpc.address
 -  qcloud.object.storage.status.port
 -  qcloud.object.storage.enable.chdfs.ranger
 -  qcloud.object.storage.zk.address
3. ranger-chdfs-security.xmlファイルの関連設定を変更します。そのうち変更が必要な設定項目を、以下に示します。設定項目の説明については、ファイル内のコメントをご参照ください。
 -  ranger.plugin.chdfs.policy.cache.dir
 -  ranger.plugin.chdfs.policy.rest.url
 -  ranger.plugin.chdfs.service.name
4. start_rpc_server.shのhadoop_conf_pathとjava.library.pathの設定を変更します。これら2つの設定はそれぞれ、hadoop設定ファイルが配置されているディレクトリ（core-site.xml、hdfs-site.xmlなど）とhadoop native libパスを指します。
5. 次のコマンドを実行して、サービスを起動します。
```
chmod +x start_rpc_server.sh
nohup ./start_rpc_server.sh &> nohup.txt &
```
6. 起動に失敗した場合は、log下のerrorログをチェックして、エラー情報があるかどうかを確認します。
7. cos-ranger-serviceは、HTTPポートステータスの表示をサポートします（ポート名はqcloud.object.storage.status.port、デフォルト値は9998）。ユーザーは次のコマンドを使用して、ステータス情報（leader、認証数の統計など）を取得できます。
```
# 以下の10.xx.xx.xxxをranger serviceがデプロイされているマシンのIPに置き換えてください
# port 9998はqcloud.object.storage.status.port設定値に設定されます
curl -v http://10.xx.xx.xxx:9998/status
```

:::
::: COS-Ranger-Clientのデプロイ
COS-Ranger-Clientは、hadoop chdfsプラグインによって動的にロードされ、COS-Ranger-Serviceにアクセスするための関連するリクエストを代行します。例えば、token、認証操作などです。

#### コードアドレス

[Github](https://github.com/tencentyun/cos-ranger-service)のcos-ranger-clientディレクトリ下から取得できます。

#### バージョン

V1.0およびそれ以降のバージョン。

#### デプロイ方法
1. cos-ranger-client jarパッケージをCHDFSプラグインと同じディレクトリ下にコピーします（ご自身のhadoopバージョンと一致するjarパッケージを選択してコピーしてください）。
2. core-site.xmlに次の設定項目を追加します。
<dx-codeblock>
::: xml
```
<configuration>
           <!--*****設定必須********-->
           <!-- zkのアドレス、クライアントはzkからranger-serviceのサービスアドレスを照会して取得します -->
           <property>
               <name>qcloud.object.storage.zk.address</name>
               <value>10.0.0.8:2121</value>
           </property>

           <!--***オプション設定****-->           
           <!-- cos ranger service端末で使用されるkerberos認証情報を設定します。cos ranger service端末の設定をご参照ください。必ず一致を維持する必要があります。認証要件がない場合、設定は必要ありません -->
           <property>                
					 <name>qcloud.object.storage.kerberos.principal</name>
					 <value>hadoop/_HOST@EMR-XXXX</value>
           </property>

         <!--***オプション設定****-->  
         <!-- zkに記録されたranger serverのipアドレスパス。ここではデフォルト値が使用され、設定は必ずcos-ranger-serviceの設定と一致する必要があります -->
          <property>              
					<name>qcloud.object.storage.zk.leader.ip.path</name> 
					<value>/ranger_qcloud_object_storage_leader_ip</value>
          </property>
</configuration>
```
:::
</dx-codeblock>
:::
::: CHDFSのデプロイ

#### バージョン

V2.1およびそれ以降のバージョン。

#### デプロイ方法

CHDFSプラグインのデプロイ方法については、[CHDFSのマウント](https://intl.cloud.tencent.com/document/product/1106/41965)ドキュメントを参照し、rangerを有効にして以下の方法を追加して行います。


<dx-codeblock>
::: plaintext 
```
    <property>
        <name>fs.ofs.ranger.enable.flag</name> 
        <value>true</value>
    </property>
```
:::
</dx-codeblock>
:::
</dx-tabs>


## 検証

1. hadoop cmdを使用して、chdfsへのアクセスに関連する操作を実行します。以下に例を示します。
```plaintext
# マウントポイント、パスなどをご自分の実際の情報に置き換えます。
hadoop fs -ls ofs://f4mxxxxyyyy-zzzz.chdfs.ap-guangzhou.myqcloud.com/doc
hadoop fs -put ./xxx.txt ofs://f4mxxxxyyyy-zzzz.chdfs.ap-guangzhou.myqcloud.com/doc/
hadoop fs -get ofs://f4mxxxxyyyy-zzzz.chdfs.ap-guangzhou.myqcloud.com/exampleobject.txt
hadoop fs -rm ofs://f4mxxxxyyyy-zzzz.chdfs.ap-guangzhou.myqcloud.com/exampleobject.txt
```
2. MR Jobを使用して検証します。検証の前に、Yarn、Hiveなどの関連サービスを再起動する必要があります。


## よくあるご質問

#### Kerberosをインストールする必要がありますか。

内部でのみ使用されるクラスターなど、所在するクラスターでユーザーが信頼できる場合は、Kerberosをインストールして認証要件を満たすことができます。ユーザーが認証操作のみを行う場合、権限を有さないお客様による誤操作を避けるため、Kerberosをインストールせずにrangerのみを使用して認証を行うことができます。
Kerberosをインストールすると、パフォーマンスが低下します。ユーザーは、ご自分の総合的なセキュリティ要件とパフォーマンス要件を考慮してください。認証が必要な場合は、Kerberosを有効にした後、COS Ranger ServiceとCOS Ranger Clientの関連する項目を設定する必要があります。

#### Rangerが有効になっていても、Policyが何も設定されていない場合、またはいずれのPolicyにもマッチしていない場合、どのように操作すればいいですか。

いずれのpolicyにもマッチしない場合、この操作はデフォルトで拒否されます。

#### rangerを有効にした後、CHDFS端末はPOSIX認証を実行しますか。

Ranger認証はクライアント環境で実行されます。rangerによって認証されたリクエストはCHDFSサーバーに送信され、サーバーはデフォルトでPOSIX認証を実行します。そのため、権限がRanger端末で制御されている場合は、CHDFSコンソールでPOSIX権限をオフにしてください。
