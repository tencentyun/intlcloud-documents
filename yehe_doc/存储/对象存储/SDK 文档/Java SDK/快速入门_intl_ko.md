## 다운로드 및 설치

#### 관련 리소스
- COS 서비스의 XML Java SDK 소스 코드 다운로드 주소: [XML Java SDK](https://github.com/tencentyun/cos-java-sdk-v5).
- SDK 고속 다운로드 주소: [XML Java SDK](https://cos-sdk-archive-1253960454.file.myqcloud.com/cos-java-sdk-v5/latest/cos-java-sdk-v5.zip).
- 예시 Demo 다운로드 주소: [COS XML Java SDK 예시](https://github.com/tencentyun/cos-java-sdk-v5/tree/master/src/main/java/com/qcloud/cos/demo).
- SDK 문서의 모든 예시 코드는 [SDK 코드 예시](https://github.com/tencentyun/cos-snippets/tree/master/Java)를 참고하십시오.
- SDK 로그 업데이트는 [ChangeLog](https://github.com/tencentyun/cos-java-sdk-v5/blob/master/CHANGELOG.md)를 참고하십시오.
- SDK FAQ는 [Java SDK FAQ](https://intl.cloud.tencent.com/document/product/436/38956)를 참고하십시오.


>? XML 버전 SDK 사용 중 함수 또는 메소드가 존재하지 않는 등의 오류 발생 시, XML 버전 SDK를 최신 버전으로 업그레이드한 후 재시도하십시오.
>


#### 환경 종속
- SDK는 JDK 1.7, 1.8 이후 버전을 지원합니다.
- JDK 설치 방법은 [Java 설치 및 설정](https://intl.cloud.tencent.com/document/product/436/10865)을 참고하십시오.

>?
>- 본 문서에 나오는 SecretId, SecretKey, Bucket 등의 명칭에 대한 의미 및 획득 방법은 [COS 용어 정보](https://intl.cloud.tencent.com/document/product/436/7751)를 참고하십시오.
>- COS Java SDK에서 주로 사용하는 클래스는 각각 다음 패키지에 포함되어 있습니다.
 - 클라이언트 설정 관련 클래스: com.qcloud.cos.\* 패키지.
 - 권한 관련 클래스: com.qcloud.cos.auth.\* 서브 패키지.
 - 이상 경고 관련 클래스: com.qcloud.cos.exception.\* 서브 패키지.
 - 요청 관련 클래스: com.qcloud.cos.model.\* 서브 패키지.
 - 리전 관련 클래스: com.qcloud.cos.region.\* 서브 패키지.
 - 고급 API 인터페이스: com.qcloud.cos.transfer.\* 서브 패키지.

#### SDK 설치
maven 및 소스 코드 방식으로 Java SDK를 설치할 수 있습니다.

- maven 설치
  maven 프로그램의 pom.xml 파일에 관련 종속을 추가합니다. 내용은 다음과 같습니다.
```shell
<dependency>
       <groupId>com.qcloud</groupId>
       <artifactId>cos_api</artifactId>
       <version>5.6.54</version>
</dependency>
```
- 소스 코드 설치
  Github [XML Java SDK](https://github.com/tencentyun/cos-java-sdk-v5) 또는 [고속 다운로드 주소](https://cos-sdk-archive-1253960454.file.myqcloud.com/cos-java-sdk-v5/latest/cos-java-sdk-v5.zip)에서 소스 코드를 다운로드하고, maven을 사용해 가져옵니다. eclipse를 예로 들면, **File > Import > maven > Existing Maven Projects**를 순서대로 선택합니다.

#### SDK 언마운트

pom 종속 또는 소스 코드를 삭제하면 SDK를 언마운트할 수 있습니다.

## 사용하기

COS Java SDK를 사용한 클라이언트 초기화, 버킷 생성, 버킷 리스트 조회, 객체 업로드, 객체 리스트 조회, 객체 다운로드, 객체 삭제 등의 기본 작업 방법은 아래와 같습니다. 예시에 나오는 클래스는 IDE에서 해당 클래스를 클릭하면 모든 필드와 함수에 대한 정의를 확인할 수 있으며, 클래스에 자세한 주석이 포함되어 있습니다.


### 클래스 이름 가져오기

COS Java SDK의 패키지 이름은 `com.qcloud.cos.*`입니다. Eclipse 또는 Intellij 등의 IDE 툴로 프로그램 실행에 필요한 클래스를 가져올 수 있습니다.

### 클라이언트 초기화

COS 서비스와 관련된 모든 요청을 실행하기 전에 COSClient 클래스 객체를 생성해야 합니다. COSClient는 COS API 인터페이스를 호출하는 객체입니다.

>!COSClient는 스레드 보안 클래스로, 멀티 스레드가 동일한 인스턴스에 액세스하는 것을 허용합니다. 인스턴스 내부는 하나의 연결 풀을 유지하기 때문에 여러 인스턴스를 생성하면 프로그램 리소스가 소진될 수 있습니다. 따라서 **프로그램 라이프사이클 내에 1개의 인스턴스만 유지**하고, 다시 사용하지 않는 인스턴스는 shutdown을 호출해 비활성화하시기 바랍니다. 인스턴스를 생성해야 하는 경우, 먼저 기존 인스턴스를 비활성화하십시오.

영구 키를 사용해 COSClient를 초기화하려면 먼저 CAM 콘솔의 [API 키 관리](https://console.cloud.tencent.com/cam/capi) 페이지에서 APPId, SecretId, SecretKey를 획득합니다. 영구 키 사용은 대부분의 응용 시나리오에 적용할 수 있으며, 참고 예시는 다음과 같습니다.

[//]: # ".cssg-snippet-global-init"
```java
// 1 사용자의 개인 정보(secretId, secretKey)를 초기화합니다.
// SECRETID와 SECRETKEY는 CAM 콘솔 https://console.cloud.tencent.com/cam/capi에 로그인하여 조회 및 관리하십시오.
String secretId = "SECRETID";
String secretKey = "SECRETKEY";
COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);
// 2 bucket의 리전 설정, COS 리전의 약칭은 https://intl.cloud.tencent.com/document/product/436/6224를 참고하십시오.
// clientConfig에 region, https(기본값: http), 타임아웃, 프록시 등을 설정하는 set 메소드가 포함되어 있습니다. 사용 시 소스 코드 또는 FAQ의 Java SDK 부분을 참고하십시오.
Region region = new Region("COS_REGION");
ClientConfig clientConfig = new ClientConfig(region);
// https 프로토콜 설정 및 사용을 권장합니다.
// 버전 5.6.54부터 https가 기본적으로 사용됩니다.
clientConfig.setHttpProtocol(HttpProtocol.https);
// 3 cos 클라이언트 생성.
COSClient cosClient = new COSClient(cred, clientConfig);
```

임시 키를 사용해 COSClient를 초기화할 수도 있습니다. 임시 키 생성 및 사용에 대한 자세한 내용은 [임시 키 생성 및 사용 가이드](https://intl.cloud.tencent.com/document/product/436/14048)를 참고하십시오. 참고 예시는 다음과 같습니다.

[//]: # ".cssg-snippet-global-init-sts"
```java
// 1 획득한 임시 키(tmpSecretId, tmpSecretKey, sessionToken) 전송
String tmpSecretId = "SECRETID";
String tmpSecretKey = "SECRETKEY";
String sessionToken = "TOKEN";
BasicSessionCredentials cred = new BasicSessionCredentials(tmpSecretId, tmpSecretKey, sessionToken);
// 2 bucket의 리전 설정. COS 리전의 약칭은 https://intl.cloud.tencent.com/document/product/436/6224를 참고하십시오.
// clientConfig에 region, https(기본값: http), 타임아웃, 프록시 등을 설정하는 set 메소드가 포함되어 있습니다. 사용 시 소스 코드 또는 FAQ의 Java SDK 부분을 참고하십시오.
Region region = new Region("COS_REGION");
ClientConfig clientConfig = new ClientConfig(region);
// 3 cos 클라이언트 생성.
COSClient cosClient = new COSClient(cred, clientConfig);
```


ClientConfig 클래스는 정보 설정 클래스입니다. 주요 구성은 다음과 같습니다.

|  멤버 이름 | 설정 방법            | 설명                                                         | 유형    |
| ------------ | ------------------- | ------------------------------------------------------------ | ------- |
| region   | 구조 함수 또는 set 메소드 | 버킷이 위치한 리전. COS 리전의 약칭은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224) 문서를 참고하십시오. | Region  |
| httpProtocol       | set 메소드 |  요청 시 사용하는 프로토콜, 기본적으로 HTTP 프로토콜을 사용해 COS와 통신됩니다.| HttpProtocol  |
| signExpired      | set 메소드 | 서명 요청 유효 시간, 단위: 초, 기본값: 3600s   | int |
| connectionTimeout      | set 메소드 | COS 서비스 연결의 타임아웃 시간, 단위: 밀리초, 기본값: 30000ms        | int |
| socketTimeout      | set 메소드 |  클라이언트가 데이터를 읽는 타임아웃 시간, 단위: 밀리초, 기본값: 30000ms          | int |
| httpProxyIp       | set 메소드 | 프록시 서버의 IP | String  |
| httpProxyPort    |  set 메소드 | 프록시 서버의 포트 | int  |


### 버킷 생성

리전 및 버킷 이름을 확인한 후, 다음 예시를 참고하여 버킷을 생성합니다.

[//]: # ".cssg-snippet-put-bucket-and-grant-acl"
```java
String bucket = "examplebucket-1250000000"; //버킷 이름, 형식: BucketName-APPID
CreateBucketRequest createBucketRequest = new CreateBucketRequest(bucket);
// bucket의 권한을 Private(개인 읽기/쓰기)으로 설정. 기타 옵션으로 PublicRead(공개 읽기 및 개인 쓰기), PublicReadWrite(공개 읽기/쓰기)가 있습니다.
createBucketRequest.setCannedAcl(CannedAccessControlList.Private);
try{
    Bucket bucketResult = cosClient.createBucket(createBucketRequest);
} catch (CosServiceException serverException) {
    serverException.printStackTrace();
} catch (CosClientException clientException) {
    clientException.printStackTrace();
}
```

### 버킷 리스트 조회

사용자의 버킷 리스트를 조회합니다. 참고 예시는 다음과 같습니다.

[//]: # ".cssg-snippet-get-service"
```java
List<Bucket> buckets = cosClient.listBuckets();
for (Bucket bucketElement : buckets) {
    String bucketName = bucketElement.getName();
    String bucketLocation = bucketElement.getLocation();
}
```

### 객체 업로드

로컬 파일 또는 입력 스트림의 크기를 알고 있는 콘텐츠를 COS에 업로드합니다. 20M 이하의 크기가 작은 이미지 파일 업로드에 적합하며, 최대 5GB 이하의 파일 업로드를 지원합니다. 5GB 이상의 파일은 반드시 멀티파트 업로드 또는 고급 API 인터페이스로 업로드하십시오.

>? 고급 API 인터페이스는 com.qcloud.cos.transfer.\* 서브 패키지 안에 있습니다.

- 로컬 파일이 대부분 20M 이상인 경우, 고급 API 인터페이스 사용을 참고하여 업로드하시기 바랍니다.
- COS에 동일한 Key의 객체가 존재하는 경우, 업로드 시 기존 객체를 덮어씁니다.
- 디렉터리 객체 생성은 [SDK는 어떻게 디렉터리를 생성하나요?](https://intl.cloud.tencent.com/document/product/436/38956#sdk-.E5.A6.82.E4.BD.95.E5.88.9B.E5.BB.BA.E7.9B.AE.E5.BD.95.EF.BC.9F)를 참고하십시오.
- 객체 키(Key)는 버킷에 있는 객체의 고유 식별자입니다. 예를 들어 객체의 액세스 도메인 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/images/picture.jpg`에서 객체 키는 images/picture.jpg입니다. 자세한 내용은 [객체 키](https://intl.cloud.tencent.com/document/product/436/13324)의 설명을 참고하십시오.


5GB 이하의 파일 업로드에 대한 참고 예시는 다음과 같습니다.

[//]: # ".cssg-snippet-put-object"
```java
// 업로드할 파일 지정
File localFile = new File(localFilePath);
// 파일을 저장할 버킷 지정
String bucketName = "examplebucket-1250000000";
// 파일을 업로드할 COS 경로(즉, 객체 키) 지정, 예를 들어 객체 키가 folder/picture.jpg인 경우 picture.jpg 파일을 folder 경로에 업로드한다는 의미입니다.
String key = "exampleobject";
PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);
PutObjectResult putObjectResult = cosClient.putObject(putObjectRequest);
```

### 객체 리스트 조회

버킷의 객체 리스트 조회에 대한 참고 예시는 다음과 같습니다.

[//]: # ".cssg-snippet-get-bucket"
```java
// Bucket 이름 생성 형식은 BucketName-APPID이며, 이 곳에 입력하는 버킷 이름은 반드시 해당 형식을 따라야 합니다.
String bucketName = "examplebucket-1250000000";
ListObjectsRequest listObjectsRequest = new ListObjectsRequest();
// bucket 이름 설정
listObjectsRequest.setBucketName(bucketName);
// prefix는 나열된 object의 key가 prefix로 시작함을 의미합니다.
listObjectsRequest.setPrefix("images/");
// delimiter는 세퍼레이터를 의미합니다. /로 설정하면 현재 디렉터리의 object를 나열하고, 공백으로 설정하면 전체 object를 나열합니다.
listObjectsRequest.setDelimiter("/");
// 순회할 객체의 최대 수량을 설정합니다. listobject 1회당 최대 1000개까지 지원합니다.
listObjectsRequest.setMaxKeys(1000);
ObjectListing objectListing = null;
do {
    try {
        objectListing = cosClient.listObjects(listObjectsRequest);
    } catch (CosServiceException e) {
        e.printStackTrace();
        return;
    } catch (CosClientException e) {
        e.printStackTrace();
        return;
    }
    // common prefix는 delimiter로 잘린 경로를 표시합니다. 예를 들어 delimiter를 /로 설정하면 common prefix는 모든 서브 디렉터리의 경로를 표시합니다.
    List<String> commonPrefixs = objectListing.getCommonPrefixes();

    // object summary는 나열된 모든 object 리스트를 표시합니다.
    List<COSObjectSummary> cosObjectSummaries = objectListing.getObjectSummaries();
    for (COSObjectSummary cosObjectSummary : cosObjectSummaries) {
        // 파일의 경로 key
        String key = cosObjectSummary.getKey();
        // 파일의 etag
        String etag = cosObjectSummary.getETag();
        // 파일의 길이
        long fileSize = cosObjectSummary.getSize();
        // 파일의 스토리지 유형
        String storageClasses = cosObjectSummary.getStorageClass();
    }

    String nextMarker = objectListing.getNextMarker();
    listObjectsRequest.setMarker(nextMarker);
} while (objectListing.isTruncated());
```

### 객체 다운로드
객체를 업로드한 후, 동일한 key를 사용하여 GetObject 인터페이스를 호출해 객체를 로컬에 다운로드할 수 있습니다. 또한 사전 서명 링크를 생성해 기타 터미널에 공유하여 다운로드할 수도 있습니다. 다운로드 시 method를 GET으로 지정합니다. 자세한 내용은 [사전 서명 URL](https://intl.cloud.tencent.com/document/product/436/31536)을 참고하십시오. 단, 파일을 개인 읽기 권한으로 설정한 경우 사전 서명 링크의 유효 기간에 주의하십시오.
파일을 로컬 지정 경로에 다운로드하는 참고 예시는 다음과 같습니다.

[//]: # ".cssg-snippet-get-object"
```java
// Bucket 이름 생성 형식은 BucketName-APPID이며, 이 곳에 입력하는 버킷 이름은 반드시 해당 형식을 따라야 합니다.
String bucketName = "examplebucket-1250000000";
// 파일이 있는 COS 경로(즉, 객체 키) 지정. 예를 들어 객체 키가 folder/picture.jpg인 경우 다운로드할 picture.jpg 파일이 folder 경로에 있다는 것을 의미합니다.
String key = "exampleobject";
// 방법1: 다운로드 입력 스트림 획득
GetObjectRequest getObjectRequest = new GetObjectRequest(bucketName, key);
COSObject cosObject = cosClient.getObject(getObjectRequest);
COSObjectInputStream cosObjectInput = cosObject.getObjectContent();
// 객체의 CRC64 다운로드
String crc64Ecma = cosObject.getObjectMetadata().getCrc64Ecma();
// 입력 스트림 비활성화
cosObjectInput.close();

// 방법2: 파일을 로컬 경로에 다운로드(예: D드라이브의 특정 디렉터리)
String outputFilePath = "exampleobject";
File downFile = new File(outputFilePath);
getObjectRequest = new GetObjectRequest(bucketName, key);
ObjectMetadata downObjectMeta = cosClient.getObject(getObjectRequest, downFile);
```

### 객체 삭제

COS에 저장된 지정 경로의 객체를 삭제하는 코드는 다음과 같습니다.

[//]: # ".cssg-snippet-delete-object"
```java
// Bucket 이름 생성 형식은 BucketName-APPID이며, 이 곳에 입력하는 버킷 이름은 반드시 해당 형식을 따라야 합니다.
String bucketName = "examplebucket-1250000000";
// 삭제할 파일이 있는 COS 경로(즉, 객체 키) 지정. 예를 들어 객체 키가 folder/picture.jpg인 경우 folder 경로에 있는 picture.jpg 파일을 삭제한다는 의미입니다.
String key = "exampleobject";
cosClient.deleteObject(bucketName, key);
```

### 요청 재시도 기본 정책

SDK로 생성한 cosClient가 발송한 요청은 기본적으로 응답 오류 요청에 대해 재시도를 진행합니다. 재시도 규칙은 다음과 같습니다.
- 재시도 횟수: 기본값은 3이며, clientConfig.setMaxErrorRetry를 통해 설정할 수 있습니다.
0으로 설정하면 모든 유형의 요청 오류에 대해 재시도하지 않습니다.
- 재시도하는 오류 유형: 클라이언트 이상 경고 중에서 IOException 오류가 보고되는 모든 오류 및 서버 이상 경고 중에서 상태 코드가 500, 502, 503, 504인 오류

사용자의 필요에 따라 재시도 정책을 설정할 수 있습니다. 코드는 다음과 같습니다.

재시도 횟수 설정:

[//]: # ".cssg-snippet-error-retry"
```java
Region region = new Region("COS_REGION");
ClientConfig clientConfig = new ClientConfig(region);
// 최대 재시도 횟수 4로 설정
clientConfig.setMaxErrorRetry = 4;
```

재시도 정책 설정:

[//]: # ".cssg-snippet-retry-policy"
```java
// 사용자 정의 재시도 정책
public class OnlyIOExceptionRetryPolicy extends RetryPolicy {
    @Override
    public <X extends CosServiceRequest> boolean shouldRetry(CosHttpRequest<X> request,
            HttpResponse response,
            Exception exception,
            int retryIndex) {
        // 클라이언트의 IOException 이상 경고인 경우 재시도하며, 그렇지 않은 경우 재시도하지 않습니다.
        if (exception.getCause() instanceof IOException) {
            return true;
        }
        return false;
    }
}

Region region = new Region("COS_REGION");
ClientConfig clientConfig = new ClientConfig(region);
RetryPolicy myRetryPolicy = new OnlyIOExceptionRetryPolicy();
// 사용자 정의한 재시도 정책 설정
clientConfig.setRetryPolicy(myRetryPolicy);
```

### 클라이언트 비활성화

cosClient를 비활성화하고 HTTP로 연결된 백그라운드 관리 스레드를 릴리스하는 코드는 다음과 같습니다.
```java
// 클라이언트 비활성화(백그라운드 스레드 비활성화)
cosClient.shutdown();
```

## FAQ

사용 과정 중 발생한 일반적인 문제에 대한 해결 방안은 [Java SDK FAQ](https://intl.cloud.tencent.com/document/product/436/38956)를 참고하시기 바랍니다.
