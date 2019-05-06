## 적용 시나리오

Tencent Cloud COS는 하나 혹은 하나 이상의 객체를 직접 삭제할 수 있도록 지원합니다. 하나의 객체만 삭제하려고 하면 객체의 이름(즉, 객체 키)만 제공하면 하나의 API를 호출하여 이를 삭제할 수 있도록 요청할 수 있습니다.

## 사용 방법

### COS 콘솔 사용
COS 콘솔을 사용하여 여러 객체를 배치로 삭제할 수 있습니다. 콘솔 안내서의 [객체 삭제](https://cloud.tencent.com/document/product/436/13323)를 참조하십시오.

### REST API 사용

RREST API를 사용하여 객체 획득 요청을 시작할 수 있습니다. [DELETE Object 문서](https://cloud.tencent.com/document/product/436/7743)를 참조할 수 있습니다.

### C++ SDK 사용

COS의 C++ SDK에서 이 방법을 제공하며 [C++ SDK API 문서의 객체 삭제 부분](https://cloud.tencent.com/document/product/436/12302#delete-object)을 참조할 수 있습니다.

#### 절차 설명

1. 구성 파일 경로를 전달하여 CosConfig 및 CosAPI 객체를 초기화합니다.
2. DeleteObject() 메서드를 실행하여 단일 객체를 삭제합니다. 버킷 이름과 객체 키 이름을 제공해야 합니다.

#### 예제 코드

다음 예제 코드는 단일 객체를 삭제하는 방법을 보여줍니다.

``` cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-12345";
std::string object_name = "test_object";

qcloud_cos::DeleteObjectReq req(bucket_name, object_name);
qcloud_cos::DeleteObjectResp resp;
qcloud_cos::CosResult result = cos.DeleteObject(req, &resp);
```

여러 버전이 켜져 있는 경우 매개변수 VersionId를 지정하여 지정된 버전의 객체를 삭제할 수 있습니다.
``` cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-12345";
std::string object_name = "test_object";

qcloud_cos::DeleteObjectReq req(bucket_name, object_name);
req.SetXCosVersionId("12345");
qcloud_cos::DeleteObjectResp resp;
qcloud_cos::CosResult result = cos.DeleteObject(req, &resp);
```
### Java SDK 사용

COS의 Java SDK에서 이 방법을 제공하며 [Java SDK API 문서의 객체 삭제 부분](https://cloud.tencent.com/document/product/436/12263#delete-object)을 참조할 수 있습니다.

#### 절차 설명

1. 클라이언트 cosClient를 초기화합니다.
2. deleteObject 방법을 실행하며 객체를 삭제합니다. bucketName과 삭제할 키를 전달합니다.

#### 예제 코드

  deleteObject를 호출하여 object를 생성합니다. 예제 코드는 다음과 같습니다.

```java
// 1 사용자 인증 정보(secretId, secretKey)를 초기화합니다.
COSCredentials cred = new BasicCOSCredentials("AKIDXXXXXXXX", "1A2Z3YYYYYYYYYY");
// 2 버킷의 지역을 설정합니다. COS 영역의 약어는 다음 링크를 참조하십시오. https://cloud.tencent.com/document/product/436/6224
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// 3 COS 클라이언트를 생성합니다.
COSClient cosclient = new COSClient(cred, clientConfig);
// 버킷 이름에는 appid가 포함되어야 합니다.
String bucketName = "mybucket-1251668577";
String key = "aaa/bbb.txt";
try {
    cosclient.deleteObject(bucketName, key);
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
}

// 클라이언트를 종료합니다.
cosclient.shutdown();
```
### JavaScript SDK 사용

COS의 JavaScript SDK에서 이 방법을 제공하며 [JavaScript SDK API 문서의 객체 삭제 부분](https://cloud.tencent.com/document/product/436/12260#delete-object)을 참조할 수 있습니다.

#### 절차 설명

1. 서명 서버를 준비하고 서명을 얻기 위해 프런트 엔드에 auth.php API를 제공합니다. 자세한 내용은 [백 엔드 서명 예시](https://github.com/tencentyun/cos-js-sdk-v5/tree/master/server)를 참조할 수 있습니다.

2. 테스트 파일 test.html을 생성하고 다음 코드를 작성합니다. 파일을 정적 서버에 두고 `http://127.0.0.1/test.html`로 접근합니다.

#### 예제 코드

다음 예제 코드는 단일 객체를 삭제하는 방법을 보여줍니다.

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

cos.deleteObject({
    Bucket: Bucket,
    Region: Region
}, function (err, data) {
    console.log(err || data);
});
</script>
```
### Node.js SDK 사용

COS의 Node.js SDK에서 이 방법을 제공하며 [Node.js SDK API 문서의 객페 삭제 부분](https://cloud.tencent.com/document/product/436/12264#delete-object)을 참조할 수 있습니다.

#### 절차 설명

1. npm 의존 패키지를 설치합니다.
```shell
npm i cos-nodejs-sdk-v5
```

2. 테스트 파일 test.js를 생성하고, 명령행에서 ```node test.js```를 실행합니다.

#### 예제 코드

다음 예제 코드는 단일 객체를 삭제하는 방법을 보여줍니다.

```javascript
var COS = require('cos-nodejs-sdk-v5');

var SecretId = 'AKIDxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'; // 사용자의 SecretId로 대체합니다
var SecretKey = 'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx';    // 사용자의 SecretKey로 대체합니다.
var Bucket = 'test-1250000000';                        // 사용자의 버킷으로 대체합니다.
var Region = 'ap-guangzhou';                           // 사용자의 지역으로 대체합니다.

var cos = new COS({SecretId: SecretId, SecretKey: SecretKey});
cos.deleteObject({
    Bucket: Bucket,
    Region: Region,
    Key: '1.jpg'
}, function (err, data) {
    console.log(err || data);
});
```
### PHP SDK 사용

COS의 PHP SDK 에서 이 방법을 제공하며 [PHP SDK API 문서의 객체 삭제 부분](https://cloud.tencent.com/document/product/436/12267#.E5.88.A0.E9.99.A4.E6.96.87.E4.BB.B6)을 참조할 수 있습니다.

#### 절차 설명

1. 클라이언트 cosClient를 초기화합니다.
2. deleteObject를 실행하여 단일 객체를 삭제합니다. 버킷 이름과 객체 키 이름을 제공해야 합니다.

#### 예제 코드

다음 예제 코드는 단일 객체를 삭제하는 방법을 보여줍니다.

```php
try {
    $result = $cosClient->deleteObject(array(
        'Bucket' => 'bucket-125000000',
        'Key' => 'hello.txt'));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}
```
### Python SDK 사용

COS의 Python SDK에서 이 방법을 제공하며 [Python SDK API 문서의 객체 삭제 부분](https://cloud.tencent.com/document/product/436/12270#.E6.96.87.E4.BB.B6.E4.B8.8B.E8.BD.BD)을 참조할 수 있습니다.

#### 절차 설명

1. CosConfig 클래스를 사용하여 클라이언트 CosS3Client를 구성하고 초기화합니다.
2. deleteObject() 방법을 실행하여 단일 객체를 삭제합니다. 버킷 이름과 객체 키 이름을 제공해야 합니다.

#### 예제 코드

다음 예제 코드는 단일 객체를 삭제하는 방법을 보여줍니다.

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
response = client.delete_object(
    Bucket=bucket,
    Key=file_name      
)
```

여러 버전이 켜져 있는 경우 매개변수 VersionId를 지정하여 지정된 버전의 객체를 삭제할 수 있습니다.
```python
bucket = 'testbucket-123456789'
file_name = 'test.txt'
response = client.delete_object(
    Bucket=bucket,
    Key=file_name,
    VersionId='MTg0NDY3NDI1NjExNjQwNDUxMzU'    
)
```

