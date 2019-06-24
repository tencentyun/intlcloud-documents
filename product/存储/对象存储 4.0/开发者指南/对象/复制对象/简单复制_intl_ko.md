## 적용 시나리오

이미 COS에 저장된 객체를 간단한 복사 작업을 통해 새로운 객체 사본을 생성할 수 있습니다. 한 번에 최대 5GB의 객체를 복사할 수 있습니다. 5GB보다 큰 객체를 복사하려면 멀티파트 업로드 API를 사용해야 합니다. 객체 복사 작업을 사용하여 다음과 같은 기능이 있습니다.

- 새로운 객체의 사본을 생성합니다.
- 객체를 복사하고 이름을 바꾸며 소스 객체를 삭제한 다음 이름을 다시 지정합니다.
- 객체의 스토리지 클래스를 수정합니다. 복사 작업에서 통일한 소스 및 대상 객체 키를 선택하고 스토리지 클래스를 수정합니다.
- 다른 COS 지역에서 객체를 복사합니다.
- 객체 메타데이터를 수정합니다. 복사 작업에서 통일한 소스 및 대상 객체 키를 선택하고 객체 메타데이터를 수정합니다.

복사 작업에서 소스 객체의 메타데이터는 기본적으로 계승되지만 생성 날짜는 새 객체의 적용을 받습니다.

## 사용 방법

### REST API 사용

REST API를 사용하여 객체 복사 요청을 시작할 수 있습니다. [Put Object Copy 문서 설명](https://cloud.tencent.com/document/product/436/10881)을 참조하십시오.

### C++ SDK 사용

COS의 C++ SDK에서 이 방법을 제공하며 [C++ SDK API 문서의 Put Object Copy 부분](https://cloud.tencent.com/document/product/436/12302#put-object-copy)을 참조할 수 있습니다.

#### 절차 설명

1. 구성 파일 경로를 전달하여 CosConfig 및 CosAPI 객체를 초기화합니다.
2. PutObjectCopy()방법을 실행하여 객체를 복사합니다. 버킷 이름, 겍체 키 이름, 복사할 소스 버킷, 소스 객체 키 및 소스 지역은 PutObjectReq에 포함되어야 합니다.

#### 예제 코드

다음 예제 코드는 객체를 간편 복사하는 방법을 보여줍니다.

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-12345";
std::string object_name = "sevenyou";

qcloud_cos::PutObjectCopyReq req(bucket_name, object_name);
req.SetXCosCopySource("sevenyousouthtest-12345656.cn-south.myqcloud.com/sevenyou_source_obj");
qcloud_cos::PutObjectCopyResp resp;
qcloud_cos::CosResult result = cos.PutObjectCopy(req, &resp);
```
### Java SDK 사용

COS의 Java SDK에서 이 방법을 제공하며 [Java SDK API 문서의 Put Object Copy 부분](https://cloud.tencent.com/document/product/436/12263#put-object-copy)을 참조할 수 있습니다.

#### 절차 설명

1. 클라이언트 cosClient를 초기화합니다.
2. copyObject API를 사용하여 복사를 완료합니다.

#### 예제 코드

`CopyObjectRequest`는 복사 겍체의 요청을 포함합니다. 소스 파일을 위치한 지역과 버킷 이름, 경로 그리고 목표 파일을 위치한 지역, 버킷 이름, 경로를 설정하여 구성합니다. 다음 예제 코드는 객체를 간편 복사하는 방법을 보여줍니다.

```java
// 1 사용자 인증 정보(secretId, secretKey)를 초기화합니다.
COSCredentials cred = new BasicCOSCredentials("AKIDXXXXXXXX", "1A2Z3YYYYYYYYYY");
// 2 버킷의 지역을 설정합니다. COS 영역의 약어는 다음 링크를 참조하십시오. https://cloud.tencent.com/document/product/436/6224
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// 3 COS 클라이언트를 생성합니다.
COSClient cosclient = new COSClient(cred, clientConfig);
// 복사할 bucket region입니다. 교차 지역 복사가 지원됩니다.
Region srcBucketRegion = new Region("ap-shanghai");
// 소스 버킷. 버킷 이름에는 appid가 포함되어야 합니다.
String srcBucketName = "srcBucket-1251668577";
// 복사할 소스 파일입니다.
String srcKey = "aaa/bbb.txt";
// 대상 버킷입니다. 버킷 이름에는 appid가 포함되어야 합니다.
String destBucketName = "destBucket-1251668577";
// 복사할 대상 파일입니다.
String destKey = "ccc/ddd.txt";

CopyObjectRequest copyObjectRequest = new CopyObjectRequest(srcBucketRegion, srcBucketName,
        srcKey, destBucketName, destKey);
try {
    CopyObjectResult copyObjectResult = cosclient.copyObject(copyObjectRequest);
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
}
cosclient.shutdown();
```

### JavaScript SDK 사용

COS의 JavaScript SDK에서 이 방법을 제공하며 [JavaScript SDK API 문서의 Put Object Copy 부분](https://cloud.tencent.com/document/product/436/12260#put-object-copy)을 참조할 수 있습니다.

#### 절차 설명

1. 서명 서버를 준비하고 서명을 얻기 위해 프런트 엔드에 auth.php API를 제공합니다. 자세한 내용은 [백 엔드 서명 예시](https://github.com/tencentyun/cos-js-sdk-v5/tree/master/server)를 참조할 수 있습니다.

2. 테스트 파일 test.html을 생성하고 다음 코드를 작성합니다. 파일을 정적 서버에 두고 `http://127.0.0.1/test.html`로 접근합니다.

#### 예제 코드

다음 예제 코드는 객체를 간편 복사하는 방법을 보여줍니다.

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

cos.putObjectCopy({
    Bucket: Bucket,
    Region: Region,
    Key: '1.new.jpg',
    CopySource: 'test-1250000000.cos.ap-guangzhou.myqcloud.com/1.jpg'
}, function (err, data) {
    console.log(err || data);
});
</script>
```
### Node.js SDK 사용

#### 절차 설명

1. npm 의존 패키지를 설치합니다.
```shell
npm i cos-nodejs-sdk-v5
```

2. 테스트 파일 test.js를 생성하고, 명령행에서 `node test.js`를 실행합니다.

#### 예제 코드

다음 예제 코드는 객체를 복사하는 방법을 보여줍니다.

```javascript
var COS = require('cos-nodejs-sdk-v5');

var SecretId = 'AKIDxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'; // 사용자의 SecretID로 대체합니다
var SecretKey = 'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx';    // 사용자의 SecretKey로 대체합니다.
var Bucket = 'test-1250000000';                        // 사용자의 버킷으로 대체합니다.
var Region = 'ap-guangzhou';                           // 사용자의 지역으로 대체합니다.

var cos = new COS({SecretId: SecretId, SecretKey: SecretKey});
cos.putObjectCopy({
    Bucket: Bucket,
    Region: Region,
    Key: '1.new.jpg',
    CopySource: 'test-1250000000.cos.ap-guangzhou.myqcloud.com/1.jpg'
}, function (err, data) {
    console.log(err || data);
});
```
### PHP SDK 사용

COS의 PHP SDK 에서 이 방법을 제공하며 [PHP SDK API 문서의 객체 복사 부분](https://cloud.tencent.com/document/product/436/12267#.E5.A4.8D.E5.88.B6.E5.AF.B9.E8.B1.A1)을 참조할 수 있습니다.

#### 절차 설명

1. 클라이언트 cosClient를 초기화합니다.
2. Copy를 실행하여 멀티파트로 객체를 복사합니다. 버킷 이름과 객체 키 이름을 제공해야 합니다.

#### 예제 코드

다음 예제 코드는 객체를 간편 복사하는 방법을 보여줍니다.
```php
try {
    $result = $cosClient->copyObject(array(
        'Bucket' => 'bucket-125000000',
        'CopySource' => 'bucket-appid.region.myqcloud.com/cos_path',
        'Key' => 'string',
    ));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}
```
### Python SDK 사용

COS의 Python SDK에서 이 방법을 제공하며 [Python SDK API 문서의 파일 복사 부분](https://cloud.tencent.com/document/product/436/12270#.E6.96.87.E4.BB.B6.E6.8B.B7.E8.B4.9D)을 참조할 수 있습니다.

#### 절차 설명

1. CosConfig 클래스를 사용하여 클라이언트 CosS3Client를 구성하고 초기화합니다.
2. Copy_object() 방법을 실행하여 객체를 복사합니다. 버킷 이름, 겍체 키 이름, 복사할 소스 버킷, 소스 객체 키 및 소스 지역이 포함되어야 합니다.

#### 예제 코드

다음 예제 코드는 객체를 간편 복사하는 방법을 보여줍니다.

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client

secret_id = 'xxxxxxxx'      # 사용자의 secretID로 대체합니다.
secret_key = 'xxxxxxx'      # 사용자의 secretKey로 대체합니다.
region = 'ap-beijing-1'     # 사용자의 지역으로 대체합니다.
token = ''                  # 임시 키를 사용하려면 Token이 전송되어야 합니다. 기본적으로 비어 있으며 입력하지 않아도 됩니다.

config = CosConfig(Secret_id=secret_id, Secret_key=secret_key, Region=region, Token=token)
client = CosS3Client(config)

bucket = 'testbucket-123456789'
file_name = 'test.txt'
response = client.copy_object(
    Bucket=bucket,
    Key=file_name,
    CopySource={
        'Bucket': 'test-121212121',
        'Key': '1MB.txt',
        'Region': 'ap-guangzhou'
    }      
)
```

