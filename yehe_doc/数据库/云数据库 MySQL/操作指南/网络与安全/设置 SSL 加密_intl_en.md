## SSL encryption overview
Secure Sockets Layer (SSL) authentication is a process that authenticates the connection from the user client to the TencentDB server. After SSL encryption is enabled, you can get a CA certificate and upload it to the server. Then, when the client accesses the database, the SSL protocol will be activated to establish an SSL secure channel between the client and the server. This implements encrypted data transfer, prevents data from being intercepted, tampered with, and eavesdropped during transfer, and ultimately ensures the data security for both the client and the server.

The SSL protocol needs to be established based on reliable TCP and has the advantage of being independent from application layer protocols; therefore, high-level application layer protocols such as HTTP, FTP, and TELNET can be transparently established on it. It completes encryption algorithm processing, communication key negotiation, and server authentication before communication is made over application layer protocols. After that, all data transferred over application layer protocols will be encrypted to ensure communication privacy.

## Background
When you connect to a database in an unencrypted manner, all information transferred over the network will be in plaintext and may be eavesdropped, tampered with, and impersonated by malicious users. The SSL protocols are designed to address these risks and can bring the following benefits theoretically:
- Information is encrypted and cannot be eavesdropped by a third party.
- There is a verification mechanism for immediate tampering detection by both parties in the communication.
- Identity certificates will be used to authenticate the identity.

TencentDB for MySQL supports enhancing the connection security by enabling SSL encryption as well as downloading and installing SSL CA certificates to the required application services.
>!SSL encryption protects the traffic between the database and the server rather than the data itself. Encrypting the network connection at the transport layer can improve the security and integrity of the communication data, but will increase the response time of the network connection.

## Prerequisites
- The instance version is MySQL 5.6/5.7/8.0.
- The instance architecture is two-node/three-node.
- The instance engine is InnoDB/RocksDB.

## Enabling SSL encryption
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb/instance). In the instance list, click an instance ID or **Manage** in the **Operation** column to enter the instance management page.
2. On the instance management page, select the **Data Security** > **SSL** tab.
![](https://qcloudimg.tencent-cloud.cn/raw/a87ff1d0edd454e3685c0b33eada0e39.png)
3. This feature is disabled by default. Toggle it on and click **OK**.
 - The window to enable SSL encryption in the source instance is as follows:
 ![](https://qcloudimg.tencent-cloud.cn/raw/4061d5b39e786248761915c8e6982b47.png)
>!During the process of enabling SSL encryption, your database instance will be restarted to load the SSL certificate. Make sure that your business has a reconnection mechanism.
>
 - The window to enable SSL encryption in a read-only instance is as follows:
![](https://qcloudimg.tencent-cloud.cn/raw/461f76f6fe377c26e36b0c4d4b2c42f4.png)
>!The configuration of the SSL encryption feature in a read-only instance will be synced to other read-only instances in its read-only group.
>
4. Click **Download** to download the SSL CA certificate.
The downloaded file is a compressed package (TencentDB-CA-Chain.zip), which contains the following three files:
 - .p7b file: It is used to import the CA certificate into Windows.
 - .jks file: It is the truststore certificate storage file in Java and always has the password `tencentdb`. It is used to import the CA certificate chain into Java.
 - .pem file: It is used to import the CA certificate into other systems or applications.

## Configuring an SSL CA certificate
After enabling SSL encryption, you need to configure an SSL CA certificate when using a client to connect to TencentDB. The following takes Navicat as an example to describe how to install an SSL CA certificate. For other applications or clients, refer to their respective documentation.
>?Every time SSL encryption is enabled or disabled for TencentDB for MySQL, a new certificate will be generated.
>
1. Open Navicat.
2. Right-click the target database and select **Edit Connection**.
3. Select the **SSL** tab, select the path of the CA certificate in .pem format, complete the settings, and click **OK**.
>? If the error message `connection is being used` is displayed, it may be because the previous session has not been disconnected. In this case, restart Navicat and try again.
>
4. Double-click the target database to test whether the connection is normal.

## Disabling SSL encryption
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb/instance). In the instance list, click an instance ID or **Manage** in the **Operation** column to enter the instance management page.
2. On the instance management page, select the **Data Security** > **SSL** tab.
3. Toggle the switch off and click **OK** in the pop-up window.
![](https://qcloudimg.tencent-cloud.cn/raw/5e6f6976d9e97ed01e37a5e722a33c1a.png)
>!During the process of disabling SSL encryption, your database instance will be restarted to uninstall the SSL certificate. Make sure that your business has a reconnection mechanism.

## Connecting to an SSL-enabled instance
To use an encrypted SSL connection to connect to the database, run the following SQL statement:
```
mysql -P <port number> -h <IP address>  -u <username> -p<password> --ssl-ca<CA certificate>
```

## Sample code for connecting to an SSL-enabled instance from common programs
- PHP
```
$conn = mysqli_init();
mysqli_ssl_set($conn,NULL,NULL, "<path of the downloaded certificate>", NULL, NULL);
mysqli_real_connect($conn, '<database access address>', '<database access username>', '<database access password>', '<the specified database to be accessed>', <access port>, MYSQLI_CLIENT_SSL);
if (mysqli_connect_errno($conn)) {
die('Failed to connect to MySQL: '.mysqli_connect_error());
}
```
- PHP (Using PDO)
```
$options = array(
    PDO::MYSQL_ATTR_SSL_CA => '<path of the downloaded certificate>'
);
$db = new PDO('mysql:host=<database access address>;port=<access port>;dbname=<the specified database to be accessed>', '<database access username>', '<database access password>', $options);
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

System.setProperty("javax.net.ssl.keyStore","<path of the downloaded certificate>");
System.setProperty("javax.net.ssl.keyStorePassword","tencentdb");
System.setProperty("javax.net.ssl.trustStore","<path of the downloaded certificate>");
System.setProperty("javax.net.ssl.trustStorePassword","tencentdb");

url = String.format("jdbc:mysql://%s/%s?serverTimezone=UTC&useSSL=true", '<database access address>', '<the specified database to be accessed>');
properties.setProperty("user", '<database access username>');
properties.setProperty("password", '<database access password>');
conn = DriverManager.getConnection(url, properties);
```
- .NET (MySqlConnector)
```
var builder = new MySqlConnectionStringBuilder
{
    Server = "<database access address>",
    UserID = "<database access username>",
    Password = "<database access password>",
    Database = "<the specified database to be accessed>",
    SslMode = MySqlSslMode.VerifyCA,
    SslCa = "<downloaded certificate>",
};
using (var connection = new MySqlConnection(builder.ConnectionString))
{
    connection.Open();
}
```
- Python (MySQLConnector Python)
```
try:
    conn = mysql.connector.connect(user='<database access username>',
                                   password='<database access password>',
                                   database='<the specified database to be accessed>',
                                   host='<database access address>',
                                   ssl_ca='<path of the downloaded certificate>')
except mysql.connector.Error as err:
    print(err)
```

- Python (PyMySQL)
```
conn = pymysql.connect(user='<database access username>',
                       password='<database access password>',
                       database='<the specified database to be accessed>',
                       host='<database access address>',
                       ssl={'ca': '<path of the downloaded certificate>'})
```

- Django (PyMySQL)
```
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': '<the specified database to be accessed>',
        'USER': '<database access username>',
        'PASSWORD': '<database access password>',
        'HOST': '<database access address>',
        'PORT': '<access port>',
        'OPTIONS': {
            'ssl': {'ca': '<path of the downloaded certificate>'}
        }
    }
}
```
- Node.js
```
var fs = require('fs');
var mysql = require('mysql');
const serverCa = [fs.readFileSync("<path of the downloaded certificate>", "utf8")];
var conn=mysql.createConnection({
    host:"<database access address>",
    user:"<database access username>",
    password:"<database access password>",
    database:"<the specified database to be accessed>",
    port:<access port>,
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
pem, _ := ioutil.ReadFile("<path of the downloaded certificate>")
if ok := rootCertPool.AppendCertsFromPEM(pem); !ok {
    log.Fatal("Failed to append PEM.")
}
mysql.RegisterTLSConfig("custom", &tls.Config{RootCAs: rootCertPool})
var connectionString string
connectionString = fmt.Sprintf("%s:%s@tcp(%s:<access port>)/%s?allowNativePasswords=true&tls=custom","<database access username>" , "<database access password>", "<database access address>", '<the specified database to be accessed>')
db, _ := sql.Open("mysql", connectionString)
```
- Ruby
```
client = Mysql2::Client.new(
        :host     => '<database access address>',
        :username => '<database access username>',
        :password => '<database access password>',
        :database => '<the specified database to be accessed>',
        :sslca => '<path of the downloaded certificate>'
    )
```

