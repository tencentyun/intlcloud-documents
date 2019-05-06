API 문서에서 초기화 과정을 완료했다고 가정합니다. API 문서는 API의 세부 목록을 보여주고 사용 방법에 대한 예시를 드는 데 중점을 둡니다. 조회 시 Command + F로 API를 조회한 후 제공된 API 설명을 참조하고 해당 프로젝트에 예시를 복사하여 실행하는 것을 권장합니다.    

> ?더 많은 기능이 필요하거나 반환된 매개변수의 의미를 이해하지 못하는 경우, 코드의 주석을 직접 찾아보십시오. 세 손가락으로 가볍게 누르고 Force-touch로 꾹 누르거나 마우스를 변수 위에 두고 Control+Command+D로 주석을 볼 수 있습니다.

## 일반 작업에 대한 우수 사례

이 절에서는 가장 일반적인 조작에 대한 우수 사례를 간략히 설명합니다. 단, 이는 시작 가이드에 지시된 초기화 작업이 완료되는 것을 전제로 합니다.

### 파일 업로드

시작 가이드의 [파일 업로드](https://cloud.tencent.com/document/product/436/11280#step---2-.E4.B8.8A.E4.BC.A0.E6.96.87.E4.BB.B6) 부분을 참조할 수 있습니다.

### 파일 업로드 시의 중단점 재개

1M보다 큰 파일의 경우 SDK는 멀티파트 업로드 방식으로 업로드를 진행합니다. 즉, 파일을 1M 크기의 파트로 분할한 다음 병렬(최대 병렬 수는 4 개임)로 업로드합니다. 백그라운드 서버가 완료된 각 멀티파트를 저장하며, 이는 업로드 시 중단점 재개의 기초가 됩니다.    

멀티파트 업로드 과정에서 초기화 멀티파트 업로드가 완료되거나 직접 업로드를 취소하면 업로드 복원에 사용될 resumeData가 생성됩니다. 이 resumetData를 통해 업로드 요청을 다시 생성한 다음 이 업로드 요청으로 이어서 업로드를 계속할 수 있고, 진도도 상응하여 중첩됩니다. 다음과 같이 ResumeData 획득의 예시를 참조할 수 있습니다.

```objective-C
QCloudCOSXMLUploadObjectRequest* put = [QCloudCOSXMLUploadObjectRequest new];
//···업로드 매개변수 설정
put.initMultipleUploadFinishBlock = ^(QCloudInitiateMultipartUploadResult * multipleUploadInitResult, QCloudCOSXMLUploadObjectResumeData resumeData) {
	//초기화 멀티파트 업로드가 완료된 후 이 block이 콜백되고, 여기서 resumeData를 획득할 수 있으며 resumeData를 통해 멀티파트 업로드 요청을 생성할 수 있습니다.
	QCloudCOSXMLUploadObjectRequest* request = [QCloudCOSXMLUploadObjectRequest requestWithRequestData:resumeData];
};

[[QCloudCOSTransferMangerService defaultCOSTransferManager] UploadObject:put];

//···초기화를 완료하고 업로드는 완료되기 전
NSError* error;
//여기서 직접 취소를 호출하고, resumetData의 예시를 생성할 수 있습니다
resumeData = [put cancelByProductingResumeData:&error];
if (resumeData) {
QCloudCOSXMLUploadObjectRequest* request = [QCloudCOSXMLUploadObjectRequest requestWithRequestData:resumeData];
 }
 //생성된 업로드 복구에 사용할 요청은 직접 업로드할 수 있습니다
 [[QCloudCOSTransferMangerService defaultCOSTransferManager] UploadObject:request];

```

주의할 점은, 멀티파트 업로드의 실행 원리에 따르면 멀티파트 업로드가 완료되면 백그라운드 서버가 해당 멀티파트를 기록하고 진도를 중첩하는 것입니다. 또한 다음의 몇 가지 상황에는 중단점 재개를 진행할 수 없고, 업로드 과정을 다시 시작합니다.

- 업로드된 파일이 1M 미만이고, 멀티파트 업로드가 실행되지 않습니다.
- QCloudCOSXMLUploadObjectRequest 유형을 사용하여 업로드를 진행하지 않고, 직접 간단 업로드 API를 사용합니다.
- resumeData 생성 취소 시 초기화 멀티파트 업로드가 아직 완료되지 않습니다(초기화 업로드 완료의 콜백이 아직 호출되지 않음).

### 파일 다운로드

시작 가이드의 [파일 다운로드](https://cloud.tencent.com/document/product/436/11280#3.-.E4.B8.8B.E8.BD.BD.E6.96.87.E4.BB.B6) 부분을 참조할 수 있습니다.

### 파일 복사

#### 설명

QCloudCOSXMLCopyObjectRequest 객체를 초기화한 다음, QCloudCOSTransferMangerService의 CopyObject 방법을 호출하면 됩니다. 비교적으로 큰 파일의 경우 멀티파트 복사 방식으로 복사를 진행합니다. 이 과정은 사용자에게 감지되지 않습니다.  

> !크로스 도메인 복사일 경우, 사용되는 transferManager가 위치한 region은 반드시 대상 버킷이 위치한 region이어야 합니다.

#### 예시

```objective-c
QCloudCOSXMLCopyObjectRequest* request = [[QCloudCOSXMLCopyObjectRequest alloc] init];
request.bucket = @"대상 Bucket";
request.object = @"대상 파일 이름";
request.sourceBucket = @"파일 소스 Bucket은 공개 읽기 또는 현재 계정에서 읽기 권한이 있어야 합니다";
request.sourceObject = @"소스 파일 이름";
request.sourceAPPID = @"소스의 APPID";
request.sourceRegion= @"소스의 지역";
[request setFinishBlock:^(QCloudCopyObjectResult* result, NSError* error) {
    // 콜백 완료
    if (nil == error) {
      //성공
    }
}];
//크로스 도메인 복사일 경우, 사용되는 transferManager가 위치한 region은 반드시 대상 버킷이 위치한 region이어야 합니다.
[[QCloudCOSTransferMangerService defaultCOSTransferManager] CopyObject:request];
```

## Service 조작

### 모든 Bucket - Get Service 나열

Get Service API는 요청자 이름 하의 모든 스토리지 공간 리스트(Bucket list)를 획득하는 데 사용됩니다.

#### 반환 결과 QCloudListAllMyBucketsResult 매개변수 설명

| 매개변수 이름 | 설명               | 유형          |
| -------- | ------------------ | ------------- |
| owner    | 버킷 소유자 정보 | QCloudOwner * |
| buckets  | 모든 bucket 정보   | NSArray<QCloudBucket*> *    |

#### 예시

```objective-c
QCloudGetServiceRequest* request = [[QCloudGetServiceRequest alloc] init];
[request setFinishBlock:^(QCloudListAllMyBucketsResult* result, NSError* error) {
//콜백 완료의 처리
}];
[[QCloudCOSXMLService defaultCOSXML] GetService:request];
```

### 사전 서명 URL의 생성 및 사용

SDK 또는 서버측은 모두 사전 서명 URL을 생성하여 업로드, 다운로드 또는 기타 작업을 진행할 수 있습니다.

#### 절차 설명

1. QCloudGetPresignedURLRequest 인스턴스를 생성합니다.
2. 요청한 Bucket, Object, HTTPMethod 등과 같은 필요한 정보를 입력합니다.
3. 사용 시 다른 HTTP 헤더 또는 매개변수를 추가하면 사전 서명 URL을 생성할 때 QCloudGetPresignedURLRequest에서 해당하는 방법을 호출하여 추가하십시오.
4. QCloudCOSXMLService의 getPresignedURL을 호출하여 요청을 보내고, 결과에서 사전 서명 URL을 획득합니다.

#### QCloudGetPresignedURLRequest 매개변수 설명

| 매개변수 이름    | 설명                                                         | 유형      | 필수 |
| ----------- | ------------------------------------------------------------ | --------- | ---- |
| bucket      | 사전 서명 요청을 사용하는 Bucket                                      | NSString* | 예   |
| object      | 사전 서명 요청을 사용하는 Object입니다. 객체 키(Key)는 버킷에서 객체의 유일한 표시입니다. 예를 들어, 객체의 접근 도메인 이름 bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg 중, 객체 키는 doc1/pic1.jpg입니다. 자세한 설명은 [객체 설명](https://cloud.tencent.com/document/product/436/13324)을 참조하십시오 | NSString* | 예   |
| HTTPMethod  | 사전 서명 URL의 요청을 사용하는 HTTP 방법입니다. 유효값(대소문자 구분): @"GET",@"PUT",@"POST",@"DELETE" | NSString* | 예   |
| contentType | 사전 서명 URL을 사용하는 요청에 헤더가 있을 경우, 여기서 설정하십시오          | NSString* | 아니요   |
| contentMD5  | 사전 서명 URL을 사용하는 요청에 헤더가 있을 경우, 여기서 설정합시시오          | NSString* | 아니요   |

**주의: ** 사전 서명 URL을 사용하여 생성한 요청의 헤더 또는 URL 매개변수를 설정할 경우, 다음의 방법으로 설정해야 합니다.    

```objective-c
/**
 사전 서명을 사용한 요청의 헤더 추가

 @param value HTTP header의 값
 @param requestHeader HTTP header의 key
 */
- (void)setValue:(NSString * _Nullable)value forRequestHeader:(NSString * _Nullable)requestHeader;

/**
 사전 서명을 사용한 요청의 URL 매개변수 추가

 @param value 매개변수 값
 @param requestParameter 매개변수의 key
 */
- (void)setValue:(NSString * _Nullable)value forRequestParameter:(NSString *_Nullable)requestParameter;
```

#### 사전 서명 URL 획득 예시

```objective-c
QCloudGetPresignedURLRequest* getPresignedURLRequest = [[QCloudGetPresignedURLRequest alloc] init];
getPresignedURLRequest.bucket = self.bucket;
getPresignedURLRequest.HTTPMethod = @"GET";
getPresignedURLRequest.object = @"testUploadWithPresignedURL";
[getPresignedURLRequest setFinishBlock:^(QCloudGetPresignedURLResult * _Nonnull result, NSError * _Nonnull error) {
if (nil == error) {
 NSString* presignedURL = result.presienedURL;
}
}
[[QCloudCOSXMLService defaultCOSXML] getPresignedURL:getPresignedURLRequest];

```

#### 사전 서명 URL 사용 예시

여기서는 사전 서명 URL을 사용하여 다운로드하는 예시를 제시합니다.

```objective-C
NSMutableURLRequest* request = [[NSMutableURLRequest alloc] initWithURL:[NSURL URLWithString:@"사전 서명 URL"]];
request.HTTPMethod = @"GET";
request.HTTPBody = [@"파일 내용" dataUsingEncoding:NSUTF8StringEncoding];
[[[NSURLSession sharedSession] downloadTaskWithRequest:request completionHandler:^(NSURL * _Nullable location, NSURLResponse * _Nullable response, NSError * _Nullable error) {
    NSInteger statusCode = [(NSHTTPURLResponse*)response statusCode];
}] resume];
```

## 버킷 조작

### 버킷 생성

#### 방식 프로토타입

COS를 사용하기 시작할 때, 객체의 사용 및 관리를 위해 지정한 계정에서 Bucket을 생성해야 하며, Bucket이 소속된 지역을 지정합니다. Bucket을 생성하는 사용자가 기본적으로 Bucket의 소유자가 됩니다. Bucket 생성 시 접근 권한을 지정하지 않으면 기본 설정은 비공개 읽기/쓰기 권한입니다. 구체적인 단계는 다음과 같습니다.    

1. QCloudPutBucketRequest를 인스턴스화하고, 필요한 매개변수를 입력합니다.
2. QCloudCOSXMLService 객체의 PutBucket 방법을 호출하여 요청을 보냅니다.
3. 콜백 된 finishBlock의 outputObject에서 구체적인 내용을 획득합니다.

#### QCloudPutBucketRequest 매개변수 설명

| 매개변수 이름          | 설명                                                         | 유형       | 필수 |
| ----------------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket            | 생성할 버킷 이름, [COS V5 콘솔](https://console.cloud.tencent.com/cos5/bucket)에서 볼 수 있습니다. 버킷 이름은 숫자와 소문자로만 생성할 수 있으며, 길이는 40자를 초과할 수 없습니다. 그렇지 않으면 생성에 실패합니다 | NSString * | 예   |
| accessControlList | Bucket의 ACL 속성을 정의합니다. 유효값: private，public-read-write，public-read, 기본값: private | NSString * | 아니요   |
| grantRead         | 피부여자에게 읽기 권한을 부여합니다. 형식: `id=" ",id=" "; 서브 계정에 권한을 부여할 경우, id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;SubUin>", 루트 계정에 권한을 부여할 경우, id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;OwnerUin>" 그중 OwnerUin은 루트 계정의 ID를 나타내며, SubUin은 서브 계정의 ID를 나타냅니다 | NSString * | 아니요   |
| grantWrite| 피부여자에게 쓰기 권한을 부여합니다. 형식은 위와 같습니다.                             | NSString * | 아니요   |
| grantFullControl  | 피부여자에게 읽기/쓰기 권한을 부여합니다. 형식은 위와 같습니다.                               | NSString *            | 아니요   |

#### 예시

```objective-c
QCloudPutBucketRequest* request = [QCloudPutBucketRequest new];
request.bucket = @"bucketname-appid"; //additional actions after finishing
[request setFinishBlock:^(id outputObject, NSError* error) {

}];
[[QCloudCOSXMLService defaultCOSXML] PutBucket:request];
```

#### 오류 코드 반환 설명

SDK 요청에 실패하면 반환된 error는 비어 있지 않으며, 개발자가 문제를 신속하게 해결할 수 있도록 오류 코드, 오류 설명 및 기타 디버깅에 필요한 정보 등이 포함됩니다.

반환된 오류 코드(반환된 error에 캡슐화됨)는 주로 두 가지를 포함합니다. 설비 자체에서 네트워크 원인으로 반환된 오류 코드와 COS가 반환한 오류 코드입니다.

- 설비 자체가 네트워크 원인으로 생성한 오류 코드는 모두 음수이며 네 자리 숫자입니다(예: -1001). 이러한 오류 코드는 애플에서 정의한 것이며 NSURLError.h 헤더 파일 내의 정의 또는 [애플 공식 웹 사이트 문서 설명](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes)을 참조할 수 있습니다.
- COS가 반환한 오류 코드는 HTTP의 상태 코드에서 나온 것이며 404, 503 유형입니다. 이러한 오류 코드에 대해서 COS 공식 웹 사이트 문서의 [오류 코드 관련 설명](https://cloud.tencent.com/document/product/436/7730)에서 해결 방안을 찾아볼 수 있습니다.

### 버킷 내 내용 열거

#### 방식 프로토타입

버킷 조작을 진행하기 전에 헤더 파일 QCloudCOSXML/QCloudCOSXML.h를 가져오기 해야 합니다. 그 전에 앞에 설명한 STEP-1 초기화 조작을 완료해야 합니다. QCloudGetBucketRequest 인스턴스를 생성한 후 필요한 예외적 제한 조건을 입력하고 내용을 획득합니다. 구체적인 단계는 다음과 같습니다.    

1. QCloudGetBucketRequest를 인스턴스화하고, 필요한 매개변수를 입력합니다.    
2. QCloudCOSXMLService 객체의 GetBucket 방법을 호출하여 요청을 보냅니다.    
3. 콜백 된 finishBlock의 QCloudListBucketResult에서 구체적인 내용을 획득합니다.   

#### QCloudGetBucketRequest 매개변수 설명

| 매개변수 이름     | 설명                                                         | 유형       | 필수 |
| ------------ | ------------------------------------------------------------ | ---------- | ---- |
| bucket       | 버킷 이름, [COS V5 콘솔](https://console.cloud.tencent.com/cos5/bucket)에서 볼 수 있으며, 형식은 &lt;bucketName&gt;-&lt;APPID&gt;입니다. 예: testBucket-1253653367 | NSString *            | 예   |
| prefix       |접두사 매칭, 반환된 파일의 접두어 주소를 지정하는 데 사용됩니다                         | NSString * | 아니요   |
| delimiter    | 구분 기호는 하나의 부호입니다.Prefix가 있을 경우, Prefix와 delimiter 사이에 동일한 경로를 같은 종류로 분류하여 Common Prefix로 정의하며, 모든 Common Prefix를 나열합니다. Prefix가 없을 경우, 경로 시작점에서 시작합니다. 끝난 부호로 이해하면 됩니다. 예를 들어 A로 끝난 결과는 delimiter를 A로 설정하면 됩니다. | NSString * | 아니요   |
| encodingType | 반환값의 인코딩 방식을 규정합니다. 선택 가능 값: url                            | NSString *| 아니요   |
| marker       | 기본 설정으로 UTF-8 이진 순서로 항목이 나열되며, 모든 나열 항목은 marker부터 시작합니다   | NSString * | 아니요   |
| maxKeys       |1회 반환 최대 항목 수량, 기본값 1000                             | int        | 아니요   |

#### 예시

```objective-c
QCloudGetBucketRequest* request = [QCloudGetBucketRequest new];
request.bucket = @“testBucket-123456789”;
request.maxKeys = 1000;
[request setFinishBlock:^(QCloudListBucketResult * result, NSError*   error) {
//additional actions after finishing
}];
[[QCloudCOSXMLService defaultCOSXML] GetBucket:request];
```

#### 오류 코드 반환 설명

SDK 요청에 실패하면 반환된 error는 비어 있지 않으며, 개발자가 문제를 신속하게 해결할 수 있도록 오류 코드, 오류 설명 및 기타 디버깅에 필요한 정보 등이 포함됩니다.

반환된 오류 코드(반환된 error에 캡슐화됨)는 주로 두 가지를 포함합니다. 설비 자체에서 네트워크 원인으로 반환된 오류 코드와 COS가 반환한 오류 코드입니다.

- 설비 자체가 네트워크 원인으로 생성한 오류 코드는 모두 음수이며 네 자리 숫자입니다(예: -1001). 이러한 오류 코드는 애플에서 정의한 것이며 NSURLError.h 헤더 파일 내의 정의 또는 [애플 공식 웹 사이트 문서 설명](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes)을 참조할 수 있습니다.
- COS가 반환한 오류 코드는 HTTP의 상태 코드에서 나온 것이며 404, 503 유형입니다. 이러한 오류 코드에 대해서 COS 공식 웹 사이트 문서의 [오류 코드 관련 설명](https://cloud.tencent.com/document/product/436/7730)에서 해결 방안을 찾아볼 수 있습니다.

### 버킷의 ACL(Access Control List) 획득

#### 방식 프로토타입

버킷 조작을 진행하기 전에 헤더 파일 QCloudCOSXML/QCloudCOSXML.h를 가져오기 해야 합니다. 그 전에 앞에 설명한 STEP-1 초기화 조작을 완료해야 합니다. QCloudGetBucketACLRequest 인스턴스를 생성한 후 필요한 예외적 제한 조건을 입력하고 내용을 획득합니다. 구체적인 단계는 다음과 같습니다.    

1. QCloudGetBucketACLRequest를 인스턴스화하고, ACL을 획득한 버킷을 입력합니다.    
2. QCloudCOSXMLService 객체의 GetBucketACL 방법을 호출하여 요청을 보냅니다.    
3. 콜백 된 finishBlock의 QCloudACLPolicy에서 구체적인 내용을 획득합니다.    

#### QCloudGetBucketACLRequest 매개변수 설명

| 매개변수 이름 | 설명                                                         | 유형       | 필수 |
| -------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket   | 버킷 이름, [COS V5 콘솔](https://console.cloud.tencent.com/cos5/bucket)에서 볼 수 있으며, 형식은 &lt;bucketName&gt;-&lt;APPID&gt;입니다. 예: testBucket-1253653367 | NSString * | 예   |

#### 반환 결과 QCloudACLPolicy 매개변수 설명

| 매개변수 이름 | 설명                               | 유형             |
| -------- | ---------------------------------- | ---------------- |
| owner    | 버킷 소유자 정보                 | QCloudACLOwner * |
| accessControlList     | 피부여자 및 권한 정보 | QCloudAccessControlList *        |

#### 예시

```objective-c
QCloudGetBucketACLRequest* getBucketACl   = [QCloudGetBucketACLRequest new];
getBucketACl.bucket = @"testbucket-123456789";
[getBucketACl setFinishBlock:^(QCloudACLPolicy * _Nonnull result, NSError * _Nonnull error) {
   //QCloudACLPolicy에는 Bucket의 ACL 정보가 포함됩니다.
}];

[[QCloudCOSXMLService defaultCOSXML] GetBucketACL:getBucketACl];

```

#### 오류 코드 반환 설명

SDK 요청에 실패하면 반환된 error는 비어 있지 않으며, 개발자가 문제를 신속하게 해결할 수 있도록 오류 코드, 오류 설명 및 기타 디버깅에 필요한 정보 등이 포함됩니다.

반환된 오류 코드(반환된 error에 캡슐화됨)는 주로 두 가지를 포함합니다. 설비 자체에서 네트워크 원인으로 반환된 오류 코드와 COS가 반환한 오류 코드입니다.

- 설비 자체가 네트워크 원인으로 생성한 오류 코드는 모두 음수이며 네 자리 숫자입니다(예: -1001). 이러한 오류 코드는 애플에서 정의한 것이며 NSURLError.h 헤더 파일 내의 정의 또는 [애플 공식 웹 사이트 문서 설명](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes)을 참조할 수 있습니다.
- COS가 반환한 오류 코드는 HTTP의 상태 코드에서 나온 것이며 404, 503 유형입니다. 이러한 오류 코드에 대해서 COS 공식 웹 사이트 문서의 [오류 코드 관련 설명](https://cloud.tencent.com/document/product/436/7730)에서 해결 방안을 찾아볼 수 있습니다.

### 버킷의 ACL(Access Control List) 설정

#### 방식 프로토타입

버킷 조작을 진행하기 전에 헤더 파일 QCloudCOSXML/QCloudCOSXML.h를 가져오기 해야 합니다. 그 전에 앞에 설명한 STEP-1 초기화 조작을 완료해야 합니다. QCloudPutBucketACLRequest 인스턴스를 생성한 후 필요한 예외적 제한 조건을 입력하고 내용을 획득합니다. 구체적인 단계는 다음과 같습니다.    

1. QCloudPutBucketACLRequest를 인스턴스화하고, 설정할 버킷을 입력한 후 설정 값의 권한 유형에 따라 각각 서로 다른 매개변수를 입력합니다.    
2. QCloudCOSXMLService 객체의 PutBucketACL 방법을 호출하여 요청을 보냅니다.    
3. 콜백 된 finishBlock에서 설정이 성공하였는지 획득하고, 설정 성공 후의 추가 작업을 실행합니다.   

#### QCloudPutBucketACLRequest 매개변수 설명

| 매개변수 이름          | 설명                                                         | 유형       | 필수 |
| ----------------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket            | 버킷 이름, [COSV5 콘솔](https://console.cloud.tencent.com/cos5/bucket)에서 볼 수 있으며, 형식은 &lt;bucketName&gt;-&lt;APPID&gt;입니다. 예: testBucket-1253653367 | NSString *            | 예   |
| accessControlList | Object의 ACL 속성을 정의합니다. 유효값: private, public-read-write, public-read; 기본값: private | NSString * | 아니요   |
| grantRead         | 피부여자에게 읽기 권한을 부여합니다. 형식: `id=" ",id=" "; <br>서브 계정에 권한을 부여할 경우, id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;", <br>루트 계정에 권한을 부여할 경우, id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt;” <br>그중 OwnerUin은 루트 계정의 ID를 나타내며, SubUin은 서브 계정의 ID를 나타냅니다 | NSString * | 아니요   |
| grantWrite| 피부여자에게 쓰기 권한을 부여합니다. 형식은 위와 같습니다.                             | NSString * | 아니요   |
| grantFullControl  | 피부여자에게 읽기/쓰기 권한을 부여합니다. 형식은 위와 같습니다.                               | NSString *            | 아니요   |

#### 예시

```objective-c
QCloudPutBucketACLRequest* putACL = [QCloudPutBucketACLRequest new];
NSString* appID = @“귀하의 APPID”;
NSString *ownerIdentifier = [NSString stringWithFormat:@"qcs::cam::uin/%@:uin/%@", appID, appID];
NSString *grantString = [NSString stringWithFormat:@"id=\"%@\"",ownerIdentifier];
putACL.grantFullControl = grantString;
putACL.bucket = @“testBucket-123456789”;
[putACL setFinishBlock:^(id outputObject, NSError *error) {
//error occucs if error != nil
}];
[[QCloudCOSXMLService defaultCOSXML] PutBucketACL:putACL];

```

#### 오류 코드 반환 설명

SDK 요청에 실패하면 반환된 error는 비어 있지 않으며, 개발자가 문제를 신속하게 해결할 수 있도록 오류 코드, 오류 설명 및 기타 디버깅에 필요한 정보 등이 포함됩니다.

반환된 오류 코드(반환된 error에 캡슐화됨)는 주로 두 가지를 포함합니다. 설비 자체에서 네트워크 원인으로 반환된 오류 코드와 COS가 반환한 오류 코드입니다.

- 설비 자체가 네트워크 원인으로 생성한 오류 코드는 모두 음수이며 네 자리 숫자입니다(예: -1001). 이러한 오류 코드는 애플에서 정의한 것이며 NSURLError.h 헤더 파일 내의 정의 또는 [애플 공식 웹 사이트 문서 설명](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes)을 참조할 수 있습니다.
- COS가 반환한 오류 코드는 HTTP의 상태 코드에서 나온 것이며 404, 503 유형입니다. 이러한 오류 코드에 대해서 COS 공식 웹 사이트 문서의 [오류 코드 관련 설명](https://cloud.tencent.com/document/product/436/7730)에서 해결 방안을 찾아볼 수 있습니다.

### 버킷의 CORS(크로스 도메인간 접근) 설정 획득

#### 방식 프로토타입

버킷 조작을 진행하기 전에 헤더 파일 QCloudCOSXML/QCloudCOSXML.h를 가져오기 해야 합니다. 그 전에 앞에 설명한 STEP-1 초기화 조작을 완료해야 합니다. QCloudGetBucketCORSRequest 인스턴스를 생성한 후 필요한 예외적 제한 조건을 입력하고 내용을 획득합니다. 구체적인 단계는 다음과 같습니다.    

1. QCloudGetBucketCORSRequest를 인스턴스화하고, CORS를 획득할 버킷을 입력합니다.    
2. QCloudCOSXMLService 객체의 GetBucketCORS 방법을 호출하여 요청을 보냅니다.    
3. 콜백 된 finishBlock에서 결과를 가져옵니다. 결과는 QCloudCORSConfiguration 객체에 캡슐화되며, 해당 객체의 rules 속성은 배열이며, 배열 안에 QCloudCORSRule 세트가 포함되고, 구체적인 CORS 설정은 QCloudCORSRule 객체에 캡슐화됩니다.   

#### QCloudGetBucketCORSRequest 매개변수 설명

| 매개변수 이름 | 설명                                                         | 유형       | 필수 |
| -------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket   | 버킷 이름, [COS V5 콘솔](https://console.cloud.tencent.com/cos5/bucket)에서 볼 수 있으며, 형식은 &lt;bucketName&gt;-&lt;APPID&gt;입니다. 예: testBucket-1253653367 | NSString * | 예   |

#### 반환 결과 QCloudCORSConfiguration 매개변수 설명

| 매개변수 이름 | 설명                                             | 유형                                |
| -------- | ------------------------------------------------ | ----------------------------------- |
| rules    | CORS의 배열, 배열 내용은 QCloudCORSRule 인스턴스 | NSArray&lt;CloudCORSRule`*`&gt; `*` |

#### QCloudCORSRule 매개변수 설명

| 매개변수 이름      | 설명                                                         | 유형                           |
| ------------- | ------------------------------------------------------------ | ------------------------------ |
| identifier    | 구성 규칙의 ID                                                | NSString *                     |
| allowedMethod |허용된 HTTP 조작, 열거값: GET, PUT, HEAD, POST, DELETE       | NSArray&lt;NSString`*`&gt;`*`  |
| allowedOrigin | 허용된 접근 리소스, 와일드카드 * 지원, 형식: 프로토콜: //도메인 이름[: 포트]예: `http://www.qq.com` | NSString *                     |
| allowedHeader | OPTIONS 요청 발송 시 서버측에게 알립니다. 이어지는 요청은 어떠한 사용자 지정 HTTP 요청 헤더를 사용할 수 있으며, 와일드카드*를 지원합니다  | NSArray&lt;NSString`*`&gt; `*` |
| maxAgeSeconds | OPTIONS 요청이 획득한 결과의 유효기간 설정                            | int                            |
| exposeHeader  |브라우저가 수신할 수 있는 서버측의 사용자 지정 헤더 정보 설정           | NSString *                     |

#### 예시

```objective-c
QCloudGetBucketCORSRequest* corsReqeust = [QCloudGetBucketCORSRequest new];
corsReqeust.bucket = @"testBucket-123456789";
[corsReqeust setFinishBlock:^(QCloudCORSConfiguration * _Nonnull result, NSError * _Nonnull error) {
   //CORS 설정은 result에 캡슐화됩니다.
}];

[[QCloudCOSXMLService defaultCOSXML] GetBucketCORS:corsReqeust];

```

#### 오류 코드 반환 설명

SDK 요청에 실패하면 반환된 error는 비어 있지 않으며, 개발자가 문제를 신속하게 해결할 수 있도록 오류 코드, 오류 설명 및 기타 디버깅에 필요한 정보 등이 포함됩니다.

반환된 오류 코드(반환된 error에 캡슐화됨)는 주로 두 가지를 포함합니다. 설비 자체에서 네트워크 원인으로 반환된 오류 코드와 COS가 반환한 오류 코드입니다.

- 설비 자체가 네트워크 원인으로 생성한 오류 코드는 모두 음수이며 네 자리 숫자입니다(예: -1001). 이러한 오류 코드는 애플에서 정의한 것이며 NSURLError.h 헤더 파일 내의 정의 또는 [애플 공식 웹 사이트 문서 설명](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes)을 참조할 수 있습니다.
- COS가 반환한 오류 코드는 HTTP의 상태 코드에서 나온 것이며 404, 503 유형입니다. 이러한 오류 코드에 대해서 COS 공식 웹 사이트 문서의 [오류 코드 관련 설명](https://cloud.tencent.com/document/product/436/7730)에서 해결 방안을 찾아볼 수 있습니다.



### 버킷의 CORS(크로스 도메인 접근) 설정

#### 방식 프로토타입

버킷 조작을 진행하기 전에 헤더 파일 QCloudCOSXML/QCloudCOSXML.h를 가져오기 해야 합니다. 그 전에 앞에 설명한 STEP-1 초기화 조작을 완료해야 합니다. QCloudPutBucketCORSRequest 인스턴스를 생성한 후 필요한 예외적 제한 조건을 입력하고 내용을 획득합니다. 구체적인 단계는 다음과 같습니다.    

1. QCloudPutBucketCORSRequest를 인스턴스화하여, 버킷을 설정하고, 필요한 CORS를 QCloudCORSRule에 로드합니다. 여러 세트의 CORS 설정이 있을 경우 여러 개의 QCloudCORSRule을 하나의 NSArray에 두고, 해당 그룹을 QCloudCORSConfiguration의 rules 속성에 입력하여 request에 둡니다.    
2. QCloudCOSXMLService 객체의 PutBucketCORS 방법을 호출하여 요청을 합니다.    
3. 콜백 된 finishBlock에서 설정이 성공하였는지(error가 비어 있는지)를 획득하고, 설정 후의 추가 작업을 실행합니다.   

#### QCloudPutBucketCORSRequest 매개변수 설명

| 매개변수 이름          | 설명                                                         | 유형                      | 필수 |
| ----------------- | ------------------------------------------------------------ | ------------------------- | ---- |
| bucket            | 버킷 이름, [COS V5 콘솔](https://console.cloud.tencent.com/cos5/bucket)에서 볼 수 있으며, 형식은 &lt;bucketName&gt;-&lt;APPID&gt;입니다. 예: testBucket-1253653367 | NSString *                | 예   |
| corsConfiguration | CORS의 구체적인 매개변수를 캡슐화합니다                                       | QCloudCORSConfiguration * | 예   |

#### QCloudCORSConfiguration 매개변수 설명

| 매개변수 이름 | 설명                                             | 유형                             |
| -------- | ------------------------------------------------ | -------------------------------- |
| rules    | CORS의 배열, 배열 내용은 QCloudCORSRule 인스턴스 |  NSArray&lt;QCloudCORSRule`*` > * |

#### QCloudCORSRule 매개변수 설명

| 매개변수 이름 | 설명                                                         | 유형                         |
| ------------- | ------------------------------------------------------------ | ---------------------------- |
| identifier    | 구성 규칙의 ID                                                | NSString *                   |
| allowedMethod |허용된 HTTP 조작, 열거값: GET, PUT, HEAD, POST, DELETE      | NSArray &lt;NSString`*`> *   |
| allowedOrigin | 허용된 접근 리소스, 와일드카드 * 지원, 형식: 프로토콜: //도메인 이름[: 포트]예: `http://www.qq.com` | NSString *                   |
| allowedHeader | OPTIONS 요청 발송 시 서버측에게 알립니다. 이어지는 요청은 어떠한 사용자 지정 HTTP 요청 헤더를 사용할 수 있으며, 와일드카드`*`를 지원합니다 | NSArray &lt;NSString `*` > * |
| maxAgeSeconds | OPTIONS 요청이 획득한                            | int                          |
| exposeHeader  |브라우저가 수신할 수 있는 서버측의 사용자 지정 헤더 정보 설정           | NSString *                   |

#### 예시

```objective-c
QCloudPutBucketCORSRequest* putCORS = [QCloudPutBucketCORSRequest new];
QCloudCORSConfiguration* cors = [QCloudCORSConfiguration new];

QCloudCORSRule* rule = [QCloudCORSRule new];
rule.identifier = @"sdk";
rule.allowedHeader = @[@"origin",@"host",@"accept",@"content-type",@"authorization"];
rule.exposeHeader = @"ETag";
rule.allowedMethod = @[@"GET",@"PUT",@"POST", @"DELETE", @"HEAD"];
rule.maxAgeSeconds = 3600;
rule.allowedOrigin = @"*";
cors.rules = @[rule];
putCORS.corsConfiguration = cors;
putCORS.bucket = @"testBucket-123456789";
[putCORS setFinishBlock:^(id outputObject, NSError *error) {
    if (!error) {
      //success
  }
}];
[[QCloudCOSXMLService defaultCOSXML] PutBucketCORS:putCORS];
```

#### 오류 코드 반환 설명

SDK 요청에 실패하면 반환된 error는 비어 있지 않으며, 개발자가 문제를 신속하게 해결할 수 있도록 오류 코드, 오류 설명 및 기타 디버깅에 필요한 정보 등이 포함됩니다.

반환된 오류 코드(반환된 error에 캡슐화됨)는 주로 두 가지를 포함합니다. 설비 자체에서 네트워크 원인으로 반환된 오류 코드와 COS가 반환한 오류 코드입니다.

- 설비 자체가 네트워크 원인으로 생성한 오류 코드는 모두 음수이며 네 자리 숫자입니다(예: -1001). 이러한 오류 코드는 애플에서 정의한 것이며 NSURLError.h 헤더 파일 내의 정의 또는 [애플 공식 웹 사이트 문서 설명](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes)을 참조할 수 있습니다.
- COS가 반환한 오류 코드는 HTTP의 상태 코드에서 나온 것이며 404, 503 유형입니다. 이러한 오류 코드에 대해서 COS 공식 웹 사이트 문서의 [오류 코드 관련 설명](https://cloud.tencent.com/document/product/436/7730)에서 해결 방안을 찾아볼 수 있습니다.



### 버킷의 지역 정보 Get Bucket Location 획득

#### 방식 프로토타입

버킷 조작을 진행하기 전에 헤더 파일 QCloudCOSXML/QCloudCOSXML.h를 가져오기 해야 합니다. 그 전에 앞에 설명한 STEP-1 초기화 조작을 완료해야 합니다. QCloudGetBucketLocationRequest 인스턴스를 생성한 후 필요한 예외적 제한 조건을 입력하고 내용을 획득합니다. 구체적인 단계는 다음과 같습니다.    

1. QCloudGetBucketLocationRequest를 인스턴스화하고, Bucket 이름을 입력합니다.    
2. QCloudCOSXMLService 객체의 GetBucketLocation 방법을 호출하여 요청을 보냅니다.    
3. 콜백된 finishBlock에서 구체적인 내용을 획득합니다.   

#### QCloudGetBucketLocationRequest 매개변수 설명

| 매개변수 이름 | 설명                                                         | 유형       | 필수 |
| -------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket   | 버킷 이름, [COS V5 콘솔](https://console.cloud.tencent.com/cos5/bucket)에서 볼 수 있으며, 형식은 &lt;bucketName&gt;-&lt;APPID&gt;입니다. 예: testBucket-1253653367 | NSString * | 예   |

#### 반환 결과 QCloudBucketLocationConstraint 매개변수 설명

| 매개변수 이름           | 설명                 | 유형
| ------------------ | -------------------- | --------- |
| locationConstraint | Bucket이 위치한 지역 설명 | NSString* |

#### 예시

```objective-c
QCloudGetBucketLocationRequest* locationReq = [QCloudGetBucketLocationRequest new];
locationReq.bucket = @"testBucket-123456789";
 __block QCloudBucketLocationConstraint* location;
[locationReq setFinishBlock:^(QCloudBucketLocationConstraint * _Nonnull result, NSError * _Nonnull error) {
       location = result;
}];
[[QCloudCOSXMLService defaultCOSXML] GetBucketLocation:locationReq];

```

#### 오류 코드 반환 설명

SDK 요청에 실패하면 반환된 error는 비어 있지 않으며, 개발자가 문제를 신속하게 해결할 수 있도록 오류 코드, 오류 설명 및 기타 디버깅에 필요한 정보 등이 포함됩니다.

반환된 오류 코드(반환된 error에 캡슐화됨)는 주로 두 가지를 포함합니다. 설비 자체에서 네트워크 원인으로 반환된 오류 코드와 COS가 반환한 오류 코드입니다.

- 설비 자체가 네트워크 원인으로 생성한 오류 코드는 모두 음수이며 네 자리 숫자입니다(예: -1001). 이러한 오류 코드는 애플에서 정의한 것이며 NSURLError.h 헤더 파일 내의 정의 또는 [애플 공식 웹 사이트 문서 설명](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes)을 참조할 수 있습니다.
- COS가 반환한 오류 코드는 HTTP의 상태 코드에서 나온 것이며 404, 503 유형입니다. 이러한 오류 코드에 대해서 COS 공식 웹 사이트 문서의 [오류 코드 관련 설명](https://cloud.tencent.com/document/product/436/7730)에서 해결 방안을 찾아볼 수 있습니다.



### 버킷 CORS 설정 삭제

#### 방식 프로토타입

버킷 조작을 진행하기 전에 헤더 파일 QCloudCOSXML/QCloudCOSXML.h를 가져오기 해야 합니다. 그 전에 앞에 설명한 STEP-1 초기화 조작을 완료해야 합니다. QCloudDeleteBucketCORSRequest 인스턴스를 생성한 후 필요한 예외적 제한 조건을 입력하고 내용을 획득합니다. 구체적인 단계는 다음과 같습니다.    

1. QCloudDeleteBucketCORSRequest를 인스턴스화하고, 필요한 매개변수를 입력합니다.    
2. QCloudCOSXMLService 객체의 방법을 호출하여 요청을 보냅니다.    
3. 콜백된 finishBlock에서 구체적인 내용을 획득합니다.   

#### QCloudDeleteBucketCORSRequest 매개변수 설명

| 매개변수 이름 | 설명                                                         | 유형       | 필수 |
| -------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket   | 버킷 이름, [COS V5 콘솔](https://console.cloud.tencent.com/cos5/bucket)에서 볼 수 있으며, 형식은 &lt;bucketName&gt;-&lt;APPID&gt;입니다. 예: testBucket-1253653367 | NSString * | 예   |

#### 예시

```objective-c
QCloudDeleteBucketCORSRequest* deleteCORS = [QCloudDeleteBucketCORSRequest new];
deleteCORS.bucket = @"testBucket-123456789";
[deleteCORS setFinishBlock:^(id outputObject, NSError *error) {
   //success if error == nil
}];
[[QCloudCOSXMLService defaultCOSXML] DeleteBucketCORS:deleteCORS];
```

#### 오류 코드 반환 설명

SDK 요청에 실패하면 반환된 error는 비어 있지 않으며, 개발자가 문제를 신속하게 해결할 수 있도록 오류 코드, 오류 설명 및 기타 디버깅에 필요한 정보 등이 포함됩니다.

반환된 오류 코드(반환된 error에 캡슐화됨)는 주로 두 가지를 포함합니다. 설비 자체에서 네트워크 원인으로 반환된 오류 코드와 COS가 반환한 오류 코드입니다.

- 설비 자체가 네트워크 원인으로 생성한 오류 코드는 모두 음수이며 네 자리 숫자입니다(예: -1001). 이러한 오류 코드는 애플에서 정의한 것이며 NSURLError.h 헤더 파일 내의 정의 또는 [애플 공식 웹 사이트 문서 설명](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes)을 참조할 수 있습니다.
- COS가 반환한 오류 코드는 HTTP의 상태 코드에서 나온 것이며 404, 503 유형입니다. 이러한 오류 코드에 대해서 COS 공식 웹 사이트 문서의 [오류 코드 관련 설명](https://cloud.tencent.com/document/product/436/7730)에서 해결 방안을 찾아볼 수 있습니다.



버킷에서 진행 중인 멀티파트 업로드를 조회합니다 List Multipart Uploads

#### 방식 프로토타입

버킷 조작을 진행하기 전에 헤더 파일 QCloudCOSXML/QCloudCOSXML.h를 가져오기 해야 합니다. 그 전에 앞에 설명한 STEP-1 초기화 조작을 완료해야 합니다. QCloudListBucketMultipartUploadsRequest 인스턴스를 생성한 후 필요한 예외적 제한 조건을 입력하고 내용을 획득합니다. 구체적인 단계는 다음과 같습니다.    

1. QCloudListBucketMultipartUploadsRequest를 인스턴스화하고, 반환 결과의 접두사, 코드 방식 등과 같은 필요한 매개변수를 입력합니다.    
2. QCloudCOSXMLService 객체의 ListBucketMultipartUploads 방법을 호출하여 요청을 합니다.    
3. 콜백된 finishBlock에서 구체적인 내용을 획득합니다.   

#### QCloudListBucketMultipartUploadsRequest 매개변수 설명

| 매개변수 이름             | 설명                                                     | 유형       | 필수 |
| -------------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket         | 버킷 이름, [COS V5 콘솔](https://console.cloud.tencent.com/cos5/bucket)에서 볼 수 있으며, 형식은 &lt;bucketName&gt;-&lt;APPID&gt;입니다. 예: testBucket-1253653367 | NSString * | 예   |
| prefix         | 반환되는 Object key의 접두사는 Prefix 여야 함에 한정합니다. prefix로 조회 시, 반환되는 key에 여전히 Prefix가 포함될 수 있음에 주의하십시오 | NSString * | 아니요   |
| delimiter    | 구분 기호는 하나의 부호입니다. Prefix가 있을 경우, 해당 Prefix 및 delimiter 사이에 동일한 경로를 같은 종류로 분류하고 Common Prefix로 정의합니다. 그런 다음 모든 Common Prefix를 나열합니다. Prefix가 없을 경우, 경로 시작점부터 시작합니다. 끝난 부호로 이해하면 되는데, 예를 들어 A로 끝난 결과는 delimiter를 A로 설정하면 됩니다.  | NSString * | 아니요   |
| encodingType | 반환값의 인코딩 방식을 규정합니다. 선택 가능 값: url                            | NSString *| No   |
| keyMarker      | 해당 key 값으로 시작되는 항목을 나열합니다                                     | NSString * | 아니요   |
| uploadIDMarker | 해당 UploadId 값으로 시작되는 항목을 나열합니다                                 | int        | 아니요   |
| maxUploads     | 반환되는 multipart 최대 수량 설정, 유효값은 1에서 1000입니다                | int        | 아니요   |

#### 반환 결과 QCloudListMultipartUploadsResult 매개변수 설명

| 매개변수 이름     | 설명                                                         | 유형       |
| ------------ | ------------------------------------------------------------ | ---------- |
| bucket            | 버킷 이름, [COS V5 콘솔](https://console.cloud.tencent.com/cos5/bucket)에서 볼 수 있으며, 형식은 &lt;bucketName&gt;-&lt;APPID&gt;입니다. 예: testBucket-1253653367 | NSString * |
| prefix         | 반환되는 Object key의 접두사는 반드시 Prefix여야 함에 한정합니다. prefix로 조회 시, 반환되는 key에 여전히 Prefix가 포함될 수 있음에 주의하십시오 | NSString * |
| delimiter    | 구분 기호는 하나의 부호입니다.Prefix가 있을 경우, 해당 Prefix와 delimiter 사이에 동일한 경로를 같은 종류로 분류하고, Common Prefix로 정의합니다. 그런 다음 모든 Common Prefix르르 나열합니다.Prefix가 없을 경우, 경로 시작점부터 시작합니다 | NSString * |
| encodingType | 반환값의 인코딩 방식을 규정합니다. 선택 가능값: url                            | NSString * |
| keyMarker    | 해당 key 값으로 시작되는 항목을 나열합니다                                      | NSString * |
| maxUploads   | 반환되는 multipart 최대 수량, 유효값은 1에서 1000입니다                 | int        |
| uploads      | 업로드된 모든 멀티파트의 정보                                       | NSArray*   |

#### 예시

```objecitve-c
QCloudListBucketMultipartUploadsRequest* uploads = [QCloudListBucketMultipartUploadsRequest new];
uploads.bucket = @"testBucket-123456789";
uploads.maxUploads = 100;
__block NSError* resulError;
__block QCloudListMultipartUploadsResult* multiPartUploadsResult;
[uploads setFinishBlock:^(QCloudListMultipartUploadsResult* result, NSError *error) {
    multiPartUploadsResult = result;
    localError = error;
}];
[[QCloudCOSXMLService defaultCOSXML] ListBucketMultipartUploads:uploads];

```

#### 오류 코드 반환 설명

SDK 요청이 실패할 경우 반환된 error는 비어 있지 않으며, 개발자가 문제를 신속하게 해결할 수 있도록 오류 코드, 오류 설명 및 기타 디버깅에 필요한 정보 등이 포함됩니다. 반환된 오류 코드(반환된 error에 캡슐화됨)는 주로 두 가지를 포함합니다. 설비 자체에서 네트워크 원인으로 반환된 오류 코드와 COS가 반환한 오류 코드입니다.

- 설비 자체가 네트워크 원인으로 생성한 오류 코드는 모두 음수이며 네 자리 숫자입니다(예: -1001). 이러한 오류 코드는 애플 회사에서 정의한 것이며 NSURLError.h 헤더 파일 내의 정의 또는 [애플 공식 웹 사이트 문서 설명](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes)을 참조할 수 있습니다.
- COS가 반환한 오류 코드는 HTTP의 상태 코드에서 나온 것이며 404, 503 유형입니다. 이러한 오류 코드에 대해서 COS 공식 웹 사이트 문서의 [오류 코드 관련 설명](https://cloud.tencent.com/document/product/436/7730)에서 해결 방안을 찾아볼 수 있습니다.



### Bucket에 Head Bucket이 존재하는지를 조회합니다

Head Bucket 요청은 해당 Bucket이 존재하는지, 접근 권한이 있는지를 확인할 수 있습니다. Head의 권한은 Read와 일치합니다. 해당 Bucket이 존재하면 200을 반환합니다; 버킷에 접근 권한이 없으면 403을 반환하며, 버킷이 존재하지 않으면 404를 반환합니다.    

#### QCloudHeadBucketRequest 매개변수 설명

| 매개변수 이름 | 설명                                                         | 유형       | 필수 |
| -------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket   | 버킷 이름, [COS V5 콘솔](https://console.cloud.tencent.com/cos5/bucket)에서 볼 수 있으며, 형식은 &lt;bucketName&gt;-&lt;APPID&gt;입니다. 예: testBucket-1253653367 | NSString * | 예   |

#### 예시

```objective-c
 QCloudHeadBucketRequest* request = [QCloudHeadBucketRequest new];
 request.bucket = @"testBucket-123456789";
 [request setFinishBlock:^(id outputObject, NSError* error) {
     //콜백 완료를 설정합니다. error가 없으면 정상적으로 bucket에 접근 할 수 있습니다. error가 있으면 error code와 message에서 구체적인 실패 원인을 획득할 수 있습니다.
 }];
 [[QCloudCOSXMLService defaultCOSXML] HeadBucket:request];
```

#### 오류 코드 반환 설명

SDK 요청에 실패하면 반환된 error는 비어 있지 않으며, 개발자가 문제를 신속하게 해결할 수 있도록 오류 코드, 오류 설명 및 기타 디버깅에 필요한 정보 등이 포함됩니다.

반환된 오류 코드(반환된 error에 캡슐화됨)는 주로 두 가지를 포함합니다. 설비 자체에서 네트워크 원인으로 반환된 오류 코드와 COS가 반환한 오류 코드입니다.

- 설비 자체가 네트워크 원인으로 생성한 오류 코드는 모두 음수이며 네 자리 숫자입니다(예, -1001). 이러한 오류 코드는 애플 회사에서 정의한 것이며 NSURLError.h 헤더 파일 내의 정의 또는 [애플 공식 웹 사이트 문서 설명](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes)을 참조할 수 있습니다.
- COS가 반환한 오류 코드는 HTTP의 상태 코드에서 나온 것이며 404, 503 유형입니다. 이러한 오류 코드에 대해서 COS 공식 웹 사이트 문서의 [오류 코드 관련 설명](https://cloud.tencent.com/document/product/436/7730)에서 해결 방안을 찾아볼 수 있습니다.

### Put Bucket Lifecycle

COS는 사용자가 수명 주기 구성의 방식으로 버킷의 객체 수명 주기를 관리할 수 있도록 지원합니다. 수명 주기 구성에는 한 세트의 객체 규칙에 적용될 한 개 또는 여러 개의 규칙 그룹이 포함됩니다(그 중 각 규칙은 COS에 대한 작업을 정의).
이러한 작업은 다음 두 가지 유형으로 구분됩니다.

- 전환 조작: 객체를 다른 스토리지 클래스로 전환할 시간을 정의합니다. 예를 들어, 객체 생성 30일 후에 STANDARD_IA(IA, 접근 빈도가 낮을 경우에 적용) 스토리지 클래스로 전환하도록 선택할 수 있습니다.
- 만료 작업: 객체의 만료 시간을 지정합니다. COS는 자동으로 사용자 대신 만료된 객체를 삭제합니다.

Put Bucket Lifecycle은 Bucket에 대한 새로운 수명 주기 구성을 생성하는 데 사용됩니다. 해당 Bucket에 수명 주기가 이미 구성되었으면, 해당 API를 사용하여 새 구성을 작성하는 동시에 원래 구성을 덮어 쓰게 됩니다.

#### 매개변수 설명

| 매개변수 이름             | 설명                                                     | 유형                          | 필수 |
| --------- | ------------------------------------------------------------ | ----------------------------- | ---- |
| bucket   | 버킷 이름, [COS V5 콘솔](https://console.cloud.tencent.com/cos5/bucket)에서 볼 수 있으며, 형식은 &lt;bucketName&gt;-&lt;APPID&gt;입니다. 예: testBucket-1253653367 | NSString*                     | 예   |
| lifeCycle | 수명 주기 구성                                                 | QCloudLifecycleConfiguration* | 예   |

#### QCloudLifecycleConfiguration 매개변수 설명

| 매개변수 이름 | 설명               | 유형                            | 필수 |
| -------- | ------------------ | ------------------------------- | ---- |
| rules    | 규칙 설명 집합의 배열 | NSArray<QCloudLifecycleRule*> * | 예   |

#### QCloudLifecycleRule 매개변수 설명

| 매개변수 이름                       | 설명                                              | 유형                                          | 필수 |
| ------------------------------ | ------------------------------------------------- | --------------------------------------------- | ---- |
| identifier                     | 유일한 표시 규칙에 사용되며, 길이는 255자를 초과할 수 없습니다.        | NSString*                                     | 예   |
| filter                         | Filter는 규칙이 영향을 주는 Object 집합을 설명하는 데 사용됩니다             | QCloudLifecycleRuleFilter*                    |      |
| status | 규칙 시동 여부 표시, 열거값: Enabled，Disabled       | QCloudLifecycleStatue                         | 예   |
| abortIncompleteMultipartUpload | 멀티파트 업로드 실행을 지속할 최장 시간을 설정합니다                | QCloudLifecycleAbortIncompleteMultipartUpload | No   |
| transition | 규칙 전환 속성, 객체가 언제 전환되는지 또는 Standard_IA로 전환되는지 등| QCloudLifecycleTransition*                    | 아니요   |
| expiration                     | 규칙 만료 속성                                      | QCloudLifecycleExpiration*                    | 아니요   |
| noncurrentVersionExpiration    | 현재 버전이 아닌 객체의 만료 시기 지정                        | QCloudLifecycleExpiration*                    | 아니요   |
| noncurrentVersionTransition    | 현재 버전이 아닌 객체가 언제 전환되는지 또는 STANDARD_IA로 전환되는지 등| QCloudNoncurrentVersionExpiration*            | No   |

#### 예시

```objective-c
QCloudPutBucketLifecycleRequest* request = [QCloudPutBucketLifecycleRequest new];
request.bucket = @"bucket 이름 입력";
__block QCloudLifecycleConfiguration* configuration = [[QCloudLifecycleConfiguration alloc] init];
QCloudLifecycleRule* rule = [[QCloudLifecycleRule alloc] init];
rule.identifier = @"identifier";
rule.status = QCloudLifecycleStatueEnabled;
QCloudLifecycleRuleFilter* filter = [[QCloudLifecycleRuleFilter alloc] init];
filter.prefix = @"0";
rule.filter = filter;

QCloudLifecycleTransition* transition = [[QCloudLifecycleTransition alloc] init];
transition.days = 100;
transition.storageClass = QCloudCOSStorageStandarIA;
rule.transition = transition;
request.lifeCycle = configuration;
request.lifeCycle.rules = @[rule];
[request setFinishBlock:^(id outputObject, NSError* error) {
   // 콜백 완료 설정
}];
[[QCloudCOSXMLService defaultCOSXML] PutBucketLifecycle:request];

```

#### 오류 코드 반환 설명

SDK 요청에 실패하면 반환된 error는 비어 있지 않으며, 개발자가 문제를 신속하게 해결할 수 있도록 오류 코드, 오류 설명 및 기타 디버깅에 필요한 정보 등이 포함됩니다.

반환된 오류 코드(반환된 error에 캡슐화됨)는 주로 두 가지를 포함합니다. 설비 자체에서 네트워크 원인으로 반환된 오류 코드와 COS가 반환한 오류 코드입니다.

- 설비 자체가 네트워크 원인으로 생성한 오류 코드는 모두 음수이며 네 자리 숫자입니다(예: -1001). 이러한 오류 코드는 애플에서 정의한 것이며 NSURLError.h 헤더 파일 내의 정의 또는 [애플 공식 웹 사이트 문서 설명](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes)을 참조할 수 있습니다.
- COS가 반환한 오류 코드는 HTTP의 상태 코드에서 나온 것이며 404, 503 유형입니다. 이러한 오류 코드에 대해서 COS 공식 웹 사이트 문서의 [오류 코드 관련 설명](https://cloud.tencent.com/document/product/436/7730)에서 해결 방안을 찾아볼 수 있습니다.



### Get Bucket Lifecycle

#### 반환 결과 QCloudLifecycleConfiguration 매개변수 설명

Put Bucket Lifecycle API의 QCloudLifecycleConfiguration과 일치합니다.

#### 예시

```objective-c
QCloudGetBucketLifecycleRequest* request = [QCloudGetBucketLifecycleRequest new];
request.bucket = @"testBucket-123456789";
[request setFinishBlock:^(QCloudLifecycleConfiguration* result,NSError* error) {
    // 콜백 완료 설정
}];
[[QCloudCOSXMLService defaultCOSXML] GetBucketLifecycle:request];

```

#### 오류 코드 반환 설명

SDK 요청에 실패하면 반환된 error는 비어 있지 않으며, 개발자가 문제를 신속하게 해결할 수 있도록 오류 코드, 오류 설명 및 기타 디버깅에 필요한 정보 등이 포함됩니다.

반환된 오류 코드(반환된 error에 캡슐화됨)는 주로 두 가지를 포함합니다. 설비 자체에서 네트워크 원인으로 반환된 오류 코드와 COS가 반환한 오류 코드입니다.

- 설비 자체가 네트워크 원인으로 생성한 오류 코드는 모두 음수이며 네 자리 숫자입니다(예: -1001). 이러한 오류 코드는 애플에서 정의한 것이며 NSURLError.h 헤더 파일 내의 정의 또는 [애플 공식 웹 사이트 문서 설명](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes)을 참조할 수 있습니다.
- COS가 반환한 오류 코드는 HTTP의 상태 코드에서 나온 것이며 404, 503 유형입니다. 이러한 오류 코드에 대해서 COS 공식 웹 사이트 문서의 [오류 코드 관련 설명](https://cloud.tencent.com/document/product/436/7730)에서 해결 방안을 찾아볼 수 있습니다.



### Delete Bucket Lifecycle

#### 반환 결과 QCloudLifecycleConfiguration 매개변수 설명

Put Bucket Lifecycle API의 QCloudLifecycleConfiguration과 일치합니다.

#### 예시

```objective-c
QCloudDeleteBucketLifeCycleRequest* request = [[QCloudDeleteBucketLifeCycleRequest alloc ] init];
request.bucket = @"testBucket-123456789";
 [request setFinishBlock:^(QCloudLifecycleConfiguration* result, NSError* error) {
 // 콜백 완료 설정
}];
 [[QCloudCOSXMLService defaultCOSXML] DeleteBucketLifeCycle:request];
```

### <span id="pbv">Put Bucket Versioning</span>   

Put Bucket Versioning API는 버킷의 버전 제어 기능을 활성화 또는 일시 중지할 수 있습니다. 이 API는 되돌릴 수 없으며 시동 후 취소할 수 없는 점을 주의하십시오.

#### QCloudPutBucketVersioningRequest 매개변수 설명

| 매개변수 이름      | 설명                                                         | 유형                                 | 필수 |
| ------------- | ------------------------------------------------------------ | ------------------------------------ | ---- |
| bucket        | 버킷 이름, [COS V5 콘솔](https://console.cloud.tencent.com/cos5/bucket)에서 볼 수 있으며, 형식은 &lt;bucketName&gt;-&lt;APPID&gt;입니다. 예: testBucket-1253653367 | NSString *                            | 예   |
| configuration | 버전 관리의 구체적인 정보                                           | QCloudBucketVersioningConfiguration* | 예   |

#### QCloudBucketVersioningConfiguration 매개변수 설명

| 매개변수 이름             | 설명                                                     | 유형                            | 필수 |
| -------- | ------------------------------------------- | ------------------------------- | ---- |
| status  | 버전 시동 여부 설명, 열거값: Suspended/Enabled| QCloudCOSBucketVersioningStatus | 예   |

#### 예시

```objective-c
QCloudPutBucketVersioningRequest* request = [[QCloudPutBucketVersioningRequest alloc] init];
request.bucket = @"testBucket-123456789";
QCloudBucketVersioningConfiguration* configuration = [[QCloudBucketVersioningConfiguration alloc] init];
request.configuration = configuration;
configuration.status = QCloudCOSBucketVersioningStatusEnabled;
[request setFinishBlock:^(id outputObject, NSError* error) {
   // 콜백 완료 설정
 }];
 [[QCloudCOSXMLService defaultCOSXML] PutBucketVersioning:request];
```

#### 오류 코드 반환 설명

SDK 요청에 실패하면 반환된 error는 비어 있지 않으며, 개발자가 문제를 신속하게 해결할 수 있도록 오류 코드, 오류 설명 및 기타 디버깅에 필요한 정보 등이 포함됩니다.

반환된 오류 코드(반환된 error에 캡슐화됨)는 주로 두 가지를 포함합니다. 설비 자체에서 네트워크 원인으로 반환된 오류 코드와 COS가 반환한 오류 코드입니다.

- 설비 자체가 네트워크 원인으로 생성한 오류 코드는 모두 음수이며 네 자리 숫자입니다(예: -1001). 이러한 오류 코드는 애플에서 정의한 것이며 NSURLError.h 헤더 파일 내의 정의 또는 [애플 공식 웹 사이트 문서 설명](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes)을 참조할 수 있습니다.
- COS가 반환한 오류 코드는 HTTP의 상태 코드에서 나온 것이며 404, 503 유형입니다. 이러한 오류 코드에 대해서 COS 공식 웹 사이트 문서의 [오류 코드 관련 설명](https://cloud.tencent.com/document/product/436/7730)에서 해결 방안을 찾아볼 수 있습니다.

### Get Bucket Versioning  

#### 반환 결과 QCloudBucketVersioningConfiguration 매개변수 설명

| 매개변수 이름 | 설명                                        | 유형                            |
| -------- | ------------------------------------------- | ------------------------------- |
| status  | 버전 시동 여부 설명, 열거값: Suspended\Enabled | QCloudCOSBucketVersioningStatus |

#### 예시

```objective-c
QCloudGetBucketVersioningRequest* request = [[QCloudGetBucketVersioningRequest alloc] init];
request.bucket = @"testBucket-123456789";
[request setFinishBlock:^(QCloudBucketVersioningConfiguration* result, NSError* error) {
   // 콜백 완료 설정
}];
[[QCloudCOSXMLService defaultCOSXML] GetBucketVersioning:request];
```

### Put Bucket Replication  

Put Bucket Replication 요청은 버전 관리가 활성화된 버킷에 replication 구성을 추가하는 데 사용됩니다. 만일 버킷에 이미 복제 구성이 있는 경우, 해당 요청은 기존의 구성을 대체합니다.    

#### QCloudPutBucketReplicationRequest 매개변수 설명

| 매개변수 이름     | 설명                                                         | 유형                                 | 필수 |
| ------------ | ------------------------------------------------------------ | ------------------------------------ | ---- |
| bucket       | 버킷 이름, [COS V5 콘솔](https://console.cloud.tencent.com/cos5/bucket)에서 볼 수 있으며, 형식은 &lt;bucketName&gt;-&lt;APPID&gt;입니다. 예: testBucket-1253653367 | NSString *                            | 예   |
| configuration | 모든 도메인 간 구성                                       | QCloudBucketReplicationConfiguration* | 예   |



> !해당 API 버킷을 사용하려면 버전 관리를 시동해야 하며, 버전 관리의 상세한 정보는 [Put Bucket Versioning](#pbv)을 참조하십시오.



#### 반환 결과  매개변수 설명

#### 예시

```objective-c
QCloudPutBucketReplicationRequest* request = [[QCloudPutBucketReplicationRequest alloc] init];
request.bucket = @"source-bucket";
QCloudBucketReplicationConfiguation* configuration = [[QCloudBucketReplicationConfiguation alloc] init];
configuration.role = [NSString identifierStringWithID:@"uin" :@"uin"];
QCloudBucketReplicationRule* rule = [[QCloudBucketReplicationRule alloc] init];
rule.identifier = @"identifier";
rule.status = QCloudQCloudCOSXMLStatusEnabled;

QCloudBucketReplicationDestination* destination = [[QCloudBucketReplicationDestination alloc] init];
//qcs:id/0:cos:[region]:appid/[AppId]:[bucketname]
NSString* destinationBucket = @"destinationBucket";
NSString* region = @"destinationRegion"
destination.bucket = [NSString stringWithFormat:@"qcs:id/0:cos:%@:appid/%@:%@",@"region",@"appid",@"destinationBucket"];
rule.destination = destination;
configuration.rule = @[rule];
request.configuation = configuration;
[request setFinishBlock:^(id outputObject, NSError* error) {
     // 콜백 완료 설정
}];
 [[QCloudCOSXMLService defaultCOSXML] PutBucketRelication:request];
```

#### 오류 코드 반환 설명

SDK 요청에 실패하면 반환된 error는 비어 있지 않으며, 개발자가 문제를 신속하게 해결할 수 있도록 오류 코드, 오류 설명 및 기타 디버깅에 필요한 정보 등이 포함됩니다.

반환된 오류 코드(반환된 error에 캡슐화됨)는 주로 두 가지를 포함합니다. 설비 자체에서 네트워크 원인으로 반환된 오류 코드와 COS가 반환한 오류 코드입니다.

- 설비 자체가 네트워크 원인으로 생성한 오류 코드는 모두 음수이며 네 자리 숫자입니다(예: -1001). 이러한 오류 코드는 애플에서 정의한 것이며 NSURLError.h 헤더 파일 내의 정의 또는 [애플 공식 웹 사이트 문서 설명](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes)을 참조할 수 있습니다.
- COS가 반환한 오류 코드는 HTTP의 상태 코드에서 나온 것이며 404, 503 유형입니다. 이러한 오류 코드에 대해서 COS 공식 웹 사이트 문서의 [오류 코드 관련 설명](https://cloud.tencent.com/document/product/436/7730)에서 해결 방안을 찾아볼 수 있습니다.

### Get Bucket Replication

Get Bucket Replication API 요청은 읽기 버킷에서 사용자의 도메인 간 구성 정보 복제를 구현합니다.

#### 반환 결과QCloudBucketReplicationConfiguation 매개변수 설명

| 매개변수 이름 | 설명                                                         | 유형                                    |
| -------- | ------------------------------------------------------------ | --------------------------------------- |
| role     | 발기자 신분 표시, 형식: qcs::cam::uin/<OwnerUin>:uin/<SubUin> | NSString*                               |
| rule     | 구체적인 구성 정보, 최대 1000개 지원, 모든 정책은 대상 버킷 하나만 가리킬 수 있습니다 | NSArray<QCloudBucketReplicationRule*> * |

#### QCloudBucketReplicationRule 매개변수 설명

| 매개변수 이름    | 설명                                                     | 유형                                |
| ----------- | -------------------------------------------------------- | ----------------------------------- |
| status      | 표지 Rule 효력 발생 여부                                       | QCloudQCloudCOSXMLStatus            |
| identifier  | 구체적인 rule의 이름을 표시하는 데 사용됩니다                                 | NSString*                           |
| prefix      | 접두사 매칭 정책, 중첩할 수 없으며 중첩 시 오류가 반환됩니다. 접두사 매칭 루트 디렉터리는 비어 있습니다 | NSString*                           |
| destination | 대상 버킷 정보                                           | QCloudBucketReplicationDestination* |

#### 예시

```objective-c
QCloudGetBucketReplicationRequest* request = [[QCloudGetBucketReplicationRequest alloc] init];
request.bucket = @"testBucket-123456789";
[request setFinishBlock:^(QCloudBucketReplicationConfiguation* result, NSError* error) {
    // 콜백 완료 설정
}];
[[QCloudCOSXMLService defaultCOSXML] GetBucketReplication:request];

```

#### 오류 코드 반환 설명

SDK 요청에 실패하면 반환된 error는 비어 있지 않으며, 개발자가 문제를 신속하게 해결할 수 있도록 오류 코드, 오류 설명 및 기타 디버깅에 필요한 정보 등이 포함됩니다.

반환된 오류 코드(반환된 error에 캡슐화됨)는 주로 두 가지를 포함합니다. 설비 자체에서 네트워크 원인으로 반환된 오류 코드와 COS가 반환한 오류 코드입니다.

- 설비 자체가 네트워크 원인으로 생성한 오류 코드는 모두 음수이며 네 자리 숫자입니다(예: -1001). 이러한 오류 코드는 애플에서 정의한 것이며 NSURLError.h 헤더 파일 내의 정의 또는 [애플 공식 웹 사이트 문서 설명](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes)을 참조할 수 있습니다.
- COS가 반환한 오류 코드는 HTTP의 상태 코드에서 나온 것이며 404, 503 유형입니다. 이러한 오류 코드에 대해서 COS 공식 웹 사이트 문서의 [오류 코드 관련 설명](https://cloud.tencent.com/document/product/436/7730)에서 해결 방안을 찾아볼 수 있습니다.



### Delete Bucket Replication  

Delete Bucket Replication API 요청은 버킷의 사용자에서 크로스 지역 복제 구성 삭제를 실시합니다.

#### 매개변수 설명

#### 반환 결과  매개변수 설명

#### 예시

```objective-c
QCloudDeleteBucketReplicationRequest* request = [[QCloudDeleteBucketReplicationRequest alloc] init];
request.bucket = @"testBucket-123456789";
[request setFinishBlock:^(id outputObject, NSError* error) {
   // 콜백 완료 설정
}];
[[QCloudCOSXMLService defaultCOSXML] DeleteBucketReplication:request];
```

## 파일 조작

COS에서 각 파일은 하나의 Object입니다(객체). 파일 조작도 객체에 대한 조작입니다.

### 간편 업로드(Put Object)

간편 업로드는 소용량 파일(20MB 이하)로 제한됩니다. 간편 업로드는 메모리에서 파일 업로드를 지원합니다.

> !현재 액세스 정책 항목은 1000으로 제한되어 있습니다. 객체에 대해 ACL 제어가 필요하지 않은 경우 업로드 시 설정하지 마십시오. 기본으로 버킷 권한은 계승됩니다.

#### QCloudPutObjectRequest 매개변수 설명

| 매개변수 이름                      | 설명                                                         | 유형                  | 필수 |
| ----------------------------- | ------------------------------------------------------------ | --------------------- | ---- |
| Object                        | 객체 키(Key)는 버킷에서 객체의 유일한 표시입니다. 예를 들어, 객체의 접근 도메인 이름 bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg 중, 객체 키는 doc1/pic1.jpg입니다. 자세한 설명은 [객체 설명](https://cloud.tencent.com/document/product/436/13324) | NSString *            | 예   |
| bucket                        | 버킷 이름, [COS V5 콘솔](https://console.cloud.tencent.com/cos5/bucket)에서 볼 수 있으며, 형식은 &lt;bucketName&gt;-&lt;APPID&gt;입니다. 예: testBucket-1253653367 | NSString *            | 예   |
| body                          | 파일이 디스크에 저장되어 있는 경우,  업로드할 파일의 경로가 되어야 하며, NSURL * 유형 변수를 입력합니다. 파일이 메모리에 저장되어 있으면, 이진 데이터 파일을 포함하는 NSData * 유형 변수를 입력할 수 있습니다 | BodyType              | 예   |
| storageClass                  | 객체의 스토리지 클래스                                               | QCloudCOSStorageClass | 예   |
| cacheControl                  | RFC 2616에 정의된 캐시 정책                                    | NSString *            | 아니요  |
| contentDisposition            | RFC 2616에 정의된 파일 이름                                     | NSString *            | 아니요  |
| expect                        | expect=@"100-Continue" 사용 시, 서버측에서 확인을 받기 전까지 요청 내용이 전송되지 않습니다 | NSString *            | 아니요  |
| expires                       | RFC 2616에 정의된 만료 시간                                     | NSString *            | 아니요  |
| initMultipleUploadFinishBlock | 해당 request가 멀티파트 업로드 요청을 생성하는 경우, 멀티파트 업로드 초기화 완료 후 이 block을 통해 콜백 되고, 해당 콜백 block에서 멀티파트 완료 후의 bucket, key, uploadID, 및 후속 업로드 실패 후 업로드 복구에 사용하는 ResumeData를 획득할 수 있습니다 | block                 | 아니요   |
| accessControlList             | Object의 ACL 속성을 정의합니다. 유효값: private, public-read-write, public-read; 기본값: private | NSString *            | 아니요   |
| grantRead         | 피부여자에게 읽기 권한을 부여합니다. 형식: `id=" ",id=" "; 서브 계정에 권한을 부여할 경우, 형식은 id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;SubUin>" 루트 계정에 권한을 부여할 경우, 형식은 id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;OwnerUin>"  그중 OwnerUin은 루트 계정의 ID를 나타내며, SubUin은 서브 계정의 ID를 나타냅니다 | NSString * | 아니요   |
| grantWrite                    | 피부여자에게 쓰기 권한을 부여합니다. 형식은 위와 같습니다.                             | NSString *            | 아니요   |
| grantFullControl              | 피부여자에게 읽기/쓰기 권한을 부여합니다. 형식은 위와 같습니다.                               | NSString *            | 아니요   |

#### 예시    

```objective-C
QCloudPutObjectRequest* put = [QCloudPutObjectRequest new];
put.object = @"object-name";
put.bucket = @"bucket-12345678";
put.body =  [@"testFileContent" dataUsingEncoding:NSUTF8StringEncoding];
[put setFinishBlock:^(id outputObject, NSError *error) {
   // 콜백 완료
  if (nil == error) {
   //성공
   }
   }];
[[QCloudCOSXMLService defaultCOSXML] PutObject:put];

```

#### 오류 코드 반환 설명

SDK 요청에 실패하면 반환된 error는 비어 있지 않으며, 개발자가 문제를 신속하게 해결할 수 있도록 오류 코드, 오류 설명 및 기타 디버깅에 필요한 정보 등이 포함됩니다.

반환된 오류 코드(반환된 error에 캡슐화됨)는 주로 두 가지를 포함합니다. 설비 자체에서 네트워크 원인으로 반환된 오류 코드와 COS가 반환한 오류 코드입니다.

- 설비 자체가 네트워크 원인으로 생성한 오류 코드는 모두 음수이며 네 자리 숫자입니다(예: -1001). 이러한 오류 코드는 애플에서 정의한 것이며 NSURLError.h 헤더 파일 내의 정의 또는 [애플 공식 웹 사이트 문서 설명](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes)을 참조할 수 있습니다.
- COS가 반환한 오류 코드는 HTTP의 상태 코드에서 나온 것이며 404, 503 유형입니다. 이러한 오류 코드에 대해서 COS 공식 웹 사이트 문서의 [오류 코드 관련 설명](https://cloud.tencent.com/document/product/436/7730)에서 해결 방안을 찾아볼 수 있습니다.



### 객체의 ACL(Access Control List) 조회

#### 방식 프로토타입

파일 조작을 진행하기 전에 헤더 파일 QCloudCOSXML/QCloudCOSXML.h를 가져오기 해야 합니다. 그 전에 앞에 설명한 STEP-1 초기화 조작을 완료해야 합니다. QCloudGetObjectACLRequest 인스턴스를 생성한 후 필요한 예외적 제한 조건을 입력하고 내용을 획득합니다. 구체적인 단계는 다음과 같습니다.    

1. QCloudGetObjectACLRequest를 인스턴스화하고, 버킷의 이름 및 조회할 객체의 이름을 입력합니다.    
2. QCloudCOSXMLService 객체의 GetObjectACL 방법을 호출하여 요청을 보냅니다.    
3. 콜백 된 finishBlock에서 획득한 QCloudACLPolicy 객체에서 캡슐화된 ACL 구체적인 정보를 획득합니다.   

#### QCloudGetObjectACLRequest 매개변수 설명

| 매개변수 이름 | 설명                                                         | 유형       | 필수 |
| -------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket   | 버킷 이름, [COS V5 콘솔](https://console.cloud.tencent.com/cos5/bucket)에서 볼 수 있으며, 형식은 &lt;bucketName&gt;-&lt;APPID&gt;입니다. 예: testBucket-1253653367 | NSString * | 예   |
| object   | 객체 키(Key)는 버킷에서 객체의 유일한 표시입니다. 예를 들어, 객체의 접근 도메인 이름 bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg 중, 객체 키는 doc1/pic1.jpg입니다. 자세한 설명은 [객체 설명](https://cloud.tencent.com/document/product/436/13324)을 참조하십시오 | NSString*           | 예   |

#### 예시

```objective-c
request.bucket = self.aclBucket;
request.object = @"객체의 이름";
request.bucket = @"testBucket-123456789"
__block QCloudACLPolicy* policy;
[request setFinishBlock:^(QCloudACLPolicy * _Nonnull result, NSError * _Nonnull error) {
     policy = result;
}];
[[QCloudCOSXMLService defaultCOSXML] GetObjectACL:request];
```

#### 오류 코드 반환 설명

SDK 요청에 실패하면 반환된 error는 비어 있지 않으며, 개발자가 문제를 신속하게 해결할 수 있도록 오류 코드, 오류 설명 및 기타 디버깅에 필요한 정보 등이 포함됩니다.

반환된 오류 코드(반환된 error에 캡슐화됨)는 주로 두 가지를 포함합니다. 설비 자체에서 네트워크 원인으로 반환된 오류 코드와 COS가 반환한 오류 코드입니다.

- 설비 자체가 네트워크 원인으로 생성한 오류 코드는 모두 음수이며 네 자리 숫자입니다(예: -1001). 이러한 오류 코드는 애플에서 정의한 것이며 NSURLError.h 헤더 파일 내의 정의 또는 [애플 공식 웹 사이트 문서 설명](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes)을 참조할 수 있습니다.
- COS가 반환한 오류 코드는 HTTP의 상태 코드에서 나온 것이며 404, 503 유형입니다. 이러한 오류 코드에 대해서 COS 공식 웹 사이트 문서의 [오류 코드 관련 설명](https://cloud.tencent.com/document/product/436/7730)에서 해결 방안을 찾아볼 수 있습니다.

### 객체의 ACL(Access Control List) 설정

현재 접근 정책 항목은 1000으로 제한되어 있습니다. 객체에 대해 ACL 제어가 필요하지 않은 경우 설정하지 마십시오. 기본으로 Bucket 권한은 계승됩니다.

#### 방식 프로토타입

객체 조작을 진행하기 전에 헤더 파일 QCloudCOSXML/QCloudCOSXML.h를 가져오기 해야 합니다. 그 전에 앞에 설명한 STEP-1 초기화 조작을 완료해야 합니다. QCloudPutObjectACLRequest 인스턴스를 생성한 후 필요한 예외적 제한 조건을 입력하고 내용을 획득합니다. 구체적인 단계는 다음과 같습니다.    

1. QCloudPutObjectACLRequest를 인스턴스화하고, 버킷의 이름 및 추가적으로 권한 부여의 구체적인 정보 등과 같은 필요한 매개변수를 입력합니다.    
2. QCloudCOSXMLService 객체의 방법을 호출하여 요청을 보냅니다.    
3. 콜백 된 finishBlock에서 설정의 완료 상황을 획득합니다. error가 비어 있는 경우 설정에 성공한 것입니다.   

#### QCloudPutObjectACLRequest 매개변수 설명

| 매개변수 이름          | 설명                                                         | 유형       | 필수 |
| ----------------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket            | 버킷 이름, [COS V5 콘솔](https://console.cloud.tencent.com/cos5/bucket)에서 볼 수 있으며, 형식은 &lt;bucketName&gt;-&lt;APPID&gt;입니다. 예: testBucket-1253653367 | NSString * | 예   |
| object            | 객체 이름                                                       | NSString * | 예   |
| accessControlList | Object의 ACL 속성을 정의합니다. 유효값: private, public-read-write, public-read; 기본값: private | NSString * | 아니요   |
| grantRead         | 피부여자에게 읽기 권한을 부여합니다. 형식: `id=" ",id=" "; <br>서브 계정에 권한을 부여할 경우, id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;", <br>루트 계정에 권한을 부여할 경우, id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt;" <br>그중 OwnerUin은 루트 계정의 ID를 나타내며, SubUin은 서브 계정의 ID를 나타냅니다 | NSString * | 아니요   |
| grantWrite| 피부여자에게 쓰기 권한을 부여합니다. 형식은 위와 같습니다.                             | NSString * | 아니요   |
| grantFullControl  | 피부여자에게 읽기/쓰기 권한을 부여합니다. 형식은 위와 같습니다.                               | NSString *            | 아니요   |

#### 예시

```objective-c
QCloudPutObjectACLRequest* request = [QCloudPutObjectACLRequest new];
request.object = @"ACL의 객체 이름을 설정해야 함";
request.bucket = @"testBucket-123456789";
NSString *ownerIdentifier = [NSString stringWithFormat:@"qcs::cam::uin/%@:uin/%@",self.appID, self.appID];
NSString *grantString = [NSString stringWithFormat:@"id=\"%@\"",ownerIdentifier];
request.grantFullControl = grantString;
__block NSError* localError;
[request setFinishBlock:^(id outputObject, NSError *error) {
     localError = error;
}];
[[QCloudCOSXMLService defaultCOSXML] PutObjectACL:request];
```

#### 오류 코드 반환 설명

SDK 요청에 실패하면 반환된 error는 비어 있지 않으며, 개발자가 문제를 신속하게 해결할 수 있도록 오류 코드, 오류 설명 및 기타 디버깅에 필요한 정보 등이 포함됩니다.

반환된 오류 코드(반환된 error에 캡슐화됨)는 주로 두 가지를 포함합니다. 즉, 설비 자체에서 네트워크 원인으로 반환된 오류 코드와 COS가 반환한 오류 코드입니다.

- 설비 자체가 네트워크 원인으로 생성한 오류 코드는 모두 음수이며 네 자리 숫자입니다(예: -1001). 이러한 오류 코드는 애플에서 정의한 것이며 NSURLError.h 헤더 파일 내의 정의 또는 [애플 공식 웹 사이트 문서 설명](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes)을 참조할 수 있습니다.
- COS가 반환한 오류 코드는 HTTP의 상태 코드에서 나온 것이며 404, 503 유형입니다. 이러한 오류 코드에 대해서 COS 공식 웹 사이트 문서의 [오류 코드 관련 설명](https://cloud.tencent.com/document/product/436/7730)에서 해결 방안을 찾아볼 수 있습니다.



### 파일 다운로드

#### 방식 프로토타입

파일 조작을 진행하기 전에 헤더 파일 QCloudCOSXML/QCloudCOSXML.h를 가져오기 해야 합니다. 그 전에 앞에 설명한 STEP-1 초기화 조작을 완료해야 합니다. 인스턴스를 생성한 후 필요한 예외적 제한 조건을 입력하고 내용을 획득합니다. 구체적인 단계는 다음과 같습니다.    

1. 인스턴스화하고 필요한 매개변수를 입력합니다.    
2. QCloudCOSXMLService 객체의 방법을 호출하여 요청을 보냅니다.    
3. 콜백된 finishBlock에서 구체적인 내용을 획득합니다.   

#### 매개변수 설명

| 매개변수 이름                   | 설명                                                         | 유형       | 필수 |
| -------------------------- | ------------------------------------------------------------ | ---------- | ---- |
| bucket                     | 버킷 이름, [COS V5 콘솔](https://console.cloud.tencent.com/cos5/bucket)에서 볼 수 있으며, 형식은 &lt;bucketName&gt;-&lt;APPID&gt;입니다. 예: testBucket-1253653367 | NSString * | 예   |
| object                     | 객체 이름                                                       | NSString * | 예   |
| range                      | RFC 2616에 정의된 지정 파일 다운로드 범위, 단위는 바이트(bytes)입니다     | NSString * | 아니요   |
| ifModifiedSince | 파일 수정 시간이 지정한 시간보다 늦으면 파일 내용을 반환합니다. 그렇지 않으면 412(not modified)를 반환합니다 | NSString * | 아니요   |
| responseContentType        | 응답 헤더 중의 Content-Type 매개변수를 설정합니다                                  | NSString      | 아니요   |
| responseContentLanguage    | 응답 헤더 중의 Content-Language 매개변수를 설정합니다                                | NSString | 아니요   |
| responseContentExpires     | 응답 헤더 중의 Content-Expires 매개변수를 설정합니다                                 | NSString * | 아니요   |
| responseCacheControl       | 응답 헤더 중의 Cache-Control 매개변수를 설정합니다                                   | NSString | 아니요   |
| responseContentDisposition | 응답 헤더 중의 Content-Disposition 매개변수를 설정합니다                             | NSString * | 아니요   |
| responseContentEncoding    | 응답 헤더 중의 Content-Encoding 매개변수를 설정합니다                                | NSString * | 아니요   |

#### 예시

```objective-c
QCloudGetObjectRequest* request = [QCloudGetObjectRequest new];
//다운로드 URL 경로를 설정합니다. 설정했다면 파일이 지정한 경로로 다운로드됩니다. 해당 매개변수를 설정하지 않으면 파일은 메모리에 다운로드되고 finishBlock의 	outputObject에 저장됩니다.
request.downloadingURL = [NSURL URLWithString:QCloudTempFilePathWithExtension(@"downding")];
request.object = @“귀하의 Object-Key”;
request.bucket = @"testBucket-123456789";
[request setFinishBlock:^(id outputObject, NSError *error) {
    //additional actions after finishing
}];
[request setDownProcessBlock:^(int64_t bytesDownload, int64_t totalBytesDownload, int64_t totalBytesExpectedToDownload) {
   //다운로드 과정의 진도
}];
[[QCloudCOSXMLService defaultCOSXML] GetObject:request];
```

#### 오류 코드 반환 설명

SDK 요청에 실패하면 반환된 error는 비어 있지 않으며, 개발자가 문제를 신속하게 해결할 수 있도록 오류 코드, 오류 설명 및 기타 디버깅에 필요한 정보 등이 포함됩니다.

반환된 오류 코드(반환된 error에 캡슐화됨)는 주로 두 가지를 포함합니다. 설비 자체에서 네트워크 원인으로 반환된 오류 코드와 COS가 반환한 오류 코드입니다.

- 설비 자체가 네트워크 원인으로 생성한 오류 코드는 모두 음수이며 네 자리 숫자입니다(예: -1001). 이러한 오류 코드는 애플에서 정의한 것이며 NSURLError.h 헤더 파일 내의 정의 또는 [애플 공식 웹 사이트 문서 설명](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes)을 참조할 수 있습니다.
- COS가 반환한 오류 코드는 HTTP의 상태 코드에서 나온 것이며 404, 503 유형입니다. 이러한 오류 코드에 대해서 COS 공식 웹 사이트 문서의 [오류 코드 관련 설명](https://cloud.tencent.com/document/product/436/7730)에서 해결 방안을 찾아볼 수 있습니다.



### Object 크로스 도메인 접근의 사전 요청

#### 방식 프로토타입

파일 조작을 진행하기 전에 헤더 파일 QCloudCOSXML/QCloudCOSXML.h를 가져오기 해야 합니다. 그 전에 앞에 설명한 STEP-1 초기화 조작을 완료해야 합니다. QCloudOptionsObjectRequest 인스턴스를 생성한 후 필요한 예외적 제한 조건을 입력하고 내용을 획득합니다. 구체적인 단계는 다음과 같습니다.    

1. QCloudOptionsObjectRequest를 인스턴스화하고, 설정할 객체 이름, 버킷 이름, 크로스 도메인 접근 요청을 시뮬레이션하는 http 방법 및 도메인 간 접근 허용을 시뮬레이션하는 접근 소스를 입력합니다.    
2. QCloudCOSXMLService 객체의 방법을 호출하여 요청을 보냅니다.    
3. 콜백된 finishBlock에서 구체적인 내용을 획득합니다.   

#### QCloudOptionsObjectRequest 매개변수 설명

| 매개변수 이름                   | 설명                                                         | 유형                        | 필수 |
| -------------------------- | ------------------------------------------------------------ | --------------------------- | ---- |
| object                     | 객체 키(Key)는 버킷에서 객체의 유일한 표시입니다. 예를 들어, 객체의 접근 도메인 이름 bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg 중, 객체 키는 doc1/pic1.jpg입니다. 자세한 설명은 [객체 설명](https://cloud.tencent.com/document/product/436/13324)을 참조하십시오 | NSString*           | 예   |
| bucket                     | 버킷 이름, [COS V5 콘솔](https://console.cloud.tencent.com/cos5/bucket)에서 볼 수 있으며, 형식은 &lt;bucketName&gt;-&lt;APPID&gt;입니다. 예: testBucket-1253653367 | NSString *                  | 예   |
| accessControlRequestMethod | 크로스 도메인 접근 요청 시뮬레이션 HTTP 방법                                   | NSArray&lt;NSString`*`> *   | 예   |
| origin                     | 크로스 도메인 접근 허용을 시뮬레이션하는 접근 소스, 와일드카드 * 지원, 형식: 프로토콜: //도메인 이름[:포트] 예: `http://www.qq.com` | NSString *                  | 예   |
| allowedHeader              | OPTIONS 요청 발송 시 서버측에게 알립니다. 이어지는 요청은 어떠한 사용자 지정 HTTP 요청 헤더를 사용할 수 있으며, 와일드카드*를 지원합니다 | NSArray&lt;NSString `*` > * | 아니요   |

#### 예시

```objective-c
QCloudOptionsObjectRequest* request = [[QCloudOptionsObjectRequest alloc] init];
request.bucket =@"버킷 이름";
request.origin = @"*";
request.accessControlRequestMethod = @"get";
request.accessControlRequestHeaders = @"host";
request.object = @"객체 이름";
__block id resultError;
[request setFinishBlock:^(id outputObject, NSError* error) {
     resultError = error;
 }];

[[QCloudCOSXMLService defaultCOSXML] OptionsObject:request];

```

#### 오류 코드 반환 설명

SDK 요청에 실패하면 반환된 error는 비어 있지 않으며, 개발자가 문제를 신속하게 해결할 수 있도록 오류 코드, 오류 설명 및 기타 디버깅에 필요한 정보 등이 포함됩니다.

반환된 오류 코드(반환된 error에 캡슐화됨)는 주로 두 가지를 포함합니다. 설비 자체에서 네트워크 원인으로 반환된 오류 코드와 COS가 반환한 오류 코드입니다.

- 설비 자체가 네트워크 원인으로 생성한 오류 코드는 모두 음수이며 네 자리 숫자입니다(예: -1001). 이러한 오류 코드는 애플에서 정의한 것이며 NSURLError.h 헤더 파일 내의 정의 또는 [애플 공식 웹 사이트 문서 설명](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes)을 참조할 수 있습니다.
- COS가 반환한 오류 코드는 HTTP의 상태 코드에서 나온 것이며 404, 503 유형입니다. 이러한 오류 코드에 대해서 COS 공식 웹 사이트 문서의 [오류 코드 관련 설명](https://cloud.tencent.com/document/product/436/7730)에서 해결 방안을 찾아볼 수 있습니다.



### 단일 객체 삭제

#### 방식 프로토타입

파일 조작을 진행하기 전에 헤더 파일 QCloudCOSXML/QCloudCOSXML.h를 가져오기 해야 합니다. 그 전에 앞에 설명한 STEP-1 초기화 조작을 완료해야 합니다. QCloudDeleteObjectRequest 인스턴스를 생성한 후 필요한 예외적 제한 조건을 입력하고 내용을 획득합니다. 구체적인 단계는 다음과 같습니다.    

1. QCloudDeleteObjectRequest를 인스턴스화하고, 필요한 매개변수를 입력합니다.    
2. QCloudCOSXMLService 객체의 방법을 호출하여 요청을 보냅니다.    
3. 콜백된 finishBlock에서 구체적인 내용을 획득합니다.   

#### QCloudDeleteObjectRequest 매개변수 설명

| 매개변수 이름 | 유형                                                         | 필수       | 설명 |
| -------- | ------------------------------------------------------------ | ---------- | ---- |
| object   | 객체 키(Key)는 버킷에서 객체의 유일한 표시입니다. 예를 들어, 객체의 접근 도메인 이름 bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg 중, 객체 키는 doc1/pic1.jpg입니다. 자세한 설명은 [객체 설명](https://cloud.tencent.com/document/product/436/13324)을 참조하십시오 | NSString *          | 예   |
| bucket   | 버킷 이름, [COS V5 콘솔](https://console.cloud.tencent.com/cos5/bucket)에서 볼 수 있으며, 형식은 &lt;bucketName&gt;-&lt;APPID&gt;입니다. 예: testBucket-1253653367 | NSString * | 예   |

#### 예시

```objective-c
QCloudDeleteObjectRequest* deleteObjectRequest = [QCloudDeleteObjectRequest new];
deleteObjectRequest.bucket = @"testBucket-123456789";
deleteObjectRequest.object = @"객체 이름";
__block NSError* resultError;
[deleteObjectRequest setFinishBlock:^(id outputObject, NSError *error) {
    resultError = error;
}];
[[QCloudCOSXMLService defaultCOSXML] DeleteObject:deleteObjectRequest];

```

#### 오류 코드 반환 설명

SDK 요청에 실패하면 반환된 error는 비어 있지 않으며, 개발자가 문제를 신속하게 해결할 수 있도록 오류 코드, 오류 설명 및 기타 디버깅에 필요한 정보 등이 포함됩니다.

반환된 오류 코드(반환된 error에 캡슐화됨)는 주로 두 가지를 포함합니다. 즉, 설비 자체에서 네트워크 원인으로 반환된 오류 코드와 COS가 반환한 오류 코드입니다.

- 설비 자체가 네트워크 원인으로 생성한 오류 코드는 모두 음수이며 네 자리 숫자입니다(예: -1001). 이러한 오류 코드는 애플에서 정의한 것이며 NSURLError.h 헤더 파일 내의 정의 또는 [애플 공식 웹 사이트 문서 설명](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes)을 참조할 수 있습니다.
- COS가 반환한 오류 코드는 HTTP의 상태 코드에서 나온 것이며 404, 503 유형입니다. 이러한 오류 코드에 대해서 COS 공식 웹 사이트 문서의 [오류 코드 관련 설명](https://cloud.tencent.com/document/product/436/7730)에서 해결 방안을 찾아볼 수 있습니다.



### 여러 객체 삭제

#### 방식 프로토타입

파일 조작을 진행하기 전에 헤더 파일 QCloudCOSXML/QCloudCOSXML.h를 가져오기 해야 합니다. 그 전에 앞에 설명한 STEP-1 초기화 조작을 완료해야 합니다. QCloudDeleteMultipleObjectRequest 인스턴스를 생성한 후 필요한 예외적 제한 조건을 입력하고 내용을 획득합니다. 구체적인 단계는 다음과 같습니다.    

1. QCloudDeleteMultipleObjectRequest를 인스턴스화하고, 필요한 매개변수를 입력합니다.    
2. QCloudCOSXMLService 객체의 방법을 호출하여 요청을 보냅니다.    
3. 콜백된 finishBlock에서 구체적인 내용을 획득합니다.   

#### QCloudDeleteMultipleObjectRequest 매개변수 설명

| 매개변수 이름             | 설명                                                         | 유형               | 필수 |
| ------------- | ------------------------------------------------------------ | ------------------ | ---- |
| object        | 객체 키(Key)는 버킷에서 객체의 유일한 표시입니다. 예를 들어, 객체의 접근 도메인 이름 bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg 중, 객체 키는 doc1/pic1.jpg입니다. 자세한 설명은 [객체 설명](https://cloud.tencent.com/document/product/436/13324)을 참조하십시오 | NSString*           | 예   |
| deleteObjects | 일괄 삭제가 필요한 여러 객체의 정보를 캡슐화합니다                           | QCloudDeleteInfo * | 예   |

#### QCloudDeleteInfo 매개변수 설명

| 매개변수 이름             | 설명                       | 유형                                      | 필수 |
| -------- | -------------------------- | ----------------------------------------- | ---- |
| objects  | 삭제할 객체 정보의 배열을 저장합니다  | NSArray&lt;QCloudDeleteObjectInfo `*` > * | 예   |

#### QCloudDeleteObjectInfo 매개변수 설명

| 매개변수 이름 | 설명                                                         | 유형       | 필수 |
| -------- | ------------------------------------------------------------ | ---------- | ---- |
| key      | 객체 키(Key)는 버킷에서 객체의 유일한 표시입니다. 예를 들어, 객체의 접근 도메인 이름 bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg 중, 객체 키는 doc1/pic1.jpg입니다. 자세한 설명은 [객체 설명](https://cloud.tencent.com/document/product/436/13324)을 참조하십시오 | NSString * | 예   |

#### 예시

```objective-c
QCloudDeleteMultipleObjectRequest* delteRequest = [QCloudDeleteMultipleObjectRequest new];
delteRequest.bucket = @"testBucket-123456789";

QCloudDeleteObjectInfo* deletedObject0 = [QCloudDeleteObjectInfo new];
deletedObject0.key = @"첫 번째 객체 이름";

QCloudDeleteObjectInfo* deleteObject1 = [QCloudDeleteObjectInfo new];
deleteObject1.key = @"두 번째 객체 이름";

QCloudDeleteInfo* deleteInfo = [QCloudDeleteInfo new];
deleteInfo.quiet = NO;
deleteInfo.objects = @[ deletedObject0,deleteObject2];
delteRequest.deleteObjects = deleteInfo;
__block NSError* resultError;
[delteRequest setFinishBlock:^(QCloudDeleteResult* outputObject, NSError *error) {
      localError = error;
      deleteResult = outputObject;
}];
[[QCloudCOSXMLService defaultCOSXML] DeleteMultipleObject:delteRequest];

```

#### 오류 코드 반환 설명

SDK 요청에 실패하면 반환된 error는 비어 있지 않으며, 개발자가 문제를 신속하게 해결할 수 있도록 오류 코드, 오류 설명 및 기타 디버깅에 필요한 정보 등이 포함됩니다.

반환된 오류 코드(반환된 error에 캡슐화됨)는 주로 두 가지를 포함합니다. 즉, 설비 자체에서 네트워크 원인으로 반환된 오류 코드와 COS가 반환한 오류 코드입니다.

- 설비 자체가 네트워크 원인으로 생성한 오류 코드는 모두 음수이며 네 자리 숫자입니다(예: -1001). 이러한 오류 코드는 애플에서 정의한 것이며 NSURLError.h 헤더 파일 내의 정의 또는 [애플 공식 웹 사이트 문서 설명](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes)을 참조할 수 있습니다.
- COS가 반환한 오류 코드는 HTTP의 상태 코드에서 나온 것이며 404, 503 유형입니다. 이러한 오류 코드에 대해서 COS 공식 웹 사이트 문서의 [오류 코드 관련 설명](https://cloud.tencent.com/document/product/436/7730)에서 해결 방안을 찾아볼 수 있습니다.



### 초기화 멀티파트 업로드

#### 방식 프로토타입

파일 조작을 진행하기 전에 헤더 파일 QCloudCOSXML/QCloudCOSXML.h를 가져오기 해야 합니다. 그 전에 앞에 설명한 STEP-1 초기화 조작을 완료해야 합니다. QCloudInitiateMultipartUploadRequest 인스턴스를 생성한 후 필요한 예외적 제한 조건을 입력하고 내용을 획득합니다. 구체적인 단계는 다음과 같습니다.    

1. QCloudInitiateMultipartUploadRequest를 인스턴스화하고, 필요한 매개변수를 입력합니다.    
2. QCloudCOSXMLService 객체의 InitiateMultipartUpload 방법을 호출하여 요청을 합니다.    
3. 콜백된 finishBlock에서 구체적인 내용을 획득합니다.   

#### 매개변수 설명

| 매개변수 이름             | 설명                                                         | 유형                  | 필수 |
| ------------------ | ------------------------------------------------------------ | --------------------- | ---- |
| Object             | 업로드 파일(객체)의 파일 이름이며 객체의 key이기도 합니다. 객체 키(Key)는 버킷에서 객체의 유일한 표시입니다. 예를 들어, 객체의 접근 도메인 이름 bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg 중, 객체 키는 doc1/pic1.jpg입니다. 자세한 설명은 [객체 설명](https://cloud.tencent.com/document/product/436/13324)을 참조하십시오 | NSString*           | 예   |
| bucket             | 버킷 이름, [COS V5 콘솔](https://console.cloud.tencent.com/cos5/bucket)에서 볼 수 있으며, 형식은 &lt;bucketName&gt;-&lt;APPID&gt;입니다. 예: testBucket-1253653367 | NSString * | 예   |
| cacheControl       | RFC 2616에 정의된 캐시 정책                                     | NSString *            | 아니요  |
| contentDisposition | RFC 2616에 정의된 파일 이름                                     | NSString *            | 아니요  |
| expect             | `expect=@"100-continue"` 사용 시, 서버측에서 확인을 받기 전까지 요청 내용이 전송되지 않습니다 | NSString *            | 아니요  |
| expires            | RFC 2616에 정의된 만료 시간                                    | NSString *            | 아니요  |
| storageClass                  | 객체의 스토리지 클래스                                               | QCloudCOSStorageClass | 아니요   |
| accessControlList  | Object의 ACL 속성을 정의합니다. 유효값: private, public-read-write, public-read; 기본값: private | NSString *            | 아니요   |
| grantRead         | 피부여자에게 읽기 권한을 부여합니다. 형식: `id=" ",id=" "; <br>서브 계정에 권한을 부여할 경우, id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;SubUin&gt;", <br>루트 계정에 권한을 부여할 경우, id="qcs::cam::uin/&lt;OwnerUin&gt;:uin/&lt;OwnerUin&gt;"  <br>그중 OwnerUin은 루트 계정의 ID를 나타내며, SubUin은 서브 계정의 ID를 나타냅니다 | NSString * | 아니요   |
| grantWrite         | 피부여자에게 쓰기 권한을 부여합니다. 형식은 위와 같습니다.                             | NSString *            | 아니요   |
| grantFullControl   | 피부여자에게 쓰기 권한을 부여합니다. 형식은 위와 같습니다.                             | NSString *            | 아니요   |

#### 예시

```objective-c
QCloudInitiateMultipartUploadRequest* initrequest = [QCloudInitiateMultipartUploadRequest new];
initrequest.bucket = @"testBucket-123456789";
initrequest.object = @"객체 이름";
__block QCloudInitiateMultipartUploadResult* initResult;
[initrequest setFinishBlock:^(QCloudInitiateMultipartUploadResult* outputObject, NSError *error) {
    initResult = outputObject;
}];
[[QCloudCOSXMLService defaultCOSXML] InitiateMultipartUpload:initrequest];

```

#### 오류 코드 반환 설명

SDK 요청에 실패하면 반환된 error는 비어 있지 않으며, 개발자가 문제를 신속하게 해결할 수 있도록 오류 코드, 오류 설명 및 기타 디버깅에 필요한 정보 등이 포함됩니다.

반환된 오류 코드(반환된 error에 캡슐화됨)는 주로 두 가지를 포함합니다. 설비 자체에서 네트워크 원인으로 반환된 오류 코드와 COS가 반환한 오류 코드입니다.

- 설비 자체가 네트워크 원인으로 생성한 오류 코드는 모두 음수이며 네 자리 숫자입니다(예: -1001). 이러한 오류 코드는 애플에서 정의한 것이며 NSURLError.h 헤더 파일 내의 정의 또는 [애플 공식 웹 사이트 문서 설명](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes)을 참조할 수 있습니다.
- COS가 반환한 오류 코드는 HTTP의 상태 코드에서 나온 것이며 404, 503 유형입니다. 이러한 오류 코드에 대해서 COS 공식 웹 사이트 문서의 [오류 코드 관련 설명](https://cloud.tencent.com/document/product/436/7730)에서 해결 방안을 찾아볼 수 있습니다.

### 객체 meta 정보 획득

#### 방식 프로토타입

파일 조작을 진행하기 전에 헤더 파일 QCloudCOSXML/QCloudCOSXML.h를 가져오기 해야 합니다. 그 전에 앞에 설명한 STEP-1 초기화 조작을 완료해야 합니다. QCloudHeadObjectRequest 인스턴스를 생성한 후 필요한 예외적 제한 조건을 입력하고 내용을 획득합니다. 구체적인 단계는 다음과 같습니다.    

1. QCloudHeadObjectRequest를 인스턴스화하고, 필요한 매개변수를 입력합니다.    
2. QCloudCOSXMLService 객체의 HeadObject 방법을 호출하여 요청을 합니다.    
3. 콜백된 finishBlock에서 구체적인 내용을 획득합니다.   

#### QCloudHeadObjectRequest 매개변수 설명

| 매개변수 이름        | 설명                                                         | 유형       | 필수 |
| --------------- | ------------------------------------------------------------ | ---------- | ---- |
| Object          | 객체 키(Key)는 버킷에서 객체의 유일한 표시입니다. 예를 들어, 객체의 접근 도메인 이름 bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg 중, 객체 키는 doc1/pic1.jpg입니다. 자세한 설명은 [객체 설명](https://cloud.tencent.com/document/product/436/13324) | NSString * | 예   |
| bucket          | 버킷 이름, [COS V5 콘솔](https://console.cloud.tencent.com/cos5/bucket)에서 볼 수 있으며, 형식은 &lt;bucketName&gt;-&lt;APPID&gt;입니다. 예: testBucket-1253653367 | NSString * | 예   |
| ifModifiedSince | 파일 수정 시간이 지정한 시간보다 늦으면 파일 내용을 반환합니다. 그렇지 않으면 304(not modified)를 반환합니다 | NSString * | 예   |

#### 예시

```objective-c
QCloudHeadObjectRequest* headerRequest = [QCloudHeadObjectRequest new];
headerRequest.object = @“객체 이름”;
headerRequest.bucket = @"testBucket-123456789";

   __block id resultError;
[headerRequest setFinishBlock:^(NSDictionary* result, NSError *error) {
      resultError = error;
}];
[[QCloudCOSXMLService defaultCOSXML] HeadObject:headerRequest];

```

#### 오류 코드 반환 설명

SDK 요청에 실패하면 반환된 error는 비어 있지 않으며, 개발자가 문제를 신속하게 해결할 수 있도록 오류 코드, 오류 설명 및 기타 디버깅에 필요한 정보 등이 포함됩니다.

반환된 오류 코드(반환된 error에 캡슐화됨)는 주로 두 가지를 포함합니다. 즉, 설비 자체에서 네트워크 원인으로 반환된 오류 코드와 COS가 반환한 오류 코드입니다.

- 설비 자체가 네트워크 원인으로 생성한 오류 코드는 모두 음수이며 네 자리 숫자입니다(예: -1001). 이러한 오류 코드는 애플에서 정의한 것이며 NSURLError.h 헤더 파일 내의 정의 또는 [애플 공식 웹 사이트 문서 설명](https://developer.apple.com/documentation/foundation/1508628-url_loading_system_error_codes)을 참조할 수 있습니다.
- COS가 반환한 오류 코드는 HTTP의 상태 코드에서 나온 것이며 404, 503 유형입니다. 이러한 오류 코드에 대해서 COS 공식 웹 사이트 문서의 [오류 코드 관련 설명](https://cloud.tencent.com/document/product/436/7730)에서 해결 방안을 찾아볼 수 있습니다.

## 사용자 지정 헤더 추가

추가할 사용자 지정 헤더가 있을 경우, 사용자 지정 헤더를 사용할 수 있습니다. 사용자 지정 헤더 추가를 지원하는 클래스는 customHeaders 속성이 있습니다.

```objective-c
@property (strong, nonatomic) NSMutableDictionary* customHeaders;
```

이 속성 내 모든 키 값 쌍은 대응하는 형식으로 요청을 생성하는 HTTP 헤더에 추가합니다.

## 서버 암호화

업로드 객체를 암호화할 경우, 다음 암호화 방식을 지원합니다

### cos 호스팅 암호화 키의 서버측 암호화(SSE-COS)를 사용하여 데이터 보호합니다

COS는 IDC를 쓸 때 자동으로 암호화하고, 해당 데이터에 접근할 때 자동으로 암호화 해제됩니다. 현재는 COS 마스터키를 사용하여 데이터에 AES-256 암호화를 지원합니다.

iOS SDK는 -(void)setCOSServerSideEncyption 방법을 호출하여 실행됩니다.

```objective-c
[request setCOSServerSideEncyption];
```

### 사용자가 제공한 암호화 키의 서버측 암호화(SSE-C)를 사용하여 데이터를 보호합니다

iOS sdk는 (void)setCOSServerSideEncyptionWithCustomerKey:(NSString *)customerKey 방법을 호출하여 실행됩니다.
  주의:

1. 서버 측을 암호화하려면 HTTPS 요청이 필요하며, “[HTTPS 서비스 시동](#https)”을 참조하십시오.
2. customerKey: 사용자가 제공한 키, 32바이트 문자열을 입력하며, 숫자, 알파벳, 문자열의 조합을 지원하며 중국어를 지원하지 않습니다
3. 업로드된 소스 파일이 해당 방법을 호출할 경우, QCloudCOSXMLDownloadObjectRequest, QCloudHeadObjectRequest, QCloudCOSXMLUploadObjectRequest, QCloudCOSXMLUploadObjectRequest를 사용하여 소스 객체에 대해 조작 시 해당 방법을 호출해야 합니다.

```objective-c
NSString *customKey = @"123456qwertyuioplkjhgfdsazxcvbnm";
[put setCOSServerSideEncyptionWithCustomerKey:customKey];
```

## <span id="https">HTTPS 서비스 시동</span>

iOS SDK는 HTTPS 요청을 지원하며, QCloudServiceConfiguration 구성 객체를 초기화할 때, 해당 endpoint의 useHTTPS를 YES로 설정하면 됩니다

```objective-c
QCloudServiceConfiguration* configuration = [QCloudServiceConfiguration new];
configuration.appID = kAppID;
configuration.signatureProvider = self;
QCloudCOSXMLEndPoint* endpoint = [[QCloudCOSXMLEndPoint alloc] init];
endpoint.regionName = kRegion;
endpoint.useHTTPS = YES;
configuration.endpoint = endpoint;
[QCloudCOSXMLService registerDefaultCOSXMLWithConfiguration:configuration];
[QCloudCOSTransferMangerService registerDefaultCOSTransferMangerWithConfiguration:configuration];
}
```
