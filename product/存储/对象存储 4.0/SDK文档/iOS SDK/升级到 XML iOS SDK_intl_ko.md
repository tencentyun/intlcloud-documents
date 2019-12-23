JSON iOS SDK와 비교해 보면 XML SDK의 문서는 간단한 업그레이드가 아님을 아셨을 것입니다. XML iOS SDK는 아키텍처, 가용성 및 안전성 면에서 상당히 향상되었을 뿐만 아니라 사용 편의성, 강력함 그리고 전송 성능에서도 많은 개선을 이루었습니다. XML iOS SDK로 업그레이드하려면 아래 지침에 따라 SDK의 업그레이드 작업을 완료하십시오.

## 기능 비교

다음 표는 JSON SDK 및 XML SDK의 주요 기능 비교입니다.

| 기능           | XML SDK         | JSON SDK                         |
| -------- | :------------: | :------------------:    |
| 파일 업로드 | 로컬 파일, 이진 데이터, 멀티파트 업로드 지원<br>기본으로 업로드 시 덮어쓰기<br>업로드 모드 스마트 결정<br>간편 업로드 최대 5G 지원<br>멀티파트 업로드 최대 48.82TB(50,000GB) 지원 | 로컬 파일 업로드만 지원<br>덮어쓰기 여부 선택 가능<br>간편 업로드 또는 멀티파트 업로드 수동 선택 필요<br>간편 업로드 최대 20MB 지원<br>멀티파트 업로드 최대 64GB 지원 |
| 파일 삭제 | 배치 삭제 지원 | 단일 파일 삭제만 지원 |
| 버킷 기본 조작 | 버킷 생성<br>버킷 획득<br>버킷 삭제   | 지원하지 않음 |
| 버킷 ACL 조작 | 버킷 ACL 설정<br>버킷 ACL 획득<br>버킷 ACL 삭제   | 지원하지 않음 |
| 버킷 수명 주기 | 버킷 수명 주기 생성<br>버킷 수명 주기 획득<br>버킷 수명 주기 삭제 | 지원하지 않음 |
| 디렉터리 조작 | API가 별도로 제공되지 않음   | 디렉터리 생성<br>디렉터리 조회<br>디렉터리 삭제 |

## 업그레이드 절차
아래 5단계에 따라 iOS SDK를 업그레이드하십시오.

**1. iOS SDK 업데이트**
cocoapods를 또는 압축된 동적 라이브러리 다운로드 방식을 통해 SDK를 통합할 수 있습니다. cocoapods 방식으로 가져오기를 진행하는 것을 권장합니다.
- **Cocoapods로 가져오기(추천)**  
Podfile 파일에서 사용:
```
  pod 'QCloudCOSXML'
```

- **압축된 동적 라이브러리로 가져오기(수동 통합 방식)**  
[Release](https://github.com/tencentyun/qcloud-sdk-ios/releases)에서 필요한 버전을 선택하여 다운로드할 수 있습니다.  
**QCloudCOSXML.framework, QCloudCore.framework 및 libmtasdk.a**를 다음 그림과 같이 프로젝트로 드래그하십시오.
![](https://main.qcloudimg.com/raw/14c8f5773ea19bc681b7f862dd6384fb.png)  

	그리고 아래 의존 라이브러리를 추가합니다.
> - CoreTelephony
> - Foundation
> - SystemConfiguration
> - libc++.tbd

**프로젝트 구성**
위의 단계를 완료한 후, Build Settings에서 Other Linker Flags를 설정하고, 아래 매개변수를 추가합니다.
```shell
-ObjC
-all_load
```

다음 그림과 같습니다.
![매개변수 구성](https://main.qcloudimg.com/raw/3bee5d2c3cb7e7f80b94c5f6bbe2ce5e.png)

**2. SDK 인증 방식 변경**

JSON SDK에서는 서명을 백 엔드에서 직접 계산하여 클라이언트에게 반환해야 합니다. XML SDK는 새로운 인증 알고리즘을 사용하므로 백 엔드에 임시 키(STS) 솔루션에 통합할 것을 강력히 권장합니다. 해당 솔루션을 하용하면 서명 계산 과정을 파악할 필요 없이 서버에 CAM을 통합하고 얻은 임시 키를 클라이언트에 반환하고, SDK에 설치하면 되고 SDK가 키를 관리하고 서명을 계산합니다. 임시 키는 일정 기간이 지나면 자동으로 만료되며 영구 키가 누출되지 않습니다.
서로 다른 세분성에 따라 액세스 권한을 제어할 수도 있습니다. 구체적인 절차는 [모바일 응용프로그램 직접 전송 사례](https://cloud.tencent.com/document/product/436/9068) 및 [임시 키 생성 및 사용 가이드](https://cloud.tencent.com/document/product/436/14048)를 참조하십시오.

여전히 백 엔드에서 수동으로 서명을 계산하고 다시 프론트 엔드에 반환하는 방식을 사용하는 경우, 서명 알고리즘에 변화가 생겼다는 점에 유의하십시오. 서명은 더 이상 1회 및 여러 차례 서명을 구분하지 않고 서명의 유효기간 설정을 통해 보안성을 보장합니다. [XML 서명 요청](https://intl.cloud.tencent.com/document/product/436/7778) 파일을 참고하여 서명을 업데이트하십시오.

**3. SDK 초기화 방식 변경**

XML SDK 초기화 API에는 일정 변경 사항이 있습니다.

- `QCloudCOSXMLService`는 `COSClient`를 대체하지만, 두 버전은 같은 효과를 냅니다. 또한 `QCloudServiceConfiguration`을 추가하며 더 많은 정보를 구성합니다.
- 초기화 시 키 제공자 `QCloudAuthentationV5Creator`를 인스턴스화하여, 유효한 키를 제공해야 합니다. 임시 키 사용을 권장합니다.

**JSON SDK의 초기화 방식은 다음과 같습니다:**

```
COSClient *client= [[COSClient alloc] initWithAppId:appId withRegion:@“sh”];
```

**XML SDK의 초기화 방식은 다음과 같습니다:**
>?예제 코드에 나온 것은 임시 키를 사용하여 서명을 획득하는 것입니다. 서버 시간을 반환하여 서명의 시작 시간으로 하고, 사용자 휴대폰의 로컬 시간과 편차가 너무 커서 서명이 부정확하게 되는 일이 없도록 할 것을 강력히 권장합니다.

```
- (void) signatureWithFields:(QCloudSignatureFields*)fileds
                     request:(QCloudBizHTTPRequest*)request
                  urlRequest:(NSURLRequest*)urlRequst
                   compelete:(QCloudHTTPAuthentationContinueBlock)continueBlock
{
  /*서명 서버에 임시 Secret ID, Secret Key, Token 요청합니다*/
   QCloudCredential* credential = [QCloudCredential new];
   credential.secretID = @"CAM 시스템에서 획득한 임시 Secret ID";
   credential.secretKey = @"CAM 시스템에서 획득한 임시 Secret Key";
   credential.token = @"CAM 시스템에서 반환된 Token, 세션 ID임"
   >!서버 반환 시간을 서명의 시작 시간으로 하고, 사용자 휴대폰의 로컬 시간과 편차가 너무 커서 서명이 부정확하게 되는 일이 없도록 할 것을 강력히 권장합니다.
   credential.startDate = /*반환된 서버 시간*/
   credential.expiretionDate	 = /*서명 만료 시간*/
   QCloudAuthentationV5Creator* creator = [[QCloudAuthentationV5Creator alloc] initWithCredential:credential];
   QCloudSignature* signature =  [creator signatureForData:urlRequst];
   continueBlock(signature, nil);

}

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
     QCloudServiceConfiguration* configuration = [QCloudServiceConfiguration new];
     configuration.appID = @"*****";
     configuration.signatureProvider = self;
     QCloudCOSXMLEndPoint* endpoint = [[QCloudCOSXMLEndPoint alloc] init];
     endpoint.regionName = @"ap-beijing";//서비스 지역 이름, 사용 가능한 지역은 주석을 참조하십시오
     configuration.endpoint = endpoint;

     [QCloudCOSXMLService registerDefaultCOSXMLWithConfiguration:configuration];
     [QCloudCOSTransferMangerService registerDefaultCOSTransferMangerWithConfiguration:configuration];

}
```


**4. 버킷 이름 및 가용 영역 약칭 변경**

XML SDK의 버킷 이름과 가용 지역의 약칭은 JSON SDK와 다르므로 상응하는 변경을 진행해야 합니다.


**버킷 Bucket**
XML SDK 버킷 이름은 두 부분으로 구성됩니다. 즉, 사용자 지정 문자열과 APPID의 두 부분이며 둘 사이에 "-"로 연결됩니다. 예를 들어 `exampleobject-1250000000`이라면 그 중 `exampleobject`은 사용자 지정 문자열이고 `1250000000`은 APPID입니다.

>?APPID는 Tencent Cloud 계정의 ID 중 하나이며, 클라우드 리소스 연결에 사용됩니다. 사용자가 Tencent Cloud 계정을 신청하면 시스템은 자동으로 사용자에게 하나의 APPID를 할당합니다. [Tencent Cloud 콘솔](https://console.cloud.tencent.com/)의 [계정 정보]를 통해 APPID를 조회할 수 있습니다.

버킷 구성 시, 다음 예제 코드를 참조하십시오.
```
NSString *bucket = "exampleobject-1250000000";
```

**버킷 가용 영역 약칭 Region**
XML SDK의 버킷 가용 지역 약칭이 변경되었으며, 다음 표에 서로 다른 지역의 JSON SDK 및 XML SDK의 대응 관계가 나와 있습니다.

| 지역       | XML SDK 지역 약칭         | JSON SDK 지역 약칭                         |
| -------- | ------------ | ---------------------------------------- |
| 베이징 1지역(화북) | ap-beijing-1 | tj |
| 베이징       | ap-beijing   | bj |
| 상하이(화동)   | ap-shanghai  | sh |
| 광저우(화남)   | ap-guangzhou | gz |
| 청두(서남)   | ap-chengdu   | cd |
| 충칭       | ap-chongqing | 없음 |
| 싱가포르      | ap-singapore | sgp |
| 홍콩       | ap-hongkong  | hk |
| 토론토      | na-toronto   | ca |
| 프랑크푸르트     | eu-frankfurt | ger |
| 뭄바이       | ap-mumbai    | 없음 |
| 서울       | ap-seoul     | 없음 |
| 실리콘 밸리       | na-siliconvalley     | 없음 |
| 버지니아       | na-ashburn     | 없음 |
| 방콕       | ap-bangkok     | 없음 |
| 모스크바       | eu-moscow     | 없음 |

초기화 시, 버킷이 있는 지역 이름을 `QCloudServiceConfiguration`의 `regionName`에 설정하십시오.

```
//AppDelegate.m

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
     QCloudServiceConfiguration* configuration = [QCloudServiceConfiguration new];
     configuration.appID = @"*****";
     configuration.signatureProvider = self;
     QCloudCOSXMLEndPoint* endpoint = [[QCloudCOSXMLEndPoint alloc] init];
     endpoint.regionName = @"ap-beijing";//서비스 지역 이름, 사용 가능한 지역은 주석을 참조하십시오
     configuration.endpoint = endpoint;

     [QCloudCOSXMLService registerDefaultCOSXMLWithConfiguration:configuration];
     [QCloudCOSTransferMangerService registerDefaultCOSTransferMangerWithConfiguration:configuration];

}
```

**5. API 변경**

XML SDK로 업그레이드한 뒤, 일부 작업의 API가 변경되었습니다. 실제 수요에 따라 그에 맞게 변경하십시오. 동시에 API를 캡슐화하여 SDK 사용 간편성을 높였습니다. 구체적인 내용은 예시와 [API 문서](https://cloud.tencent.com/document/product/436/12258)를 참조하십시오.

API 변경 내용은 다음의 세 가지입니다.

**1)독립적인 디렉터리 API 없음**

XML SDK에서는 별도의 디렉토리 API를 더 이상 제공하지 않습니다. COS에 폴더와 디렉터리라는 게 없으며 COS는 객체 project/a.txt가 업로드되기 때문에 project 폴더를 생성하지 않습니다. 사용자의 사용 습관을 충족시키기 위해 COS는 콘솔이나 COS browser와 같은 그래픽 도구에 [폴더] 또는 [디렉터리] 표시 방식을 시뮬레이션합니다. 이는 키 값이 project/이고 내용이 비어 있는 객체를 생성하여 구현하며, 표시 방식은 기존 폴더와 유사합니다.

예: 객체 project/doc/a.txt를 업로드합니다. 구분 문자 /는 [폴더]의 디스플레이 방식을 시뮬레이션하게 되기 때문에 콘솔에 [폴더] project와 doc가 나타나게 됩니다. 그 중 doc는 project의 하위 [폴더]이며 a.txt 파일을 포함합니다.

따라서 단지 파일 업로드 시나리오의 경우, 바로 업로드하면 되며, 먼저 폴더를 생성할 필요가 없습니다.

적용 시나리오에 폴더의 개념이 있으면 폴더를 생성하는 기능을 제공해야 합니다. 경로가 '/'로 끝나는 0KB 파일 하나를 업로드하면 됩니다. 그러면 `GetBucket` API를 사용했을 때 해당 파일을 폴더로 할 수 있습니다.


**2)QCloudCOSTransferMangerService**

XML SDK에서는 간편 업로드(복사) 또는 멀티파트 업로드(복사)를 지능적으로 선택하는 작업이 캡슐화되어 있으며, 이를 `QCloudCOSTransferMangerService`라고 명명하였습니다. 또한 API 디자인 및 전송 성능을 모두 최적화하였으므로 직접 사용할 것을 권장합니다. `QCloudCOSTransferMangerService`의 주요 특성은 다음과 같습니다.

* 중단점 업로드 재개를 지원합니다.
* 파일 크기에 따라 간편 업로드(복사) 또는 멀티파트 업로드(복사)를 지능적으로 선택할 수 있습니다.

`QCloudCOSTransferMangerService`를 사용하여 업로드된 예제 코드:

```
  QCloudCOSXMLUploadObjectRequest* put = [QCloudCOSXMLUploadObjectRequest new];
  NSURL* url = /*파일의 URL*/;
  put.object = @"파일명.jpg";
  put.bucket = @"exampleobject-1250000000";
  put.body =  url;
  [put setSendProcessBlock:^(int64_t bytesSent, int64_t totalBytesSent, int64_t totalBytesExpectedToSend) {
      NSLog(@"upload %lld totalSend %lld aim %lld", bytesSent, totalBytesSent, totalBytesExpectedToSend);
  }];
  [put setFinishBlock:^(id outputObject, NSError* error) {

  }];
  [[QCloudCOSTransferMangerService defaultCOSTransferManager] UploadObject:put];

```
`QCloudCOSTransferMangerService`를 사용하여 파일 업로드 시 중단점 업로드 재개 예제 코드:

```
QCloudCOSXMLUploadObjectRequest* put = [QCloudCOSXMLUploadObjectRequest new];
  //•••일부 업로드 매개변수 설정
  put.initMultipleUploadFinishBlock = ^(QCloudInitiateMultipartUploadResult * multipleUploadInitResult, QCloudCOSXMLUploadObjectResumeData resumeData) {
	//초기화 멀티파트 업로드가 완료된 후 이 block이 콜백되고, 여기서 resumeData를 획득할 수 있으며 resumeData를 통해 멀티파트 업로드 요청을 생성할 수 있습니다.
	 QCloudCOSXMLUploadObjectRequest* request = [QCloudCOSXMLUploadObjectRequest requestWithRequestData:resumeData];
  };

  [[QCloudCOSTransferMangerService defaultCOSTransferManager] UploadObject:put];
  //•••초기화를 완료하고, 업로드는 완성되기 전
  NSError* error;
  //여기서 직접 취소를 호출하고, resumetData의 예시를 생성할 수 있습니다
  resumeData = [put cancelByProductingResumeData:&error];
  if (resumeData) {
    QCloudCOSXMLUploadObjectRequest* request = [QCloudCOSXMLUploadObjectRequest requestWithRequestData:resumeData];
  }
  //생성된 업로드 복구에 사용할 요청은 직접 업로드할 수 있습니다
  [[QCloudCOSTransferMangerService defaultCOSTransferManager] UploadObject:request];

```
>!멀티파트 업로드의 작동 원리에 따르면 멀티파트 업로드가 완료되면 백 엔드 서버가 해당 멀티파트를 기록하고 진행률을 누적합니다. 또한 다음의 몇 가지 상황에는 중단점 재개를 진행할 수 없고, 그 대신 업로드 프로세스를 다시 시작합니다.
 - 업로드된 파일이 1M 미만이고, 멀티파트 업로드가 수행되지 않습니다.
 - QCloudCOSXMLUploadObjectRequest를 사용하여 업로드를 진행하지 않고, 직접 간편 업로드 API를 사용합니다.
 - resumeData 생성 취소 시 멀티파트 업로드 초기화가 아직 완료되지 않았습니다(업로드 초기화 완료의 콜백이 아직 호출되지 않음).

**3) API 새로 추가**

XML SDK가 많은 API를 새로 추가하여 필요에 따라 호출할 수 있습니다. 다음을 포함합니다.
* 버킷 작업, QCloudPutBucketRequest, QCloudGetBucketRequest, QCloudListBucketRequest 등.
* 버킷 ACL의 작업, QCloudPutBucketACLRequest, QCloudGetBucketACLRequest 등.
* 버킷의 수명 주기 조작, PQCloudutBucketLifecycleRequest, QCloudGetBucketLifecycleRequest 등.

자세한 내용은 [iOS SDK API 문서](https://cloud.tencent.com/document/product/436/12258)를 참조하십시오.
