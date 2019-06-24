## 개발 준비

### SDK 획득 

- COS 서비스의 iOS SDK 주소: [XML iOS SDK](https://github.com/tencentyun/qcloud-sdk-ios.git).   
- 압축된 Framework 형식의 SDK를 다운로드할 경우 [realease](https://github.com/tencentyun/qcloud-sdk-ios/releases)에서 필요한 버전을 선택하여 다운로드를 진행할 수 있습니다.
- 더 많은 예시는 Demo: [ XML iOS  SDK Demo](https://github.com/tencentyun/qcloud-sdk-ios-samples.git)를 참조하십시오.
- COS XML 버전의 진화는 [XML iOS  SDK  ChangeLog](https://github.com/tencentyun/qcloud-sdk-ios/blob/master/CHANGELOG.md)을 참조하십시오.

### 개발 준비

- SDK는 iOS 8.0 이상 버전의 시스템을 지원합니다.
- 휴대폰에는 네트워크(GPRS, 3G 또는 Wi-Fi 네트워크 등)가 있어야 합니다.
- [COS V5 콘솔](https://console.cloud.tencent.com/cos5)에서 APPID, SecretId, SecretKey를 획득합니다.

> ?문서에서 나오는 SecretId, SecretKey, Bucket 등과 같은 명칭의 함의 및 획득 방법은 [COS 용어집](https://cloud.tencent.com/document/product/436/7751)을 참조하십시오.

### SDK 구성

#### SDK 가져오기

cocoapods를 또는 압축된 동적 라이브러리 다운로드 방식을 통해 SDK를 통합할 수 있습니다. cocoapods 방식으로 가져오기를 진행하는 것을 권장합니다.

- **Cocoapods로 가져오기(추천)**  
  Podfile 파일에서 사용:

```
  pod 'QCloudCOSXML'
```

- **압축된 동적 라이브러리로 가져오기(수동 통합 방식)**  
  **QCloudCOSXML.framework, QCloudCore.framework 및 libmtasdk.a**를 다음 그림과 같이 프로젝트로 드래그하십시오.
  ![](https://main.qcloudimg.com/raw/ce990d8871293daec0aa434f28b152e6.png)  
  그리고 아래 의존 라이브러리를 추가합니다.

> 1. CoreTelephony
> 2. Foundation
> 3. SystemConfiguration
> 4. libc++.tbd

#### 프로젝트 구성

Build Settings에서 Other Linker Flags를 설정하고, 아래 매개변수를 추가합니다.

```shell
-ObjC
-all_load
```

다음 그림과 같습니다.
![매개변수 구성](https://main.qcloudimg.com/raw/2736ab0172191942e41e3268838a1e88.png)

> !
> - Tencent Cloud COS XML iOS의 SDK는 HTTP 프로토콜을 사용합니다. iOS 시스템에서의 실행을 보장하기 위해 HTTP를 통해 전송하기를 허용하도록 설정해야 합니다.
>   다음 두 가지 방식으로 HTTP를 통해 전송을 허용할 수 있습니다.
>  - **수동 설정 방식**
>   프로젝트 info.plist 파일에 App Transport Security Settings 유형을 추가하고, App Transport Security Settings에 Allow Arbitrary Loads 유형 Boolean을 추가하며, 값을 YES로 설정합니다.
>  - **코드 설정 방식**
>   SDK를 통합한 App의 info.plist에 다음과 같은 코드를 추가할 수 있습니다.
> ```
>  <key>NSAppTransportSecurity</key>
> <dict>
> <key>NSExceptionDomains</key>
> <dict>
> 	<key>myqcloud.com</key>
> 	<dict>
> 		<key>NSIncludesSubdomains</key>
> 		<true/>
> 		<key>NSTemporaryExceptionAllowsInsecureHTTPLoads</key>
> 		<true/>
> 	</dict>
> </dict>
> </dict>
> ```
>
> - 동시에 SDK에 Tencent Mobile Analytics(mta) 기능도 가져왔는데 해당 기능을 종료하려면 다음과 같이 설정하십시오.
>  - 헤더 파일 가져오기 ` #import <QCloudCore/MTAConfig.h>`
>  - 기본 cosxml 서비스를 등록한 후, 다음 코드를 추가합니다.
>   `[TACMTAConfig getInstance].statEnable = NO;`

### 초기화  

SDK 기능을 사용하기 전에 몇 가지 필요한 헤더 파일을 가져와 초기화 작업을 실행해야 합니다.
SDK 업로드의 헤더 파일 가져오기:

```objective-c
QCloudCore.h,    
QCloudCOSXML/QCloudCOSXML.h
```

> !
>
> 1. SDK로 작업을 하기 전, 먼저 기본 클라우드 서비스 구성 객체 QCloudServiceConfiguration을 인스턴스화하고, 그다음 QCloudCOSXMLService 및 QCloudCOSTransferManagerService 객체를 인스턴스화해야 합니다.  
> 2. QCloudServiceConfiguration이 변경되면, `registerCOSTransferMangerWithConfiguration:(QCloudServiceConfiguration*)configuration withKey:(NSString*)key`를 통해 새로운 QCloudCOSTransferManagerService를 등록할 수 있습니다. 하지만 기본 QCloudCOSTransferManagerService는 하나만 가능합니다.

#### 방식 프로토타입

QCloudServiceConfiguration 객체 인스턴스화:

```
 QCloudServiceConfiguration* configuration = [QCloudServiceConfiguration new];
 configuration.appID = @""//프로젝트 ID;
```

QCloudCOSXMLService 객체 인스턴스화:

```
+ (QCloudCOSXMLService*) registerDefaultCOSXMLWithConfiguration:(QCloudServiceConfiguration*)configuration;
```

QCloudCOSTransferManagerService 객체 인스턴스화:

```
+ (QCloudCOSTransferMangerService*) registerDefaultCOSTransferMangerWithConfiguration:(QCloudServiceConfiguration*)configuration;
```

#### QCloudServiceConfiguration 매개변수 설명

| 매개변수 이름 | 설명                     | 유형                   | 필수 |
| -------- | ------------------------ | ---------------------- | ---- |
| appID    | 프로젝트 ID, 즉, APPID.      | NSString *             | 아니요   |
| endpoint | endpoint 관련 정보 구성. | QCloudCOSXMLEndPoint * | 예   |

#### QCloudCOSXMLEndPoint 매개변수 설명

| 매개변수 이름 | 설명                     | 유형                   | 필수 |
| ----------- | -------------------------------- | ---------- | ---- |
| regionName  | 서비스가 속한 지역입니다.                 | NSString * | 예   |
| serviceName | 도메인 이름, 기본 설정: myqcloud.com       | NSString * | 아니요   |
| useHTTPS    |  HTTPS 서비스 사용 여부, 기본값은 NO. | BOOL       | 아니요   |
| suffix    | 사용자 지정 http://bucketname.suffix를 지원합니다 | NSString       | 아니요   |


#### 초기화 예시
아래 예시 중 사용된 appID, SecretId, SecretKey 등은 [COS v5 콘솔](https://console.cloud.tencent.com/cos5)에서 획득할 수 있습니다.

```objective-c
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

## 시작 가이드

여기서는 업로드 및 다운로드의 기본 프로세스가 설명되어 있습니다. 자세한 내용은 [XML iOS SDK Demo](https://github.com/tencentyun/qcloud-sdk-ios-samples)를 참조하십시오. API 사용법에 대한 자세한 내용은 Demo에 제공된 유닛 테스트 파일을 참조하십시오.

> !이 단계를 진행하기 전에 반드시 [Tencent Cloud 콘솔](https://console.cloud.tencent.com/cos4/secret)에서 COS 비즈니스의 APPID를 신청해야 합니다.

### 초기화

> !QCloudServiceConfiguration의 signatureProvider 객체는 QCloudSignatureProvider 프로토콜을 구현해야 합니다.

#### 예시 1단계

```objective-c
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

### 예시 2단계

```objective-c
//AppDelegate.m
- (void) signatureWithFields:(QCloudSignatureFields*)fileds
                     request:(QCloudBizHTTPRequest*)request
                  urlRequest:(NSURLRequest*)urlRequst
                   compelete:(QCloudHTTPAuthentationContinueBlock)continueBlock
{
//서명 과정을 구현하려면, 서버 측에서 서명 과정을 구현하는 것을 권장합니다. 자세한 내용은 다음 "서명 생성" 장을 참조하십시오.
}
```

### 파일 업로드

이미 비즈니스 Bucket을 신청했다면, 사실상, SDK의 모든 요청은 해당 Request 유형에 대응됩니다. 대응 요청을 생성하고 해당 속성을 설정한 다음 요청을 QCloudCOSTransferMangerService 객체로 전송하면, 대응 동작이 완료됩니다. 그중, request의 body 부분 가져오기는 업로드한 파일이 로컬 URL에 있어야 합니다(NSURL\* 유형).    

파일을 업로드한 API는 서명을 사용하여 신분 인증을 진행해야 하며, 보낸 요청은 초기화 시 지정한 QCloudSignatureProvider 프로토콜을 준수한 객체에 대해 자동으로 서명을 요청합니다. 서명 생성 방법은 다음 섹션 [서명 생성](#.E7.94.9F.E6.88.90.E7.AD.BE.E5.90.8D)을 참조하십시오.

> !URL에 대응하는 파일은 업로드 과정 중에 변경될 수 없습니다. 그렇지 않으면 오류가 발생합니다.

#### 예시

```objective-c
    QCloudCOSXMLUploadObjectRequest* put = [QCloudCOSXMLUploadObjectRequest new];
    NSURL* url = [NSURL fileURLWithPath:@"filePathString"] /*파일의 URL*/;
    put.object = @"파일명.jpg";
    put.bucket = @"test-123456789";
    put.body =  url;
    [put setSendProcessBlock:^(int64_t bytesSent, int64_t totalBytesSent, int64_t totalBytesExpectedToSend) {
        NSLog(@"upload %lld totalSend %lld aim %lld", bytesSent, totalBytesSent, totalBytesExpectedToSend);
    }];
    [put setFinishBlock:^(id outputObject, NSError* error) {

    }];
    [[QCloudCOSTransferMangerService defaultCOSTransferManager] UploadObject:put];
```

#### QCloudCOSXMLUploadObjectRequest 매개변수 설명

| 매개변수 이름                      | 설명                                                         | 유형                  | 필수 |
| ----------------------------- | ------------------------------------------------------------ | --------------------- | ---- |
| Object                        | 객체 키(Key)는 버킷에서 객체의 유일한 표시입니다. 예를 들어, 객체의 접근 도메인 이름 bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/doc1/pic1.jpg 중, 객체 키는 doc1/pic1.jpg입니다. 자세한 설명은 [객체 설명](https://cloud.tencent.com/document/product/436/13324) | NSString *            | 예   |
| bucket                        | 버킷 이름, [COS V5 콘솔](https://console.cloud.tencent.com/cos5/bucket)에서 볼 수 있으며, 형식은 &lt;bucketName&gt;-&lt;APPID&gt;입니다. 예: testBucket-1253653367 | NSString *            | 예   |
| body                          | 업로드할 파일의 경로. NSURL * 유형 변수 입력                   | BodyType              | 예   |
| storageClass                  | 객체의 스토리지 클래스                                               | QCloudCOSStorageClass | 예   |
| cacheControl                  | RFC 2616에 정의된 캐시 정책                                    | NSString *            | 아니요  |
| contentDisposition            | RFC 2616에 정의된 파일 이름                                    | NSString *            | 아니요   |
| expect                        | expect=@"100-Continue" 사용 시, 서버측의 확인을 받은 후에 요청 내용이 전송됩니다 | NSString *            | 아니요   |
| expires                       | RFC 2616에 정의된 만료 시간                                    | NSString *            | 아니요   |
| initMultipleUploadFinishBlock | 해당 request가 멀티파트 업로드 요청을 생성하는 경우, 멀티파트 업로드 초기화 완료 후 이 block을 통해 콜백 되고, 해당 콜백 block에서 멀티파트 완료 후의 bucket, key, uploadID, 및 후속 업로드 실패 후 업로드 복구에 사용하는 ResumeData를 획득할 수 있습니다 | block                 | 아니요   |
| accessControlList             | Object의 ACL 속성을 정의합니다. 유효값: private, public-read-write, public-read; 기본값: private | NSString *            | 아니요   |
| grantRead         | 피부여자에게 읽기 권한을 부여합니다. 형식: `id=" ",id=" "; 서브 계정에 권한을 부여할 경우, 형식은 id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;SubUin>" 루트 계정에 권한을 부여할 경우, 형식은 id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;OwnerUin>"  그중 OwnerUin은 루트 계정의 ID를 나타내며, SubUin은 서브 계정의 ID를 나타냅니다 | NSString * | 아니요   |
| grantWrite                    | 피부여자에게 쓰기 권한 부여. 형식은 위와 같음                               | NSString *            | 아니요   |
| grantFullControl              | 피부여자에게 읽기/쓰기 권한 부여. 형식은 위와 같음                               | NSString *            | 아니요   |

### 파일 다운로드

#### 예시

```objective-c
  QCloudGetObjectRequest* request = [QCloudGetObjectRequest new];
  //다운로드의 경로 URL 설정, 설정하면 파일이 지정 경로로 파일이 다운로드됩니다
  request.downloadingURL = [NSURL URLWithString:QCloudTempFilePathWithExtension(@"downding")];
  request.object = @“귀하의 Object-Key”;
  request.bucket = @"test-123456789";
  [request setFinishBlock:^(id outputObject, NSError \*error) {
    //additional actions after finishing
}];
[request setDownProcessBlock:^(int64_t bytesDownload, int64_t totalBytesDownload, int64_t totalBytesExpectedToDownload) {
	 //다운로드 과정의 진도
	}];
[[QCloudCOSXMLService defaultCOSXML] GetObject:request];
```

## 서명 생성

SDK 요청에 서명을 사용으로 접근한 사용자의 신분을 확인하고 접근 보안성을 확보합니다. 서명이 정확하지 않을 때는 대부분의 COS 서비스에 접근할 수 없으며 403 오류 코드가 반환됩니다. SDK에서 서명을 생성할 수 있으며, 각 요청은 QCloudServiceConfiguration 객체의 signatureProvider 객체에 서명 생성을 요청합니다. 서명 생성을 담당하는 객체는 처음부터 signatureProvider에게 값을 부여할 수 있습니다. 해당 서명 생성 객체는 QCloudSignatureProvider 프로토콜을 준수해야 하며, 서명 생성 방법을 구현해야 합니다.

```objective-c
- (void) signatureWithFields:(QCloudSignatureFields* )fileds    
                     request:(QCloudBizHTTPRequest* )request    
                  urlRequest:(NSURLRequest* )urlRequst    
                   compelete:(QCloudHTTPAuthentationContinueBlock)continueBlock
```

### CAM 시스템 액세스로 임시 서명 구현(추천)

로컬에서 영구적인 SecretId 및 SecretKey로 서명을 생성하는 API를 제공하지만, 영구적인 SecretId 및 SecretKey를 로컬에 저장하는 것은 매우 위험하며 누출로 인한 불필요한 손실을 초래할 수 있다는 점을 주의하십시오. 따라서 보안성을 위하여 서버 측에서 서명 과정을 구현하는 것을 권장합니다.

>!서버 반환 시간을 서명의 시작 시간으로 하고, 사용자 휴대폰의 로컬 시간과 편차가 너무 커서 서명이 부정확하게 되는 일이 없도록 할 것을 강력히 권장합니다.

자신의 서명 서버 내에서 Tencent Cloud의 CAM(Cloud Access Manager, 접근 관리)에 액세스하여 전체 서명 과정을 구현하는 것을 권장합니다.

![CAM 서명 배포 다이어그램 액세스](http://ericcheung-1253653367.cosgz.myqcloud.com/Logical%20View.png)      

서명 서버를 구축하여 CAM 시스템에 액세스하는 방법은 [모바일 응용 프로그램 직접 전송 사례](/document/product/436/9068)를 참조하십시오.

서명 서버가 CAM 시스템에 액세스한 후 클라이언트가 서명 서버에 서명을 요청하면, 서명 서버는 CAM 시스템에 임시 인증서를 요청하고 이를 클라이언트에 반환합니다. CAM 시스템은 영구적인 SecretId 및 SecretKey를 기반으로 임시 Secret ID, Secret Key 및 임시 Token을 생성하여 서명을 생성하며, 가장 높은 한도의 보안성을 제공합니다. 터미널은 이러한 임시 키의 정보를 수신한 후, QCloudCredential 객체를 생성한 다음, 이 QCloudCredentail 객체를 통해 QCloudAuthentationCreator를 생성하며, 마지막으로 이 Creator를 사용하여 서명 정보를 포함하는 QCloudSignature 객체를 생성합니다. 구체적인 작업은 다음의 예시를 참고하십시오.

```objective-c
- (void) signatureWithFields:(QCloudSignatureFields*)fileds
                     request:(QCloudBizHTTPRequest*)request
                  urlRequest:(NSURLRequest*)urlRequst
                   compelete:(QCloudHTTPAuthentationContinueBlock)continueBlock
{
    /*서명 서버에 임시 Secret ID, Secret Key, Token 요청함*/
    QCloudCredential* credential = [QCloudCredential new];
    credential.secretID = @"CAM 시스템에서 획득한 임시 Secret ID";
    credential.secretKey = @"CAM 시스템에서 획득한 임시 Secret Key";
    credential.token = @"CAM 시스템에서 반환된 Token, 세션 ID임"
    /*서버 반환 시간을 서명의 시작 시간으로 하고, 사용자 휴대폰의 로컬 시간과 편차가 너무 커서 서명이 부정확하게 되는 일이 없도록 할 것을 강력히 권장합니다. */
    credential.startDate = /*반환한 서버 시간*/
    credential.expiretionDate	 = /*서명 만료 시간*/
    QCloudAuthentationV5Creator* creator = [[QCloudAuthentationV5Creator alloc] initWithCredential:credential];
    QCloudSignature* signature =  [creator signatureForData:urlRequst];
    continueBlock(signature, nil);
}

```

### 터미널에서 영구적 키를 사용하여 서명 생성(비추천)

>!터미널에서 영구적 키를 사용하여 서명을 생성하면 데이터 누출의 위험이 있으므로 추천하지 않습니다.

예제 코드는 다음과 같습니다.

```objective-c
- (void) signatureWithFields:(QCloudSignatureFields*)fileds
                     request:(QCloudBizHTTPRequest*)request
                  urlRequest:(NSMutableURLRequest*)urlRequst
                   compelete:(QCloudHTTPAuthentationContinueBlock)continueBlock
{

    QCloudCredential* credential = [QCloudCredential new];
    credential.secretID = @"영구적 SecretID";
    credential.secretKey = @"영구적 SecretKey";
    QCloudAuthentationV5Creator* creator = [[QCloudAuthentationV5Creator alloc] initWithCredential:credential];
    QCloudSignature* signature =  [creator signatureForData:urlRequst];
    continueBlock(signature, nil);
}

```

### 스캐폴딩 도구로 비동기화 서명 관리

이 단계에 오면 서명을 생성하여 SDK 내부의 API를 사용할 수 있습니다. 하지만 임시 서명을 쉽게 구현하기 위해, 스캐폴딩 도구를 제공으로 tempSecretKey 등 임시 서명에 필요한 정보를 서버 측에서 가져올 수 있습니다. 위의 코드에 따라 서명을 생성하거나 스캐폴딩 도구 QCloudCredentailFenceQueue로 임시 서명을 획득할 수 있습니다. QCloudCredentailFenceQueue는 배리어 메커니즘을 제공합니다. 즉, QCloudCredentailFenceQueue로 서명을 획득하면 서명 획득이 필요한 모든 요청은 실행 전에 서명이 완료될 때까지 대기하므로, 비동기화 과정을 직접 관리할 필요가 없습니다.   
QCloudCredentailFenceQueue 사용 시 우선 하나의 인스턴스를 생성해야 합니다.

```objective-c
//AppDelegate.m
//AppDelegate는 QCloudCredentailFenceQueueDelegate 프로토콜을 준수해야 함
//
- (BOOL)application:(UIApplication * )application didFinishLaunchingWithOptions:(NSDictionary * )launchOptions {
    // init step
    self.credentialFenceQueue = [QCloudCredentailFenceQueue new];
    self.credentialFenceQueue.delegate = self;
    return YES;
}
```

다음 QCloudCredentailFenceQueue 클래스의 호출은 QCloudCredentailFenceQueueDelegate를 따라야 하며 프로토콜 내 정의를 구현하는 방법은 아래와 같습니다.

```objective-c
- (void) fenceQueue:(QCloudCredentailFenceQueue * )queue requestCreatorWithContinue:(QCloudCredentailFenceQueueContinue)continueBlock
```

QCloudCredentailFenceQueue로 서명 획득 시 모든 서명이 필요한 SDK의 요청은 모두 해당 프로토콜 정의의 방법 내에서 서명이 필요한 매개변수를 획득하고 유효한 서명을 생성한 후 실행됩니다. 아래 예시를 참조하십시오.

```objective-c
//AppDelegate.m
- (void) fenceQueue:(QCloudCredentailFenceQueue * )queue requestCreatorWithContinue:(QCloudCredentailFenceQueueContinue)continueBlock
{
   QCloudCredential* credential = [QCloudCredential new];
   //여기서 프로세스를 동기화하여 서버에서 임시 서명에 필요한 secretID, secretKey, expirationDate 및 token 매개변수를 획득할 수 있도록 도와줍니다
   credential.secretID = @"****";
   credential.secretKey = @"****";
   /*서버 반환 시간을 서명의 시작 시간으로 하고, 사용자 휴대폰의 로컬 시간과 편차가 너무 커서 서명이 부정확하게 되는 일이 없도록 할 것을 강력히 권장합니다. */ 
   credential.startDate =[NSDate dateWithTimeIntervalSince1970:@"반환한 서버 시간"]
   credential.experationDate = [NSDate dateWithTimeIntervalSince1970:1504183628];
   credential.token = @"****";
   QCloudAuthentationV5Creator* creator = [[QCloudAuthentationV5Creator alloc] initWithCredential:credential];
   continueBlock(creator, nil);
}
- (void) signatureWithFields:(QCloudSignatureFields*)fileds
                     request:(QCloudBizHTTPRequest*)request
                  urlRequest:(NSMutableURLRequest*)urlRequst
                   compelete:(QCloudHTTPAuthentationContinueBlock)continueBlock
{
    [self.credentialFenceQueue performAction:^(QCloudAuthentationCreator *creator, NSError *error) {
        if (error) {
            continueBlock(nil, error);
        } else {
            QCloudSignature* signature =  [creator signatureForData:urlRequst];
            continueBlock(signature, nil);    
        }
    }];
}
```

여기서는 제공된 스캐폴딩 도구를 통해 임시 서명을 생성할 수 있고, 물론 자체적으로 구체적인 서명 과정을 구현할 수도 있습니다.

## 라이트 버전 SDK 사용 가이드

업로드 및 다운로드 기능만 사용하고 SDK 체적에 대한 요구가 비교적으로 높은 사용자의 경우, 업로드 및 다운로드 기능만 있는 라이트 버전 SDK를 제공하며, 통합 후의 패키지 증가량은 정식 버전의 절반에 불과합니다.  

라이트 버전 SDK는 Cocoapods의 Subspec 기능을 통해 구현되므로, 현재는 Cocoapods 통합 방식으로 라이트 버전 SDK를 통합하는 것만 지원합니다. 라이트 버전 SDK를 사용하려면 Podfile에 다음을 추가하면 됩니다.

```
pod 'QCloudCOSXML/Transfer'
```

> !Mobile Line 사용자의 경우, **사용하지 않는** TACStorage의 경우에만 라이트 버전 SDK를 사용할 수 있습니다. 또한, [Cocoapods](https://github.com/CocoaPods/Specs)의 공식 출처가 **모든 출처 앞**(Podfile의 제1행 권장)에 와야 합니다. 기타 사용자는 이 설명을 무시해도 됩니다.

라이트 버전 SDK에는 QCloudCOSXML.h 헤더 파일이 없습니다. 이 헤더 파일을 대체하는 것은 초기화 시 가져오기 해야 하는 다음의 헤더 파일입니다.

```
#import <QCloudCOSXML/QCloudCOSXMLTransfer.h>
#import <QCloudCore/QCloudCore.h>
```

라이트 버전 SDK의 초기화 과정에서 업로드 및 다운로드의 API는 정식 버전 SDK와 일치합니다.

