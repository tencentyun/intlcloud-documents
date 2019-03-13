인스턴스를 초기화 한 후에 MongoDB Shell 또는 각종 언어 드라이브로 데이터베이스를 액세스하여 관리 작업을 진행합니다. CVM을 사용하여 사설망으로 액세스해야 합니다. 공중망 액세스는 아직 지원하지 않습니다.

## 세부 정보
### 클라이언트 버전
TencentDB for MongoDB 서비스를 연결하려면 3.2 이상 버전을 요구합니다. **최신 버전**의 클라이언트 드라이브(Shell 슈트, java jar 패킷, PHP 확장, Nodejs 모듈 등)를 사용하여 최고의 호환성을 확보합니다. 자세한 내용은 [MongoDB 공식 웹사이트 드라이브 소개](https://docs.mongodb.com/ecosystem/drivers/)를 참조하십시오.
### MongoDB Shell 방식
mongo shell은 MongoDB의 대화형 JavaScript shell입니다. shell에서 명령행을 사용하여 MongoDB 인스턴스와 상호 작용할 수 있습니다. 또한 mongo shell로 데이터를 조회 및 업데이트하거나 관리 작업을 수행할 수 있습니다. mongo shell은 MongoDB 릴리스 버전의 일부입니다. 먼저 MongoDB를 다운로드하고 설치한 다음 mongo shell을 사용하여 MongoDB 인스턴스에 연결합니다. MongoDB 릴리스 버전을 다운로드하려면 [링크](https://www.mongodb.com/download-center#community)를 클릭합니다. 구체적인 절차는 다음과 같습니다.
```
    cd <mongodb installation dir>
	./bin/mongo -umongouser -plxh2081* 172.16.0.56:27017/admin
```
> 위 예제 중, -u 매개변수는 사용자 이름을 지정하고, -p 매개변수는 비밀번호를 지정하여, 172.16.0.56과 27017은 각각 MongoDB 인스턴스의 IP와 포트를 가리킵니다.

### URI 방식
MongoDB 서비스는 기존의 매개변수 전송 방식으로 연결합니다. 또한, 대부분의 드라이브는 URI 형식도 지원하여 연결할 수 있습니다. MongoDB는 공식으로 URI로 MongoDB 서비스를 연결하는 것을 권장합니다. 자주 사용되는 URI는 다음과 같습니다.

예제 1
```
mongodb://username:password@IP:27017/admin
```
예제 2
```
mongodb://username:password@IP:27017/somedb?authSource=admin
```
예제 3
```
mongodb://username:password@IP:27017/somedb?authSource=admin&readPreference=secondaryPreferred
```

URI 구성 요소에 대한 설명은 다음과 같습니다.

| 매개변수 | 설명 | 필수 여부 |
|---------|---------|---------|
| mongodb:// | 특정한 문자열, MognoDB 프로토콜을 의미합니다. | 예|
| username | MongoDB 서비스에 로그인하는 데 사용되는 사용자 이름 |예, 이 페이지의 "[기본 사용자 이름](#.E9.BB.98.E8.AE.A4.E7.94.A8.E6.88.B7.E5.90.8D)" 참조|
| password | MongoDB 서비스에 로그인하는 데 사용되는 비밀번호 |예|
| IP:27017 | MongoDB 서비스 IP와 포트 |예|
| /admin | 인증할 데이터베이스, TencentDB for MongoDB는 admin으로 고정 |예, 이 페이지의 "[데이터베이스 인증](#.E8.AE.A4.E8.AF.81.E6.95.B0.E6.8D.AE.E5.BA.93)" 참조|
| authMechanism=MONGODB-CR | 인증 메커니즘 |이 페이지의 "[인증 메커니즘](#.E8.AE.A4.E8.AF.81.E6.9C.BA.E5.88.B6)" 참조|
| authSource=admin | 신분 인증용 데이터베이스, TencentDB for MongoDB는 admin으로 고정 |예, 이 페이지의 "[데이터베이스 인증](#.E8.AE.A4.E8.AF.81.E6.95.B0.E6.8D.AE.E5.BA.93)" 참조|
| readPreference=secondaryPreferred | 우선 슬레이브 데이터베이스 읽기 설정 가능 |아니요, 이 페이지의 "[읽기 작업 마스터/슬레이브 우선 수준](#.E8.AF.BB.E6.93.8D.E4.BD.9C.E7.9A.84.E4.B8.BB.E4.BB.8E.E4.BC.98.E5.85.88.E7.BA.A7)" 참조|
여기서는 일부 MongoDB가 URI에 연결하는 매개변수만 나열하였습니다. 더 많은 내용은 [MongoDB 공식 웹사이트 문서](https://docs.mongodb.com/manual/reference/connection-string/)를 참조하십시오.

### 기본 사용자

TecentDB for MongoDB의 릴리스 버전에 따라 다르지만, 최신 생성한 인스턴스의 경우 당사는 내부적으로 "rwuser"와 "mongouser" 두 개 기본 사용자를 생성합니다. 비교적 오래된 인스턴스는 rwuser(이러한 인스턴스는 당사가 사전에 사용자에게 연락하여 업그레이드를 진행합니다)만 있습니다. 사용자는 TencentDB for MongoDB 콘솔에서 계정 및 권한을 관리하여 비즈니스의 수요를 충족시킬 수 있습니다.

#### rwuser(MONGODB-CR 인증) URI 예제
**rwuser는 유일하게 MONGODB-CR 인증을 사용하는 사용자입니다.**
```
mongodb://rwuser:password@10.66.100.186:27017/admin?authMechanism=MONGODB-CR
또는
mongodb://rwuser:password@10.66.100.186:27017/somedb?authMechanism=MONGODB-CR&authSource=admin
```

#### mongouser(SCRAM-SHA-1인증) URI 예제
**mongouser 및 클라우드 콘솔에서 생성한 사용자는 모두 SCRAM-SHA-1 인증을 사용합니다.**
```
mongodb://mongouser:password@10.66.100.186:27017/admin
또는
mongodb://mongouser:password@10.66.100.186:27017/somedb?authSource=admin
```

### 데이터베이스 인증
TencentDB for MongoDB는 일괄적으로 "admin" 데이터베이스를 로그인 인증 데이터베이스로 사용합니다. 따라서 인증 데이터베이스를 지정하려면 URI의 포트 뒤에 반드시 "**/admin**"을 추가해야 합니다. 인증 통과 후 다시 구체적인 비즈니스용 데이터베이스로 전환하여 읽기/쓰기 작업을 실행합니다. URI 예제:

```
mongodb://username:password@IP:27017/admin
```

물론, 읽기/쓰기 대상 데이터베이스와 별도의 인증 데이터베이스 매개변수(authSource=admin)를 직접적으로 지정하여 바로 대상 데이터베이스에 도달할 수도 있습니다. URI 예제:

```
mongodb://username:password@IP:27017/somedb?authSource=admin
```

사용자는 반드시 한 가지 방식을 선택하여 admin을 인증 데이터베이스로 URI에 추가해야 합니다.

### 인증 메커니즘
MongoDB는 여러 인증 메커니즘을 지원합니다. 현재는 공식으로 "SCRAM-SHA-1"을 권장합니다.
TencentDB for MongoDB는 "MONGODB-CR"과 "SCRAM-SHA-1" 인증 방식을 지원합니다.
상기 내용에 따라, TecentDB for MongoDB는 내부에 "rwuser"와 "mongouser" 두 개 기본 사용자를 생성합니다. 또한, TecentDB for MongoDB 콘솔에서 따로 사용자를 생성할 수 있습니다. 이러한 사용자는 두 유형으로 나뉘어져 각각 다른 인증 메커니즘을 사용합니다. 유형은 다음과 같습니다.

| 사용자 이름 | 인증 메커니즘 | URI 처리 |
|---------|---------|---------|
| rwuser | MONGODB-CR | 매개변수 "authMechanism=MONGODB-CR" 추가 필수|
|mongouser 및 클라우드 콘솔에서 생성한 사용자 |SCRAM-SHA-1 (권장) |매개변수 추가 필요없음|

###  읽기 작업의 마스터/슬레이브 우선 수준
TencentDB for MongoDB는 로드밸런싱 IP를 제공하여 전체 복제본 세트에 액세스할 수 있습니다. 슬레이브 데이터베이스의 읽기 작옵을 액세스해야 하는 경우 URI에 "readPreference" 매개변수를 추가하십시오. 관련 값은 아래에 설명되어 있습니다.

| 값 | 의미 | 기본값 여부|
|---------|---------|---------|
| primary |마스터 노드만 읽기 |예|
| primaryPreferred |마스터 노드는 우선이고, 마스터 노드를 사용할 수 없을 경우, 슬레이브 노드 읽기 |　|
| secondary | 슬레이브 노드만 읽기, 슬레이브 노드를 사용할 수 없을 경우 오류를 보고할 것입니다|　|
| secondaryPreferred |  슬레이브 노드는 우선이고, 슬레이브 노드를 사용할 수 없는 경우, 마스터 노드 읽기|　|

슬레이브 노드를 우선적으로 읽으려면 예제에 따라 URI를 병합할 수 있습니다.

```
mongodb://username:password@IP:27017/admin?readPreference=secondaryPreferred
```

## 각종 언어 예제

### Shell
[Shell 연결 예제](https://cloud.tencent.com/doc/product/240/Shell%E8%BF%9E%E6%8E%A5%E7%A4%BA%E4%BE%8B)
### PHP
[PHP 연결 예제](https://cloud.tencent.com/doc/product/240/PHP%E8%BF%9E%E6%8E%A5%E7%A4%BA%E4%BE%8B)
### Node.js
[Node.js 연결 예제](https://cloud.tencent.com/doc/product/240/Node.js%E8%BF%9E%E6%8E%A5%E7%A4%BA%E4%BE%8B)
 [Mongoose 예제](https://cloud.tencent.com/doc/product/240/Node.js%E8%BF%9E%E6%8E%A5%E7%A4%BA%E4%BE%8B#node.js-mongoose-.E8.BF.9E.E6.8E.A5.E7.A4.BA.E4.BE.8B)
### Java
[Java 연결 예제](https://cloud.tencent.com/doc/product/240/Java%E8%BF%9E%E6%8E%A5%E7%A4%BA%E4%BE%8B)
### Python
[Python 연결 예제](https://cloud.tencent.com/doc/product/240/Python%E8%BF%9E%E6%8E%A5%E7%A4%BA%E4%BE%8B)
### 재연결 메커니즘
[재연결 메커니즘](https://cloud.tencent.com/doc/product/240/4980)
