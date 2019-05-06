## 적용 시나리오

Tencent Cloud COS는 여러 객체를 배치로 삭제할 수 있습니다. 콘솔, API, SDK 등 다양한 방식으로 객체를 배치로 삭제할 수 있습니다.

기본적으로 삭제 작업이 성공적으로 완료되면 반환된 콘텐츠는 일반적으로 비어 있습니다. 오류가 발생하면 오류 메시지가 반환됩니다.

> 참고: 단일 요청에서 최대 1000개의 객체를 삭제할 수 있습니다. 더 많은 객체를 삭제해야 하는 경우 리스트를 분할하고 별도로 요청을 보냅니다.

## 사용 방법

### COS 콘솔 사용
COS 콘솔을 사용하여 여러 객체를 배치로 삭제할 수 있습니다. 콘솔 안내서의 [객체 삭제](https://cloud.tencent.com/document/product/436/13323)를 참조하십시오.

### REST API 사용

REST API를 사용하여 하나의 객체 배치 삭제 요청을 직접적으로 시작할 수 있으며 [여러 객채 삭제](https://cloud.tencent.com/document/product/436/8289) 문서를 참조할 수 있습니다.

### Java SDK 사용

COS의 Java SDK에서 이 방법을 제공하며 [Java SDK API 문서의 객체 삭제 부분](https://cloud.tencent.com/document/product/436/12263#delete-object)을 참조할 수 있습니다.

#### 절차 설명

1. 클라이언트 cosClient를 초기화합니다.
2. deleteObjects를 실행하여 객체를 삭제합니다. 삭제할 객체 키 이름을 제공해야 합니다.
3. 실행이 성공하면 삭제된 객체 키를 모두 포함하는 DeleteObjectsResult 객체가 리턴됩니다. 실행이 부분적으로 성공하고 부분적으로 실패한 경우(예를 들어, 이 객체를 삭제할 권한이 없는 경우), MultiObjectDeleteException 클래스가 반환됩니다. 다른 실패로 인한 예외가 발생하면 예외 클래스 (CosClientException/CosServiceException)가 반환됩니다. SDK 예외 클래스 설명을 참조하십시오.

#### 예제 코드

(1) 다음 코드는 여러 객체(다중 버전 없음)를 삭제하는 방법을 보여줍니다.

```java
// 1 사용자 인증 정보(secretId, secretKey)를 초기화합니다.
COSCredentials cred = new BasicCOSCredentials("AKIDXXXXXXXX", "1A2Z3YYYYYYYYYY");
// 2 버킷의 지역을 설정합니다. COS 영역의 약어는 다음 링크를 참조하십시오. https://cloud.tencent.com/document/product/436/6224
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// 3 COS 클라이언트를 생성합니다.
COSClient cosclient = new COSClient(cred, clientConfig);
// 버킷 이름에는 appid가 포함되어야 합니다.
String bucketName = "mybucket-1251668577";

DeleteObjectsRequest deleteObjectsRequest = new DeleteObjectsRequest(bucketName);
// 삭제할 키 리스트를 설정합니다. 한 번에 최대 1000개의 키를 삭제할 수 있습니다.
ArrayList<KeyVersion> keyList = new ArrayList<>();
// 삭제할 파일의 이름을 전달합니다.
keyList.add(new KeyVersion("aaa.txt"));
keyList.add(new KeyVersion("bbb.mp4"));
keyList.add(new KeyVersion("ccc/ddd.jpg"));
deleteObjectsRequest.setKeys(keyList);

// 파일을 배치로 삭제합니다.
try {
    DeleteObjectsResult deleteObjectsResult = cosclient.deleteObjects(deleteObjectsRequest);
    List<DeletedObject> deleteObjectResultArray = deleteObjectsResult.getDeletedObjects();
} catch (MultiObjectDeleteException mde) { // 실행이 부분적으로 실패한 경우 MultiObjectDeleteException이 반환됩니다.
    List<DeletedObject> deleteObjects = mde.getDeletedObjects();
    List<DeleteError> deleteErrors = mde.getErrors();
} catch (CosServiceException e) { // 매개변수 오류나 신분 인증 검증 실패와 같은 다른 오류가 발생하면 CosServiceException을 throw될 것입니다.
    e.printStackTrace();
} catch (CosClientException e) { // COS 연결 실패와 같은 클라이언트 오류가 발생하는 경우
    e.printStackTrace();
}
```

(2) 다음 코드는 여러 객체(여러 버전 있음)를 삭제하는 예제 코드를 보여줍니다.

```java
// 1 사용자 인증 정보(secretId, secretKey)를 초기화합니다.
COSCredentials cred = new BasicCOSCredentials("AKIDXXXXXXXX", "1A2Z3YYYYYYYYYY");
// 2 버킷의 지역을 설정합니다. COS 영역의 약어는 다음 링크를 참조하십시오. https://cloud.tencent.com/document/product/436/6224
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// 3 COS 클라이언트를 생성합니다.
COSClient cosclient = new COSClient(cred, clientConfig);
// 버킷 이름에는 appid가 포함되어야 합니다.
String bucketName = "mybucket-1251668577";

DeleteObjectsRequest deleteObjectsRequest = new DeleteObjectsRequest(bucketName);
// 삭제할 키 리스트를 설정합니다. 한 번에 최대 1000개의 키를 삭제할 수 있습니다.
ArrayList<KeyVersion> keyList = new ArrayList<>();
// 삭제할 파일의 이름을 전달합니다.
keyList.add(new KeyVersion("aaa.txt", "axbefagagaxxfafa"));
keyList.add(new KeyVersion("bbb.mp4", "awcafa1faxg0lx"));
keyList.add(new KeyVersion("ccc/ddd.jpg", "kafa1kxxaa2ymh"));
deleteObjectsRequest.setKeys(keyList);

// 파일을 배치로 삭제합니다.
try {
    DeleteObjectsResult deleteObjectsResult = cosclient.deleteObjects(deleteObjectsRequest);
    List<DeletedObject> deleteObjectResultArray = deleteObjectsResult.getDeletedObjects();
} catch (MultiObjectDeleteException mde) { // 실행이 부분적으로 실패한 경우 MultiObjectDeleteException이 반환됩니다.
    List<DeletedObject> deleteObjects = mde.getDeletedObjects();
    List<DeleteError> deleteErrors = mde.getErrors();
} catch (CosServiceException e) { // 매개변수 오류나 신분 인증 검증 실패와 같은 다른 오류가 발생하면 CosServiceException을 throw될 것입니다.
    e.printStackTrace();
} catch (CosClientException e) { // COS 연결 실패와 같은 클라이언트 오류가 발생하는 경우
    e.printStackTrace();
}
```



### JavaScript SDK 사용

COS의 JavaScript SDK에서 이 방법을 제공하며 [JavaScript SDK API 문서의 객체 삭제 부분](https://cloud.tencent.com/document/product/436/12260#delete-object)을 참조할 수 있습니다.

#### 절차 설명

1. 서명 서버를 준비하고 서명을 얻기 위해 프런트 엔드에 auth.php API를 제공합니다. 자세한 내용은 [백 엔드 서명 예시](https://github.com/tencentyun/cos-js-sdk-v5/tree/master/server)를 참조할 수 있습니다.

2. 테스트 파일 test.html을 생성하고 다음 코드를 작성합니다. 파일을 정적 서버에 두고 `http://127.0.0.1/test.html`로 접근합니다.

#### 예제 코드

다음 예제 코드는 여러 객체를 삭제하는 방법을 보여줍니다.

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

cos.deleteMultipleObject({
    Bucket: Bucket,
    Region: Region,
    Objects: [
        {Key: '1mb.zip'},
        {Key: '3mb.zip'},
    ]
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

다음 예제 코드는 여러 객체를 삭제하는 방법을 보여줍니다.

```javascript
var COS = require('cos-nodejs-sdk-v5');

var SecretId = 'AKIDxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'; // 사용자의 SecretKey로 대체합니다.
var SecretKey = 'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx';    // 사용자의 SecretKey로 대체합니다.
var Bucket = 'test-1250000000';                        // 사용자의 버킷으로 대체합니다.
var Region = 'ap-guangzhou';                           // 사용자의 지역으로 대체합니다.

var cos = new COS({SecretId: SecretId, SecretKey: SecretKey});
cos.deleteMultipleObject({
    Bucket: Bucket,
    Region: Region,
    Objects: [
        {Key: '1mb.zip'},
        {Key: '3mb.zip'},
    ]
}, function (err, data) {
    console.log(err || data);
});
```
### PHP SDK 사용

COS의 PHP SDK 에서 이 방법을 제공하며 [PHP SDK API 문서의 객체 삭제 부분](https://cloud.tencent.com/document/product/436/12267#.E5.88.A0.E9.99.A4.E6.96.87.E4.BB.B6)을 참조할 수 있습니다.

#### 절차 설명

1. 클라이언트 cosClient를 초기화합니다.
2. deleteObjects를 실행하여 여러 객체를 삭제합니다. 버킷 이름과 객체 키 이름을 제공해야 합니다.

#### 예제 코드

다음 예제 코드는 여러 객체를 삭제하는 방법을 보여줍니다.

```php
try {
    $result = $cosClient->deleteObjects(array(
        'Bucket' => 'bucket-125000000',
        'Objects' => array(
            array(
                'Key' => 'string',
            ),
            // ... repeated
        ),
    ));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}
```
### Python SDK 사용

COS의 Python SDK에서 이 방법을 제공하며 [Python SDK API 문서의 객체 삭제 부분](https://cloud.tencent.com/document/product/436/12270#.E6.96.87.E4.BB.B6.E4.B8.8B.E8.BD.BD)을 참조할 수 있습니다.

#### 절차 설명

1. CosConfig 클래스를 사용하여 클라이언트 CosS3Client를 구성하고 초기화합니다.
2. delete_objects() 방법을 실행하여 여러 객체를 삭제합니다. 버킷 이름과 여러 객체 키 이름을 제공해야 합니다.

#### 예제 코드

다음 예제 코드는 여러 객체를 삭제하는 방법을 보여줍니다.

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
response = client.delete_objects(
    Bucket=bucket,
    Delete={
        "Quiet": "true",
        "Object": [
            {
                "Key": "test1.txt"
            },
            {
                "Key": "test2.txt"
            }
        ]
    }    
)
```

여러 버전이 켜져 있는 경우 매개변수 VersionId를 지정하여 지정된 버전의 객체를 삭제할 수 있습니다.
```python
bucket = 'testbucket-123456789'
response = client.delete_objects(
    Bucket=bucket,
    Delete={
        "Quiet": "true",
        "Object": [
            {
                "Key": "test1.txt",
                "VersionId": "MTg0NDY3NDI1NjExNjQwNDUxMzU"
            },
            {
                "Key": "test2.txt",
                "VersionId": "MTg0NDY3NDI1NjExNjQwNDUxMzA"
            }
        ]
    }    
)
```
