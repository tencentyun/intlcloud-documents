このドキュメントでは、Tencent Cloudを使用し始めたばかりの個人ユーザーのために、CentOSシステムでJava Webプロジェクトを配置する方法を紹介します。
## ソフトウェアバージョン
例のステップにおけるこのドキュメントのソフトウェアバージョンは以下のとおりですが、実際に操作する時は、実際のソフトウェアのバージョンを基準にしてください。
- オペレーティングシステム：CentOS 7.5
- Tomcatのバージョン：apache-tomcat-8.5.37
- JDKのバージョン：JDK 1.8.0_201

## JDKのインストール
購入完了後、CVMの詳細ページで【ログイン】をクリックするとCVMに直接ログインすることができます。自身のユーザー名とパスワードを入力した後、Java Web環境の構築が開始されます。CVMインスタンスの作成方法については、[CVMインスタンスの購入と起動](https://cloud.tencent.com/document/product/213/4855)を参照してください。
### JDKのダウンロードとコマンドの入力
```
mkdir /usr/java  # javaフォルダの作成
cd /usr/java     # javaフォルダに進む
# コマンド：wgetを使用してリンクを直接ダウンロードします。ダウンロードされた圧縮パッケージは解凍できません。これは直接ダウンロードされた圧縮パッケージがデフォルトでOracle BSDに許可されていないためです。各人のcookieは異なるため、https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.htmlページに進み使用許諾契約に同意し且つ自身のcookieを含むダウンロードリンクを取得してください（JDKインストール圧縮パッケージを直接ダウンロードし、インスタンスにアップロードすることもできます）。
wget --no-check-certificate --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie" https://download.oracle.com/otn-pub/java/jdk/8u201-b09/42970487e3af4f5aa5bca3f542482c60/jdk-8u201-linux-x64.tar.gz

# 解凍
chmod +x jdk-8u201-linux-x64.tar.gz
tar -xzvf jdk-8u201-linux-x64.tar.gz
```
### 環境変数の設定
1. /etc/profileを開きます。
```
vi /etc/profile
```
2. iキーを押して編集モードに入り、このファイルに以下の情報を追加します。
```
# set java environment
export JAVA_HOME=/usr/java/jdk1.8.0_201
export CLASSPATH=$JAVA_HOME/lib/tools.jar:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib
export PATH=$JAVA_HOME/bin:$PATH
```
3. Escを押して編集モードを終了し、:wqと入力して保存しファイルを閉じます。
4. 環境変数を読み込みます。
```
source /etc/profile
```
### JDKのインストールが成功したかどうかの確認
java-versionコマンドを実行してJDKバージョン情報を表示させると、JDKが正常にインストールされたことが表示されます。
![](https://main.qcloudimg.com/raw/42b10335d8bf6b38246bf2d853a7e08e.png)


## Tomcatのインストール
### Tomcatのダウンロードとコマンドの入力
```
# Tomcatのダウンロードと解凍
wget http://mirrors.shu.edu.cn/apache/tomcat/tomcat-8/v8.5.37/bin/apache-tomcat-8.5.37.tar.gz
tar -xzvf apache-tomcat-8.5.37.tar.gz
mv apache-tomcat-8.5.37 /usr/local/tomcat/
```
/usr/local/tomcat/ディレクトリにおいて、
bin：スクリプトファイルであり、Tomcatサービスの起動スクリプトと停止スクリプトが含まれています。
conf：様々なグローバル構成ファイルであり、そのうち最も重要なのはserver.xmlとweb.xmlです。
webapps：Tomcatの主なWeb公開ディレクトリであり、デフォルトではWebアプリケーションファイルをこのディレクトリに置きます。
logs：Tomcat実行時のログファイルを保存します。
### ユーザーの追加
```
# Tomcatを実行するための一般ユーザーwwwの作成
useradd www

# Webサイトルートディレクトリの作成
mkdir -p /data/wwwroot/default

# 配置する必要のあるJava WebプロジェクトファイルのWARパッケージをWebサイトのルートディレクトリにアップロードし、その後、Webサイトルートディレクトリにおけるファイルの権限をwwwに変更します。この例では、WebサイトのルートディレクトリにおいてTomcatのテストページを直接作成します。
試用
echo Hello Tomcat! > /data/wwwroot/default/index.jsp
chown -R www.www /data/wwwroot
```
### JVMメモリパラメータの設定
/usr/local/tomcat/bin/setenv.shを作成します
```
vi /usr/local/tomcat/bin/setenv.sh
```
 iキーを押して編集モードに入り、以下の情報を追加して保存します。
```
JAVA_OPTS='-Djava.security.egd=file:/dev/./urandom -server -Xms256m -Xmx496m -Dfile.encoding=UTF-8'
```

### server.xmlの構成
1. /usr/local/tomcat/conf/ディレクトリに切り替えます。
```
cd /usr/local/tomcat/conf/
```
2. server.xmlのバックアップを取ります。
```
mv server.xml server_default.xml
```
3. 新しいserver.xmlファイルを作成します。
```
vi server.xml
```
4. iキーを押して編集モードに入り、以下の情報を追加します。
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
5. Escキーを押して編集モードを終了し、:wqと入力して保存し編集を終了します。

## Tomcatの起動
###方法1
Tomcatサーバーのbinディレクトリに進み、その後、"./startup.sh"コマンドを実行してTomcatサーバーを起動します。
```
cd /usr/local/tomcat/bin
./startup.sh
```
![](https://main.qcloudimg.com/raw/c118899986968ecd5982eb8cdb2beff9.png)

###方法2
クイックスタートを設定すると、service tomcat startによりどこからでもTomcatを起動することができます
```
wget https://github.com/lj2007331/oneinstack/raw/master/init.d/Tomcat-init
mv Tomcat-init /etc/init.d/tomcat
chmod +x /etc/init.d/tomcat
```
以下のコマンドを実行し、起動スクリプトJAVA_HOMEを設定します
```
sed -i 's@^export JAVA_HOME=.*@export JAVA_HOME=/usr/java/jdk1.8.0_201@' /etc/init.d/tomcat
```
自動起動の設定
```
chkconfig --add tomcat
chkconfig tomcat on
```
Tomcatの起動
```
# Tomcatの起動
service tomcat start

# Tomcat実行状態の確認
service tomcat status

# Tomcatの終了
service tomcat stop
```
![](https://main.qcloudimg.com/raw/78800e85c09820d98a0a15dc2792aaa8.png)
権限がないと提示された場合、以下のとおり入力します
```
cd /usr/local
chmod -R 777 tomcat
```
ブラウザのアドレスバーにhttp://パブリックネットワークIP:ポート（ポートはserver.xmlで設定したconnector port）を入力してアクセスします。下図に示すページが現れたら、インストール完了です。
![](https://main.qcloudimg.com/raw/74ec003775915c33a61f7f2434d59a23.png)

### セキュリティグループの構成
アクセスに失敗した場合、セキュリティグループを確認してください。上記の例では、server.xml中のconnector portは8080なので、対応するCVMでバインディングされるセキュリティグループでTCP:8080を開放する必要があります。
![](https://main.qcloudimg.com/raw/8f6fcdade7dec6c1a80dbb9af3711796.png)

