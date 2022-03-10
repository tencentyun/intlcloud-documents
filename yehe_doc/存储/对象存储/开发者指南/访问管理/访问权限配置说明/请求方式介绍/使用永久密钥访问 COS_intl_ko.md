## 배경 소개

RESTful API를 통해 COS(Cloud Object Storage)에 대한 HTTP 익명 요청 또는 HTTP 서명 요청을 제안할 수 있습니다. 익명 요청은 일반적으로 정적 웹 사이트 호스팅과 같이 공개 액세스가 필요한 시나리오에서 사용되며 대부분의 시나리오는 서명된 요청을 통해 완료해야 합니다.

서명된 요청은 익명 요청에 비해 서명 값을 하나 더 가지고 있으며 서명은 키(SecretId/SecretKey)와 요청 정보를 기반으로 암호화되어 생성된 문자열입니다. SDK는 자동으로 서명을 계산하므로 사용자 정보를 초기화할 때 키를 설정하기만 하면 되며 서명 계산은 신경 쓰지 않아도 됩니다. RESTful API를 통해 발송된 요청의 경우 서명 알고리즘에 따라 서명을 계산하고 요청에 추가해야 합니다.

## 영구 키 가져오기

CAM 콘솔의 [API 키 관리](https://console.cloud.tencent.com/cam/capi) 페이지에서 영구 키를 얻을 수 있으며 영구 키는 계정의 영구 신분을 나타내는 SecretId 및 SecretKey를 포함하며 만료되지 않습니다.
- SecretId: API 호출자를 식별하기 위해 사용합니다.
- SecretKey: 서명 문자열을 암호화하고 서버에서 서명 문자열을 인증하는 데 사용되는 키입니다.


## 영구 키를 사용한 COS 액세스

### API 요청을 통해 COS 액세스

API 요청을 사용할 때는 프라이빗 버킷에 대해 서명된 요청을 사용해야 합니다. 영구 키를 통해 서명을 생성하고 이를 Authorization 헤더에 넣어 서명 요청을 형성합니다. 요청이 COS로 전송되고 COS는 서명이 요청과 일치하는지 인증합니다.

>? 서명 생성 알고리즘이 복잡하므로  SDK를 직접 사용하여 요청을 제안하고 이 링크를 생략하는 것이 좋습니다.
>

1. 영구 키로 서명 생성
서명 알고리즘에 대한 소개는 [서명 요청](https://intl.cloud.tencent.com/document/product/436/7778) 문서를 참고하십시오. COS에서도 서명 생성 툴을 제공하고 있으며, SDK를 통해서도 서명을 생성할 수 있습니다. [SDK 서명 구현](https://intl.cloud.tencent.com/document/product/436/7778#sdk-.E7.AD.BE.E5.90.8D.E5.AE.9E.E7.8E.B0)을 참고하십시오. 자체 프로그램을 작성하여 서명을 생성할 수도 있지만 서명 알고리즘은 더 복잡하기 때문에 이 방법은 일반적으로 권장되지 않습니다.
2. Authorization 헤더 입력
API 요청을 제안할 때 표준 Http Authorization 헤더에 서명을 입력합니다. 다음은 GetObject 요청의 예시입니다.
```
GET /<ObjectKey> HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: q-sign-algorithm=sha1&q-ak=SecretId&q-sign-time=KeyTime&q-key-time=KeyTime&q-header-list=HeaderList&q-url-param-list=UrlParamList&q-signature=Signature
```

### SDK 툴을 통해 COS 액세스

1. 영구 키로 신분 정보 초기화
SDK 툴을 설치한 후, 먼저 사용자 신분 정보를 초기화하고 루트 계정 또는 서브 계정의 영구 키(SecretId 및 SecretKey)를 입력해야 합니다.
2. SDK를 직접 사용하여 COS 요청
SDK 툴이 사용자를 대신하여 키를 통해 서명을 생성하고 COS에 요청을 제안하기 때문에 초기화 후 SDK 툴을 사용하여 API 요청처럼 직접 서명을 생성하는 대신 업로드 및 다운로드와 같은 기본 작업을 직접 수행할 수 있습니다. 

예를 들어 다음 Java SDK 코드, 더 많은 언어 demo는 [SDK 개요](https://intl.cloud.tencent.com/document/product/436/6474)의 시작하기 문서를 참고하십시오.
```
// 1 사용자의 개인 정보(secretId, secretKey)를 초기화합니다.
// SECRETID와 SECRETKEY는 CAM 콘솔 https://console.cloud.tencent.com/cam/capi에 로그인하여 조회 및 관리
String secretId = "SECRETID";
String secretKey = "SECRETKEY";
COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);
// 2 bucket의 리전 설정. COS 리전의 약칭은 https://cloud.tencent.com/document/product/436/6224 참고 바랍니다. 
// clientConfig에 region, https(기본값: http), 타임아웃, 프록시 등을 설정하는 set 메소드가 포함되어 있습니다. 사용 시 소스 코드 또는 FAQ의 Java SDK 부분을 참고하십시오.
Region region = new Region("COS_REGION");
ClientConfig clientConfig = new ClientConfig(region);
// https 프로토콜 설정 및 사용 권장
// 버전 5.6.54부터 https가 기본적으로 사용됨
clientConfig.setHttpProtocol(HttpProtocol.https);
// 3 cos 클라이언트 생성.
COSClient cosClient = new COSClient(cred, clientConfig);

```


