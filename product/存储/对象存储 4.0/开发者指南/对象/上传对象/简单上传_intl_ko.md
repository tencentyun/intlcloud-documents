## 적용 시나리오

이 작업은 단일 요청으로 5GB 미만의 객체를 업로드할 때 사용됩니다. 5GB보다 큰 객체의 경우, 멀티파트 업로드를 사용해야 합니다.

객체가 큰(예: 100 MB) 경우 고 대역폭 또는 약한 네트워크 환경에서 멀티파트 업로드를 사용하는 것을 권장합니다.

## 사용 방법
### REST API 사용

REST API를 사용하여 간편 업로드 요청을 보낼 수 있습니다. [PUT Object 문서 설명](https://cloud.tencent.com/document/product/436/7749)을 참조하십시오.

### C++ SDK 사용

이 방법은 COS의 C ++ SDK에서 제공됩니다. [C ++ SDK API 문서 Put Object 섹션](https://cloud.tencent.com/document/product/436/12302#put-object)을 참조하십시오.

#### 절차 설명

1. 구성 파일 경로를 전달하여 CosConfig 및 CosAPI 객체를 초기화합니다.
2. PutObject() 방법을 실행하여 객체를 업로드합니다. 버킷 이름, 객체 키 이름 및 업로드할 내용이 필요합니다.

#### 예제 코드

아래 예제 코드는 객체의 간편 업로드를 하는 방법을 보여줍니다.

``` cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "cpp_sdk_v5-12345";
std::string object_name = "object_name";
// request의 구조 함수에서 로컬 파일 경로의 전송이 필요합니다.
qcloud_cos::PutObjectByFileReq req(bucket_name, object_name, "/path/to/local/file");
// Set 방법을 호출하여 메타데이터 또는 ACL를 설정합니다.
req.SetXCosStorageClass("STANDARD_IA");

qcloud_cos::PutObjectByFileResp resp;
qcloud_cos::CosResult result = cos.PutObject(req, &resp);
```

파일 스트림 객체를 지정하여 파일 스트림을 COS에 업로드할 수 있습니다.

``` cpp
std::istringstream iss("put object");

// request의 구조 함수에서 istream의 전송이 필요합니다.
qcloud_cos::PutObjectByStreamReq req(bucket_name, object_name, iss);
qcloud_cos::PutObjectByStreamResp resp;

qcloud_cos::CosResult result = cos.PutObject(req, &resp);
```
### Java SDK 사용

이 방법은 COS의 Java SDK에서 제공됩니다. [Java SDK API 문서의 PUT Object섹션](https://cloud.tencent.com/document/product/436/12263#put-object.EF.BC.88.E4.B8.8A.E4.BC.A0-object.EF.BC.89)을 참조하십시오.

#### 절차 설명

1. 클라이언트 cosClient를 초기화합니다.
2. putObject 방법을 실행하여 객체를 업로드합니다. 로컬 파일 또는 입력 스트림을 COS에 업로드할 수 있습니다.

#### 예제 코드

(1)`PutObjectRequest`은 간편 업로드의 요청을 캡슐화합니다. 로컬 파일 경로와 COS 경로를 전송하여 스토리지 클래스 및 사용 권한 정보 등을 설정할 수 있습니다. 업로드가 완료되면 `PutObjectResult`가 반환됩니다. 업로드가 실패하면 이상이 발생합니다. 예제 코드는 다음과 같습니다.

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
File localFile = new File("src/test/resources/len10M.txt");
PutObjectRequest putObjectRequest = new PutObjectRequest(bucketName, key, localFile);
// 스토리지 클래스를 설정합니다. 기본적으로 표준(Standard), 저빈도(standard_ia)입니다.
putObjectRequest.setStorageClass(StorageClass.Standard_IA);
try {
    PutObjectResult putObjectResult = cosclient.putObject(putObjectRequest);
    // putobjectResult는 파일의 etag를 반환합니다.
    String etag = putObjectResult.getETag();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
}

// 클라이언트를 종료합니다.
cosclient.shutdown();
```

(2)`PutObjectRequest`는 입력 스트림의 전송과 스트림에서 COS로 업로드를 동시에 지원하는데 길이를 지정해야 합니다. 예제 코드는 다음과 같습니다.

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
File localFile = new File("src/test/resources/len10M.txt");

InputStream input = new ByteArrayInputStream(new byte[10]);
ObjectMetadata objectMetadata = new ObjectMetadata();
// 입력 스트림에서 업로드할 때 반드시 content length를 지정해야 합니다. 그렇지 않으면 http 클라이언트가 모든 데이터를 캐시 하여 메모리 OOM에 저장할 것입니다.
objectMetadata.setContentLength(10);
// contenttype을 설정하여 기본적 다운로드를 할 경우 COS 경로 키의 접미어에 따라 해당 contenttype을 반환합니다. 업로드 시 contenttype 설정이 기본값을 덮어씁니다.
objectMetadata.setContentType("image/jpeg");

PutObjectRequest putObjectRequest =
        new PutObjectRequest(bucketName, key, input, objectMetadata);
// 스토리지 클래스를 설정합니다. 기본적으로 표준(Standard), 저빈도(standard_ia)입니다.
putObjectRequest.setStorageClass(StorageClass.Standard_IA);
try {
    PutObjectResult putObjectResult = cosclient.putObject(putObjectRequest);
    // putobjectResult는 파일의 etag를 반환합니다.
    String etag = putObjectResult.getETag();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
}

// 클라이언트를 종료합니다.        
cosclient.shutdown();
```
### JavaScript SDK 사용

이 방법은 COS의 JavaScript SDK에서 제공됩니다. [JavaScript SDK API 문서의 Put Object 섹션](https://cloud.tencent.com/document/product/436/12260#put-object)을 참조하십시오.

#### 절차 설명

1. 서명 서버를 준비하고 서명을 얻기 위해 프런트 엔드에 auth.php API를 제공합니다. 자세한 내용은 [백 엔드 서명 예시](https://github.com/tencentyun/cos-js-sdk-v5/tree/master/server)를 참조할 수 있습니다.

2. 테스트 파일 test.html을 생성하고 다음 코드를 작성합니다. 파일을 정적 서버에 두고 `http://127.0.0.1/test.html`로 접근합니다.

#### 예제 코드

아래 예제 코드는 객체의 간편 업로드를 하는 방법을 보여줍니다.

```html
<script src="dist/cos-js-sdk-v5.min.js"></script>
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

// 수신자 파일 선택
document.getElementById('file-selector').onchange = function () {

    var file = this.files[0];
    if (!file) return;

    cos.putObject({
        Bucket: Bucket,
        Region: Region,
        Key: file.name,
        Body: file,
    }, function (err, data) {
        console.log(err, data);
    });

};
</script>
```
### Node.js SDK 사용

이 방법은 COS의 Node.js SDK에 제공됩니다. [Node.js SDK API 문서의 Put Object 섹션](https://cloud.tencent.com/document/product/436/12264#put-object)을 참조하십시오.

#### 절차 설명

1. npm 의존 패키지를 설치합니다.
```shell
npm i cos-nodejs-sdk-v5
```

2. 현재 디렉터리에 업로드될 1.jpg 파일을 넣습니다.
3. 테스트 파일 test.js를 생성하고, 명령행에서 `node test.js`를 실행합니다.

#### 예제 코드

아래 예제 코드는 객체의 간편 업로드를 하는 방법을 보여줍니다.

```javascript
var fs = require('fs');
var path = require('path');
var COS = require('cos-nodejs-sdk-v5');

var SecretId = 'AKIDxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'; // 사용자의 SecretKey로 대체합니다.
var SecretKey = 'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx';    // 사용자의 SecretKey로 대체합니다.
var Bucket = 'test-1250000000';                        // 사용자의 버킷으로 대체합니다.
var Region = 'ap-guangzhou';                           // 사용자의 지역으로 대체합니다.

var cos = new COS({SecretId: SecretId, SecretKey: SecretKey});
cos.putObject({
    Bucket: Bucket,
    Region: Region,
    Key: '1.jpg',
    Body: fs.readFileSync(path.resolve(__dirname, '1.jpg'))
}, function (err, data) {
    console.log(err || data);
});
```
### PHP SDK 사용

이 방법은 COS의 PHP SDK에서 제공됩니다. [PHP SDK API 문서의 간단한 파일 업로드 섹션](https://cloud.tencent.com/document/product/436/12267#.E7.AE.80.E5.8D.95.E6.96.87.E4.BB.B6.E4.B8.8A.E4.BC.A0)을 참조하십시오 .

#### 절차 설명

1. 클라이언트 cosClient를 초기화합니다.
2. putObject 방법을 실행하여 데이터 스트림을 업로드합니다. 버킷 이름과 객체 키 이름이 필요합니다.
3. fopen을 통해 파일 스트림을 업로드합니다.

#### 예제 코드

아래 예제 코드는 객체의 간편 업로드를 하는 절차를 보여줍니다.

* 메모리 업로드:
```php
try {
    $result = $cosClient->putObject(array(
        'Bucket' => 'testbucket-125000000',
        'Key' => '11',
        'Body' => 'Hello World!'));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}
```
* 파일 스트림 업로드:
```php
try {
    $result = $cosClient->putObject(array(
        'Bucket' => 'testbucket-125000000',
        'Key' => '11',
        'Body'   => fopen($pathToFile, 'r+')));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}
'Body'   => fopen($pathToFile, 'r+')
```
### Python SDK 사용

이 방법은 COS의 Python SDK에서 제공됩니다. [Python SDK API 문서의 간단한 파일 업로드 섹션](https://cloud.tencent.com/document/product/436/12270#.E7.AE.80.E5.8D.95.E6.96.87.E4.BB.B6.E4.B8.8A.E4.BC.A0)을 참조하십시오.

#### 절차 설명

1. CosConfig 클래스를 사용하여 클라이언트 CosS3Client를 구성하고 초기화합니다.
2. put_object () 방법을 실행하여 객체를 업로드합니다. 버킷 이름, 객체 키 이름 및 업로드 할 내용이 필요합니다.

#### 예제 코드

아래 예제 코드는 객체의 간편 업로드를 하는 방법을 보여줍니다.

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
file_name = 'test.txt'

response = client.put_object(
    Bucket=bucket,
    Key=file_name,
    Body='1234'         
)
```

파일 스트림 객체를 지정하여 파일 스트림을 COS에 업로드할 수 있습니다.
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
file_name = 'test.txt'

# 파일 하나 생성
with open(file_name, 'wb') as fp:
    fp.write('helloworld!')
with open(file_name, 'rb') as fp:
    response = client.put_object(
        Bucket=bucket,
        Key=file_name,
        Body=fp
    )
```

특정 매개변수를 설정하여 객체의 메타 정보를 설정할 수 있습니다.
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
file_name = 'test.txt'

response = client.put_object(
    Bucket=bucket,
    Key=file_name,
    Body='123',
    StorageClass='STANDARD',
    ACL='public-read',
    CacheControl='no-cache',
    ContentDisposition='attachment; filename=test.txt',
    ContentEncoding='gzip',
    ContentLanguage='zh-cn',
    ContentType='text/html',
    Expires='Tue, 05 Dec 2017 10:01:19 GMT',
    Metadata={
        'x-cos-meta-key1': 'value1',
        'x-cos-meta-key2': 'value2'
    }
)
```
