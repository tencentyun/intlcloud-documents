## 概要

Kerberosはビッグデータエコシステムにおいて幅広く用いられている統一認証サービスです。GooseFSはビッグデータおよびデータレイクのシーンにおけるアクセラレーションストレージサービスとして、クラスターノードとユーザーアクセスのKerberos認証サービスとの統合をサポートしています。ここではGooseFSへのKerberos認証サービスの統合設定方法およびHadoop Delegation Token認証の使用方法について詳細にご説明します。

## GooseFSへのKerberos認証接続アーキテクチャ

![](https://qcloudimg.tencent-cloud.cn/raw/f3fa3d97e385d113faf053cb989edef7.png)

## GooseFS Kerberos認証のメリット

- HDFSとKerberosを接続する場合の認証アーキテクチャおよびフローと基本的には同じです。HDFS上でのKerberos認証有効化フローはGooseFSに容易に移行できます。
- HadoopのDelegation Token認証メカニズムをサポートしているため、Hadoopエコシステムの適用作業との間で良好な互換性を有します。

## GooseFSへのKerberos認証の接続設定

### 前提条件

- GooseFS 1.3.0およびそれ以降のバージョン。
- 環境内にすでにKerberos KDCサービスが存在し、かつGooseFSおよび適用するクライアントがKerberos KDCサービスの関連ポートに正常にアクセスできることを確認してください。

### Kerberos KDCにGooseFS関連のID情報を作成する

その後の接続設定に進む前に、まずKerberos KDCにGooseFSクラスターのServerとClientに関連するKerberos ID情報を作成する必要があります。ここでは**Kerberos KDCサーバー**上で、インタラクティブツール`kadmin.local`を利用して作成を行います。
>! `kadmin.local`ツールはroot/sudo権限で実行する必要があります。
>

```shell
$ sudo kadmin.local
```

実行に成功すると、kadminのインタラクティブshell環境に入ります。

```shell
Authenticating as principal root/admin@GOOSEFS.COM with password.
kadmin.local:  
```

このうち、`kadmin.local`はこのインタラクティブ実行環境のコマンドプロンプトを表します。

#### GooseFS Server / Clientに関連するID情報を作成する

以下で、簡単なテストクラスターとユースケースサンプルによって、Kerberosの設定プロセス全体についてご説明します。
1. クラスター環境の説明
1 Master+2 WorkerのStandaloneデプロイアーキテクチャを採用します。
 - Master(JobMaster): 172.16.0.1
 - Worker1(JobWorker1): 172.16.0.2
 - Worker2(JobWorker2): 172.16.0.3
 - Client: 172.16.0.4
2. `kadmin.local`にServerとClientのID認証関連情報を作成します。
```shell
kadmin.local: addprinc -randkey goosefs/172.16.0.1@GOOSEFS.COM
kadmin.local: addprinc -randkey client/172.16.0.4@GOOSEFS.COM
```
>! ここで`-randkey`オプションを使用する理由は、GooseFSがServerログインとClientログインの両方で`keytab`ファイル認証を使用し、平文のパスワードは使用しないためです。ID情報をpasswordログインに用いる必要がある場合は、このオプションを削除することができます。
>
3. 各IDに対応する`keytab`ファイルを生成してエクスポートします。
```shell
kadmin.local: xst -k goosefs_172_16_0_1.keytab goosefs/172.16.0.1@GOOSEFS.COM
kadmin.local: xst -k client_172_16_0_4.keytab client/172.16.0.4@GOOSEFS.COM
```

### Kerberos認証を使用してGooseFS Server/Clientへの接続を設定する

1. 上記でエクスポートした`keytab`ファイルを対応するマシン上に配信します。ここで推奨するパスは`${GOOSEFS_HOME}/conf/`です。
```shell
$ scp goosefs_172_16_0_1.keytab <username>@172.16.0.1:${GOOSEFS_HOME}/conf/
$ scp goosefs_172_16_0_1.keytab <username>@172.16.0.2:${GOOSEFS_HOME}/conf/
$ scp goosefs_172_16_0_1.keytab <username>@172.16.0.3:${GOOSEFS_HOME}/conf/
$ scp client_172_16_0_4.keytab <username>@172.16.0.4:${HOME}/.goosefs/
```
2. 対応するマシン上で、Server Principal KeyTabファイルの所属ユーザー/ユーザーグループをGooseFS Server起動時に使用するユーザーとユーザーグループに変更します（GooseFSが起動時に十分な権限によって読み取りを行えるようにするためです）。
```shell
$ chown <GooseFS_USER>:<GOOSEFS_USERGROUP> goosefs_172_16_0_1.keytab
$ # Unixのアクセスパーミッションビットを同時に変更します
$ chmod 0440 goosefs_172_16_0_1.keytab
```
3. ClientのKeyTabの所属ユーザー/ユーザーグループを、GooseFSリクエストを送信するクライアントアカウントに変更します。これも同様に、Clientにこのファイルを読み取るための十分な権限を保証することが目的です。
```shell
$ chown <client_user>:<client_usergroup> client_172_16_0_4.keytab
$ # Unixのアクセスパーミッションビットを同時に変更します
$ chmod 0440 client_172_16_0_4.keytab
```

#### ServerとClientのGooseFS設定

1. Master/Worker Serverのgoosefs-site.properties
```properties

# Security properties
# Kerberos properties
goosefs.security.authorization.permission.enabled=true
goosefs.security.authentication.type=KERBEROS
goosefs.security.kerberos.unified.instance.name=172.16.0.1
goosefs.security.kerberos.server.principal=goosefs/172.16.0.1@GOOSEFS.COM
goosefs.security.kerberos.server.keytab.file=${GOOSEFS_HOME}/conf/goosefs_172_16_0_1.keytab

```
GooseFS Serverの認証設定を完了した後、クラスター全体を再起動して設定を有効にします。
2. Clientのgoosefs-site.properties
```properties
# Security properties
# Kerberos properties
goosefs.security.authorization.permission.enabled=true
goosefs.security.authentication.type=KERBEROS
goosefs.security.kerberos.unified.instance.name=172.16.0.1
goosefs.security.kerberos.server.principal=goosefs/172.16.0.1@GOOSEFS.COM
goosefs.security.kerberos.client.principal=client/172.16.0.4@GOOSEFS.COM
goosefs.security.kerberos.client.keytab.file=${GOOSEFS_HOME}/conf/client_172_16_0_4.keytab

```
>! Client側でServerのprincipalを指定する必要があります。その理由は、Kerberos認証システムにおいて、KDCは現在ClientがアクセスしているServiceを知る必要があるためです。一方、GooseFSはServerのprincipalによってClientが現在リクエストしているServiceを判別します。
>

これでGooseFSへのKerberosの基本認証は完了です。これ以降、クライアントが送信したリクエストはすべてKerberosによってID認証が行われます。

