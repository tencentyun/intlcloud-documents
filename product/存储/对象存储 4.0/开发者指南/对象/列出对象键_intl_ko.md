## 적용 시나리오

Tencent Cloud COS는 접두사 순서로 객체 키를 나열하는 것을 지원합니다. 객체 키에서 `/` 문자를 사용하여 전통 파일 시스템과 유사한 계층적 구조를 구현할 수 있습니다. COS에서는 구분 기호로 계층적 구조의 선택과 탐색을 지원합니다.

단일 버킷의 모든 객체 키를 접두사의 UTF-8 이진 순서로 나열하거나 접두어를 지정하여 객체 키 목록을 필터링할 수 있습니다. 예를 들어, 매개변수 `t`를 추가함으로써 `tapd`의 객체를 나열할 수 있고 `a` 또는 다른 문자를 접두사로 하는 객체는 건너 뛸 수 있습니다.

추가된 구분 기호 `/`를 기반으로 객체 키를 다시 구성할 수 있습니다. 접두사와 구분 기호를 함께 사용하여 폴더 검색과 같은 기능을 구현할 수 있습니다. 예를 들어 접두사 매개변수`t`와 분리 기호 `/`를 추가하면 `tapd/file`과 같은 객체 키가 직접 나열됩니다.

Tencent Cloud COS는 하나의 버킷에 무제한 수량의 객체를 저장하는 것을 지원하므로 객체 키 목록이 매우 클 수 있습니다. 편리하게 관리하기 위해 단일 객체 API를 나열하면 최대 1000개의 키값이 반환되는 동시에 결과가 잘리는지 알려주는 표시기가 반환됩니다. 표시기와 구분 기호를 기반으로 일련의 객체 키 나열 요청을 보내 모든 키값을 나열하거나 필요한 내용을 검색할 수 있습니다.

## 사용 방법

### REST API 사용

RREST API를 사용하여 객체 획득 요청을 시작할 수 있습니다. [Get Bucket 문서](https://cloud.tencent.com/document/product/436/7734)를 참조할 수 있습니다.

### C++ SDK 사용

이 방법은 COS의 C ++ SDK에서 제공됩니다. [C ++ SDK API 문서의 Get Bucket 섹션](https://cloud.tencent.com/document/product/436/12302#get-bucket)을 참조하십시오.

#### 절차 설명

1. 구성 파일 경로를 전달하여 CosConfig 및 CosAPI 객체를 초기화합니다.
2. GetBucket() 방법을 실행하여 객체를 나열합니다. 버킷 이름이 필요합니다.

#### 예제 코드

아래 예제 코드는 객체 키를 나열하는 방법을 보여줍니다.

``` cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-12345";

// GetBucketReq 구조 함수는 bucket_name 입력이 필요합니다.
qcloud_cos::GetBucketReq req(bucket_name);
qcloud_cos::GetBucketResp resp;
qcloud_cos::CosResult result = cos.GetBucket(req, &resp);
```

매개변수를 지정하여 나열된 객체 키를 제어할 수 있습니다. MaxKeys는 매번 반환되는 객체의 최대 개수를 지정합니다. Prefix는 지정된 접두사가 있는 객체 키만 반환되는 것을 지정합니다. Delimiter는 구분 기호가 포함된 객체 키만 반환되는 것을 지정합니다.
``` cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-12345";

// GetBucketReq 구조 함수는 bucket_name 입력이 필요합니다.
qcloud_cos::GetBucketReq req(bucket_name);
req.SetPrefix("prefix");
req.SetDelimiter(";");
qcloud_cos::GetBucketResp resp;
qcloud_cos::CosResult result = cos.GetBucket(req, &resp);
```
### Java SDK 사용

이 방법은 COS의 Java SDK에서 제공됩니다. [Java SDK API 문서의 Get Bucket (List Objects) 섹션](https://cloud.tencent.com/document/product/436/12263#get-bucket-(list-objects))을 참조하십시오.

#### 절차 설명

1. 클라이언트 cosClient를 초기화합니다.
2. listObjects를 사용하여 object를 나열합니다. 한 번에 최대 1000개의 object를 나열할 수 있습니다. 1000개 이상 혹은 전체 object를 나열하려면 listObjects를 반복적으로 호출해야 합니다.

#### 예제 코드
(1) `ListObjectsRequest`에 Object를 나열하는 요청이 포합됩니다. 나열할 Object의 접두사 및 구분 기호를 설정할 수 있습니다. 예제 코드는 다음과 같습니다.

```java
// 1 사용자 인증 정보(secretId, secretKey)를 초기화합니다.
COSCredentials cred = new BasicCOSCredentials("AKIDXXXXXXXX", "1A2Z3YYYYYYYYYY");
// 2 버킷의 지역을 설정합니다. COS 영역의 약어는 다음 링크를 참조하십시오. https://cloud.tencent.com/document/product/436/6224
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// 3 COS 클라이언트를 생성합니다.
COSClient cosclient = new COSClient(cred, clientConfig);
// 버킷 이름에는 appid가 포함되어야 합니다.
String bucketName = "mybucket-1251668577";

ListObjectsRequest listObjectsRequest = new ListObjectsRequest();
// bucket 이름 설정
listObjectsRequest.setBucketName(bucketName);
// prefix는 나열된 object의 key가 prefix로 시작한다는 것을 나타냅니다.
listObjectsRequest.setPrefix("aaa/bbb");
// deliter는 구분 기호를 나타냅니다. "/"를 설정하면 현재 디렉터리의 object를 나열하는 것을 나타내며, null로 설정하면 모든 객체를 나열하는 것을 나타냅니다.
listObjectsRequest.setDelimiter("");
// object 경로에 특수 문자가 포함되어 있으면 URL 인코딩을 사용하는 것을 권장합니다. object key를 가져온 후에 url decode을 실행합니다.
listObjectsRequest.setEncodingType("url");
// 통과 객체의 최대 수를 설정합니다. 한 번에 listobject는 최대 1000개를 지원합니다.
listObjectsRequest.setMaxKeys(1000);
ObjectListing objectListing = null;
try {
    objectListing = cosclient.listObjects(listObjectsRequest);
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
}
// common prefix는 delimiter로 잘린 경로를 나타냅니다. delimter를 "/"로 설정할 경우 common prefix는 모든 하위 디렉터리의 경로를 나타냅니다.
List<String> commonPrefixs = objectListing.getCommonPrefixes();

// object summary은 나열된 모든 object의 목록을 나타냅니다.
List<COSObjectSummary> cosObjectSummaries = objectListing.getObjectSummaries();
for (COSObjectSummary cosObjectSummary : cosObjectSummaries) {
    // 파일의 경로 key
    String key = cosObjectSummary.getKey();
    // 사용하는 encodingtype이 url이면 url decode을 실행합니다.
    try {                                                               
        key = URLDecoder.decode(key, "utf-8");
    } catch (UnsupportedEncodingException e) {                          
        continue;                                                       
    }
    // 파일의 etag
    String etag = cosObjectSummary.getETag();
    // 파일의 길이
    long fileSize = cosObjectSummary.getSize();
    // 파일의 스토리지 클래스
    String storageClasses = cosObjectSummary.getStorageClass();
}

cosclient.shutdown();
```
(2) MaxKey 수량을 초과하는 Object 또는 전체 Object를 가져오려면 앞에 반환된 next marker를 다음 호출할 marker로 사용하여 반환하는 truncated가 false가 될 때까지 listobject를 반복적으로 호출해야 합니다.

```java
// 1 사용자 인증 정보(secretId, secretKey)를 초기화합니다.
COSCredentials cred = new BasicCOSCredentials("AKIDXXXXXXXX", "1A2Z3YYYYYYYYYY");
// 2 버킷의 지역을 설정합니다. COS 영역의 약어는 다음 링크를 참조하십시오. https://cloud.tencent.com/document/product/436/6224
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// 3 COS 클라이언트를 생성합니다.
COSClient cosclient = new COSClient(cred, clientConfig);
// 버킷 이름에는 appid가 포함되어야 합니다.
String bucketName = "mybucket-1251668577";

ListObjectsRequest listObjectsRequest = new ListObjectsRequest();
// bucket 이름 설정
listObjectsRequest.setBucketName(bucketName);
// prefix는 나열된 object의 key가 prefix로 시작한다는 것을 나타냅니다.
listObjectsRequest.setPrefix("aaa/bbb");
// deliter는 구분 기호를 나타냅니다. "/"를 설정하면 현재 디렉터리의 object를 나열하는 것을 나타내며, null로 설정하면 모든 객체를 나열하는 것을 나타냅니다.
listObjectsRequest.setDelimiter("");
// object 경로에 특수 문자가 포함되어 있으면 URL 인코딩을 사용하는 것을 권장합니다. object key를 가져온 후에 url decode을 실행합니다.
listObjectsRequest.setEncodingType("url");
// 통과 객체의 최대 수를 설정합니다. 한 번에 listobject는 최대 1000개를 지원합니다.
listObjectsRequest.setMaxKeys(1000);
ObjectListing objectListing = null;
do {

    try {
        objectListing = cosclient.listObjects(listObjectsRequest);
    } catch (CosServiceException e) {
        e.printStackTrace();
        return;
    } catch (CosClientException e) {
        e.printStackTrace();
        return;
    }
    // common prefix는 delimiter로 잘린 경로를 나타냅니다. delimter를 "/"로 설정할 경우 common prefix는 모든 하위 디렉터리의 경로를 나타냅니다.
    List<String> commonPrefixs = objectListing.getCommonPrefixes();

    // object summary은 나열된 모든 object의 목록을 나타냅니다.
    List<COSObjectSummary> cosObjectSummaries = objectListing.getObjectSummaries();
    for (COSObjectSummary cosObjectSummary : cosObjectSummaries) {
        // 파일의 경로 key
        String key = cosObjectSummary.getKey();
        // 사용하는 encodingtype이 url이면 url decode을 실행합니다.
        try {
            key = URLDecoder.decode(key, "utf-8");
        } catch (UnsupportedEncodingException e) {
            continue;
        }
        // 파일의 etag
        String etag = cosObjectSummary.getETag();
        // 파일의 길이
        long fileSize = cosObjectSummary.getSize();
        // 파일의 스토리지 클래스
        String storageClasses = cosObjectSummary.getStorageClass();
    }

    // 다음 요청에 대한 next marker를 가져옵니다.
    String nextMarker = "";
    try {
        nextMarker = URLDecoder.decode(objectListing.getNextMarker(), "utf-8");
    } catch (UnsupportedEncodingException e) {
        e.printStackTrace();
        return;
    }
    listObjectsRequest.setMarker(nextMarker);
} while (objectListing.isTruncated());

cosclient.shutdown();
```

### JavaScript SDK 사용

이 방법은 COS의 JavaScript SDK에서 제공됩니다. [JavaScript SDK API 문서의 Get Bucket 섹션](https://cloud.tencent.com/document/product/436/12260#get-bucket)을 참조하십시오.

#### 절차 설명

1. 서명 서버를 준비하고 서명을 얻기 위해 프런트 엔드에 auth.php API를 제공합니다. 자세한 내용은 [백 엔드 서명 예시](https://github.com/tencentyun/cos-js-sdk-v5/tree/master/server)를 참조할 수 있습니다.

2. 테스트 파일 test.html을 생성하고 다음 코드를 작성합니다. 파일을 정적 서버에 두고 `http://127.0.0.1/test.html`로 접근합니다.

#### 예제 코드

아래 예제 코드는 객체 키를 나열하는 방법을 보여줍니다.

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

cos.getBucket({
    Bucket: Bucket,
    Region: Region,
}, function (err, data) {
    console.log(err, data);
});
</script>
```
### Node.js SDK 사용

이 방법은 COS의 Node.js SDK에서 제공됩니다. [Node.js SDK API 문서의 Get Bucket 섹션](https://cloud.tencent.com/document/product/436/12264#get-bucket)을 참조하십시오.

#### 절차 설명

1. npm 의존 패키지를 설치합니다.
```shell
npm i cos-nodejs-sdk-v5
```

2. 테스트 파일 test.js를 생성하고, 명령행에서 ```node test.js```를 실행합니다.

#### 예제 코드

아래 예제 코드는 객체 키를 나열하는 방법을 보여줍니다.

```javascript
var COS = require('cos-nodejs-sdk-v5');

var SecretId = 'AKIDxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'; // 사용자의 SecretKey로 대체합니다.
var SecretKey = 'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx';    // 사용자의 SecretKey로 대체합니다.
var Bucket = 'test-1250000000';                        // 사용자의 버킷으로 대체합니다.
var Region = 'ap-guangzhou';                           // 사용자의 지역으로 대체합니다.

var cos = new COS({SecretId: SecretId, SecretKey: SecretKey});
cos.getBucket({
    Bucket: Bucket,
    Region: Region,
    Prefix: '',    // 접두사,
    MaxKeys: '100' // 수량 나열
}, function (err, data) {
    console.log(err || data);
});
```
### PHP SDK 사용

이 방법은 COS의 PHP SDK에서 제공됩니다. [PHP SDK API 문서의 Bucket 목록 가져오기](https://cloud.tencent.com/document/product/436/12267#.E8.8E.B7.E5.8F.96bucket.E5.88.97.E8.A1.A8)를 참조하십시오.

#### 절차 설명

1. 클라이언트 cosClient를 초기화합니다.
2. listObjects를 실행하여 객체를 나열합니다. 버킷 이름이 필요합니다.

#### 예제 코드

아래 예제 코드는 객체 키를 나열하는 방법을 보여줍니다.

```php
try {
    $result = $cosClient->listObjects(array(
        'Bucket' => 'testbucket-125000000'));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}
```
### Python SDK 사용

이 방법은 COS의 Python SDK에서 제공됩니다. [Python SDK API 문서의 파일 목록 가져오기 섹션](https://cloud.tencent.com/document/product/436/12270#.E8.8E.B7.E5.8F.96.E6.96.87.E4.BB.B6.E5.88.97.E8.A1.A8)을 참조하십시오.

#### 절차 설명

1. CosConfig 클래스로 구성하고 클라이언트 CosS3Client를 초기화합니다.
2. list_objects () 방법을 실행하여 객체를 나열합니다. 버킷 이름이 필요합니다.

#### 예제 코드

아래 예제 코드는 객체 키를 나열하는 방법을 보여줍니다.

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client

secret_id = 'xxxxxxxx'      # 사용자의 SecretId로 대체합니다.
secret_key = 'xxxxxxx'      # 사용자의 secretKey로 대체합니다.
region = 'ap-beijing-1'     # 사용자의 지역으로 대체합니다.
token = ''                  # 임시 키를 사용하려면 Token이 전송되어야 합니다. 기본적으로 비어 있으며 입력하지 않아도 됩니다.

config = CosConfig(Secret_id=secret_id, Secret_key=secret_key, Region=region, Token=token)
client = CosS3Client(config)

bucket = 'testbucket-123456789'
response = client.list_objects(
    Bucket=bucket       
)
```

매개변수를 지정하여 나열된 객체 키를 제어할 수 있습니다. MaxKeys는 매번 반환되는 객체의 최대 개수를 지정합니다. Prefix는 지정된 접두사가 있는 객체 키만 반환되는 것을 지정합니다. Delimiter는 구분 기호가 포함된 객체 키만 반환되는 것을 지정합니다.
```python
bucket = 'testbucket-123456789'
response = client.list_objects(
    Bucket=bucket,
    Delimiter='/',
    MaxKeys=100,
    Prefix='test'
)
```
