ここではCentOSシステムにJava Webプロジェクトをデプロイする方法について詳細にご説明します。Tencent Cloudのご利用を開始したばかりの個人ユーザーの方向けの内容となります。
## ソフトウェアバージョン
ここで例に挙げる手順で使用するソフトウェアバージョンは次のとおりです。実際の操作の際は、お使いのソフトウェアバージョンに準じてください。
- OS：CentOS 7.5
- Tomcatバージョン：apache-tomcat-8.5.39
- JDKバージョン：JDK 1.8.0_201

## JDKのインストール
CLBサービスをご購入後、CVMの詳細ページで【ログイン】をクリックすると、CVMに直接ログインできます。ご自身のユーザー名とパスワードを入力すると、Java Web環境の構築を開始できます。CVMインスタンスの作成方法に関しては、[CVM-インスタンスの作成](https://intl.cloud.tencent.com/document/product/213/4855)をご参照ください。

### JDKのダウンロード
次のコマンドを入力します。
```
mkdir /usr/java  # javaフォルダを作成する
cd /usr/java     # javaフォルダに移動する
```
<pre>
<code># JDKインストールパッケージをアップロードする（推奨）
<a href="https://winscp.net/eng/docs/lang:chs" target="_blank">WinSCP</a>またはその他のツールを使用してJDKインストールパッケージを上記のjavaフォルダにアップロードすることを推奨します。その後、インストールパッケージを解凍します。
もしくは
# コマンドを直接使用する（JDKインストールパッケージをアップロードする方法を推奨します）： wgetダウンロードリンクからダウンロードした圧縮パッケージは解凍できません。直接ダウンロードした圧縮パッケージはOracle BSDライセンスをデフォルトで拒否するためです。ご自身のcookieに応じて、https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.htmlページでライセンス規約に同意し、ご自身のcookieが含まれるダウンロードリンクを取得してください。
wget --no-check-certificate --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie" https://download.oracle.com/otn-pub/java/jdk/8u201-b09/42970487e3af4f5aa5bca3f542482c60/jdk-8u201-linux-x64.tar.gz</code>
</pre>
```
# 解凍
chmod +x jdk-8u201-linux-x64.tar.gz
tar -xzvf jdk-8u201-linux-x64.tar.gz
```

### 環境変数の設定
1. `/etc/profile`ファイルを開きます。
```
vi /etc/profile
```
2. i キーを押して編集モードに進み、このファイルに次の情報を追加します。
```
# set java environment
export JAVA_HOME=/usr/java/jdk1.8.0_201
export CLASSPATH=$JAVA_HOME/lib/tools.jar:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib
export PATH=$JAVA_HOME/bin:$PATH
```
3. Escキーを押して編集モードを終了し、`:wq`を入力してファイルを閉じます。
4. 環境変数をロードします。
```
source /etc/profile
```

### JDKのインストール成否の確認
`java -version`コマンドを実行し、JDKのバージョン情報が表示されれば、JDKのインストールに成功しています。
![](https://main.qcloudimg.com/raw/6d3531f4d466e5428885ec38a3542c2e.png)

## Tomcatのインストール
### Tomcatのダウンロード
次のコマンドを入力します。
```
# ミラーアドレスは変更される場合があり、Tomcatのバージョンアップも継続的に行われます。ダウンロードリンクが無効になっている場合は、[Tomcat公式サイト](https://tomcat.apache.org/download-80.cgi)で適切なインストールパッケージアドレスを選択してください。
wget http://mirrors.tuna.tsinghua.edu.cn/apache/tomcat/tomcat-8/v8.5.39/bin/apache-tomcat-8.5.39.tar.gz
tar -xzvf apache-tomcat-8.5.39.tar.gz
mv apache-tomcat-8.5.39 /usr/local/tomcat/
```
`/usr/local/tomcat/`ディレクトリには次のファイルが含まれます。
- bin：スクリプトファイルです。Tomcatサービススクリプトの起動と終了が含まれます。
- conf：各種グローバル設定ファイルです。このうち最も重要なものはserver.xmlとweb.xmlです。
- webapps：Tomcatの主なWebリリースディレクトリです。デフォルトではWebアプリケーションファイルはこのディレクトリに保存されます。
- logs：Tomcat実行時のログファイルを保存します。

>!ダウンロードリンクが無効になっている場合は、[Tomcat公式サイト](https://tomcat.apache.org/download-80.cgi)の最新のダウンロードリンクに切り替えてください。

### ユーザーの追加
```
# 一般ユーザーwwwを追加してTomcatを実行
useradd www
# ウェブサイトルートディレクトリの作成
mkdir -p /data/wwwroot/default
# デプロイしたいJava WebプロジェクトファイルのWARパッケージをウェブサイトルートディレクトリ下にアップロードします。その後、ウェブサイトルートディレクトリ下のファイルの権限をwwwに変更します。この例ではウェブサイトルートディレクトリ下にTomcatテストページを直接新規作成します。
echo Hello Tomcat! > /data/wwwroot/default/index.jsp
chown -R www.www /data/wwwroot
```

### JVMメモリパラメータの設定
1. `/usr/local/tomcat/bin/setenv.sh`スクリプトファイルを作成します。
```
vi /usr/local/tomcat/bin/setenv.sh
```
2. i キーを押して編集モードに進み、次の内容を追加します。
```
JAVA_OPTS='-Djava.security.egd=file:/dev/./urandom -server -Xms256m -Xmx496m -Dfile.encoding=UTF-8'
```
3. Escキーを押して編集モードを終了し、`:wq`を入力して保存し、編集を終了します。

### server.xmlの設定
1. `/usr/local/tomcat/conf/`ディレクトリに切り替えます。
```
cd /usr/local/tomcat/conf/
```
2. server.xmlファイルをバックアップします。
```
mv server.xml server_default.xml
```
3. 新しいserver.xmlファイルを作成します。
```
vi server.xml
```
4. i キーを押して編集モードに進み、次の内容を追加します。
```
<?xml version="1.0" encoding="UTF-8"?>
<Server port="8006" shutdown="SHUTDOWN">
<Listener className="org.apache.catalina.core.JreMemoryLeakPreventionListener"/>
<Listener className="org.apache.catalina.mbeans.GlobalResourcesLifecycleListener"/>
<Listener className="org.apache.catalina.core.ThreadLocalLeakPreventionListener"/>
<Listener className="org.apache.catalina.core.AprLifecycleListener"/>
<GlobalNamingResources>
<Resource name="UserDatabase" auth="Container"
 type="org.apache.catalina.UserDatabase"
 description="User database that can be updated and saved"
 factory="org.apache.catalina.users.MemoryUserDatabaseFactory"
 pathname="conf/tomcat-users.xml"/>
</GlobalNamingResources>
<Service name="Catalina">
<Connector port="8080"
 protocol="HTTP/1.1"
 connectionTimeout="20000"
 redirectPort="8443"
 maxThreads="1000"
 minSpareThreads="20"
 acceptCount="1000"
 maxHttpHeaderSize="65536"
 debug="0"
 disableUploadTimeout="true"
 useBodyEncodingForURI="true"
 enableLookups="false"
 URIEncoding="UTF-8"/>
<Engine name="Catalina" defaultHost="localhost">
<Realm className="org.apache.catalina.realm.LockOutRealm">
<Realm className="org.apache.catalina.realm.UserDatabaseRealm"
  resourceName="UserDatabase"/>
</Realm>
<Host name="localhost" appBase="/data/wwwroot/default" unpackWARs="true" autoDeploy="true">
<Context path="" docBase="/data/wwwroot/default" debug="0" reloadable="false" crossContext="true"/>
<Valve className="org.apache.catalina.valves.AccessLogValve" directory="logs"
prefix="localhost_access_log." suffix=".txt" pattern="%h %l %u %t &quot;%r&quot; %s %b" />
</Host>
</Engine>
</Service>
</Server>
```
5. Escキーを押して編集モードを終了し、`:wq`を入力して保存し、編集を終了します。

## Tomcatの起動
### 方法1
Tomcatサーバーのbinディレクトリに進み、`./startup.sh`コマンドを実行してTomcatサーバーを起動します。
```
cd /usr/local/tomcat/bin
./startup.sh
```
実行結果は次のとおりです。
![](https://main.qcloudimg.com/raw/c118899986968ecd5982eb8cdb2beff9.png)
### 方法2
1. クイックスタートを設定すると、service tomcat startによってどこででもTomcatを起動することができます。
```
wget https://github.com/lj2007331/oneinstack/raw/master/init.d/Tomcat-init
mv Tomcat-init /etc/init.d/tomcat
chmod +x /etc/init.d/tomcat
```
2. 次のコマンドを実行し、起動スクリプトJAVA_HOMEを設定します。
```
sed -i 's@^export JAVA_HOME=.*@export JAVA_HOME=/usr/java/jdk1.8.0_201@' /etc/init.d/tomcat
```
3. 自動起動を設定します。
```
chkconfig --add tomcat
chkconfig tomcat on
```
4. Tomcatを起動します。
```
# Tomcatの起動
service tomcat start
# Tomcatの実行ステータスの確認
service tomcat status
# Tomcatの終了
service tomcat stop
```
実行結果は次のとおりです。
![](https://main.qcloudimg.com/raw/78800e85c09820d98a0a15dc2792aaa8.png)
5. 権限がないと表示された場合は、rootユーザーに切り替えて権限の変更を行ってください。
```
cd /usr/local
chmod -R 777 tomcat
```
6. ブラウザのアドレスバーに`http://パブリックIP:ポート`（ポートはserver.xmlで設定したconnector portです）を入力してアクセスします。以下のページが表示された場合、インストールは成功です。
![](https://main.qcloudimg.com/raw/a8d7c77aafc94c9bba262c06125b6c18.png)

### セキュリティグループの設定
アクセスできない場合は、セキュリティグループをチェックしてください。上の例ではserver.xmlのconnector portが8080なので、対応するCVMにバインドしたセキュリティグループ上でTCP:8080を許可する必要があります。
![](https://main.qcloudimg.com/raw/6ffabfd2ef027e4fc69e4fc1a85dde9f.png)
