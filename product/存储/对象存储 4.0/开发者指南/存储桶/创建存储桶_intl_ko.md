## 적용 시나리오

COS를 사용하기 시작할 때 객체의 사용과 관리를 위해 버킷을 생성해야 합니다. 콘솔, API , 또는 SDK를 통해 버킷을 생성할 수 있습니다.

버킷이 존재하지 않을 때 다음과 같은 예제 코드로 지정된 지역에 버킷을 생성할 수 있습니다. 버킷이 지원되는 매개변수는 다음과 같습니다.

- Bucket: 완전한 버킷 명칭을 지정하는데 사용되며, 예를 들어 `testbuc-125235912`
- Region: Tencent 클라우드 서비스 지역을 선택하십시오. 생성이 완료되면 버킷을 이동하거나 수정할 수 없습니다. 사용할 수 있는 지역 명칭은 [가용 지역](https://cloud.tencent.com/document/product/436/6224) 문서를 참조하십시오.

## 사용 방법
### COS 콘솔 사용
COS 콘솔을 사용하여 버킷을 생성하는 방법에 대한 자세한 내용은 [생성 및 삭제](https://cloud.tencent.com/document/product/436/13309) 콘솔 안내 문서를 참조하십시오.

### REST API 사용
REST API를 사용하여 버킷 생성 요청할 수 있습니다. 자세한 내용은 [Put Bucket 문서 설명](https://cloud.tencent.com/document/product/436/7738)을 참조하십시오.
### C++ SDK 사용

이 방법은 COS의 C++ SDK에서 제공됩니다. 자세한 내용은 [C ++ SDK API 파일 Put Bucket 부분](https://cloud.tencent.com/document/product/436/12302#put-bucket)을 참조하십시오.

#### 절차 설명

1. 구성 파일 경로를 전달하여 CosConfig 및 CosAPI 객체를 초기화합니다.
2. PutBucketReq, PutBucketResp를 생성합니다. 그중에 PutBucketReq는 Bucket Name에 의하여 구조화됩니다.
3. PutBucket 방법을 실행하여 버킷을 생성합니다.

#### 예제 코드

다음 예제 코드에서 버킷 생성 방법을 보여 줍니다.

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-12345";

qcloud_cos::PutBucketReq req(bucket_name);
qcloud_cos::PutBucketResp resp;
qcloud_cos::CosResult result = cos.PutBucket(req, &resp);
```
### Java SDK 사용

COS의 Java SDK에서 이 방법을 제공하며 [Java SDK API 파일 Put Bucket 부분](https://cloud.tencent.com/document/product/436/12263#put-bucket)을 참조하십시오.

#### 절차 설명

1. 클라이언트 cosClient를 초기화합니다.
2. createBucket을 실행하여 버킷을 생성합니다. 생성 시 버킷의 권한(공개 읽기/쓰기 또는 비공개 읽기)을 지정할 수 있습니다.

#### 예제 코드

createBucket을 호출하여 버킷을 생성합니다. 예제 코드는 다음과 같습니다.

```java
// 1 사용자 인증 정보(appid, secretId, 및 secretKey)를 초기화합니다.
COSCredentials cred = new BasicCOSCredentials("AKIDXXXXXXXX", "1A2Z3YYYYYYYYYY");
// 2 버킷의 지역을 설정합니다. COS 영역의 약어는 다음 링크를 참조하십시오. https://cloud.tencent.com/document/product/436/6224
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// 3 COS 클라이언트를 생성합니다.
COSClient cosclient = new COSClient(cred, clientConfig);

String bucketName = "publicreadbucket-1251668577";
CreateBucketRequest createBucketRequest = new CreateBucketRequest(bucketName);
// 버킷 권한을 PublicRead(공개 읽기 및 비공개 쓰기)를 설정합니다. 기타는 Private(비공개 읽기/쓰기), PublicReadWrite(공개 읽기/쓰기)를 선택합니다.
createBucketRequest.setCannedAcl(CannedAccessControlList.PublicRead);
Bucket bucket = cosclient.createBucket(createBucketRequest);
```
### JavaScript SDK 사용

#### 절차 설명

1. 서명 서버를 준비하고 서명을 얻기 위해 프런트 엔드에 auth.php API를 제공합니다. 자세한 내용은 [백 엔드 서명 예시](https://github.com/tencentyun/cos-js-sdk-v5/tree/master/server)를 참조할 수 있습니다.

2. 테스트 파일 test.html을 생성하고 다음 코드를 작성합니다. 파일을 정적 서버에 두고 `http://127.0.0.1/test.html`로 접근합니다.

#### 예제 코드

다음 예제 코드에서 버킷 생성 방법을 보여 줍니다.

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

cos.putBucket({
    Bucket: Bucket,
    Region: Region
}, function (err, data) {
    console.log(err || data);
});
</script>
```
### Node.js SDK 사용

이 방법은 COS의 Node.js SDK에서 제공됩니다. 자세한 내용은 [Node.js SDK API 파일 Put Bucket 부분](https://cloud.tencent.com/document/product/436/12264#put-bucket)을 참조하십시오.

#### 절차 설명

1. npm 의존 패키지를 설치합니다.
```shell
npm i cos-nodejs-sdk-v5
```

2. 테스트 파일 test.js를 생성하고, 명령행에서 `node test.js`를 실행합니다.

#### 예제 코드

다음 예제 코드에서 버킷 생성 방법을 보여 줍니다.

```javascript
var COS = require('cos-nodejs-sdk-v5');

var SecretId = 'AKIDxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'; // 사용자의 SecretId로 대체합니다.
var SecretKey = 'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx';    // 사용자의 SecretKey로 대체합니다.
var Bucket = 'test-1250000000';                        // 사용자의 버킷으로 대체합니다.
var Region = 'ap-guangzhou';                           // 사용자의 지역으로 대체합니다.

var cos = new COS({SecretId: SecretId, SecretKey: SecretKey});
cos.putBucket({
    Bucket: Bucket,
    Region: Region
}, function (err, data) {
    console.log(err || data);
});
```
### PHP SDK 사용

이 방법은 COS의 PHP SDK에서 제공됩니다. 자세한 내용은 [PHP SDK API 파일 생성 버킷 부분](https://cloud.tencent.com/document/product/436/12267#.E5.88.9B.E5.BB.BAbucket)을 참조하십시오.

#### 절차 설명

1. 클라이언트 cosClient를 초기화합니다.
2. createBucket을 실행하여 버킷을 생성합니다. 버킷 명칭이 필요합니다.

#### 예제 코드

다음 예제 코드에서 버킷 생성 방법을 보여 줍니다.

```php
try {
    $result = $cosClient->createBucket(array('Bucket' => 'testbucket-125000000'));
    print_r($result);
    } catch (\Exception $e) {
    echo "$e\n";
}
```
### Python SDK 사용

이 방법은 COS의 Python SDK에서 제공됩니다. 자세한 내용은 [Python SDK API 파일 생성 버킷 부분](https://cloud.tencent.com/document/product/436/12270#.E5.88.9B.E5.BB.BA-bucket)을 참조하십시오.

#### 절차 설명

1. CosConfig 클래스로 구성하고 클라이언트 CosS3Client를 초기화합니다.
2. create_bucket() 방법을 실행하여 버킷을 생성합니다. 버킷 명칭은 필요합니다.

#### 예제 코드

다음 예제 코드에서 버킷 생성 방법을 보여 줍니다.

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
response = client.create_bucket(
    Bucket=bucket    
)
```

