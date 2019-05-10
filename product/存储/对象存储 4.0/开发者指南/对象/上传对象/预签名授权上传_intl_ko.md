## 적용 시나리오

모든 버킷 및 객체는 기본적으로 비공개입니다. 타사에서 버킷에 객체를 업로드할 수 있지만 CAM 계정이나 임시 키 등 방식을 사용하지 못하게 하려면 임시 업로드 작업을 완료하기 위해 사전 서명 URL 방식으로 서명을 제출할 수 있습니다. 유효한 사전 서명 URL을 받은 사람은 누구나 객체를 업로드할 수 있습니다.

사전 서명 URL을 생성할 때 서명에 객체 키를 포함시켜 지정된 경로의 업로드를 허용하는 것을 설정할 수 있습니다. 그리고 HTTP 요청 방법을 지정하여 업로드, 다운로드 및 삭제 등 구체적인 객체 작업을 제한할 수 있습니다. 게다가 SDK에 사전 서명 URL의 유효 기간을 지정하여 만료된 URL이 권한이 없는 사용자에 의해 사용되지 않도록 할 수 있습니다.

## 사용 방법

### REST API 사용

REST API를 사용하여 객체 획득 요청을 시작할 수 있습니다. [GET Object 문서](https://cloud.tencent.com/document/product/436/7753)를 참조할 수 있습니다.

### Java SDK 사용

COS의 Java SDK에서 이 방법을 제공하며 [Java SDK API 문서의 사전 서명 생성 부분](https://cloud.tencent.com/document/product/436/12263#.E7.94.9F.E6.88.90.E9.A2.84.E7.AD.BE.E5.90.8D.E9.93.BE.E6.8E.A5)을 참조할 수 있습니다.

#### 절차 설명

1. 클라이언트 cosClient를 초기화합니다.
2. generatePresignedUrl 방법을 실행하여 업로드 서명을 가져와서 http 방법에 전송하며 매개변수는 PUT입니다.

#### 예제 코드

아래 예제 코드는 사전 서명 업로드 URL을 생성하여 객체를 업로드하는 방법을 보여줍니다.

```java
// 1 사용자 인증 정보(secretId, secretKey)를 초기화합니다.
COSCredentials cred = new BasicCOSCredentials("AKIDXXXXXXXX", "1A2Z3YYYYYYYYYY");
// 2 버킷의 지역을 설정합니다. COS 영역의 약어는 다음 링크를 참조하십시오. https://cloud.tencent.com/document/product/436/6224
ClientConfig clientConfig = new ClientConfig(new Region("ap-beijing-1"));
// 3 COS 클라이언트 생성
COSClient cosclient = new COSClient(cred, clientConfig);
// 버킷 이름에는 appid가 포함되어야 합니다.
String bucketName = "mybucket-1251668577";

String key = "aaa.txt";
Date expirationTime = new Date(System.currentTimeMillis() + 30 * 60 * 1000);
// 사전 서명 업로드 URL을 생성합니다.
URL url = cosclient.generatePresignedUrl(bucketName, key, expirationTime, HttpMethodName.PUT);

// 사전 서명 URL으로 파일을 업로드합니다.
try {
    HttpURLConnection connection = (HttpURLConnection) url.openConnection();
    connection.setDoOutput(true);
    connection.setRequestMethod("PUT");
    OutputStreamWriter out = new OutputStreamWriter(connection.getOutputStream());
    // 업로드할 데이터를 입력합니다. 
    out.write("This text uploaded as object.");
    out.close();
    int responseCode = connection.getResponseCode();
    System.out.println("Service returned response code " + responseCode);
} catch (ProtocolException e) {
    e.printStackTrace();
} catch (IOException e) {
    e.printStackTrace();
}

cosclient.shutdown();
```

### Node.js SDK 사용

#### 절차 설명

1. npm 의존 패키지를 설치합니다.
```shell
npm i cos-nodejs-sdk-v5
```

2. 테스트 파일 test.js를 생성하고, 명령행에서 ```node test.js```를 실행합니다.

#### 예제 코드

```javascript
var COS = require('cos-nodejs-sdk-v5');
var request = require('request');

var SecretId = 'AKIDxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'; // 사용자의 SecretKey로 대체합니다.
var SecretKey = 'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx';    // 사용자의 SecretKey로 대체합니다.
var Bucket = 'test-1250000000';                        // 사용자의 버킷으로 대체합니다.
var Region = 'ap-guangzhou';                           // 사용자의 지역으로 대체합니다.

var cos = new COS({SecretId: SecretId, SecretKey: SecretKey});
var url = cos.getObjectUrl({
    Bucket: Bucket,
    Region: Region,
    Method: 'PUT',
    Key: '1.jpg', // 다운로드할 파일의 경로로 바꿉니다.
    Expires: 60
});
console.log(url);

// 자체로 파일 업로드
request({
    method: 'PUT',
    url: url,
    body: fs.readFileSync('./1.jpg'),
}, function (err, response, body) {
    console.log(response.statusCode);
    console.log(response.headers.etag);
    console.log(body);
});
```

