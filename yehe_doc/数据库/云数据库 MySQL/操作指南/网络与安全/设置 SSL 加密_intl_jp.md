## SSL暗号化の概要
SSL（Secure Sockets Layer）認証は、クライアントからクラウドデータベースサーバー側への認証であり、ユーザーとサーバーに対して認証を行います。SSL暗号化をオンにすると、CA証明書を取得し、CA証明書をサーバーにアップロードすることができます。クライアントがデータベースにアクセスすると、 SSLプロトコルがアクティブ化され、クライアントとデータベースサーバーとの間にSSLセキュリティチャネルが確立されます。データ情報の暗号化送信が実現されるため、送信過程においてデータがキャプチャ、改ざん、盗聴されるのを防止し、双方におけるデータ転送の安全性を保証します。

SSLプロトコルは、信頼性の高いトランスポート層プロトコル（TCP）上に構築することが要求されます。その優位性は、それがアプリケーション層プロトコルに依存しておらず、上位のアプリケーション層プロトコル（例えば、HTTP、FTP、TELNETなど）が、SSLプロトコル上に透過的に構築できるということです。SSLプロトコルは、アプリケーション層プロトコル通信の前に、暗号化アルゴリズム、通信キーのネゴシエーション、サーバーの認証作業をすでに完了させているため、その後にアプリケーション層プロトコルから伝送されるデータはすべて暗号化され、それによって通信のプライバシーが保証されます。

## 背景
非暗号化方式を使用してデータベースに接続した場合は、ネットワークにおいて伝送されるすべての情報は平文となるため、不正なユーザーによる盗聴、改ざん、なりすましの3つのリスクがあります。SSLプロトコルは、この3つのリスクに対処するために設計されており、理論上次のことを実現できます：
- 情報は暗号化されて送信されます。サードパーティが盗聴することはできません。
- 検証メカニズムがあり、一度改ざんされると、通信をしている双方がすぐに発見することができます。
- 身分証明書を装備しており、IDのなりすましを防止しています。

TencentDB for MySQLはSSL暗号化の有効化によるリンクセキュリティの強化も、必要なアプリケーションサービスへのSSL CA証明書のダウンロードとインストールもサポートします。
>!SSL暗号化はデータ自体を保護するのではなく、データベースとサーバー間のトラフィックの安全性を確保します。トランスポート層でネットワーク接続を暗号化することで、通信データの安全性と完全性を高めるが、同時にネットワーク接続の応答時間を長くすることができます。

##  前提条件
- インスタンスバージョンが、MySQL 5.6/5.7/8.0であること。
- インスタンスアーキテクチャが、2ノード/3ノードであること。
- インスタンスエンジンが、InooDB/RocksDBであること。

## SSL暗号化をオンにする
1. [MySQLコンソール](https://console.cloud.tencent.com/cdb/instance)にログインし、インスタンスリストでインスタンスIDまたは操作列の**管理**をクリックして、インスタンス管理ページに進みます。
2. インスタンス管理ページの**データセキュリティ**のページで、**SSL**ページを選択します。
![](https://qcloudimg.tencent-cloud.cn/raw/a87ff1d0edd454e3685c0b33eada0e39.png)
3. この機能は、ステータスがデフォルトでは有効化されていません。スイッチをオンにしてから**OK**をクリックし、SSL暗号化をオンにします。
 - マスターインスタンスをオンにするSSLウィンドウは次のとおりです：
 ![](https://qcloudimg.tencent-cloud.cn/raw/4061d5b39e786248761915c8e6982b47.png)
>!SSLをオンにするプロセスで、SSL証明書のロードのため、データベースインスタンスが再起動されますので、業務に再接続のメカニズムがあることを確認してください。
>
 - ROインスタンスを起動するSSLインターフェースは次のとおりです：
![](https://qcloudimg.tencent-cloud.cn/raw/461f76f6fe377c26e36b0c4d4b2c42f4.png)
>!ROインスタンスSSL機能の設定から、所属するROグループのその他のROインスタンスを同期設定することができます。
>
4. **ダウンロード**をクリックし、SSL CA証明書をダウンロードしてください。
ダウンロードされたファイルは圧縮パッケージ（TencentDB-CA-Chain.zip）で、次の3つのファイルを含みます：
 - p7bファイル：WindowsシステムでCA証明書をインポートするために使用します。
 - jksファイル：Javaのtruststore証明書ストレージファイルで、パスワードがtencentdbに統一されています。JavaプログラムにCA証明書チェーンをインポートするために使用します。
 - pemファイル：その他のシステムまたはアプリケーションにCA証明書をインポートするために使用します。

## SSL CA証明書の設定
SSL暗号化をオンにし、クライアントを使用してクラウドデータベースに接続する場合は、SSL CA証明書を設定する必要があります。以下でNavicatを例に、SSL CA証明書のインストール方法を説明します。その他のアプリケーションまたはクライアントについては、対応する製品の使用説明をご参照ください。
>?TencentDB for MySQLのSSL暗号化が有効または無効になるたびに、その証明書が新しく生成されます。
>
1. Navicatを開きます。
2. 対応するデータベースでマウスを右クリックし、**接続の編集**をクリックします。
3. SSLタブビューを選択し、.pem形式のCA証明書のパスを選択します。下図の設定が完了したら、**OK**をクリックします。
>?connection is being usedエラーが発生した場合は、以前のセッションが切断されていない可能性があるので、Navicatを閉じてから、もう一度お試しください。
>
4. 対応するデータベースをダブルクリックして、正常に接続できているかをテストします。

## SSL暗号化をオフにする
1. [MySQLコンソール](https://console.cloud.tencent.com/cdb/instance)にログインし、インスタンスリストでインスタンスIDまたは操作列の**管理**をクリックして、インスタンス管理ページに進みます。
2. インスタンス管理ページの**データセキュリティ**のページで、**SSL**ページを選択します。
3. すでに有効化してあるスイッチボタンをクリックし、ポップアップしたダイアログボックスで、**OK**をクリックします。
![](https://qcloudimg.tencent-cloud.cn/raw/5e6f6976d9e97ed01e37a5e722a33c1a.png)
>?SSLをオフにするプロセスで、SSL証明書がアンインストールされたため、データベースインスタンスが再起動されますので、業務に再接続のメカニズムがあることを確認してください。

## SSL接続暗号化のインスタンスをオンにして接続
SSL接続暗号化方式を使用したデータベースSQLへの接続は次のとおりです：
```
mysql -P <ポート番号> -h <IPアドレス>  -u <ユーザー名> -p<パスワード> --ssl-ca<ca証明書>
```

## SSL有効化インスタンスに接続するために一般的に使用されるプログラムのコードサンプル
- PHP
```
$conn = mysqli_init();
mysqli_ssl_set($conn,NULL,NULL, "<ダウンロードした証明書のパス>", NULL, NULL);
mysqli_real_connect($conn, '<データベースアクセスアドレス>', '<データベースアクセスユーザー名>', '<データベースアクセスパスワード>', '<指定アクセスデータベース>', <アクセスポート>, MYSQLI_CLIENT_SSL);
if (mysqli_connect_errno($conn)) {
die('Failed to connect to MySQL: '.mysqli_connect_error());
}
```
- PHP (Using PDO)
```
$options = array(
    PDO::MYSQL_ATTR_SSL_CA => '<ダウンロードした証明書のパス>’
);
$db = new PDO('mysql:host=<データベースアクセスアドレス>;port=<アクセスポート>;dbname=<指定アクセスデータベース>', '<データベースアクセスユーザー名>', '<データベースアクセスパスワード>', $options);
```
- Java (MySQL Connector for Java)
```
# generate truststore and keystore in code

String importCert = " -import "+
    " -alias mysqlServerCACert "+
    " -file " + ssl_ca +
    " -keystore truststore "+
    " -trustcacerts " +
    " -storepass password -noprompt ";
String genKey = " -genkey -keyalg rsa " +
    " -alias mysqlClientCertificate -keystore keystore " +
    " -storepass password123 -keypass password " +
    " -dname CN=MS ";
sun.security.tools.keytool.Main.main(importCert.trim().split("\\s+"));
sun.security.tools.keytool.Main.main(genKey.trim().split("\\s+"));

# use the generated keystore and truststore

System.setProperty("javax.net.ssl.keyStore","<ダウンロードした証明書のパス>");
System.setProperty("javax.net.ssl.keyStorePassword","tencentdb");
System.setProperty("javax.net.ssl.trustStore","<ダウンロードした証明書のパス>");
System.setProperty("javax.net.ssl.trustStorePassword","tencentdb");

url = String.format("jdbc:mysql://%s/%s?serverTimezone=UTC&useSSL=true", '<データベースアクセスアドレス>', '<指定アクセスデータベース>');
properties.setProperty("user", '<データベースアクセスユーザー名>');
properties.setProperty("password", '<データベースアクセスパスワード>');
conn = DriverManager.getConnection(url, properties);
```
- .NET (MySqlConnector)
```
var builder = new MySqlConnectionStringBuilder
{
    Server = "<データベースアクセスアドレス>",
    UserID = "<データベースアクセスユーザー名>",
    Password = "<データベースアクセスパスワード>",
    Database = "<指定アクセスデータベース>",
    SslMode = MySqlSslMode.VerifyCA,
    SslCa = "<ダウンロードした証明書>",
};
using (var connection = new MySqlConnection(builder.ConnectionString))
{
    connection.Open();
}
```
- Python (MySQLConnector Python)
```
try:
    conn = mysql.connector.connect(user='<データベースアクセスユーザー名>',
                                   password='<データベースアクセスパスワード>',
                                   database='<指定アクセスデータベース>',
                                   host='<データベースアクセスアドレス>',
                                   ssl_ca='<ダウンロードした証明書のパス>')
except mysql.connector.Error as err:
    print(err)
```

- Python (PyMySQL)
```
conn = pymysql.connect(user='<データベースアクセスユーザー名>',
                       password='<データベースアクセスパスワード>',
                       database='<指定アクセスデータベース>',
                       host='<データベースアクセスアドレス>',
                       ssl={'ca': '<ダウンロードした証明書のパス>'})
```

- Django (PyMySQL)
```
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': '<指定アクセスデータベース>',
        'USER': '<データベースアクセスユーザー名>',
        'PASSWORD': '<データベースアクセスパスワード>',
        'HOST': '<データベースアクセスアドレス>',
        'PORT': '<アクセスポート>',
        'OPTIONS': {
            'ssl': {'ca': '<ダウンロードした証明書のパス>'}
        }
    }
}
```
- Node.js
```
var fs = require('fs');
var mysql = require('mysql');
const serverCa = [fs.readFileSync("<ダウンロードした証明書のパス>", "utf8")];
var conn=mysql.createConnection({
    host:"<データベースアクセスアドレス>",
    user:"<データベースアクセスユーザー名>",
    password:"<データベースアクセスパスワード>",
    database:"<指定アクセスデータベース>",
    port:<アクセスポート>,
    ssl: {
        rejectUnauthorized: true,
        ca: serverCa
    }
});
conn.connect(function(err) {
  if (err) throw err;
});
```
- Golang
```
rootCertPool := x509.NewCertPool()
pem, _ := ioutil.ReadFile("<ダウンロードした証明書のパス>")
if ok := rootCertPool.AppendCertsFromPEM(pem); !ok {
    log.Fatal("Failed to append PEM.")
}
mysql.RegisterTLSConfig("custom", &tls.Config{RootCAs: rootCertPool})
var connectionString string
connectionString = fmt.Sprintf("%s:%s@tcp(%s:<アクセスポート>)/%s?allowNativePasswords=true&tls=custom","<データベースアクセスユーザー名>" , "<データベースアクセスパスワード>", "<データベースアクセスアドレス>", '<指定アクセスデータベース>')
db, _ := sql.Open("mysql", connectionString)
```
- Ruby
```
client = Mysql2::Client.new(
        :host     => '<データベースアクセスアドレス>',
        :username => '<データベースアクセスユーザー名>',
        :password => '<データベースアクセスパスワード>',
        :database => '<指定アクセスデータベース>',
        :sslca => '<ダウンロードした証明書のパス>’
    )
```

