
## 背景

Hadoop Ranger権限システムは、ビッグデータのシーンにおける権限ソリューションです。ユーザーはストレージ・コンピューティング分離を使用した後、Cloud Object Storage（COS）でデータをホストします。COSが使用するのはTencent CloudのCloud Access Management（CAM）権限システムで、ユーザーのID、権限ポリシーなどにかかわらず、ローカルのHadoop Rangerシステムと異なります。クライアントが使用している習慣を維持するため、 COSのRangerアクセスソリューションを提供します。


## メリット

- 細かい粒度の権限制御、Hadoop権限ロジックとの互換性によって、ユーザーはビッグデータコンポーネントとクラウド側のホスティング・ストレージの権限を一元管理できます。
- プラグイン側がcore-siteでキーを設定する必要がありません。キーはすべてCOS Ranger Serviceで設定されるため、平文キーの漏洩を防ぐことができます。


## ソリューションアーキテクチャ

![](https://main.qcloudimg.com/raw/47bcff91b29614141b9c88efd39e50c1.png)

Hadoop権限システムでは、認証はKerberosによって提供され、権限承認と認証はRangerが担当します。これをベースとして、以下のコンポーネントを提供し、COSのRanger権限スキームをサポートします。


1. COS Ranger Plugin：Rangerサーバー用のサービス定義プラグインを提供します。権限の種類、必要なパラメータ定義（例えばCOSのbucketパラメータとregionパラメータ）を含む、Ranger側のCOSサービスの説明が提供されます。プラグインがデプロイされると、ユーザーはRangerの制御ページで対応する権限ポリシーを入力できるようになります。
2. COS Ranger Service：このサービスは、Rangerのクライアントを統合し、Rangerサーバーから権限ポリシーを定期的に同期し、クライアントの認証リクエストを受信した後、ローカルで権限チェックを行います。同時に、HadoopでのDelegationTokenの発行や更新などのインターフェースを提供します。すべてのインターフェースは、Hadoop IPCを介して定義されます。
3. COS Ranger Client：COSNプラグインはそれを動的にロードし、権限チェックのリクエストをCOS Ranger Serviceに転送します。

## デプロイ環境

- Hadoop環境。
- ZooKeeper、Ranger、Kerberosサービス（認証の必要がある場合は、デプロイします）。
>? 以上のサービスは成熟したオープンソースコンポーネントであるため、お客様はご自身でインストールすることができます。
>

## コンポーネントのデプロイ
コンポーネントのデプロイは、CHDFS Ranger Plugin、COS Ranger Service、COS Ranger Client、COSNに従って、順番に行ってください。
<dx-tabs>
::: COS Ranger Pluginのデプロイ
COS-Ranger-Pluginは、Ranger Adminコンソールにおけるサービスの種類を拡張します。ユーザーはRangerコンソールで、COSに関連する操作権限を設定することができます。


#### コードアドレス
[Github](https://github.com/tencentyun/cos-ranger-service)のranger-pluginディレクトリから取得できます。
#### バージョン
V1.0およびそれ以降のバージョン。
#### デプロイ手順
1. Rangerのサービス定義ディレクトリの下にCOSディレクトリを新規作成します（注意：ディレクトリの権限には、少なくともxとrの権限が必要です）。
a. Tencent CloudのEMR環境の場合、パスはranger/ews/webapp/WEB-INF/classes/ranger-pluginsです。
b. セルフビルドのhadoop環境では、rangerディレクトリ下でhdfsなどのrangerサービスに接続されているコンポーネントを探し、ディレクトリの場所を見つけることができます。
![](https://main.qcloudimg.com/raw/793f47a53343657a000b34b7ac66b074.png)
2. COSのディレクトリ下で、cos-chdfs-ranger-plugin-xxx.jarを追加します。（注意：jarパッケージには、少なくともrの権限が必要です）。同時に、cos-ranger.jsonファイルを追加する必要があるため、 [Github](https://github.com/tencentyun/cos-ranger-service/tree/main/ranger-plugin)に移動して取得してください。
3. Rangerサービスを再起動します。
4. RangerにCOS Serviceを登録します。次のコマンドを参照できます。
<dx-codeblock>
:::  plaintext
##サービスを発行するには、Ranger管理者アカウントのパスワードとRangerサービスのアドレスを渡す必要があります。
##Tencent Cloud EMRクラスターの場合、管理者ユーザーはrootであり、パスワードはemrクラスターの構築時に設定されたrootパスワードです。rangerサービスのIPは、EMRのmasterノードのIPに置き換えられます。
adminUser=root
##EMRクラスターを構築した際に設定したパスワードです。また、rangerサービスのwebページのログインパスワードでもあります。
adminPasswd=xxxxxx
##rangerサービスに複数のmasterノードがある場合は、任意のmasterを選択してください。
rangerServerAddr=10.0.0.1:6080
##コマンドラインの-dでステップ2のjsonファイルを指定します。
curl -v -u${adminUser}:${adminPasswd} -X POST -H "Accept:application/json" -H "Content-Type:application/json" -d @./cos-ranger.json http://${rangerServerAddr}/service/plugins/definitions
##定義されたサービスを削除する場合は、作成されたばかりのサービスが渡され、サービスIDが返されます
serviceId=102
curl -v -u${adminUser}:${adminPasswd} -X DELETE -H "Accept:application/json" -H "Content-Type:application/json" http://${rangerServerAddr}/service/plugins/definitions/${serviceId}
:::
</dx-codeblock>
5. 次に示すように、サービスの作成に成功すると、RangerコンソールにCOSサービスが表示されます。
![](https://main.qcloudimg.com/raw/d1a6e2722d11f7177636a5e2c54226e3.png)
6. COSサービス側の<b>+</b>をクリックして、新しいサービスインスタンスを定義します。サービスインスタンス名は、`cos`や`cos_test`などにカスタマイズできます。サービスの設定は次のとおりです。
![](https://main.qcloudimg.com/raw/2be86fb2b8232b16679b29e908f82d3a.png)
そのなかでpolicy.grantrevoke.auth.usersは、COS Ranger Serviceを後で起動するためのユーザー名（つまり権限ポリシーの取得を許可するユーザー）を設定する必要があります。通常はhadoopに設定することをお勧めします。その後のCOS Ranger Serviceは、このユーザー名で起動できます。
7. 新しく生成されたCOSサービスインスタンスをクリックします。
![](https://qcloudimg.tencent-cloud.cn/raw/bc48921e23571e81367b1c3aa8ca52a8.png)
次に示すように、policyを追加します。
![](https://main.qcloudimg.com/raw/58ded7125d5c5d161ca6e2f5a98d8e7b.png)
8. ジャンプインターフェースで、以下のパラメータを設定します。説明は次のとおりです。
 - **bucket**：バケット名、例えばexamplebucket-1250000000は、[COSコンソール](https://console.cloud.tencent.com/cos5/bucket)にログインし、確認することができます。
 - **path**：COSオブジェクトパスです。COSのオブジェクトパスは、/で開始することができないので、ご注意ください
    - include：設定された権限がpath自体またはpath以外の他のパスに適用されることを示します。
    - recursive：権限がpathだけでなく、path下のサブメンバー（つまり、再帰的なサブメンバー）にも適用できることを示します。通常、pathがディレクトリに設定されている場合に用いられます。
 - **user/group**：ユーザー名とユーザーグループ。ここでは「OR」関係です。ユーザー名またはユーザーグループがそれらのうちいずれかを満たす場合、対応する操作権限を有することができます。
 - **Permissions**:
    -  Read：読み取り操作。オブジェクトのダウンロード、オブジェクトメタデータの照会など、Cloud Object StorageでのGET、HEADといった操作に対応します。
    -  Write：書き込み操作。オブジェクトのアップロードなど、COS内のPUTといった変更操作に対応します。
    -  Delete：削除操作。COS内のObjectの削除に対応します。HadoopのRename操作の場合、元のパスに対する削除操作権限と、新しいパスに対する書き込み操作権限が必要です。
    -  List：トラバース権限。COS内のList Objectに対応します。
![](https://main.qcloudimg.com/raw/00a619b4b963a9acf766411fad722fe4.png)
:::
::: COS Ranger Serviceのデプロイ
COS Ranger Serviceは、権限システム全体のコアであり、rangerクライアントの統合、ranger client認証リクエストの受信、token発行・更新のリクエストや一時キー発行リクエストを担当します。同時に、センシティブ情報（Tencent Cloudのキー情報）が配置されているエリアでもあり、通常はBastion Hostにデプロイされ、クラスター管理者のみが操作や設定の確認などを行うことができます。

COS Ranger Serviceは、1つの本番データベースと1つ以上のスタンバイによるHAデプロイをサポートし、DelegationTokenのステータスはHDFSに永続化されます。ZKを介してロックを取得することにより、Leaderの身分を決定します。Leaderの身分を取得するサービスは、COS Ranger Clientがルーティング・アドレッシングを実行できるように、アドレスをZKに書き込みます。

#### コードアドレス
[Github](https://github.com/tencentyun/cos-ranger-service)のcos-ranger-serverディレクトリ下から取得できます。

#### バージョン
V5.1.2およびそれ以降のバージョン。

#### デプロイ手順
1. COS Ranger Serviceサービスコードをクラスター内の複数のマシンにコピーします。本番環境は、少なくとも2台のマシン（1台は本番データベースでもう1台はスタンバイ）にすることをお勧めします。センシティブ情報が含まれるため、踏み台サーバーまたは厳格に制御されているマシンにすることをお勧めします。
2. cos-ranger.xmlファイルの関連設定を変更します。そのなかで必ず変更が必要な設定項目は、次のとおりです。設定項目の説明については、ファイルのコメントの説明（ファイルの設定は[Github](https://github.com/tencentyun/cos-ranger-service)のcos-ranger-service/confに進みディレクトリ下で取得します）をご参照ください。
 -  qcloud.object.storage.rpc.address
 -  qcloud.object.storage.status.port
 -  qcloud.object.storage.enable.cos.ranger
 -  qcloud.object.storage.zk.address （zkアドレスは、cos ranger serviceを起動し、zkで登録します）
 -  qcloud.object.storage.cos.secret.id
 -  qcloud.object.storage.cos.secret.key
3. ranger-cos-security.xmlファイルの関連設定を変更します。そのなかで必ず変更が必要な設定項目は、次のとおりです。設定項目の説明については、ファイルのコメントの説明（ファイルの設定は[Github](https://github.com/tencentyun/cos-ranger-service)のcos-ranger-service/confに進みディレクトリ下で取得します）をご参照ください。
 -  ranger.plugin.cos.policy.cache.dir
 -  ranger.plugin.cos.policy.rest.url
 -  ranger.plugin.cos.service.name
4. start_rpc_server.shのhadoop_conf_pathとjava.library.pathの設定を変更します。これら2つの設定はそれぞれ、hadoop設定ファイルが配置されているディレクトリ（core-site.xml、hdfs-site.xmlなど）とhadoop native libパスを指します。
5. 次のコマンドを実行して、サービスを起動します。
```
chmod +x start_rpc_server.sh
nohup ./start_rpc_server.sh &> nohup.txt &
```
6. 起動に失敗した場合は、log下のerrorログをチェックして、エラー情報があるかどうかを確認します。
7. COS Ranger Serviceは、HTTPポートステータスの表示をサポートします（ポート名はqcloud.object.storage.status.portで、デフォルト値は9998です）。ユーザーは次のコマンドを使用して、ステータス情報（leader、認証数の統計などを含むかどうか）を取得できます。
```
# 以下の10.xx.xx.xxxをranger serviceがデプロイされているマシンのIPに置き換えてください
# port 9998はqcloud.object.storage.status.port設定値に設定されます
curl -v http://10.xx.xx.xxx:9998/status
```
 - 1つのcos ranger serviceノードのみをデプロイする場合は、上記のインターフェースレスポンスで現在のノードがleaderになったことを確認できます。
 - 複数のcos ranger serviceをデプロイする場合は、上記のインターフェースレスポンスでその他のノードがleaderになったことを確認できます。すべてのノードの再起動が完了すると、最も早く再起動が完了したノードがleaderになったことを確認できます。

:::
::: COS Ranger Clientのデプロイ
COS Ranger Clientは、hadoop cosnプラグインによって動的にロードされ、COS Ranger Serviceにアクセスするための関連するリクエストを代行します。例えば、一時キーの取得、tokenの取得、認証操作などです。

#### コードアドレス

[Github](https://github.com/tencentyun/cos-ranger-service)のcos-ranger-clientおよびcosn-ranger-interfaceディレクトリ下から取得できます。

#### バージョン

cos-ranger-clientは、V5.0およびそれ以降のバージョンを要求されます。  
cosn-ranger-interfaceは、v1.0.4およびそれ以降のバージョンを要求されます。

#### デプロイ方法
1. cos-ranger-client jarパッケージとcosn-ranger-interface jarパッケージをCOSNと同一のディレクトリ下にコピーします。通常は/usr/local/service/hadoop/share/hadoop/common/lib/ディレクトリ下です。自身のhadoopサイズのバージョンと一致するjarパッケージを選択し、コピーしてください。最後に、jarパッケージに読み取り権限があることを確認してください。
2. core-site.xmlに次の設定項目を追加します。
<dx-codeblock>
::: xml
```
<configuration>
           <!--*****設定必須********-->
           <!-- 前のステップでデプロイしたcos ranger serverのアドレス -->
           <property>
               <name>qcloud.object.storage.ranger.service.address</name>
               <value>10.0.0.8:9999,10.0.0.10:9999</value>
           </property>

           <!--***オプション設定****-->           
           <!-- cos ranger service端末で使用されるkerberos認証情報を設定します。cos ranger service端末の設定をご参照ください。必ず一致を維持する必要があります。認証要件がない場合、設定は必要ありません -->
           <property>                
					 <name>qcloud.object.storage.kerberos.principal</name>
					 <value>hadoop/_HOST@EMR-XXXX</value>
           </property>

         <!--***オプション設定****-->  
         <!-- zkに記録されたranger serverのIPアドレスパスです。ここではデフォルト値が使用され、設定は必ずCOS Ranger Serviceの設定と一致する必要があります -->
          <property>              
					<name>qcloud.object.storage.zk.leader.ip.path</name> 
					<value>/ranger_qcloud_object_storage_leader_ip</value>
          </property>
         <!-- zkに記録されたcos ranger service followerのIPアドレスパスです。ここではデフォルト値が使用され、必ずCOS Ranger Serviceの設定と一致する必要があります。マスターとスタンバイノードが同時にサービスを提供します -->
          <property>
                    <name>qcloud.object.storage.zk.follower.ip.path</name>
                    <value>/ranger_qcloud_object_storage_follower_ip</value>
          </property>
</configuration>
```
:::
</dx-codeblock>
:::
::: COSNのデプロイ
#### バージョン
V8.0.1およびそれ以降のバージョン。

####  デプロイ方式
COSNプラグインのデプロイ方法は [Hadoopツール](https://intl.cloud.tencent.com/document/product/436/6884)ドキュメントをご参照ください。ただし、次のいくつかの点にご注意ください。

1. rangerを使用した後、fs.cosn.userinfo.secretIdおよび fs.cosn.userinfo.secretKeyキー情報を設定する必要はありません。COSNプラグインに続いて、COSRangerServiceから一時キーを取得します。
2. fs.cosn.credentials.providerは、 org.apache.hadoop.fs.auth.RangerCredentialsProviderに設定することで、次に示すとおり、 Rangerから認証を行うことができます。
<dx-codeblock>
:::  plaintext 
```
<property>
         <name>fs.cosn.credentials.provider</name>
         <value>org.apache.hadoop.fs.auth.RangerCredentialsProvider</value>
</property>
```
:::
</dx-codeblock>
:::
</dx-tabs>


## 検証

1. hadoop cmdを使用してCOSNへのアクセスに関連する操作を実行します。現在ユーザーが実行した操作が、ルートアカウントの権限設定予想に適合しているかどうかを確認します。以下に例を示します。
```plaintext
#bucket、パスなどをルートアカウントの実際の情報に置き換えます。
hadoop fs -ls cosn://examplebucket-1250000000/doc
hadoop fs -put ./xxx.txt cosn://examplebucket-1250000000/doc/
hadoop fs -get cosn://examplebucket-1250000000/doc/exampleobject.txt
hadoop fs -rm cosn://examplebucket-1250000000/doc/exampleobject.txt
```
2. MR Jobを使用して検証します。検証の前に、Yarn、Hiveなどの関連サービスを再起動する必要があります。


## よくあるご質問

#### Kerberosをインストールする必要がありますか。
Kerberosは、内部でのみ使用するクラスターのように、存在するクラスターやユーザーがすべて信頼できる場合、認証のニーズを満たします。ユーザーが認証操作のみを行う場合は、権限のないクライアントが誤った操作を行うのを回避するため、Kerberosをインストールせず、rangerのみを使用して認証を行うことができます。また、Kerberosはパフォーマンスを低下させます。クライアントは、自身のセキュリティへのニーズとパフォーマンスへのニーズを総合的に考慮してください。認証が必要な場合は、Kerberosを有効にした後、COS Ranger ServiceおよびCOS Ranger Clientの関連する項目を設定する必要があります。
#### Rangerが有効になっていても、Policyが何も設定されていない場合、またはいずれのPolicyにもマッチしていない場合、どのように操作すればいいですか。
いずれのpolicyにもマッチしない場合、この操作はデフォルトで拒否されます。
#### COS Ranger Serviceを設定する側のキーは、サブアカウントでも可能ですか。
サブアカウントでも可能です。ただし、操作されたbucketに対応する権限を所有していることが必要で、それにより一時キーを発行してCOSNプラグインに渡し、対応する操作ができるようになります。通常はここで設定したキーが、このbucketの所有権限をもつことをお勧めしています。
#### 一時キーはどのように更新すればよいですか。COSにアクセスする前に、COS Ranger Serviceから都度取得する必要がありますか。
一時キーは、COSNプラグイン側でcacheされ、定期的に非同期で更新されます。
#### rangerページで変更したPolicyが有効化されない場合は、どのようにすればよいですか。
ranger-cos-security.xmlドキュメントの設定項目を変更してください。ranger.plugin.cos.policy.pollIntervalMsは、この設定項目を小さくしてから（単位はミリ秒）、COS Ranger Serviceサービスを再起動します。Policyに関するテストが完了した後は、元の値に戻すことをお勧めします（時間間隔が短すぎるとポーリング頻度が高くなり、CPU使用率が高止まりします）。
