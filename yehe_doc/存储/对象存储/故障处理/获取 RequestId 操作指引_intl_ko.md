## 소개

COS(Cloud Object Storage) 서비스에서 요청이 전송될 때마다, COS 서버는 해당 요청에 대한 ID, 즉 RequestId를 생성합니다. 본문은 각 시나리오에서 RequestId를 획득하는 방법에 대해 소개합니다. 

## 콘솔에서 브라우저를 통해 획득

1. [COS 콘솔](https://console.cloud.tencent.com/cos5)에 로그인한 후, 왼쪽 사이드바에서 **버킷 리스트**를 클릭해 버킷 리스트 페이지로 이동합니다.
2. 액세스할 버킷을 클릭하여 이동합니다. 
3. ‘F12’를 눌러 브라우저의 개발자 툴 페이지로 이동합니다. 
4. 개발자 툴 상단의 **Network**를 클릭합니다. 
![](https://main.qcloudimg.com/raw/0a201a890f54bfabc4267e9c86c89338.png)
5. 다운로드할 파일명 우측의 **다운로드**를 클릭합니다. 개발자 툴 페이지에서 다운로드할 파일명 입력 및 필터링하여 파일을 선택하고, **Headers**를 클릭하여 **Response Headers** 섹션에서 RequestId 정보를 획득합니다. 
![](https://main.qcloudimg.com/raw/f5e5453f257fbd86a38d2c8508c968bd.png)

## 파일 액세스 실패 시 획득

파일 액세스에 실패할 경우 페이지에서 표시한 반환된 XML 정보에서 **RequestId 노드 정보**를 획득합니다. 
![](https://main.qcloudimg.com/raw/e0d4149121fb0022640465ff690810e1.png)

아래의 작업을 통해서도 획득할 수 있습니다.
1. ‘F12’를 눌러 브라우저의 개발자 툴 페이지로 이동합니다. 
2. 페이지 상단의 **Network**를 클릭하여 All 유형을 선택하면 Response Headers에서 RequestId 필드 정보를 찾을 수 있습니다. 
![](https://main.qcloudimg.com/raw/ac6902c6ac615a9ec2978a5999a49073.png)

## SDK를 통해 획득

SDK에는 너무 많은 인터페이스가 포함되어 있어 모든 인터페이스 예시를 하나씩 나열하는 것이 불가능하므로 모든 SDK는 **파일 업로드**를 예시로 현재 작업의 RequestId를 얻는 방법을 나타냅니다.

### .NET SDK를 통해 획득

```
try
{
 String bucket = "examplebucket-1250000000"; //버킷, 형식: BucketName-APPID
 string cosPath = "test.cs"; // 객체 키
 byte[] data = System.Text.Encoding.Default.GetBytes("Hello COS"); // 이진법 데이터
 PutObjectRequest putObjectRequest = new PutObjectRequest(bucket, cosPath, data);
 
 PutObjectResult result = cosXml.PutObject(putObjectRequest);
 string requestId = result.responseHeaders.GetValueOrDefault("x-cos-request-id")[0];
 Console.WriteLine(requestId);
}
catch (COSXML.CosException.CosClientException clientEx)
{
 //요청 실패
 Console.WriteLine("CosClientException: " + clientEx);
}
catch (COSXML.CosException.CosServerException serverEx)
{
 //요청 실패
 Console.WriteLine("CosServerException: " + serverEx.GetInfo());
}
```

 

### Go SDK를 통해 획득

```
package main
 
import (
   "context"
   "fmt"
   "net/http"
   "net/url"
   "strings"
   "github.com/tencentyun/cos-go-sdk-v5"
)
 
func main() {
   // examplebucket-1250000000과 COS_REGION을 실제 정보로 수정합니다.
   u, _ := url.Parse("https://examplebucket-1250000000.cos.COS_REGION.myqcloud.com")
   b := &cos.BaseURL{BucketURL: u}
   c := cos.NewClient(b, &http.Client{
       Transport: &cos.AuthorizationTransport{
           SecretID:  "SECRETID",
           SecretKey: "SECRETKEY",
       },
   })
   // 객체 키(Key)는 버킷 내 객체의 고유 식별자입니다.
   // 예를 들어, 객체의 액세스 도메인 `examplebucket-1250000000.cos.COS_REGION.myqcloud.com/test.go`에서 객체 키는 test.go입니다.
   name := "test.go"
   // 1. 문자열로 객체 업로드
   f := strings.NewReader("Hello COS")
 
   response, err := c.Object.Put(context.Background(), name, f, nil)
   if err != nil {
       // error정보에는 RequestId 필드가 포함되어 있습니다. 
       panic(err)
   }
   requestId := response.Header.Get("X-Cos-Request-Id")
   fmt.Println(requestId)
}
```

### Java SDK를 통해 획득

```
// 1 사용자의 개인 정보(secretId, secretKey)를 초기화합니다.
String secretId = "SECRETID";
String secretKey = "SECRETKEY";
COSCredentials cred = new BasicCOSCredentials(secretId, secretKey);
// 2 bucket의 리전 설정. COS 리전의 약칭은 https://cloud.tencent.com/document/product/436/6224 참고 바랍니다. 
// clientConfig에 region, https(기본값: http), 타임아웃, 프록시 등을 설정하는 set 메소드가 포함되어 있습니다. 사용 시 소스 코드 또는 FAQ의 Java SDK 부분을 참고하십시오.
Region region = new Region("COS_REGION");
ClientConfig clientConfig = new ClientConfig(region);
// https 프로토콜 설정 및 사용 권장
clientConfig.setHttpProtocol(HttpProtocol.https);
// 3 cos 클라이언트 생성
COSClient cosClient = new COSClient(cred, clientConfig);
// Bucket 이름 생성 형식은 BucketName-APPID이며, 이 곳에 입력하는 버킷 이름은 반드시 해당 형식을 따라야 합니다.
String bucketName = "examplebucket-1250000000";
 
String content = "Hello COS";
String key = "test.java";
PutObjectResult putObjectResult = cosClient.putObject(bucketName, key, content);
String requestId = putObjectResult.getRequestId();
System.out.println(requestId);
```


### Python SDK를 통해 획득

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
import sys
import logging

# 일반적으로 로그 레벨은 INFO이며 위치 지정이 필요한 경우 DEBUG로 수정할 수 있으며 이 때 SDK는 서버와의 통신 정보를 출력합니다.
logging.basicConfig(level=logging.INFO, stream=sys.stdout)

# 1. secret_id, secret_key, region 등을 포함한 사용자 속성을 설정합니다. Appid는 CosConfig에서 제거되었습니다. 매개변수 Bucket에 Appid를 포함시키십시오. Bucket은 BucketName-Appid로 구성됩니다.
secret_id = 'SecretId'     # 사용자의 SecretId로 대체합니다. CAM 콘솔에 로그인하여 확인 및 관리하십시오. https://console.cloud.tencent.com/cam/capi
secret_key = 'SecretKey'   # 사용자의 SecretKey로 대체합니다. CAM 콘솔에 로그인하여 확인 및 관리하십시오. https://console.cloud.tencent.com/cam/capi
region = 'ap-beijing'      # 사용자의 region으로 대체합니다. 생성된 버킷이 속한 region은 콘솔에서 확인 가능합니다. https://console.cloud.tencent.com/cos5/bucket
                           # COS에서 지원되는 모든 region 목록은 다음을 참고하십시오. https://cloud.tencent.com/document/product/436/6224
token = None               # 영구 키를 사용하는 경우 token을 입력할 필요가 없으나, 임시 키를 사용하는 경우 입력해야 합니다. 임시 키 생성 및 사용 가이드는 다음을 참고하십시오. https://cloud.tencent.com/document/product/436/14048
scheme = 'https'            # http/https 프로토콜로 COS에 액세스 지정. 기본값: https, 입력하지 않아도 됨

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)
client = CosS3Client(config)

try:
    response = client.put_object(
        Bucket='examplebucket-1250000000',
        Key='exampleobject',
        Body=b'abcdefg'
    )

    # 요청 정상 반환 시 response를 통해 request-id 조회
    if 'x-cos-request-id' in response:  
        print(response['x-cos-request-id'])

# 요청 실패 시 이상 경고를 통해 request-id 조회
except CosServiceError as e:
    print(e.get_request_id())
```

### JavaScript SDK를 통해 획득

```
cos.putObject({
    Bucket: ’examplebucket-1250000000’, /* 필수 */
    Region: 'COS_REGION',    /* 필수 */
    Key: 'test.js',              /* 필수 */
    StorageClass: ’STANDARD’,
    Body: 'Hello COS',
    onProgress: function(progressData) {
        console.log(JSON.stringify(progressData));
    }
}, function(err, data) {
    var requestId = (err || data).headers['x-cos-request-id'];
    console.log(requestId );
});
```

 

### Node.js SDK를 통해 획득

```
var COS = require('cos-nodejs-sdk-v5');
var cos = new COS({
    SecretId: 'SECRETID',
    SecretKey: 'SECRETKEY'
});
 
cos.putObject({
    Bucket: ’examplebucket-1250000000’, /* 필수 */
    Region: 'COS_REGION',    /* 필수 */
    Key: 'test.nodejs',              /* 필수 */
    StorageClass: ’STANDARD’,
    Body: Buffer.from('Hello COS'),
    onProgress: function(progressData) {
        console.log(JSON.stringify(progressData));
    }
}, function(err, data) {
    var requestId = (err || data).headers['x-cos-request-id'];
    console.log(requestId );
});
```

### WeChat 미니프로그램 SDK를 통해 획득

```
var COS = require('cos-wx-sdk-v5');
var cos = new COS({
    SecretId: 'SECRETID',
    SecretKey: 'SECRETKEY'
});
 
cos.putObject({
    Bucket: ’examplebucket-1250000000’, /* 필수 */
    Region: 'COS_REGION',    /* 필수 */
    Key: 'test.js',              /* 필수 */
    StorageClass: ’STANDARD’,
    Body: 'Hello COS',
    onProgress: function(progressData) {
        console.log(JSON.stringify(progressData));
    }
}, function(err, data) {
    var requestId = (err || data).headers['x-cos-request-id'];
    console.log(requestId );
});
```

 

### PHP SDK를 통해 획득

```
$secretId = "SECRETID"; //"Tencent Cloud API 키 SecretId";
$secretKey = "SECRETKEY"; //"Tencent Cloud API 키 SecretKey";
$region = "COS_REGION"; //기본 버킷 리전 설정
$cosClient = new Qcloud\Cos\Client(
   array(
       'region' => $region,
       'schema' => 'https', //프로토콜 헤더, 기본값: http
       'credentials'=> array(
           'secretId'  => $secretId ,
           'secretKey' => $secretKey)));
# 파일 업로드
## putObject(업로드 인터페이스, 최대 5G 파일까지 업로드 가능)
### 메모리에 있는 문자열 업로드
try {
   $bucket = "examplebucket-1250000000"; //버킷 이름. 형식: BucketName-APPID
   $key = "test.php"; //여기서 key는 객체 키로, 버킷 내 객체의 고유 식별자입니다. 
   $result = $cosClient->putObject(array(
       'Bucket' => $bucket,
       'Key' => $key,
       'Body' => 'Hello COS'));
   $requestId = $result['RequestId'];
   print_r($requestId);
} catch (\Exception $e) {
   echo "$e\n";
}
```


### iOS SDK를 통해 획득

```
QCloudCOSXMLUploadObjectRequest* put = [QCloudCOSXMLUploadObjectRequest new];
/** 로컬 파일 경로. URL이 file:// 로 시작되는지 확인하십시오. 형식은 다음과 같습니다.
1. [NSURL URLWithString:@"file:////var/mobile/Containers/Data/Application/DBPF7490-D5U8-4ABF-A0AF-CC49D6A60AEB/Documents/exampleobject"]
2. [NSURL fileURLWithPath:@"/var/mobile/Containers/Data/Application/DBPF7490-D5U8-4ABF-A0AF-CC49D6A60AEB/Documents/exampleobject"]
*/
NSURL* url = [NSURL fileURLWithPath:@"파일의 URL"];
// BucketName-Appid로 구성된 버킷 이름. COS 콘솔에서 조회할 수 있습니다. https://console.cloud.tencent.com/cos5/bucket
put.bucket = @"examplebucket-1250000000";
// 객체 키, 객체의 COS 상의 전체 경로로, 디렉터리가 있을 경우 형식은 "video/xxx/movie.mp4"입니다.
put.object = @"exampleobject";
// 업로드할 객체 콘텐츠입니다. NSData* 또는 NSURL* 유형의 변수를 전달할 수 있습니다.
put.body =  url;
// 업로드 진행률 수신
[put setSendProcessBlock:^(int64_t bytesSent,
                           int64_t totalBytesSent,
                           int64_t totalBytesExpectedToSend) {
    //      bytesSent                 발송할 바이트 수(대용량 파일은 여러 번으로 나누어 발송해야 할 수 있습니다.)
    //      totalBytesSent            발송한 바이트 수
    //      totalBytesExpectedToSend  이번 업로드에서 발송할 총 바이트 수(파일 1개의 크기)
}];
// 업로드 결과 수신
[put setFinishBlock:^(QCloudUploadObjectResult *result, NSError *error) {
    // requestid 가져오기
   [result.__originHTTPURLResponse__.allHeaderFields objectForKey:@"x-cos-request-id"]
}];
[put setInitMultipleUploadFinishBlock:^(QCloudInitiateMultipartUploadResult *
                                        multipleUploadInitResult,
                                        QCloudCOSXMLUploadObjectResumeData resumeData) {
    // 멀티파트 업로드 초기화 완료 후 해당 block 콜백, 이곳에서 resumeData, uploadid를 획득할 수 있습니다.
    NSString* uploadId = multipleUploadInitResult.uploadId;
}];
[[QCloudCOSTransferMangerService defaultCOSTransferManager] UploadObject:put];
```


### Android SDK를 통해 가져오기

```
// 1. TransferService 초기화. 동일 설정의 경우 동일한 TransferService를 재사용해야 합니다.
TransferConfig transferConfig = new TransferConfig.Builder()
        .build();
CosXmlServiceConfig cosXmlServiceConfig = new CosXmlServiceConfig.Builder()
        .setRegion(COS_REGION)
        .builder();
CosXmlService cosXmlService = new CosXmlService(context, cosXmlServiceConfig, credentialProvider);
TransferService transferService = new TransferService(cosXmlService, transferConfig);

// 2. PutObjectRequest 초기화
String bucket = "examplebucket-1250000000"; //버킷. 형식: BucketName-APPID
String cosPath = "exampleobject"; //버킷 내 객체 위치 식별자, 즉 객체 키
String srcPath = "examplefilepath"; //로컬 파일의 절대 경로
PutObjectRequest putObjectRequest = new PutObjectRequest(bucket,
        cosPath, srcPath);

// 3. upload 메소드를 호출하여 파일 업로드
final COSUploadTask uploadTask = transferService.upload(putObjectRequest);
uploadTask.setCosXmlResultListener(new CosXmlResultListener() {
    @Override
    public void onSuccess(CosXmlRequest request, CosXmlResult result) {
        // 업로드 성공, 여기에서 requestId를 얻을 수 있습니다.
        String requestId = result.getHeader("x-cos-request-id");
    }

    @Override
    public void onFail(CosXmlRequest request,
                       CosXmlClientException clientException,
                       CosXmlServiceException serviceException) {
        // CosXmlServiceException 예외 발생 시에만 requestId가 있습니다.
        if (serviceException != null) {
            String requestId = serviceException.getRequestId();
        }
    }
});
```




