
### MongoDB의 연결이 끊어지면 어떻게 해야 하나요?
인증 문제를 해결하려면 [연결 예제](https://cloud.tencent.com/document/product/240/3563)를 참조하십시오.

### MongoDB에 "Remote server has closed the connection" 정보가 나타나면 어떻게 해야 하나요?
먼저 [연결 예제](https://cloud.tencent.com/document/product/240/3563)를 참조하여 인증 문제를 해결합니다. 연결될 수 있지만 여전히 문제가 있을 경우, 재연결 메커니즘이 필요할 수도 있습니다. 자세한 내용은 [재연결 예제](https://cloud.tencent.com/document/product/240/4980)를 참조하십시오.

### WiredTiger 3.2는 테이블 잠금 문제가 존재합니다. TencentDB for MongoDB에도 이와 비슷한 문제가 있나요?
특정 상황에 달려 있습니다. 예를 들어, 기본적으로 인덱스를 작성하려면 전역 잠금이 필요하며 fsynclock 명령을 실행할 때도 잠금이 필요합니다.
잠금은 데이터베이스의 기능 중 하나입니다. 동시 발생 액세스에 관한 여러 가지 문제를 처리하기 때문에 정상적인 잠금은 필수적입니다. 따라서 비즈니스의 정상 운영만 영향 받지 않는다면 괜찮습니다.

### MongoDB는 어떤 버전의 드라이버를 선택해야 하나요?
최신 버전을 사용하는 것을 권장합니다. 예: PHP의 경우, mongo-1.6 이상 버전을 선택할 수 있습니다.
 
### MongoDB는 어떤 언어의 연결 방식을 제공하나요?
TencentDB for MongoDB는 다양한 언어의 연결 방식을 제공합니다. 예를 들어 Shell, PHP, Node.js, Java, Python이 있습니다. 자세한 내용은 [연결 예제](https://cloud.tencent.com/document/product/240/3563)를 참조하십시오.

### TencentDB for MongoDB가 지원하는 클라이언트의 언어는 무엇인가요?
TencentDB for MongoDB는 클라이언트에 대해 MongoDB와 동일한 호환성을 제공합니다. TencentDB for MongoDB는 공식 MongoDB 버전이 지원하는 모든 클라이언트를 지원합니다. 예: C, C++, C#, java, node.js, python, php, perl 등. 자세한 내용은 [MongoDB 공식 문서](https://docs.mongodb.org/ecosystem/drivers/)를 참조하십시오.

### shell에서 TencentDB for MongoDB를 연결하는 방법?
자세한 내용은 [Shell 연결 예제](https://cloud.tencent.com/doc/product/240/3978)를 참조하십시오.

### 서비스 응용프로그램에서 MongoDB를 연결할 수 있는 URI는 어떤 것인가요?
자세한 내용은 [연결 예제](https://cloud.tencent.com/doc/product/240/3563)를 참조하십시오.

### meteor 등 각종 프레임, 클래스 데이터베이스로 TencentDB for MongoDB에 연결할 수 없는 경우 어떻게 해야 하나요?
일반적으로는 연결 방식 또는 URI 병합에 문제가 발생했기 때문입니다. 먼저 확인하십시오.

### PHP에서 MongoDB의 최대 연결 수를 설정하는 방법?
MongoDB 드라이브([PHP 공식 문서](http://php.net/manual/en/set.mongodb.php))는 URL 링크에서 maxPoolSize 매개변수를 설정하여 연결 수를 제어할 수 있습니다.
MongoDB 드라이브([PHP 공식 문서](http://php.net/manual/en/set.mongodb.php))는 Mongo::setPoolSize()의 방법으로 연결 수를 설정할 수 있습니다. 자세한 내용은 [MongoPool::setSize](http://php.net/manual/en/mongopool.setsize.php)를 참조하십시오.
 

### MongoDB의 연결 수는 얼마까지 제한하나요?
![이미지 설명](//bot1024-1253841380.file.myqcloud.com/3defdf809c3d11e7bd8b525400a3183e.png)
연결 수의 상한은 노드가 아닌 인스턴스에 적용합니다. 자세한 내용은 [제한 설명](https://cloud.tencent.com/document/product/240/622)을 참조하십시오.
 
### MongoDB를 수동으로 재연결하는 방법?
TencentDB for MongoDB가 쉬운 mongos 액세스만 제공한 게가 아니라 액세스용 로드밸런싱 IP도 제공합니다. 그 후에 해당 IP의 연결 대상은 mongos와 같은 라우팅 액세스 레이어입니다.
클라이언트 드라이브는 로드밸런싱 IP를 통하여 접속 서버와 지속적인 연결을 구축합니다. 이 연결이 장시간 동안 액티브 상태일 때, 당사는 이에 대해 어떠한 간섭도 하지 않습니다. 그러나 지속적인 연결의 휴면 시간이 1일(이 시간은 버전의 최적화에 따라 조정될 수 있음)을 초과할 경우, 라우팅 액세스 레이어는 이 연결을 끊을 수 있습니다.
일반적으로 클라이언트 드라이브는 자동 이중 연결 과정을 구현합니다. 그러나 일부 언어의 드라이브는 구현되지 못합니다. 자동 재연결을 구현할 수 없는 언어의 드라이브의 경우 사용자가 이미 끊긴 연결을 TencentDB for MongoDB에 시도하면 "Remote server has closed the connection"라는 메시지가 나타날 수도 있습니다. 따라서, 수동으로 재연결해야 합니다. 다음은 PHP 재연결의 Demo입니다.

**PHP Mongo 기반 드라이브의 재연결 구현**  
![이미지 설명](//bot1024-1253841380.file.myqcloud.com/aa398f929c4211e79a34525400a3183e.png)


### mongoose로 TencentDB for MonogoDB를 연결하는 방법?
Mongoose로 TencentDB for MonogoDB를 연결하는 매개변수는 다음과 같습니다.

``` 
var dbUri = " mongodb:// " + user + " : " +password + " @ " +host + ":" +port + " / " + dbName;

var opts = {
　　auth：｛
　　　　authMechanism : ' MONDODB-CR'
      ｝
}；
var connection = mongodb.createConnection(dbUri, opts);
```

### MongoDB는 공중망 연결을 지원하나요?
MongoDB는 현재 사설망만 지원합니다. 연결 방식은 [연결 예제](https://cloud.tencent.com/document/product/240/3563)를 참조하십시오.
아직 공중망 액세스를 지원하지 않습니다. 로컬에서 MongoDB를 연결하려면, MongoDB와 같은 계정, 같은 사설망의 서버를 포트로 포워딩합니다.
 

