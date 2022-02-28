## 클라이언트 연결
TDSQL for MySQL은 MySQL과 호환되는 연결 방식을 지원합니다. 아래와 같이 IP 주소, 포트 번호, 사용자 이름 및 암호를 사용하여 연결할 수 있습니다.
```
mysql -hxxx.xxx.xxx.xxx -Pxxxx -uxxx -pxxx -c
```
>!TDSQL for MySQL은 버전 4.0 이전 클라이언트 및 압축 프로토콜을 지원하지 않습니다. 고급 기능을 사용할 수 있도록 클라이언트 사용 시 `-c` 옵션을 추가하는 것을 권장합니다.

## PHP MySQLi 연결
PHP에서 TDSQL for MySQL에 연결하려면 MySQLi 확장을 활성화해야 합니다. demo는 다음과 같습니다.
```
header("Content-Type:text/html;charset=utf-8");
$host="10.10.10.10";  //인스턴스 proxy_host_ip
$user="test";  //인스턴스 사용자
$pwd="test";  //인스턴스 비밀번호
$db="aaa";  //데이터베이스 이름
$port="15002";  //proxy_host 포트 번호
$sqltool=new MySQLli($host,$user,$pwd,$db,$port);
//기타 필요한 코드
$sqltool->close();
echo "ok"."\n";
```

## JDBC 연결
JDBC를 사용하여 다음과 같이 TDSQL for MySQL에 연결할 수 있습니다.
```
private final String USERNAME = "test";  
private final String PASSWORD = "123456"; 
private final String DRIVER = "com.mysql.jdbc.Driver";   
private final String URL = "jdbc:mysql://10.10.10.10:3306?userunicode=true&characterEncoding=utf8mb4";  
private Connection connection;  
private PreparedStatement pstmt;  
private ResultSet resultSet;  
```

## 기타 연결 방법
TDSQL for MySQL은 navicat 및 odbc와 같이 MySQL과 호환되는 다른 연결 방법을 지원합니다.
