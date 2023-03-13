## SSL 암호화 개요
SSL(Secure Sockets Layer) 인증은 클라이언트에서 클라우드 데이터베이스 서버로의 인증으로 사용자와 서버를 인증합니다. SSL 암호화를 활성화하여 CA 인증서를 얻고 CA 인증서를 서버에 업로드합니다. 클라이언트가 데이터베이스에 액세스하면 SSL 프로토콜이 활성화되고 클라이언트와 데이터베이스 서버 사이에 SSL 보안 터널이 설정되어 암호화된 데이터 정보 전송을 실현하며, 전송 중 데이터 가로채기, 변조 및 도청을 방지하고 양측이 전송하는 정보의 보안성을 보증합니다.

SSL 프로토콜은 신뢰할 수 있는 전송 제어 프로토콜(TCP)에 기반을 두고 구축되어야 하며, 응용 레이어 프로토콜과 독립적이며, 높은 레이어의 응용 레이어 프로토콜(예시: HTTP, FTP, TELNET 등)은 SSL 프로토콜 위에 투명하게 구축될 수 있다는 장점이 있습니다. SSL 프로토콜은 응용 레이어 프로토콜의 통신 전에 암호화 알고리즘, 통신 키 협상 및 서버 인증을 완료한 후 응용 레이어 프로토콜이 전송하는 데이터를 암호화하여 통신의 비밀성을 보장합니다.

## 배경
비암호화 방식으로 데이터베이스에 연결할 경우, 네트워크에서 전송되는 모든 정보는 플레인 텍스트이기 때문에 불법 사용자로부터 도청, 변조, 사칭의 3가지 리스크가 있으며 SSL 프로토콜은 이러한 3가지 리스크를 해결하도록 설계되어 이론상 다음을 달성할 수 있습니다:
- 정보는 암호화되어 전송되며 제 3자가 도청할 수 없습니다.
- 인증 메커니즘을 사용하여 변조되면 통신의 양측은 즉시 알 수 있습니다.
- 본인 인증을 통해 명의 도용을 방지합니다.

TencentDB for MySQL은 SSL 암호화를 활성화하고 SSL CA 인증서를 필요한 애플리케이션 서비스에 다운로드 및 설치하여 연결 보안성을 향상할 수 있도록 지원합니다.
>!SSL 암호화는 데이터 자체를 보호하지 않습니다. 대신 데이터베이스와 서버 간의 트래픽 보안을 보장합니다. 전송 레이어에서 네트워크 연결을 암호화하면 통신 데이터의 보안성과 완정성을 향상시킬 수 있지만 네트워크 연결의 응답 시간이 늘어납니다.

## 전제 조건
- 인스턴스 버전은 MySQL 5.6/5.7/8.0입니다.
- 인스턴스 아키텍처는 2노드/3노드입니다.
- 인스턴스 엔진은 InooDB/RocksDB입니다.

## SSL 암호화 활성화
1. [TencentDB for MySQL 콘솔](https://console.cloud.tencent.com/cdb/instance) 로그인 후, 인스턴스 리스트에서 인스턴스 ID 또는 작업 열의 **관리**를 클릭하여 인스턴스 관리 페이지로 이동합니다.
2. 인스턴스 관리 페이지의 **데이터 보안** 페이지에서 **SSL** 페이지를 선택합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/a87ff1d0edd454e3685c0b33eada0e39.png)
3. 이 기능은 기본적으로 비활성화되어 있으며 스위치를 활성화하여 **확인**을 클릭하고 SSL 암호화를 활성화합니다.
 - 원본 인스턴스는 다음과 같이 SSL 창을 활성화합니다.
 ![](https://qcloudimg.tencent-cloud.cn/raw/4061d5b39e786248761915c8e6982b47.png)
>!SSL 활성화 과정 중 데이터베이스 인스턴스가 재시작되어 SSL 인증서를 로딩합니다. 비즈니스에 재연결 메커니즘이 있는지 확인하십시오.
>
 - RO 인스턴스는 다음과 같이 SSL 인터페이스를 활성화합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/461f76f6fe377c26e36b0c4d4b2c42f4.png)
>!RO 인스턴스를 구성하는 SSL 기능은 동일한 RO 그룹의 다른 RO 인스턴스의 구성을 동기화합니다.
>
4. **다운로드**를 클릭하여 SSL CA 인증서를 다운로드합니다.
다운로드한 파일은 압축 패키지(TencentDB-CA-Chain.zip)이며 다음 세개의 파일이 포함되어 있습니다:
 - p7b 파일: Windows 시스템에서 CA 인증서를 가져오기 위해 사용됩니다.
 - jks 파일: Java의 truststore 인증서 저장 파일, 비밀번호는 tencentdb로 통합되어 Java 프로그램에서 CA 인증서 링크를 가져오는 데 사용됩니다.
 - pem 파일: 다른 시스템이나 애플리케이션에서 CA 인증서를 가져오기 위해 사용됩니다.

## SSL CA 인증서 구성
SSL 암호화를 활성화한 후 클라이언트를 사용하여 클라우드 데이터베이스에 연결할 때 SSL CA 인증서를 구성해야 합니다. 다음은 Navicat을 예로 들어 SSL CA 인증서를 설치하는 방법을 소개합니다. 다른 애플리케이션이나 클라이언트의 경우 해당 제품의 사용 설명서를 참고하십시오.
>?TencentDB for MySQL에 대해 SSL 암호화가 활성화 또는 비활성화될 때마다 새 인증서가 생성됩니다.
>
1. Navicat을 엽니다.
2. 해당 데이터베이스를 우클릭하고 **연결 편집**을 선택합니다.
3. SSL 탭을 선택하고 .pem 형식의 CA 인증서 경로를 선택합니다. 아래 이미지의 설정을 완료한 후 **확인**을 클릭합니다.
>?connection is being used 오류가 발생하면 이전 세션이 연결 해제되지 않았기 때문일 수 있습니다. Navicat을 비활성화하고 다시 시도하십시오.
>
4. 해당 데이터베이스를 더블 클릭하여 연결이 정상인지 테스트합니다.

## SSL 암호화 비활성화
1. [TencentDB for MySQL 콘솔](https://console.cloud.tencent.com/cdb/instance) 로그인 후, 인스턴스 리스트에서 인스턴스 ID 또는 작업 열의 **관리**를 클릭하여 인스턴스 관리 페이지로 이동합니다.
2. 인스턴스 관리 페이지의 **데이터 보안** 페이지에서 **SSL** 페이지를 선택합니다.
3. 활성화 됨 앞의 스위치 버튼을 클릭하고 팝업 창에서 **확인**을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/5e6f6976d9e97ed01e37a5e722a33c1a.png)
>?SSL 비활성화 중 데이터베이스 인스턴스가 재시작되어 SSL 인증서를 언마운트합니다. 비즈니스에 재연결 메커니즘이 있는지 확인하십시오.

## SSL 연결 암호화가 활성화된 인스턴스에 연결
SSL 연결 암호화를 사용하여 다음과 같이 데이터베이스 SQL에 연결합니다:
```
mysql -P <포트 번호> -h <IP 주소>  -u <사용자 이름> -p<비밀번호> --ssl-ca<ca 인증서>
```

## 일반 프로그램에서 SSL가 활성화된 인스턴스 연결을 위한 예시 코드
- PHP
```
$conn = mysqli_init();
mysqli_ssl_set($conn,NULL,NULL, "<다운로드된 인증서 경로>", NULL, NULL);
mysqli_real_connect($conn, '<데이터베이스 액세스 주소>', '<데이터베이스 액세스 사용자 이름>', '<데이터베이스 액세스 비밀번호>', '<액세스할 지정된 데이터베이스>', <액세스 포트>, MYSQLI_CLIENT_SSL);
if (mysqli_connect_errno($conn)) {
die('Failed to connect to MySQL: '.mysqli_connect_error());
}
```
- PHP (Using PDO)
```
$options = array(
    PDO::MYSQL_ATTR_SSL_CA => '<다운로드된 인증서의 경로>'
);
$db = new PDO('mysql:host=<데이터베이스 액세스 주소>;port=<액세스 포트>;dbname=<액세스할 지정된 데이터베이스>', '<데이터베이스 액세스 사용자 이름>', '<데이터베이스 액세스 비밀번호>', $options);
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

System.setProperty("javax.net.ssl.keyStore","<다운로드한 인증서의 경로>");
System.setProperty("javax.net.ssl.keyStorePassword","tencentdb");
System.setProperty("javax.net.ssl.trustStore","<다운로드된 인증서의 경로>");
System.setProperty("javax.net.ssl.trustStorePassword","tencentdb");

url = String.format("jdbc:mysql://%s/%s?serverTimezone=UTC&useSSL=true", '<데이터베이스 액세스 주소>', '<액세스할 지정된 데이터베이스>');
properties.setProperty("user", '<데이터베이스 액세스 사용자 이름>');
properties.setProperty("password", '<데이터베이스 액세스 비밀번호>');
conn = DriverManager.getConnection(url, properties);
```
- .NET (MySqlConnector)
```
var builder = new MySqlConnectionStringBuilder
{
    Server = "<데이터베이스 액세스 주소>",
    UserID = "<데이터베이스 액세스 사용자 이름>",
    Password = "<데이터베이스 액세스 비밀번호>",
    Database = "<액세스할 지정된 데이터베이스>",
    SslMode = MySqlSslMode.VerifyCA,
    SslCa = "<다운로드된 인증서>",
};
using (var connection = new MySqlConnection(builder.ConnectionString))
{
    connection.Open();
}
```
- Python (MySQLConnector Python)
```
try:
    conn = mysql.connector.connect(user='<데이터베이스 액세스 사용자 이름>',
                                   password='<데이터베이스 액세스 비밀번호>',
                                   database='<액세스할 지정된 데이터베이스>',
                                   host='<데이터베이스 액세스 주소>',
                                   ssl_ca='<다운로드한 인증서 경로>')
except mysql.connector.Error as err:
    print(err)
```

- Python (PyMySQL)
```
conn = pymysql.connect(user='<데이터베이스 액세스 사용자 이름>',
                       password='<데이터베이스 액세스 비밀번호>',
                       database='<액세스할 지정된 데이터베이스>',
                       host='<데이터베이스 액세스 주소>',
                       ssl={'ca': '<다운로드한 인증서 경로>'})
```

- Django (PyMySQL)
```
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': '<액세스할 지정된 데이터베이스>',
        'USER': '<데이터베이스 액세스 사용자 이름>',
        'PASSWORD': '<데이터베이스 액세스 비밀번호>',
        'HOST': '<데이터베이스 액세스 주소>',
        'PORT': '<액세스 포트>',
        'OPTIONS': {
            'ssl': {'ca': '<다운로드한 인증서의 경로>'}
        }
    }
}
```
- Node.js
```
var fs = require('fs');
var mysql = require('mysql');
const serverCa = [fs.readFileSync("<다운로드된 인증서의 경로>", "utf8")];
var conn=mysql.createConnection({
    host:"<데이터베이스 액세스 주소>",
    user:"<데이터베이스 액세스 사용자 이름>",
    password:"<데이터베이스 액세스 비밀번호>",
    database:"<액세스할 지정된 데이터베이스>",
    port:<액세스 포트>,
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
pem, _ := ioutil.ReadFile("<다운로드된 인증서의 경로>")
if ok := rootCertPool.AppendCertsFromPEM(pem); !ok {
    log.Fatal("Failed to append PEM.")
}
mysql.RegisterTLSConfig("custom", &tls.Config{RootCAs: rootCertPool})
var connectionString string
connectionString = fmt.Sprintf("%s:%s@tcp(%s:<액세스 포트>)/%s?allowNativePasswords=true&tls=custom","<데이터베이스 액세스 사용자 이름>" , "<데이터베이스 액세스 비밀번호>", "<데이터베이스 액세스 주소>", '<액세스할 지정된 데이터베이스>')
db, _ := sql.Open("mysql", connectionString)
```
- Ruby
```
client = Mysql2::Client.new(
        :host     => '<데이터베이스 액세스 주소>',
        :username => '<데이터베이스 액세스 사용자 이름>',
        :password => '<데이터베이스 액세스 비밀번호>',
        :database => '<액세스할 지정된 데이터베이스>',
        :sslca => '<다운로드된 인증서의 경로>'
    )
```

