## 소개
Java SDK는 사전 서명된 URL 요청을 획득하거나 서명 인터페이스를 생성하여 클라이언트에 배포할 수 있습니다. 이는 다운로드 또는 업로드에 사용됩니다. 파일 권한이 개인 읽기인 경우 사전 서명된 링크에 유효 시간이 있으므로 주의하시기 바랍니다.
생성된 사전 서명된 URL은 프로토콜명 (HTTP 또는 HTTPS)을 포함합니다. 해당 프로토콜명과 사전 서명을 요청한 COS(Cloud Object Storage) 클라이언트가 설정한 프로토콜은 일치합니다.
구체적인 사용 방법은 요청 예시를 참고하십시오.

>?
> - 사용자는 임시 키를 사용하여 사전 서명을 생성하고, 임시 승인을 통해 사전 서명 업로드 및 다운로드 요청의 보안성을 강화할 것을 권장합니다. 임시 키 신청 시, [최소 권한의 원칙 설명](https://intl.cloud.tencent.com/document/product/436/32972)을 준수하여 타깃 버킷이나 객체 이외의 리소스가 유출되지 않도록 하시기 바랍니다.
> - 사전 서명 생성을 위해 영구 키를 사용해야 하는 경우, 리스크 방지를 위해 영구 키 권한을 업로드 또는 다운로드 작업으로 제한할 것을 권장합니다.
> 


## 사전 서명된 URL 요청 가져오기 

#### 메소드 프로토타입

```java
public URL generatePresignedUrl(GeneratePresignedUrlRequest req) throws CosClientException
```

#### 매개변수 설명

| 매개변수 이름 | 설명         | 유형                        |
| -------- | ------------ | --------------------------- |
| req      | 사전 서명 요청 클래스 | GeneratePresignedUrlRequest |

Request 멤버 설명:

| Request 멤버    | 설정 메소드            | 설명                                                         | 유형                    |
| --------------- | ------------------- | ------------------------------------------------------------ | ----------------------- |
| method          | 구조 함수 또는 set 메소드 | HTTP 메소드, 옵션: GET, POST, PUT, DELETE, HEAD                | HttpMethodName          |
| bucketName      | 구조 함수 또는 set 메소드 | 버킷 이름, 버킷의 이름 생성 포맷은 BucketName-APPID이며, 자세한 내용은 [버킷 이름 생성 규칙](https://intl.cloud.tencent.com/document/product/436/13312)을 참고하십시오. | String |
| key             | 구조 함수 또는 set 메소드 | 객체 키(Key)는 버킷에 있는 객체의 고유 식별자입니다. 자세한 내용은 [객체 키](https://intl.cloud.tencent.com/document/product/436/13324)를 참고하십시오. | String                  |
| expiration      | set 메소드            | 서명 만료 시간을 임의로 설정할 수 있으며 설정하지 않으면 기본값은 1시간입니다.              | Date                    |
| contentType     | set 메소드            | 서명 요청의 Content-Type                                | String                  |
| contentMd5      | set 메소드            | 서명 요청의 Content-Md5                                 | String                  |
| responseHeaders | set 메소드            | 서명 다운로드 요청 중 덮어쓰고 반환할 HTTP 헤더                      | ResponseHeaderOverrides |
| versionId | set 메소드            | 버킷에 여러 버전을 활성화할 경우, 객체의 버전 번호 지정                       | String |


#### 예시 1

영구 키를 사용해 서명이 있는 다운로드 링크를 생성하는 예시 코드는 다음과 같습니다.

[//]: # (.cssg-snippet-get-presign-download-url)
```java
// 영구 키 정보 초기화
// SECRETID와 SECRETKEY는 CAM 콘솔에 로그인하여 조회 및 관리합니다.
String secretId = "SECRETID";
String secretKey = "SECRETKEY";
COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);
Region region = new Region("COS_REGION");
ClientConfig clientConfig = new ClientConfig(region);
// https 프로토콜을 사용하는 URL을 생성할 경우, 이 행을 설정하길 권장합니다.
// clientConfig.setHttpProtocol(HttpProtocol.https);
// cos 클라이언트 생성
COSClient cosClient = new COSClient(cred, clientConfig);
// 버킷의 이름 생성 포맷은 BucketName-APPID이며, 입력할 버킷 이름은 반드시 본 포맷을 따라야 합니다.
String bucketName = "examplebucket-1250000000";
// 여기서 key는 객체 키로, 버킷 내 객체의 고유 식별자입니다.
String key = "exampleobject";
GeneratePresignedUrlRequest req =
        new GeneratePresignedUrlRequest(bucketName, key, HttpMethodName.GET);
// 서명 만료 시간 설정(옵션), 설정하지 않을 경우 기본적으로 ClientConfig의 서명 만료 시간(1시간)을 사용합니다.
// 임의로 시간을 설정할 수 있으며 만료 시간은 10분에서 3일 사이로 설정하는 것을 권장합니다.
// 본 예시에서는 30분 후 만료로 설정합니다.
Date expirationDate = new Date(System.currentTimeMillis() + 30L * 60L * 1000L);
req.setExpiration(expirationDate);

// 이번 요청의 매개변수를 입력합니다.
req.addRequestParameter("param1", "value1");
// 이번 요청의 헤더를 입력합니다. Host 헤더는 자동으로 완성되며 입력할 필요가 없습니다.
req.putCustomRequestHeader("header1", "value1");

URL url = cosClient.generatePresignedUrl(req);
System.out.println(url.toString());
cosClient.shutdown();
```

#### 예시 2

영구 키를 사용해 무기한 유효 서명이 있는 다운로드 링크를 생성하는 예시 코드는 다음과 같습니다.

```java
// 영구 키 정보 초기화
// SECRETID와 SECRETKEY는 CAM 콘솔에 로그인하여 조회 및 관리합니다.
String secretId = "SECRETID";
String secretKey = "SECRETKEY";
COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);
Region region = new Region("COS_REGION");
ClientConfig clientConfig = new ClientConfig(region);
// https 프로토콜을 사용하는 URL을 생성할 경우, 이 행을 설정하길 권장합니다.
// clientConfig.setHttpProtocol(HttpProtocol.https);
// cos 클라이언트 생성.
COSClient cosClient = new COSClient(cred, clientConfig);
// 버킷의 이름 생성 포맷은 BucketName-APPID이며, 입력할 버킷 이름은 반드시 본 포맷을 따라야 합니다.
String bucketName = "examplebucket-1250000000";
// 여기서 key는 객체 키로, 버킷 내 객체의 고유 식별자입니다.
String key = "exampleobject";

GeneratePresignedUrlRequest req =
        new GeneratePresignedUrlRequest(bucketName, key, HttpMethodName.GET);
// 서명 만료 기간을 아주 먼 미래의 날짜로 설정합니다. 예시: 3000년 12월 31일
Date expirationDate = new Date(3000, 12, 31);
req.setExpiration(expirationDate);

// 이번 요청의 매개변수를 입력합니다.
req.addRequestParameter("param1", "value1");
// 이번 요청의 헤더를 입력합니다. Host 헤더는 자동으로 완성되며 입력할 필요가 없습니다.
req.putCustomRequestHeader("header1", "value1");

URL url = cosClient.generatePresignedUrl(req);
System.out.println(url.toString());
cosClient.shutdown();
```

#### 예시 3

임시 키를 사용해 서명이 있는 다운로드 링크를 생성하고, 반환할 일부 공용 헤더(예: content-type, content-language)를 덮어쓰도록 설정합니다. 예시 코드는 다음과 같습니다.

[//]: # (.cssg-snippet-get-presign-download-url-override-headers)
```java
// 획득한 임시 키(tmpSecretId, tmpSecretKey, sessionToken) 전송
String tmpSecretId = "SECRETID";
String tmpSecretKey = "SECRETKEY";
String sessionToken = "TOKEN";
COSCredentials cred = new BasicSessionCredentials(tmpSecretId, tmpSecretKey, sessionToken);
// bucket 리전 설정. COS 리전의 약칭은 https://cloud.tencent.com/document/product/436/6224를 참고하십시오.
// clientConfig에 region, https(기본값: http), 타임아웃, 프록시 등을 설정하는 set 메소드가 포함되어 있습니다. 사용 시 소스 코드 또는 FAQ의 Java SDK 부분을 참고하십시오.
Region region = new Region("COS_REGION");
ClientConfig clientConfig = new ClientConfig(region);
// https 프로토콜을 사용하는 URL을 생성할 경우, 이 행을 설정하길 권장합니다.
// clientConfig.setHttpProtocol(HttpProtocol.https);
// cos 클라이언트 생성
COSClient cosClient = new COSClient(cred, clientConfig);
// 버킷의 이름 생성 포맷: BucketName-APPID 
String bucketName = "examplebucket-1250000000";
// 여기서 key는 객체 키로, 버킷 내 객체의 고유 식별자입니다.
String key = "exampleobject";
GeneratePresignedUrlRequest req =
        new GeneratePresignedUrlRequest(bucketName, key, HttpMethodName.GET);
// 다운로드 시 반환하는 http 헤더 설정
ResponseHeaderOverrides responseHeaders = new ResponseHeaderOverrides();
String responseContentType = "image/x-icon";
String responseContentLanguage = "zh-CN";
// 반환 헤더에 포함되는 파일명 정보 설정
String responseContentDispositon = "filename=\"exampleobject\"";
String responseCacheControl = "no-cache";
String cacheExpireStr =
        DateUtils.formatRFC822Date(new Date(System.currentTimeMillis() + 24L * 3600L * 1000L));
responseHeaders.setContentType(responseContentType);
responseHeaders.setContentLanguage(responseContentLanguage);
responseHeaders.setContentDisposition(responseContentDispositon);
responseHeaders.setCacheControl(responseCacheControl);
responseHeaders.setExpires(cacheExpireStr);
req.setResponseHeaders(responseHeaders);
// 서명 만료 시간 설정(옵션). 설정하지 않을 경우 기본적으로 ClientConfig의 서명 만료 시간(1시간)을 사용합니다.
// 본 예시에서는 30분 후 만료로 설정합니다.
Date expirationDate = new Date(System.currentTimeMillis() + 30L * 60L * 1000L);
req.setExpiration(expirationDate);

// 이번 요청의 매개변수를 입력합니다.
req.addRequestParameter("param1", "value1");
// 이번 요청의 헤더를 입력합니다. Host 헤더는 자동으로 완성되며 입력할 필요가 없습니다.
req.putCustomRequestHeader("header1", "value1");

URL url = cosClient.generatePresignedUrl(req);
System.out.println(url.toString());
cosClient.shutdown();
```

#### 예시 4

공개 읽기 Bucket(익명 읽기 가능)의 서명이 필요 없는 링크를 생성하는 예시 코드는 다음과 같습니다.

[//]: # (.cssg-snippet-get-presign-download-url-public)
```java
// 익명 요청 서명을 생성하려면 익명의 cosClient를 다시 초기화해야 합니다.
// 사용자 자격 정보 초기화. 익명 자격은 SecretId, SecretKey 등의 키 정보를 전달할 필요 없습니다.
COSCredentials cred = new AnonymousCOSCredentials();
// bucket 리전 설정. COS 리전의 약칭은 https://cloud.tencent.com/document/product/436/6224를 참고하십시오.
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing"));
// cos 클라이언트 생성
COSClient cosClient = new COSClient(cred, clientConfig);
// bucket 이름에는 반드시 appid를 포함
String bucketName = "examplebucket-1250000000";

// 여기서 key는 객체 키로, 버킷 내 객체의 고유 식별자입니다.
String key = "exampleobject";
GeneratePresignedUrlRequest req =
        new GeneratePresignedUrlRequest(bucketName, key, HttpMethodName.GET);
URL url = cosClient.generatePresignedUrl(req);
System.out.println(url.toString());
cosClient.shutdown();
```

#### 예시 5

클라이언트에 직접 배포해 파일을 업로드할 수 있는 사전 서명된 업로드 링크를 생성하는 예시 코드는 다음과 같습니다.

[//]: # (.cssg-snippet-get-presign-upload-url)
```java
// 버킷의 이름 생성 포맷은 BucketName-APPID이며, 입력할 버킷 이름은 반드시 본 포맷을 따라야 합니다.
String bucketName = "examplebucket-1250000000";
// 여기서 key는 객체 키로, 버킷 내 객체의 고유 식별자입니다.
String key = "exampleobject";
// 서명 만료 시간 설정(옵션). 설정하지 않을 경우 기본적으로 ClientConfig의 서명 만료 시간(1시간)을 사용합니다.
// 본 예시에서는 30분 후 만료로 설정합니다.
Date expirationTime = new Date(System.currentTimeMillis() + 30L * 60L * 1000L);

// 이번 요청의 header를 입력합니다. Host 헤더는 자동으로 완성되며 기타 헤더만 입력하면 됩니다.
Map<String, String> headers = new HashMap<String,String>();
// 이번 요청의 params를 입력합니다.
Map<String, String> params = new HashMap<String,String>();

URL url = cosClient.generatePresignedUrl(bucketName, key, expirationTime, HttpMethodName.PUT, headers, params);
System.out.println(url.toString());
cosClient.shutdown();
```

## 서명 생성

COSSigner 클래스는 COS 서명을 구성하는 방법을 제공합니다. 이는 모바일 SDK에 배포하는 데 사용되며, 파일을 업로드 및 다운로드할 수 있습니다. 서명의 경로는 배포 후 작업할 key와 매칭되어야 합니다.

#### 메소드 프로토타입

```java
// COS 서명 구성
// 생성한 서명은 업로드 및 다운로드 작업 시 반드시 해당 header와 param을 수반해야 합니다.
public String buildAuthorizationStr(HttpMethodName methodName, String resouce_path,
        Map<String, String> headerMap, Map<String, String> paramMap, COSCredentials cred,
        Date expiredTime);
```

#### 매개변수 설명

| 매개변수 이름     | 설명                                                         | 유형           |
| ------------ | ------------------------------------------------------------ | -------------- |
| methodName   | HTTP 요청 메소드. PUT, GET, DELETE, HEAD, POST 설정 가능           | HttpMethodName |
| resouce_path | 서명할 경로. 업로드 파일의 key와 동일해야 하며 `/`로 시작해야 합니다.                | HttpMethodName |
| cred         | 키 정보                                                     | COSCredentials |
| expiredTime  | 만료 시간                                                     | Date           |
| headerMap    | 서명할 HTTP Header map, 전달되는 Host, Content-Type, Content-Md5 및 x로 시작하는 header에 서명을 진행합니다. | Map            |
| paramMap     | 서명할 URL Param map                                        | Map            |

#### 반환값
서명 문자열이며, 유형은 String입니다.


#### 예시 1: 업로드 서명 생성

[//]: # (.cssg-snippet-get-authorization-for-upload)
```java
// SECRETID와 SECRETKEY는 CAM 콘솔에 로그인하여 조회 및 관리합니다.
String secretId = "SECRETID";
String secretKey = "SECRETKEY";
COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);
COSSigner signer = new COSSigner();
//만료 시간을 1시간으로 설정
Date expiredTime = new Date(System.currentTimeMillis() + 3600L * 1000L);
// 서명할 key, 생성된 서명은 해당 key 업로드에만 사용 가능합니다.
// 여기서 key는 객체 키로, 버킷 내 객체의 고유 식별자입니다.
String key = "exampleobject";

// 이번 요청의 header를 입력합니다. Host 헤더는 자동으로 완성되며 기타 헤더만 입력하면 됩니다.
Map<String, String> headers = new HashMap<String,String>();
// 이번 요청의 params를 입력합니다.
Map<String, String> params = new HashMap<String,String>();

String sign = signer.buildAuthorizationStr(HttpMethodName.PUT, key, headers, params, cred, expiredTime);
```

#### 예시 2: 다운로드 서명 생성

[//]: # (.cssg-snippet-get-authorization-for-download)
```java
// SECRETID와 SECRETKEY는 CAM 콘솔에 로그인하여 조회 및 관리합니다.
String secretId = "SECRETID";
String secretKey = "SECRETKEY";
COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);
COSSigner signer = new COSSigner();
// 만료 시간을 1시간으로 설정
Date expiredTime = new Date(System.currentTimeMillis() + 3600L * 1000L);
// 서명할 key, 생성된 서명은 해당 key 다운로드에만 사용 가능합니다.
// 여기서 key는 객체 키로, 버킷 내 객체의 고유 식별자입니다.
String key = "exampleobject";

// 이번 요청의 header를 입력합니다. Host 헤더는 자동으로 완성되며 기타 헤더만 입력하면 됩니다.
Map<String, String> headers = new HashMap<String,String>();
// 이번 요청의 params를 입력합니다.
Map<String, String> params = new HashMap<String,String>();

String sign = signer.buildAuthorizationStr(HttpMethodName.GET, key, headers, params, cred, expiredTime);
```

#### 예시 3: 삭제 서명 생성

[//]: # (.cssg-snippet-get-authorization-for-delete)
```java
// SECRETID와 SECRETKEY는 CAM 콘솔에 로그인하여 조회 및 관리합니다.
String secretId = "SECRETID";
String secretKey = "SECRETKEY";
COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);
COSSigner signer = new COSSigner();
// 만료 시간을 1시간으로 설정
Date expiredTime = new Date(System.currentTimeMillis() + 3600L * 1000L);
// 서명할 key, 생성된 서명은 해당 key 삭제에만 사용 가능합니다.
// 여기서 key는 객체 키로, 버킷 내 객체의 고유 식별자입니다.
String key = "exampleobject";

// 이번 요청의 header를 입력합니다. Host 헤더는 자동으로 완성되며 기타 헤더만 입력하면 됩니다.
Map<String, String> headers = new HashMap<String,String>();
// 이번 요청의 params를 입력합니다.
Map<String, String> params = new HashMap<String,String>();

String sign = signer.buildAuthorizationStr(HttpMethodName.DELETE, key, headers, params, cred, expiredTime);
```
