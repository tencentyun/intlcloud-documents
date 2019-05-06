## 적용 시나리오

COS에서 객체를 직접적으로 가져오기 위한 요청을 시작할 수 있습니다. 객체를 가져올 때 다음 옵션을 사용할 수 있습니다.

- 완전한 객체 가져오기: 직접적으로 GET 요청을 시작하여 완전한 객체 데이터를 가져올 수 있습니다.
- 객체의 일부 가져오기: GET 요청에서 `Range` 요청 헤더를 사용하여 특정 바이트 범위를 검색할 수 있습니다. 여러 범위의 검색은 지원되지 않습니다.

객체의 메타데이터는 HTTP 응답 헤더로 객체의 콘텐츠와 함께 반환됩니다. GET 요청이 URL 매개변수를 사용하는 방식으로 응답에서 일부 특정 응답 메타데이터 값(예: `Content-Dispositon`의 응답 값)을 무시할 수 있습니다. 수정 가능한 응답 헤더에는 다음 내용이 포함됩니다.

- Content-Type
- Content-Language
- Expires
- Cache-Control
- Content-Disposition
- Content-Encoding

## 사용 방법

### REST API 사용

REST API를 사용하여 객체 획득 요청을 시작할 수 있습니다. [GET Object 문서](https://cloud.tencent.com/document/product/436/7753)를 참조할 수 있습니다.

### C++ SDK 사용

COS의 C++ SDK에서 이 방법을 제공하며 [C++ SDK API 문서의 객체 획득 부분](https://cloud.tencent.com/document/product/436/12302#get-object)을 참조할 수 있습니다.

#### 절차 설명

1. 구성 파일 경로를 전달하여 CosConfig 및 CosAPI 객체를 초기화합니다.
2. GetObject() 방법을 실행하여 로컬 또는 데이터 스트림으로 파일을 다운로드합니다. 버킷 이름과 객체 키 이름이 필요합니다.

#### 예제 코드

다음 예제 코드는 간단하게 객체를 획득하는 방법을 보여줍니다.

``` cpp
// 로컬로 다운로드
{
    // 매개변수 appid, bucketname, object 및 로컬 경로(파일 이름 포함)가 요청에 필요해야 합니다.
    qcloud_cos::GetObjectByFileReq req(bucket_name, object_name, local_path);
    qcloud_cos::GetObjectByFileResp resp;
    qcloud_cos::CosResult result = cos.GetObject(req, &resp);
    if (result.IsSucc()) {
        // 다운로드가 성공하었습니다. GetObjectByFileResp의 멤버 함수를 호출할 수 있습니다.
    } else {
        // 다운로드가 실패하였습니다. CosResult의 멤버 함수를 호출하여 requestID와 같은 오류 정보를 출력할 수 있습니다.
    }
}

// 스트림으로 다운로드
{
    // 매개변수 appid, bucketname, object 및 출력 스트림이 요청에 필요해야 합니다.
    std::ostringstream os;
    qcloud_cos::GetObjectByStreamReq req(bucket_name, object_name, os);
    qcloud_cos::GetObjectByStreamResp resp;
    qcloud_cos::CosResult result = cos.GetObject(req, &resp);
    if (result.IsSucc()) {
        // 다운로드가 성공하었습니다. GetObjectByStreamResp의 멤버 함수를 호출할 수 있습니다.
    } else {
        // 다운로드가 실패하였습니다. CosResult의 멤버 함수를 호출하여 requestID와 같은 오류 정보를 출력할 수 있습니다.
    }
}

// 여러 스레드로 로컬에 다운로드
{
    // 매개변수 appid, bucketname, object 및 로컬 경로(파일 이름 포함)가 요청에 필요해야 합니다.
    qcloud_cos::MultiGetObjectReq req(bucket_name, object_name, local_path);
    qcloud_cos::MultiGetObjectResp resp;
    qcloud_cos::CosResult result = cos.GetObject(req, &resp);
    if (result.IsSucc()) {
        // 다운로드가 성공하었습니다. MultiGetObjectResp의 멤버 함수를 호출할 수 있습니다.
    } else {
        // 다운로드가 실패하였습니다. CosResult의 멤버 함수를 호출하여 requestID와 같은 오류 정보를 출력할 수 있습니다.
    }
}
```

요청의 멤버 함수를 설정하여 특정 응답 헤더를 설정할 수 있습니다.

``` cpp
// 응답 헤더에 Content-Type 매개변수를 설정합니다.
void SetResponseContentType(const std::string& str);

// 응답 헤더에 Content-Language 매개변수를 설정합니다.
void SetResponseContentLang(const std::string& str);

// 응답 헤더에 Content-Expires 매개변수를 설정합니다.
void SetResponseExpires(const std::string& str);

// 응답 헤더에 Cache-Control 매개변수를 설정합니다.
void SetResponseCacheControl(const std::string& str);

// 응답 헤더에 Content-Disposition 매개변수를 설정합니다.
void SetResponseContentDisposition(const std::string& str);

// 응답 헤더에 Content-Encoding 매개변수를 설정합니다.
void SetResponseContentEncoding(const std::string& str);
```
### Java SDK 사용

COS의 Java SDK에서 이 방법을 제공하며 [Java SDK API 문서의 객체 획득 부분](https://cloud.tencent.com/document/product/436/12263#get-object)을 참조할 수 있습니다.

#### 절차 설명

1. 클라이언트 cosClient를 초기화합니다.
2. getObject 방법을 실행하여 입력 스트림을 취득하거나 컨텐츠를 로컬에 저장합니다.

#### 예제 코드
(1) 다음 예제 코드는 객체(버전 제어 없음)를 다운로드하는 방법을 보여줍니다.

```java
// 1 사용자 인증 정보(appid, secretId, 및 secretKey)를 초기화합니다.
COSCredentials cred = new BasicCOSCredentials("1250000", "AKIDXXXXXXXX", "1A2Z3YYYYYYYYYY");
// 2 버킷의 지역을 설정합니다. COS 영역의 약어는 다음 링크를 참조하십시오. https://cloud.tencent.com/document/product/436/6224
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// 3 COS 클라이언트를 생성합니다.
COSClient cosclient = new COSClient(cred, clientConfig);
// 버킷 이름을 설정합니다.
String bucketName = "mybucket";
String key = "aaa.txt";

try {
    // 파일을 다운로드합니다.
    COSObject cosObject = cosclient.getObject(bucketName, key);
    // 입력 스트림을 획득합니다.
    COSObjectInputStream cosObjectInput = cosObject.getObjectContent();
    // 입력 스트림을 종료합니다.
    cosObjectInput.close();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
}
```
(2)`GetObjectRequest`는 객체로부터 검색할 데이터 바이트의 범위를 지정하는 것을 지원합니다. 다음 예제 코드는 바이트 범위를 지정하는 방법을 보여줍니다.

```java
// 1 사용자 인증 정보(appid, secretId, 및 secretKey)를 초기화합니다.
COSCredentials cred = new BasicCOSCredentials("1250000", "AKIDXXXXXXXX", "1A2Z3YYYYYYYYYY");
// 2 버킷 지역을 설정합니다. COS 지역의 약칭: https://cloud.tencent.com/document/product/436/6224
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// 3 COS 클라이언트를 생성합니다.
COSClient cosclient = new COSClient(cred, clientConfig);
// 버킷 이름을 설정합니다.
String bucketName = "mybucket";
String key = "aaa.txt";

try {
    GetObjectRequest getObjectRequest = new GetObjectRequest(bucketName, key);
    // 다운로드에 첫 11 바이트를 설정합니다.
    getObjectRequest.setRange(0, 10);
    // 파일을 다운로드합니다.
    COSObject cosObject = cosclient.getObject(bucketName, key);
    // 입력 스트림을 획득합니다.
    COSObjectInputStream cosObjectInput = cosObject.getObjectContent();
    // 입력 스트림을 종료합니다.
    cosObjectInput.close();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
}
```
(3) 객체를 검색할 때,`ResponseHeaderOverrides` 객체를 사용하고 응답 헤더 값을 대체하기 위해 해당하는 요청 속성을 설정할 수 있습니다. 다음은 예시입니다.

```java
// 1 사용자 인증 정보(appid, secretId, 및 secretKey)를 초기화합니다.
COSCredentials cred = new BasicCOSCredentials("1250000", "AKIDXXXXXXXX", "1A2Z3YYYYYYYYYY");
// 2 버킷의 지역을 설정합니다. COS 영역의 약어는 다음 링크를 참조하십시오. https://cloud.tencent.com/document/product/436/6224
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// 3 COS 클라이언트를 생성합니다.
COSClient cosclient = new COSClient(cred, clientConfig);
// 버킷 이름을 설정합니다.
String bucketName = "mybucket";
String key = "aaa.txt";

try {
    GetObjectRequest getObjectRequest = new GetObjectRequest(bucketName, key);
    ResponseHeaderOverrides responseHeaders = new ResponseHeaderOverrides();
    String responseContentType="image/x-icon";
    String responseContentEncoding = "gzip,deflate,compress";
    String responseContentLanguage = "zh-CN";
    String responseContentDispositon = "filename=\"abc.txt\"";
    String responseCacheControl = "no-cache";
    String expireStr = DateUtils.formatRFC822Date(new Date(System.currentTimeMillis() + 24 * 3600 * 1000));
    responseHeaders.setContentType(responseContentType);
    responseHeaders.setContentEncoding(responseContentEncoding);
    responseHeaders.setContentLanguage(responseContentLanguage);
    responseHeaders.setContentDisposition(responseContentDispositon);
    responseHeaders.setCacheControl(responseCacheControl);
    responseHeaders.setExpires(expireStr);
    getObjectRequest.setResponseHeaders(responseHeaders);
    // 파일을 다운로드합니다.
    COSObject cosObject = cosclient.getObject(bucketName, key);
    // 입력 스트림을 획득합니다.
    COSObjectInputStream cosObjectInput = cosObject.getObjectContent();
    // 입력 스트림을 종료합니다.
    cosObjectInput.close();
} catch (CosServiceException e) {
    e.printStackTrace();
} catch (CosClientException e) {
    e.printStackTrace();
}
```
### JavaScript SDK 사용

#### 절차 설명

1. 서명 서버를 준비하고 서명을 얻기 위해 프런트 엔드에 auth.php API를 제공합니다. 자세한 내용은 [백 엔드 서명 예시](https://github.com/tencentyun/cos-js-sdk-v5/tree/master/server)를 참조할 수 있습니다.

2. 테스트 파일 test.html을 생성하고 다음 코드를 작성합니다. 파일을 정적 서버에 두고 `http://127.0.0.1/test.html`로 접근합니다.

#### 예제 코드

다음 예제 코드는 간단하게 객체를 획득하는 방법을 보여줍니다.

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

cos.getObject({
    Bucket: config.Bucket,
    Region: config.Region,
    Key: '1.txt',
}, function (err, data) {
    console.log(err || '파일 내용 크기：' + data.Body.length);
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
다음 예제 코드는 간단하게 객체를 획득하는 방법을 보여줍니다.

```javascript
var fs = require('fs');
var path = require('path');
var COS = require('..');

var SecretId = 'AKIDxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'; // 사용자의 SecretId로 대체합니다
var SecretKey = 'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx';    // 사용자의 SecretKey로 대체합니다.
var Bucket = 'test-1250000000';                        // 사용자의 버킷으로 대체합니다.
var Region = 'ap-guangzhou';                           // 사용자의 지역으로 대체합니다.

var cos = new COS({SecretId: SecretId, SecretKey: SecretKey});
cos.getObject({
    Bucket: Bucket,
    Region: Region,
    Key: '1.jpg',
    Output: fs.createWriteStream(path.resolve(__dirname, '1.download.jpg'))
}, function (err, data) {
    console.log(err || data);
});
```
### PHP SDK 사용

COS의 PHP SDK 에서 이 방법을 제공하며 [PHP SDK API 문서의 파일 다운로드 부분](https://cloud.tencent.com/document/product/436/12267#.E4.B8.8B.E8.BD.BD.E6.96.87.E4.BB.B6)을 참조할 수 있습니다.

#### 절차 설명

1. 클라이언트 cosClient를 초기화합니다.
2. getObject 방법을 실행하여 객체를 획득합니다. 버킷 이름이 필요합니다.
3. SaveAs 필드를 추가하여 가져온 데이터 스트림을 로컬 파일로 저장합니다.

#### 예제 코드

다음 예제 코드는 간단하게 객체를 획득하는 방법을 보여줍니다.

```php
try {
    $result = $cosClient->getObject(array(
        'Bucket' => 'testbucket-125000000',
        'Key' => 'hello.txt',
        'SaveAs' => 'hello.txt'));
    echo($result['Body']);
} catch (\Exception $e) {
    echo "$e\n";
}
```
### Python SDK 사용

COS의 Python SDK에서 이 방법을 제공하며 [Python SDK API 문서의 객체 다운로드 부분](https://cloud.tencent.com/document/product/436/12270#.E6.96.87.E4.BB.B6.E4.B8.8B.E8.BD.BD)을 참조할 수 있습니다.

#### 절차 설명

1. CosConfig 클래스를 사용하여 클라이언트 CosS3Client를 구성하고 초기화합니다.
2. get_object() 방법을 실행하여 데이터 스트림을 획득합니다. 버킷 이름과 객체 키 이름이 필요합니다.

#### 예제 코드

다음 예제 코드는 간단하게 객체를 획득하는 방법을 보여줍니다.

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
response = client.get_object(
    Bucket=bucket,
    Key=file_name,
)
# 객체를 로컬 파일로 획득합니다.
response['Body'].get_stream_to_file('output.txt')
```

get_raw_stream() 방법을 사용하여 객체의 파일 스트림을 가져올 수 있습니다.
```python
response = client.get_object(
    Bucket=bucket,
    Key=file_name,
)
fp = response['Body'].get_raw_stream()
# read() 방법을 호출하여 파일 스트림을 읽습니다.
print fp.read(2)
```

bytes = first-last의 형식으로 Range 매개변수를 설정하여 객체의 특정 바이트 범위를 가져올 수 있습니다.
```python
# 객체의 처음 10바이트를 가져옵니다.
response = client.get_object(
    Bucket=bucket,
    Key=file_name,
    Range='bytes=0-9'
)
```

Response Header 매개변수를 설정하여 특정 응답 헤더를 설정할 수 있습니다.
```python
response = client.get_object(
    Bucket=bucket,
    Key=file_name,
    ResponseCacheControl='no-cache',
    ResponseContentDisposition='attachment; filename=test.txt',
    ResponseContentEncoding='gzip',
    ResponseContentLanguage='zh-cn',
    ResponseContentType='text/html',
    ResponseExpires='Tue, 05 Dec 2017 10:01:19 GMT'
)
```
