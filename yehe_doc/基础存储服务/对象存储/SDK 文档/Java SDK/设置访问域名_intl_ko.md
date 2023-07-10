## 소개

본 문서는 기본 도메인이 아닌 도메인으로 COS 서비스를 요청하는 방법을 제공합니다.

### 기본 CDN 가속 도메인

#### 기능 설명

COS 콘솔에서 버킷에 기본 CDN 가속 도메인을 활성화한 후 SDK 코드에 해당 도메인을 설정해 편리하게 기본 가속 도메인을 구현할 수 있습니다.
기본 가속 도메인 활성화 방법은 [기본 CDN 가속 도메인 활성화](https://intl.cloud.tencent.com/document/product/436/31505)를 참조하십시오.

#### 방법 모델

```java
void com.qcloud.cos.ClientConfig.setEndPointSuffix(String endPointSuffix)
```

#### 요청 예시

```java
// 1 CDN 가속 도메인으로 사용. COS의 인증 정보로 재발송 불필요
COSCredentials cred = new AnonymousCOSCredentials();
// 2 bucket의 리전 약칭 설정. COS 리전의 약칭은 https://cloud.tencent.com/document/product/436/6224 참조
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing"));
// https 프로토콜 사용 권장
clientConfig.setHttpProtocol(HttpProtocol.https);
// 3 기본 CDN 가속 도메인 확장자 설정
String cdnSuffix = "file.myqcloud.com";
clientConfig.setEndPointSuffix(cdnSuffix);
// 4 cos 클라이언트 생성
COSClient cosclient = new COSClient(cred, clientConfig);
```

#### 매개변수 설명

| 매개변수 이름            | 설명                          | 유형           |
| ------------------ | ---------------------------- | -------------- |
| endPointSuffix     | 도메인 확장자를 설정하여 CDN 가속 도메인 사용 | String         |

### 사용자 정의 CDN 가속 도메인

#### 기능 설명

COS 콘솔에서 버킷에 사용자 정의 CDN 가속 도메인을 설정한 후 SDK 코드에 해당 도메인을 설정해 편리하게 사용자 정의 도메인에 가속 기능을 구현할 수 있습니다. 사용자 정의 CDN 가속 도메인 활성화 방법은 [사용자 정의 CDN 가속 도메인 활성화](https://intl.cloud.tencent.com/document/product/436/31506)를 참조하십시오.

#### 방법 모델

```java
void com.qcloud.cos.ClientConfig.setEndpointBuilder(EndpointBuilder endpointBuilder)
```

#### 요청 예시

```java
// 1 CDN 가속 도메인으로 사용. COS의 인증 정보로 재발송 불필요
COSCredentials cred = new AnonymousCOSCredentials();
// 2 bucket의 리전 약칭 설정. COS 리전의 약칭은 https://cloud.tencent.com/document/product/436/6224 참조
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing"));
// https 프로토콜 사용 권장. https 프로토콜을 사용하는 경우 사용자 정의 도메인에 관련 https 인증서 필요
clientConfig.setHttpProtocol(HttpProtocol.https);
// 3 CDN 사용자 정의 도메인 설정
//  get service 요청은 이 도메인을 사용하며, 이 도메인은 사용자 정의할 수 없음
String serviceApiEndpoint = "service.cos.myqcloud.com";
String cdnEndpoint = "xxx.xxx.com";
UserSpecifiedEndpointBuilder endPointBuilder = new UserSpecifiedEndpointBuilder(cdnEndpoint, serviceApiEndpoint);
clientConfig.setEndpointBuilder(endPointBuilder);
// 4 cos 클라이언트 생성
COSClient cosclient = new COSClient(cred, clientConfig);
```

#### 매개변수 설명

| 매개변수 이름               | 설명                          | 유형                            |
| --------------------- | ---------------------------- | ------------------------------ |
| endPointerBuilder     | 사용자 정의 CDN 가속 도메인 구축 시 사용하는 매개변수  | UserSpecifiedEndpointBuilder   |

UserSpecifiedEndpointBuilder 설명:

| 매개변수 이름                  | 설명                                | 유형                            |
| ------------------------ | ---------------------------------- | ------------------------------ |
| generalApiEndpoint       | 사용자 정의 CDN 가속 도메인 입력                    | String                         |
| getServiceApiEndpoint    | `service.cos.myqcloud.com`만 입력 가능 | String                         |


### 사용자 정의 원본 서버 도메인

#### 기능 설명

COS 콘솔에서 버킷에 사용자 정의 원본 서버 도메인을 설정한 후 SDK 코드에 해당 도메인을 설정해 편리하게 COS 리소스에 액세스할 수 있습니다. 사용자 정의 원본 서버 도메인 설정 방법은 [사용자 정의 원본 서버 도메인](https://intl.cloud.tencent.com/document/product/436/31507)을 참조하십시오.

#### 방법 모델

```java
void com.qcloud.cos.ClientConfig.setEndpointBuilder(EndpointBuilder endpointBuilder)
```

#### 요청 예시

```java
// 1 사용자 자격 정보 초기화(secretId, secretKey)
COSCredentials cred = new BasicCOSCredentials("AKIDXXXXXXXX", "1A2Z3YYYYYYYYYY");
// 2 bucket의 리전 약칭 설정. COS 리전의 약칭은 https://cloud.tencent.com/document/product/436/6224 참조
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing"));
// https 프로토콜 사용 권장
clientConfig.setHttpProtocol(HttpProtocol.https);
// 3 사용자 정의 도메인 설정
//  get service 요청은 이 도메인을 사용하며, 이 도메인은 사용자 정의할 수 없음
String serviceApiEndpoint = "service.cos.myqcloud.com";
String userEndpoint = "xxx.xxx.com";
UserSpecifiedEndpointBuilder endPointBuilder = new UserSpecifiedEndpointBuilder(userEndpoint, serviceApiEndpoint);
clientConfig.setEndpointBuilder(endPointBuilder);
// 4 cos 클라이언트 생성
COSClient cosclient = new COSClient(cred, clientConfig);
```

#### 매개변수 설명

| 매개변수 이름               | 설명                          | 유형                            |
| --------------------- | ---------------------------- | ------------------------------ |
| endPointerBuilder     | 사용자 정의 원본 서버 도메인 구축 시 사용하는 매개변수           | UserSpecifiedEndpointBuilder   |

UserSpecifiedEndpointBuilder 설명:

| 매개변수 이름                  | 설명                                 | 유형                            |
| --------------------- | ------------------------- | ------------------------------ |
| generalApiEndpoint       | 사용자 정의 원본 서버 도메인 입력                        | String      |
| getServiceApiEndpoint    | `service.cos.myqcloud.com`만 입력 가능  | String         |


### 글로벌 가속 도메인

#### 기능 설명

COS 콘솔에서 버킷에 글로벌 가속 도메인을 활성화한 후 SDK 코드에 해당 도메인을 설정해 편리하게 글로벌 가속 기능을 실현할 수 있습니다. 글로벌 가속 기능에 대한 소개는 [글로벌 가속 기능 개요](https://intl.cloud.tencent.com/document/product/436/33409)를 참조하십시오.

#### 방법 모델

```java
void com.qcloud.cos.ClientConfig.setEndPointSuffix(String endPointSuffix)
```

#### 요청 예시

```java
// 1 사용자 자격 정보 초기화(secretId, secretKey)
COSCredentials cred = new BasicCOSCredentials("AKIDXXXXXXXX", "1A2Z3YYYYYYYYYY");
// 2 bucket의 리전 약칭 설정. COS 리전의 약칭은 https://cloud.tencent.com/document/product/436/6224 참조
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing"));
// https 프로토콜 사용 권장
clientConfig.setHttpProtocol(HttpProtocol.https);
// 3 글로벌 가속 도메인 확장자 설정
String cosSuffix = "cos.accelerate.myqcloud.com";
clientConfig.setEndPointSuffix(cosSuffix);
// 4 cos 클라이언트 생성
COSClient cosclient = new COSClient(cred, clientConfig);
```

#### 매개변수 설명

| 매개변수 이름            | 설명                          | 유형           |
| ------------------ | ---------------------------- | -------------- |
| endPointSuffix     | 도메인 확장자를 설정하여 글로벌 가속 도메인 사용 | String         |
