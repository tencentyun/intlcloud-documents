## 개발 전 준비

### 관련 리소스

COS 서비스의 XML Java SDK 리소스 다운로드 주소: [XML Java SDK](https://github.com/tencentyun/cos-java-sdk-v5).

### 환경 의존

- SDK는 JDK 1.7, 1.8 이상 버전을 지원합니다.
- JDK 설치 방법은 [Java 설치 및 구성](/document/product/436/10865)을 참조하십시오.

> ?문서에서 나오는 SecretId, SecretKey, Bucket 등과 같은 명칭의 함의 및 획득 방법은 [COS 용어집](https://cloud.tencent.com/document/product/436/7751)을 참조하십시오.

### SDK 설치

SDK의 두가지 설치 방식: maven 설치 및 오리진 코드 설치.

- maven 설치
  maven 프로젝트에서는 pom.xml 을 사용하여 관련 종속성을 추가하며 내용은 다음과 같습니다.
```shell
<dependency>
            <groupId>com.qcloud</groupId>
            <artifactId>cos_api</artifactId>
            <version>5.4.10</version>
</dependency>
```

- 오리진 코드 설치
  [XML Java SDK](https://github.com/tencentyun/cos-java-sdk-v5)에서 오리진 코드를 다운로드하고 maven을 통해 가져오기 합니다. eclipse일 경우, 차례로 File -> Import -> maven -> Existing Maven Projects를 선택합니다.

### SDK 탑재 해제

pom 종속성 또는 오리진 코드를 삭제하면 SDK를 탑재 해제할 수 있습니다.

## 시작 가이드

### 클라이언트 초기화 COSClient

`COSClient`는 COS API 를 호출하는 객체입니다. `COSClient` 인스턴스를 생성한 후 반복적으로 사용할 수 있으며 스레드는 안전합니다. 마지막 응용프로그램 또는 서비스를 종료할 경우 클라이언트를 끄면 됩니다.

#### 영구 클라우드 API 키를 사용한 정보 초기화

클라우드 API 키는 영구 키이며 Tencent Cloud [CAM 콘솔](https://console.qcloud.com/cam/capi)에서 획득하여 생성하고 대부분 응용프로그램 시나리오에 적용됩니다.

Java SDK 클라우드 API 키의 초기화 방법은 다음과 같습니다.

```java
// 1 사용자 ID 정보 초기화(secretId, secretKey).
COSCredentials cred = new BasicCOSCredentials("AKIDXXXXXX", "XXXXXXXXXXXXXXX");
// 2 버킷의 지역을 설정합니다. COS 영역의 약어는 다음 링크를 참조하십시오. https://cloud.tencent.com/document/product/436/6224
// clientConfig에 region 설정, https(기본 http), 시간 초과, 프록시 등 set 방법을 포함하며, 사용방법은 오리진 코드 또는 API 문서 FAQ 중 설명을 참조하십시오.
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// 3 cos 클라이언트를 생성합니다.
COSClient cosClient = new COSClient(cred, clientConfig);
//버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 반드시 이 형식이어야 합니다
String bucketName = "mybucket-1251668577";
```

#### 임시 키를 사용한 초기화

Tencent Cloud CAM 서비스를 통해 임시 키를 신청할 경우 임시 키 생성 및 사용은 [임시 키 생성 및 사용 가이드](https://cloud.tencent.com/document/product/436/14048)를 참조하십시오.

Java SDK는 임시 키 가져오기를 통한 클라이언트 초기화를 지원합니다. 임시 키의 초기화 방법은 다음과 같습니다.

```java
// 1 획득한 임시 키 가져오기 (tmpSecretId, tmpSecretKey, sessionToken)
BasicSessionCredentials cred = new BasicSessionCredentials("a-demo-secretId", "a-demo-secretKey", "a-demo-session-token");
// 2 bucket의 지역을 설정하며, COS 지역의 약칭은 https://cloud.tencent.com/document/product/436/6224를 참조하십시오
// clientConfig 에 region 설정, https(기본 http), 시간 초과, 프록시 등 set 방법을 포함하며, 사용방법은 오리진 코드 또는 API 문서 FAQ를 참조하십시오.
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// 3 COS 클라이언트 생성
COSClient cosClient = new COSClient(cred, clientConfig);
//버킷의 명명 규칙은 {name}-{appid}입니다. 여기에 입력된 버킷 이름은 반드시 이 형식이어야 합니다
String bucketName = "mybucket-1251668577";
```

### 파일 업로드

로컬 파일 또는 알려진 길이의 입력 스트림 내용을 COS에 업로드합니다. 20MB 이하 이미지 유형의 작은 파일을 업로드하는 데 적용되며, 최대 5GB를 초과하지 않는 파일의 업로드를 지원합니다. 5GB 이상의 파일은 멀티파트 업로드 또는 고급 API 업로드를 사용하십시오.

- 로컬 파일이 대부분 20M 이상인 경우 사용 API 문서의 고급 API를 참조하여 업로드할 것을 권장합니다
-  COS 에 이미 같은 Key의 객체가 존재하면 업로드 시 덮어쓰기 됩니다.
- 디렉터리 객체를 생성할 경우 COS에 디렉터리가 존재하지 않으므로 [API 문서](https://cloud.tencent.com/document/product/436/12263#.E5.B8.B8.E8.A7.81.E9.97.AE.E9.A2.98)  FAQ 부분을 참조하십시오.
- 객체 키(Key)는 버킷에서 객체의 유일한 ID입니다. 예를 들어, 객체의 접근 도메인 이름 `bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg` 중, 객체 키는 doc1/pic1.jpg입니다. 자세한 정보는 [객체 키](https://cloud.tencent.com/document/product/436/13324)의 설명을 참조하십시오.
- 업로드 후에, 같은 키`key`로, `GetObject` API를 호출하여 로컬에 파일을 다운로드하거나 사전 서명 링크를 생성하여(다운로드 시 method를 ‘GET’으로 지정하고, 구체적인 API 설명은 [API 문서](https://cloud.tencent.com/document/product/436/12263)를 참조하십시오), 다른 포트로 보내 다운로드할 수 있습니다. 단, 파일이 비공개 읽기 권한인 경우 사전 서명 링크는 일정한 유효 기간이 있다는 점에 주의하십시오.

예제 코드는 다음과 같습니다.

```java
File localFile = new File("src/test/resources/len5M.txt");
// 업로드할 버킷 지정
String bucketName = "demoBucket-1250000000";
// 업로드할 COS의 객체 키 지정
String key = "upload_single_demo.txt";

PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);
PutObjectResult putObjectResult = cosClient.putObject(putObjectRequest);
```

### 파일 다운로드

파일을 로컬에 다운로드하거나 파일 다운로드 스트림을 획득합니다. 다음 예제 코드를 참조하십시오.

```java
// 다운로드할 로컬 경로 지정
File downFile = new File("src/test/resources/mydown.txt");
// 파일 소재 버킷 지정
String bucketName = "demoBucket-1250000000";
// COS에서의 파일 객체 키 지정
String key = "upload_single_demo.txt";

GetObjectRequest getObjectRequest = new GetObjectRequest(bucketName, key);
ObjectMetadata downObjectMeta = cosClient.getObject(getObjectRequest, downFile);
```

### 파일 삭제

COS의 지정한 경로 파일을 삭제하며, 코드는 다음과 같습니다.

```java
// 파일 소재 버킷 지정
String bucketName = "demoBucket-1250000000";
// COS에서의 파일 객체 키 지정
String key = "upload_single_demo.txt";

cosClient.deleteObject(bucketName, key);
```

### 클라이언트 종료

cosClient를 종료하고, HTTP 연결의 백그라운드 관리 스레드를 릴리스합니다. 코드는 다음과 같습니다.

```
// 클라이언트 종료(백그라운드 스레드 종료)
cosClient.shutdown();
```
