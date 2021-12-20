## 소개

본 문서는 객체 콘텐츠 인덱스 작업 관련 API 개요 및 SDK 예시 코드를 제공합니다.

| API                                                          | 작업명         | 작업 설명                                  |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [SELECT Object Content](https://intl.cloud.tencent.com/document/product/436/32360) | 객체 콘텐츠 인덱스 | 지정된 객체(CSV 형식 또는 JSON 형식)에서 콘텐츠 인덱스                   |

## SDK API 참고

SDK 모든 인터페이스의 구체적인 매개변수와 방법 설명은 [SDK API](https://cos-dotnet-sdk-doc-1253960454.file.myqcloud.com/)를 참고하십시오.

## 객체 콘텐츠 인덱스

#### 기능 설명

COS Select는 다음과 같은 객체 데이터 형식의 인덱스를 지원합니다.

* CSV 형식: CSV 형식의 객체 스토리지, 고정 세퍼레이터로 구분.
* JSON 형식: JSON 형식의 객체 스토리지, JSON 파일 또는 JSON 리스트.

> !
>- COS Select 사용의 경우, `cos:GetObject` 라이선스가 필수임.
>- CSV, JSON 객체는 UTF-8 형식으로 인코딩 해야 함.
>- COS Select는 GZIP 또는 BZIP2 압축한 CSV, JSON 객체 인덱스를 지원함.
>- COS Select는 SSE-COS 암호화 CSV, JSON 객체 인덱스를 지원함.

#### 예시 코드

[//]: # (.cssg-snippet-select-object)
```objective-c
QCloudSelectObjectContentRequest *request = [QCloudSelectObjectContentRequest new];
// BucketName-Appid로 구성된 버킷 이름. COS 콘솔에서 조회할 수 있습니다. https://console.cloud.tencent.com/cos5/bucket
request.bucket = @"examplebucket-1250000000";
// 객체 키. 객체의 COS 상의 전체 경로로, 디렉터리가 있을 경우 형식은 "dir1/object1"입니다.
request.object = @"exampleobject";
request.selectType = @"2";
// 파일 선택 설정
QCloudSelectObjectContentConfig *config= [QCloudSelectObjectContentConfig new];
/**SQL 표현식, 요청할 인덱스 작업을 나타냄. 예: SELECT s._1 FROM COSObject s.
 이 표현식으로 CSV 형식 객체에서 첫 번째 열 콘텐츠를 인덱스 할 수 있습니다. SQL 관련 표현식의 상세 소개는,
 (Select)[https://cloud.tencent.com/document/product/436/37636] 명령을 참고하십시오.
*/
config.express = @"select * from COSObject";
/**
표현식 유형, 본 항목은 확장 항목으로, 현재 SQL 표현식과 SQL 매개변수만 지원합니다.
*/
config.expressionType = QCloudExpressionTypeSQL;
/**
 인덱스할 객체의 형식 설명.
 */
QCloudInputSerialization *inputS = [QCloudInputSerialization new];
inputS.compressionType = QCloudCOSXMLCompressionTypeNONE;
/**
JSON 객체 형식에 필요한 파일 매개변수 설명
*/
QCloudSerializationJSON *inputJson = [QCloudSerializationJSON new];
/**
    SON 파일 유형:
    DOCUMENT는 JSON 파일에 독립된 JSON 객체 하나 만을 포함하고 있음을 나타내며, 해당 객체는 여러 행으로 나눠질 수 있습니다.
    LINES는 JSON 객체 중의 모든 행이 독립된 JSON 객체 하나를 포함하고 있음을 나타냅니다.
    유효 값: DOCUMENT, LINES
    */
inputJson.type = QCloudInputJSONFileTypeDocument;
inputS.serializationJSON = inputJson;
config.inputSerialization = inputS;
/**
 인덱스 결과 출력 형식 설명
 */
QCloudOutputSerialization *outputS = [QCloudOutputSerialization new];

QCloudSerializationJSON *outputJson = [QCloudSerializationJSON new];
/**
    출력 결과의 기록을 여러 행의 문자로 구분합니다. 기본적으로 \n을 통해 구분하며, 다음과 같은 8진수 문자를 임의로 지정할 수 있습니다:
 쉼표, 세미콜론, Tab 등. 해당 매개변수는 최대 2바이트를 지원하며, \r\n와 같은 형식의 세퍼레이터를 입력할 수 있습니다. 기본 설정: \n.
    */
outputJson.outputRecordDelimiter = @"\n";
/**
     JSON 객체 형식에 필요한 파일 매개변수 설명
     */
outputS.serializationJSON = outputJson;

config.outputSerialization = outputS;
/**
 QueryProgress 쿼리 진행률 정보 반환 여부, COS Select를 선택할 경우 주기적으로 쿼리 진행률을 반환합니다.
 */
QCloudRequestProgress *requestProgress = [QCloudRequestProgress new];
requestProgress.enabled = @"FALSE";
config.requestProgress =requestProgress;
request.selectObjectContentConfig  = config;
/**
 파일 저장 로컬 경로
 */
request.downloadingURL = [NSURL fileURLWithPath:QCloudFileInSubPath(@"test", @"2.json")];
[request setDownProcessBlock:^(int64_t bytesDownload, int64_t totalBytesDownload, int64_t totalBytesExpectedToDownload) {
    NSLog(@"⏬⏬⏬⏬DOWN [Total]%lld  [Downloaded]%lld [Download]%lld", totalBytesExpectedToDownload, totalBytesDownload, bytesDownload);
}];

[request setFinishBlock:^(id  _Nonnull result, NSError * _Nonnull error) {
    NSLog(@"result = %@",result);
}];
[[QCloudCOSXMLService defaultCOSXML] SelectObjectContent:request];
```

>?더 많은 전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/ListObjects.m)를 참고하십시오.

**Swift**

[//]: # (.cssg-snippet-select-object)
```swift
let request = QCloudSelectObjectContentRequest.init();
// BucketName-Appid로 구성된 버킷 이름. COS 콘솔에서 조회할 수 있습니다. https://console.cloud.tencent.com/cos5/bucket
request.bucket = "examplebucket-1250000000";
// 객체 키. 객체의 COS 상의 전체 경로로, 디렉터리가 있을 경우 형식은 "dir1/object1"입니다.
request.object = "exampleobject";
//이 인터페이스 버전 정보를 나타냅니다.
request.selectType = "2";
// 파일 선택 설정
let config = QCloudSelectObjectContentConfig();
/**SQL 표현식, 요청할 인덱스 작업을 나타냄. 예: SELECT s._1 FROM COSObject s.
 이 표현식으로 CSV 형식 객체에서 첫 번째 열 콘텐츠를 인덱스 할 수 있습니다. SQL 관련 표현식의 상세 소개는,
 (Select)[https://cloud.tencent.com/document/product/436/37636] 명령을 참고하십시오.
*/

config.express = "Select * from COSObject";
/**
표현식 유형, 본 항목은 확장 항목으로, 현재 SQL 표현식과 SQL 매개변수만 지원합니다.
*/
config.expressionType = .SQL;

/**
 인덱스할 객체의 형식 설명.
 */
let inputS = QCloudInputSerialization();
inputS.compressionType = .NONE;
/**
    JSON 객체 형식에 필요한 파일 매개변수 설명
    */
let inputJson = QCloudSerializationJSON.init();
/**
    SON 파일 유형:
    DOCUMENT는 JSON 파일에 독립된 JSON 객체 하나 만을 포함하고 있음을 나타내며, 해당 객체는 여러 행으로 나눠질 수 있습니다.
    LINES는 JSON 객체 중의 모든 행이 독립된 JSON 객체 하나를 포함하고 있음을 나타냅니다.
    유효 값: DOCUMENT, LINES
    */
inputJson.type = .document;

inputS.serializationJSON = inputJson;

config.inputSerialization = inputS;

/**
 인덱스 결과 출력 형식 설명
 */
let outputS = QCloudOutputSerialization.init();

let outputJson = QCloudSerializationJSON.init();
/**
    출력 결과의 기록을 여러 행의 문자로 구분합니다. 기본적으로 \n을 통해 구분하며, 다음과 같은 8진수 문자를 임의로 지정할 수 있습니다:
 쉼표, 세미콜론, Tab 등. 해당 매개변수는 최대 2바이트를 지원하며, \r\n와 같은 형식의 세퍼레이터를 입력할 수 있습니다. 기본 설정: \n.
    */
outputJson.outputRecordDelimiter = "\n";
outputS.serializationJSON = outputJson;

config.outputSerialization = outputS;
/**
 QueryProgress 쿼리 진행률 정보 반환 여부, COS Select를 선택할 경우 주기적으로 쿼리 진행률을 반환합니다.
 */
let requestProgress = QCloudRequestProgress.init();
requestProgress.enabled = "FALSE";
config.requestProgress = requestProgress;
request.selectObjectContentConfig = config;
//파일 로컬 스토리지 경로
request.downloadingURL = NSURL.fileURL(withPath: QCloudFileInSubPath("test", "2.json"));
request.finishBlock = {(result,error) in
    if error != nil{
        print(error!)
    }else{
        print(result!);
    }
 }

QCloudCOSXMLService.defaultCOSXML().selectObjectContent(request);
```

>?더 많은 전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/SelectObject.swift)를 참고하십시오.
