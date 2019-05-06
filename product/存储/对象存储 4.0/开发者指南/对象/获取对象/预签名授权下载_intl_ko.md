## 적용 시나리오

기본적으로 모든 버킷 및 객체는 비공개입니다. 타사에서 객체를 다운로드할 수 있지만 CAM 계정이나 임시 키를 사용하는 것을 원하지 않을 때 다운로드 작업을 위해 사전 서명된 URL로 서명을 타사에게 제출할 수 있습니다. 유효한 사전 서명 URL을 받은 사람은 누구나 객체를 다운로드할 수 있습니다.

사전 서명된 URL을 생성할 때 서명에 객체 키를 포함시켜 지정된 객체만 다운로드할 수 있습니다. SDK에서 사전 서명된 URL의 유효 기간을 지정하여 권한이 없는 사용자가 만료된 URL을 사용할 수 없게 됩니다.

## 사용 방법

### Java SDK 사용

COS의 Java SDK에서 이 방법을 제공하며 [Java SDK API 문서의 사전 서명 생성 부분](https://cloud.tencent.com/document/product/436/12263#.E7.94.9F.E6.88.90.E9.A2.84.E7.AD.BE.E5.90.8D.E9.93.BE.E6.8E.A5)을 참조할 수 있습니다.

#### 절차 설명

1. 클라이언트 cosClient를 초기화합니다.
2. generatePresignedUrl 방법을 실행하여 다운로드 서명을 획득하고 http 방법에 GET을 전달합니다.

#### 예제 코드

(1) 다음 예제 코드는 사전 서명된 다운로드 URL을 생성하는 방법을 보여줍니다.

```java
// 1 사용자 인증 정보(appid, secretId, 및 secretKey)를 초기화합니다.
COSCredentials cred = new BasicCOSCredentials("AKIDXXXXXXXX", "1A2Z3YYYYYYYYYY");
// 2 버킷의 지역을 설정합니다. COS 영역의 약어는 다음 링크를 참조하십시오. https://cloud.tencent.com/document/product/436/6224
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// 3 COS 클라이언트를 생성합니다.
COSClient cosclient = new COSClient(cred, clientConfig);
// 버킷 이름을 설정합니다. 버킷 이름에는 appid가 포함되어야 합니다.
String bucketName = "mybucket-125110000";
String key = "aaa.txt";

GeneratePresignedUrlRequest req =
        new GeneratePresignedUrlRequest(bucketName, key, HttpMethodName.GET);
// 서명 만료 시간을 설정합니다(옵션). 만료 시간은 제한되지 않지만 현재 시간보다 늦어야 합니다. 설정되어 있지 않으면 기본적으로 ClientConfig의 서명 만료 시간(5분)이 사용됩니다.
// 서명을 30분 후 만료되도록 설정합니다.
Date expirationDate = new Date(System.currentTimeMillis() + 30 * 60 * 1000);
req.setExpiration(expirationDate);

URL url = cosclient.generatePresignedUrl(req);
System.out.println(url.toString());
```

(2)`GeneratePresignedUrlRequest`는 content-type, content-disposition과 같이 다운로드를 위한 반환되는 http 헤더 설정을 지원합니다. 예제 코드는 다음과 같습니다.

```java
// 1 사용자 인증 정보(appid, secretId, 및 secretKey)를 초기화합니다.
COSCredentials cred = new BasicCOSCredentials("AKIDXXXXXXXX", "1A2Z3YYYYYYYYYY");
// 2 버킷의 지역을 설정합니다. COS 영역의 약어는 다음 링크를 참조하십시오. https://cloud.tencent.com/document/product/436/6224
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// 3 COS 클라이언트를 생성합니다.
COSClient cosclient = new COSClient(cred, clientConfig);
// 버킷 이름을 설정합니다. 버킷 이름에는 appid가 포함되어야 합니다.
String bucketName = "mybucket-125110000";
String key = "aaa.txt";

GeneratePresignedUrlRequest req =
        new GeneratePresignedUrlRequest(bucketName, key, HttpMethodName.GET);
// 다운로드 시 반환된 HTTP 헤더를 설정합니다.
ResponseHeaderOverrides responseHeaders = new ResponseHeaderOverrides();
String responseContentType = "image/x-icon";
String responseContentLanguage = "zh-CN";
String responseContentDispositon = "filename=\"abc.txt\"";
String responseCacheControl = "no-cache";
String expireStr =
        DateUtils.formatRFC822Date(new Date(System.currentTimeMillis() + 24 * 3600 * 1000));
responseHeaders.setContentType(responseContentType);
responseHeaders.setContentLanguage(responseContentLanguage);
responseHeaders.setContentDisposition(responseContentDispositon);
responseHeaders.setCacheControl(responseCacheControl);
responseHeaders.setExpires(expireStr);
req.setResponseHeaders(responseHeaders);
URL url = cosclient.generatePresignedUrl(req);

System.out.println(url.toString());
```

(3)`GeneratePresignedUrlRequest`는 익명 버킷에 대한 다운로드 URL 생성을 지원합니다. 익명 버킷 다운로드 URL에는 서명이 필요하지 않으므로 키 정보를 입력할 필요가 없습니다. 예제 코드는 다음과 같습니다.

```java
// 1. 익명 버킷의 경우 사용자 인증 정보가 필요하지 않습니다.
COSCredentials cred = new AnonymousCOSCredentials();
// 2 버킷의 지역을 설정합니다. COS 영역의 약어는 다음 링크를 참조하십시오. https://cloud.tencent.com/document/product/436/6224
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// 3 COS 클라이언트를 생성합니다.
COSClient cosclient = new COSClient(cred, clientConfig);
// 버킷 이름을 설정합니다. 버킷 이름에는 appid가 포함되어야 합니다.
String bucketName = "mybucket-125110000";
String key = "aaa.txt";

GeneratePresignedUrlRequest req =
        new GeneratePresignedUrlRequest(bucketName, key, HttpMethodName.GET);
URL url = cosclient.generatePresignedUrl(req);

System.out.println(url.toString());
```

### JavaScript SDK 사용

#### 절차 설명

1. 서명 서버를 준비하고 서명을 얻기 위해 프런트 엔드에 auth.php API를 제공합니다. 자세한 내용은 [백 엔드 서명 예시](https://github.com/tencentyun/cos-js-sdk-v5/tree/master/server)를 참조할 수 있습니다.

2. 테스트 파일 test.html을 생성하고 다음 코드를 작성합니다. 파일을 정적 서버에 두고 `http://127.0.0.1/test.html`로 접근합니다.

#### 예제 코드

다음 예제 코드는 사전 서명된 URL로 다운로드하는 방법을 보여줍니다.

```html
<script src="cos-js-sdk-v5.min.js"></script>
<script>
var Bucket = 'test-1250000000'; // 사용자의 버킷으로 대체합니다.
var Region = 'ap-guangzhou';    // 사용자의 지역으로 대체합니다.

// 인스턴스 초기화
var cos = new COS({
    getAuthorization: function (options, callback) {
        // 비동기 서명 획득
        var url = 'auth.php?method=' + options.Method.toLowerCase() + '&pathname=' + encodeURIComponent('/' + (options.Key || ''));
        var xhr = new XMLHttpRequest();
        xhr.open('GET', url, true);
        xhr.onload = function (e) {
            callback(e.target.responseText);
        };
        xhr.send();
    }
});

cos.getObjectUrl({
    Bucket: Bucket,
    Region: Region,
    Key: '1.jpg', // 다운로드할 파일의 경로로 바꿉니다.
    Expires: 60
}, function (err, data) {
    console.log(err || data.Url);
});
</script>
```

### Node.js SDK 사용

#### 절차 설명

1. npm 의존 패키지를 설치합니다.
```shell
npm i cos-nodejs-sdk-v5
```

2. 테스트 파일 test.js를 생성하고, 명령행에서 ```node test.js```를 실행합니다.

#### 예제 코드

다음 예제 코드는 사전 서명된 URL로 다운로드하는 방법을 보여줍니다.

```javascript
var COS = require('cos-nodejs-sdk-v5');

var SecretId = 'AKIDxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'; // 사용자의 SecretId로 대체합니다
var SecretKey = 'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx';    // 사용자의 SecretKey로 대체합니다.
var Bucket = 'test-1250000000';                        // 사용자의 버킷으로 대체합니다.
var Region = 'ap-guangzhou';                           // 사용자의 지역으로 대체합니다.

var cos = new COS({SecretId: SecretId, SecretKey: SecretKey});
var url = cos.getObjectUrl({
    Bucket: Bucket,
    Region: Region,
    Key: '1.jpg', // 다운로드할 파일의 경로로 바꿉니다.
    Expires: 60
});
console.log(url);
```
### Python SDK 사용

#### 절차 설명

1. CosConfig 클래스를 사용하여 클라이언트 CosS3Client를 구성하고 초기화합니다.
2. get_presigned_download_url() 방법을 실행하여 사잔 서명을 획득하고 객첵를 다운로드합니다. 버킷 이름과 객체 키 이름이 필요합니다.

#### 예제 코드

다음 예제 코드는 사전 서명된 URL로 다운로드하는 방법을 보여줍니다.

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client

secret_id = 'xxxxxxxx'      # 사용자의 secretId로 대체합니다.
secret_key = 'xxxxxxx'      # 사용자의 secretKey로 대체합니다.
region = 'ap-beijing-1'     # 사용자의 지역으로 대체합니다.
token = ''                  # 임시 키를 사용하려면 Token이 전송되어야 합니다. 기본적으로 비어 있으며 입력하지 않아도 됩니다.

config = CosConfig(Secret_id=secret_id, Secret_key=secret_key, Region=region, Token=token)
client = CosS3Client(config)

bucket = 'testbucket-123456789'
file_name = 'test.txt'
download_url = client.get_presigned_download_url(
    Bucket=bucket,
    Key=file_name,
)
print download_url
```
