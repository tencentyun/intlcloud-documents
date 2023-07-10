## 소개
Java SDK는 객체가 액세스하는 URL의 인터페이스를 제공하며 클라이언트에게 배포하여 익명 다운로드 혹은 배포에 사용할 수 있습니다. 
>! 파일의 권한이 **개인 읽기**일 경우 해당 인터페이스에서 생성된 URL은 리소스 액세스에 직접 사용될 수 없습니다. 
>
생성한 사전 서명된 URL은 프로토콜명(HTTP 혹은 HTTPS)을 포함하며 해당 프로토콜명은 사전 서명을 요청한 COS(Cloud Object Storage) 클라이언트가 설정한 프로토콜과 동일해야 합니다. 구체적인 사용 방법은 요청 예시를 참고 바랍니다. 

## 객체 액세스 URL 획득

#### 메소드 프로토타입

```java
public URL getObjectUrl(String bucketName, String key);
public URL getObjectUrl(String bucketName, String key, String versionId);
```



#### 요청 예시1: 객체 액세스 URL 획득

```java
// getObjectUrl 신분 인증이 필요하지 않습니다.
COSCredentials cred = new AnonymousCOSCredentials();
// bucket의 리전 설정, COS 리전의 약칭은 https://www.qcloud.com/document/product/436/6224 참고 바랍니다. 
ClientConfig clientConfig = new ClientConfig(new Region("ap-guangzhou"));
// 생성된 URL의 프로토콜명 설정
clientConfig.setHttpProtocol(HttpProtocol.https);
// cos 클라이언트 생성
COSClient cosclient = new COSClient(cred, clientConfig);

String key = "picture/photo.jpg";
String bucketName = "examplebucket-1250000000";

System.out.println(cosclient.getObjectUrl(bucketName, key));
```

#### 요청 예시2: 지정 버전의 액세스 URL 획득

```java
// getObjectUrl 신분 인증이 필요하지 않습니다.
COSCredentials cred = new AnonymousCOSCredentials();
// bucket의 리전 설정, COS 리전의 약칭은 https://www.qcloud.com/document/product/436/6224 참고 바랍니다. 
ClientConfig clientConfig = new ClientConfig(new Region("ap-guangzhou"));
// 생성된 URL의 프로토콜명 설정
clientConfig.setHttpProtocol(HttpProtocol.https);
// cos 클라이언트 생성
COSClient cosclient = new COSClient(cred, clientConfig);

String key = "picture/photo.jpg";
String bucketName = "examplebucket-1250000000";
String versionId = "xxxyyyzzz111222333";

System.out.println(cosclient.getObjectUrl(bucketName, key, versionId));
```

#### 요청 예시3: 지정 도메인의 액세스 URL 획득

```java
// getObjectUrl 신분 인증이 필요하지 않습니다.
COSCredentials cred = new AnonymousCOSCredentials();
// bucket의 리전 설정, COS 리전의 약칭은 https://www.qcloud.com/document/product/436/6224 참고 바랍니다. 
ClientConfig clientConfig = new ClientConfig(new Region("ap-guangzhou"));
// 생성된 URL의 프로토콜명 설정
clientConfig.setHttpProtocol(HttpProtocol.https);
// 사용자 정의 도메인 설정
UserSpecifiedEndpointBuilder endpointBuilder = new UserSpecifiedEndpointBuilder("test.endpoint.com", "service.cos.myqcloud.com");
clientConfig.setEndpointBuilder(endpointBuilder);
// cos 클라이언트 생성
COSClient cosclient = new COSClient(cred, clientConfig);

String key = "picture/photo.jpg";
String bucketName = "examplebucket-1250000000";
String versionId = "xxxyyyzzz111222333";

System.out.println(cosclient.getObjectUrl(bucketName, key, versionId));
```

#### 매개변수 설명

| 매개변수 이름   | 매개변수 설명         |유형       | 필수 입력 여부         | 
| --------- | -------------- |---------- | ----------- |
| Bucket    | 버킷 이름. BucketName-APPID로 구성 |  String |  예 | 
| key             |객체 키(Key)는 버킷에 있는 객체의 고유 식별자임. 자세한 내용은 [객체 키](https://intl.cloud.tencent.com/document/product/436/13324)를 참고 바랍니다. | String | 예 | 
| VersionId | 버킷에서 버전 제어를 활성화할 경우 객체의 버전 넘버를 지정합니다.  | String |아니요|

