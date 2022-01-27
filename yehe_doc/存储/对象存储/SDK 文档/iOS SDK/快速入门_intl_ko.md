## 관련 리소스

- SDK 소스 코드 주소는 [XML iOS SDK](https://github.com/tencentyun/qcloud-sdk-ios.git)를 참고하십시오.
- 예시 Demo는 [XML iOS SDK Demo](https://github.com/tencentyun/qcloud-sdk-ios-samples.git)를 참고하십시오.
- SDK 인터페이스와 매개변수 문서는 [SDK API 참고](https://cos-ios-sdk-doc-1253960454.file.myqcloud.com)를 참고하십시오.
- SDK 문서의 모든 예시 코드는 [SDK 코드 예시](https://github.com/tencentyun/cos-snippets/tree/master/iOS)를 참고하십시오.
- SDK 로그 업데이트는 [ChangeLog](https://github.com/tencentyun/qcloud-sdk-ios/blob/master/CHANGELOG.md)를 참고하십시오.
- SDK FAQ는 [iOS SDK FAQ](https://intl.cloud.tencent.com/document/product/436/38957)를 참고하십시오.

>? XML 버전 SDK 사용 중 함수 또는 메소드가 존재하지 않는 등의 오류 발생 시, XML 버전 SDK를 최신 버전으로 업그레이드한 후 재시도하십시오.
>

## 준비 작업

1. iOS 애플리케이션이 필요합니다. 기존의 프로젝트 또는 새로 생성한 프로젝트 모두 가능합니다.
2. 애플리케이션이 iOS 8.0 이상인 버전의 SDK를 기반으로 구축되었는지 확인합니다.
3. Tencent Cloud 임시 키를 받을 수 있는 원격 주소가 필요합니다. 임시 키에 관한 설명은 [모바일 애플리케이션 다이렉트 업로드 사례](https://intl.cloud.tencent.com/document/product/436/30618)를 참고하십시오.

## 1단계: SDK 설치

### 방법 1: Cocoapods로 통합(권장)

#### 표준 버전 SDK

프로젝트의 `Podfile` 파일에서 다음을 사용하십시오.

```shell
pod 'QCloudCOSXML'
```
#### 라이트 버전 SDK

업로드/다운로드 기능만 사용하고 대용량의 SDK가 필요한 경우 Tencent Cloud의 라이트 버전 SDK를 사용할 수 있습니다.

라이트 버전 SDK는 Cocoapods의 Subspec 기능을 통해 실현되기 때문에 현재 자동 통합만 지원됩니다. 프로젝트의 `Podfile` 파일에서 다음을 사용하십시오.

```shell
pod 'QCloudCOSXML/Transfer'
```

### 방법2: 수동 통합

정식 패키지의 최신 버전은 [퀵 다운로드 주소](https://cos-sdk-archive-1253960454.file.myqcloud.com/qcloud-sdk-ios/latest/qcloud-sdk-ios.zip)에서 다운로드할 수 있으며, 이전 버전은 [SDK Releases](https://github.com/tencentyun/qcloud-sdk-ios/releases)에서 찾을 수 있습니다.

#### 1. 바이너리 라이브러리 가져오기

**QCloudCOSXML.framework, QCloudCore.framework, BeaconAPI_Base.framework, QimeiSDK.framework**를 프로젝트로 끌어옵니다.

![](https://qcloudimg.tencent-cloud.cn/raw/a461545c9de56424126943fc16a3d381.png)  

다음의 종속 라이브러리를 추가합니다.
 - CoreTelephony
 - Foundation
 - SystemConfiguration
 - libc++.tbd

#### 2. 프로젝트 설정

Build Settings에서 Other Linker Flags를 설정하고 다음과 같은 매개변수를 추가합니다.

```shell
-ObjC
-all_load
```

![](https://main.qcloudimg.com/raw/125218fad3f4781cae8f992d9a152057.png)


>? SDK는 비즈니스 니즈에 따라 자체 패키징되는 패키징 스크립트를 제공합니다(패키징 스크립트는 cocoapods에 따라 다르므로 Cocoapods가 개발 환경에 설치되어 있는지 확인하십시오). 패키징 방법은 다음과 같습니다.
> 1. 소스 코드 `git clone https://github.com/tencentyun/qcloud-sdk-ios`를 다운로드 합니다.
> 2. 패키징 스크립트 `source package.sh`를 실행합니다.
> 3. 패키징 산출물을 프로젝트로 드래그한 후 위의 수동 통합 방법에 따라 작업합니다.
>  - iOS: ios 폴더의 제품을 프로젝트로 드래그합니다.
>  - macOS: osx 폴더의 제품을 프로젝트로 드래그합니다.
![](https://main.qcloudimg.com/raw/631ae93aab3955149e5d0d8023eeac1b.png)


## 2단계: 사용하기

### 1. 헤더 파일 가져오기

**Objective-c**

```objective-c
#import <QCloudCOSXML/QCloudCOSXML.h>
```

**swift**

```swift
import QCloudCOSXML
```

라이트 버전 SDK에는 다음 파일을 가져옵니다.

**Objective-c**

```objective-c
#import <QCloudCOSXML/QCloudCOSXMLTransfer.h>
```

**swift**

```swift
import QCloudCOSXMLTransfer
```

### 2. COS 서비스 초기화 및 서명 프로토콜 구현

#### 방법 1: 임시 키 쌍 요청 라이선스 획득(권장)

SDK가 요청을 보낼 때 서명을 계산하기 위해 임시 키를 얻어야 하므로 `QCloudSignatureProvider` 프로토콜을 구현해야 합니다. 프로토콜에서 키를 얻은 후 매개변수`continueBlock`을 통해 키를 SDK에 콜백합니다.

초기화 프로세스를 `AppDelegate` 또는 **프로그램 싱글톤**에 두는 것을 권장합니다.

구체적인 절차는 아래의 전체 샘플 코드를 참고하십시오.

**Objective-c**

```objective-c
//AppDelegate.m
//AppDelegate 는 QCloudSignatureProvider를 따라야 합니다. 
@interface AppDelegate()<QCloudSignatureProvider>
@end

@implementation AppDelegate

- (BOOL)application:(UIApplication * )application 
        didFinishLaunchingWithOptions:(NSDictionary * )launchOptions {

    QCloudServiceConfiguration* configuration = [QCloudServiceConfiguration new];
    QCloudCOSXMLEndPoint* endpoint = [[QCloudCOSXMLEndPoint alloc] init];
    
    // 사용자의 region으로 대체합니다. 생성된 버킷이 속한 region은 콘솔에서 확인 가능합니다. https://console.cloud.tencent.com/cos5/bucket
    // COS에서 지원되는 모든 region 목록은 다음을 참고하십시오. https://www.qcloud.com/document/product/436/6224
    endpoint.regionName = @"COS_REGION";
    // HTTPS 사용
    endpoint.useHTTPS = true;
    configuration.endpoint = endpoint;
    // 키 제공자: 호스트
    configuration.signatureProvider = self;
    // COS 서비스 초기화 예시
    [QCloudCOSXMLService registerDefaultCOSXMLWithConfiguration:configuration];
    [QCloudCOSTransferMangerService registerDefaultCOSTransferMangerWithConfiguration:
        configuration];
    return YES;
}


// 서명을 얻는 메소드 게이트입니다. 임시 키를 얻고 서명을 계산하는 과정을 보여줍니다.
// 서명 계산 과정을 사용자 정의할 수 있습니다.
- (void) signatureWithFields:(QCloudSignatureFields*)fileds
                     request:(QCloudBizHTTPRequest*)request
                  urlRequest:(NSMutableURLRequest*)urlRequst
                   compelete:(QCloudHTTPAuthentationContinueBlock)continueBlock
{
        //백그라운드 서버에서 가져온 임시 키를 여기에서 동기화합니다. 임시 키의 가용성을 최대한 보장하기 위해 임시 키를 가져오는 로직은 이곳에 배치하는 것을 강력히 권장합니다.
    //...
    QCloudCredential* credential = [QCloudCredential new];

    // 임시 키 SecretId 
    // sercret_id를 사용자의 SecretId로 대체합니다. CAM 콘솔에 로그인하여 키를 확인하십시오. https://console.cloud.tencent.com/cam/capi
    credential.secretID = @"SECRETID";
    // 임시 키 SecretKey
    // sercret_key를 사용자의 SecretKey로 대체합니다. CAM 콘솔에 로그인하여 키를 확인하십시오. https://console.cloud.tencent.com/cam/capi
    credential.secretKey = @"SECRETKEY";
    // 임시 키 Token
    // 영구 키를 사용하는 경우 token을 입력할 필요가 없으나, 임시 키를 사용하는 경우 입력해야 합니다. 임시 키 생성 및 사용 가이드는 다음을 참고하십시오. https://cloud.tencent.com/document/product/436/14048
    credential.token = @"TOKEN";
    /** 휴대폰 로컬 시간과의 편차가 너무 커서 서명이 부정확해지지 않도록 서버 시간을 서명 시작 시간으로 반환할 것을 권장합니다(매개변수 startTime과 expiredTime의 단위: 초).
    */
    credential.startDate = [NSDate dateWithTimeIntervalSince1970:startTime]; // 단위: 초
    credential.expirationDate = [NSDate dateWithTimeIntervalSince1970:expiredTime]];// 단위: 초
  
    QCloudAuthentationV5Creator* creator = [[QCloudAuthentationV5Creator alloc]
        initWithCredential:credential];
    QCloudSignature *signature = [creator signatureForData:urlRequst];
    continueBlock(signature, nil);
}


@end
```

**Swift**

```swift
//AppDelegate.swift
//AppDelegate 는 QCloudSignatureProvider를 따라야 합니다. 

class AppDelegate: UIResponder, UIApplicationDelegate,
    QCloudSignatureProvider {

    func application(_ application: UIApplication, 
        didFinishLaunchingWithOptions launchOptions: 
        [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
        let config = QCloudServiceConfiguration.init();

        let endpoint = QCloudCOSXMLEndPoint.init();

        // 사용자의 region으로 대체합니다. 생성된 버킷이 속한 region은 콘솔에서 확인 가능합니다. https://console.cloud.tencent.com/cos5/bucket
        // COS에서 지원되는 모든 region 목록은 다음을 참고하십시오. https://www.qcloud.com/document/product/436/6224
        endpoint.regionName = "COS_REGION";
        // HTTPS 사용
        endpoint.useHTTPS = true;
        config.endpoint = endpoint;
        // 키 제공자: 호스트
        config.signatureProvider = self;

        // COS 서비스 초기화 예시
        QCloudCOSXMLService.registerDefaultCOSXML(with: config);
        QCloudCOSTransferMangerService.registerDefaultCOSTransferManger(
            with: config);
        return true
    }


    // 서명을 얻는 메소드 게이트입니다. 임시 키를 얻고 서명을 계산하는 과정을 보여줍니다.
    // 서명 계산 과정을 사용자 정의할 수 있습니다.
    func signature(with fileds: QCloudSignatureFields!, 
        request: QCloudBizHTTPRequest!, 
        urlRequest urlRequst: NSMutableURLRequest!, 
        compelete continueBlock: QCloudHTTPAuthentationContinueBlock!) {
        
                //여기서 동기화하여 백그라운드 서버에서 임시 키를 획득합니다.
        //...

        let credential = QCloudCredential.init();
        // 임시 키 SecretId 
        // sercret_id를 사용자의 SecretId로 대체합니다. CAM 콘솔에 로그인하여 키를 확인하십시오. https://console.cloud.tencent.com/cam/capi
        credential.secretID = "SECRETID";
        // 임시 키 SecretKey
        // sercret_key를 사용자의 SecretKey로 대체합니다. CAM 콘솔에 로그인하여 키를 확인하십시오. https://console.cloud.tencent.com/cam/capi
        credential.secretKey = "SECRETKEY";
        // 임시 키 Token
        // 영구 키를 사용하는 경우 token을 입력할 필요가 없으나, 임시 키를 사용하는 경우 입력해야 합니다. 임시 키 생성 및 사용 가이드는 다음을 참고하십시오. https://cloud.tencent.com/document/product/436/14048
        credential.token = "TOKEN";
        /** 휴대폰 로컬 시간과의 편차가 너무 커서 서명이 부정확해지지 않도록 서버 시간을 서명 시작 시간으로 반환할 것을 권장합니다(매개변수 startTime과 expiredTime의 단위: 초).
        */
        credential.startDate = Date.init(timeIntervalSince1970: TimeInterval(startTime)!) DateFormatter().date(from: "startTime");
        credential.expirationDate = Date.init(timeIntervalSince1970: TimeInterval(expiredTime)!) 

        let creator = QCloudAuthentationV5Creator.init(credential: credential);
        let signature = creator?.signature(forData: urlRequst);
        continueBlock(signature,nil);
        
    }
}
```

>! 
>- APPID는 Tencent Cloud 계정 신청 후 획득하게 되는 계정으로 시스템에서 자동으로 할당합니다. 변경 불가능한 고유 ID로, [계정 정보](https://console.cloud.tencent.com/developer)에서 확인할 수 있습니다. Tencent Cloud 계정 APPID는 계정 ID와 유일한 상관 관계를 갖는 애플리케이션 ID입니다.
>- SecretId와 SecretKey를 통칭하여 Cloud API 키라고 부르며, 사용자가 Tencent Cloud API에 액세스 시 인증할 때 사용하는 보안 자격 증명으로 [API 키 관리](https://console.cloud.tencent.com/cam/capi)에서 획득할 수 있습니다. SecretKey는 서명 문자열 및 서버 인증 서명 문자열 키를 암호화하는 데 사용되며, SecretId는 API 호출자의 ID를 식별하는 데 사용됩니다. APPID별로 여러 개의 Cloud API 키를 생성할 수 있습니다.
>

SDK는 임시 키의 캐시 및 재사용을 실현하기 위해 `QCloudCredentailFenceQueue`의 스캐폴드를 제공합니다. 키가 만료된 후 스캐폴드는 키 만료 시간이 디바이스의 현재 시간보다 클 때까지 새 키를 얻기 위해 프로토콜을 다시 호출합니다.

>! 스캐폴드는 키의 만료 시간이 기기의 현재 시간보다 긴지 여부에 따라 키 재사용 가능 여부만을 판단하며, 키 신청 시 복잡한 정책을 설정할 경우 스캐폴드 툴을 사용하지 않는 것을 권장합니다.

초기화 프로세스를 `AppDelegate` 또는 **프로그램 싱글톤**에 두는 것을 권장합니다. 스캐폴딩을 사용하려면 다음 두 가지 프로토콜을 구현해야 합니다.

- QCloudSignatureProvider
- QCloudCredentailFenceQueueDelegate


전체 샘플 코드는 다음을 참고하십시오.


**Objective-c**

```objective-c
//AppDelegate.m
//AppDelegate는 QCloudSignatureProvider와 
//QCloudCredentailFenceQueueDelegate 프로토콜을 따라야 합니다.

@interface AppDelegate()<QCloudSignatureProvider, QCloudCredentailFenceQueueDelegate>

// 스캐폴드 인스턴스
@property (nonatomic) QCloudCredentailFenceQueue* credentialFenceQueue;

@end

@implementation AppDelegate

- (BOOL)application:(UIApplication * )application 
        didFinishLaunchingWithOptions:(NSDictionary * )launchOptions {
    QCloudServiceConfiguration* configuration = [QCloudServiceConfiguration new];
    QCloudCOSXMLEndPoint* endpoint = [[QCloudCOSXMLEndPoint alloc] init];

    // 사용자의 region으로 대체합니다. 생성된 버킷이 속한 region은 콘솔에서 확인 가능합니다. https://console.cloud.tencent.com/cos5/bucket
    // COS에서 지원되는 모든 region 목록은 다음을 참고하십시오. https://www.qcloud.com/document/product/436/6224
    endpoint.regionName = @"COS_REGION";
    // HTTPS 사용
    endpoint.useHTTPS = true;
    configuration.endpoint = endpoint;
    // 키 제공자: 호스트
    configuration.signatureProvider = self;
    // COS 서비스 초기화 예시
    [QCloudCOSXMLService registerDefaultCOSXMLWithConfiguration:configuration];
    [QCloudCOSTransferMangerService registerDefaultCOSTransferMangerWithConfiguration:
        configuration];

    // 임시 키 스캐폴드 초기화
    self.credentialFenceQueue = [QCloudCredentailFenceQueue new];
    self.credentialFenceQueue.delegate = self;

    return YES;
}

- (void) fenceQueue:(QCloudCredentailFenceQueue * )queue requestCreatorWithContinue:(QCloudCredentailFenceQueueContinue)continueBlock
{
    //백그라운드 서버에서 가져온 임시 키를 여기에서 동기화합니다. 임시 키의 가용성을 최대한 보장하기 위해 임시 키를 가져오는 로직은 이곳에 배치하는 것을 강력히 권장합니다.
    //...

    QCloudCredential* credential = [QCloudCredential new];
    // 임시 키 SecretId 
    // sercret_id를 사용자의 SecretId로 대체합니다. CAM 콘솔에 로그인하여 키를 확인하십시오. https://console.cloud.tencent.com/cam/capi
    credential.secretID = @"SECRETID";
    // 임시 키 SecretKey
    // sercret_key를 사용자의 SecretKey로 대체합니다. CAM 콘솔에 로그인하여 키를 확인하십시오. https://console.cloud.tencent.com/cam/capi
    credential.secretKey = @"SECRETKEY";
    // 임시 키 Token
    // 영구 키를 사용하는 경우 token을 입력할 필요가 없으나, 임시 키를 사용하는 경우 입력해야 합니다. 임시 키 생성 및 사용 가이드는 다음을 참고하십시오. https://cloud.tencent.com/document/product/436/14048
    credential.token = @"TOKEN";
    /** 휴대폰 로컬 시간과의 편차가 너무 커서 서명이 부정확해지지 않도록 서버 시간을 서명 시작 시간으로 반환할 것을 권장합니다(매개변수 startTime과 expiredTime의 단위: 초).
    */
    credential.startDate = [NSDate dateWithTimeIntervalSince1970:startTime]; // 단위: 초
    credential.expirationDate = [NSDate dateWithTimeIntervalSince1970:expiredTime]];// 단위: 초

    QCloudAuthentationV5Creator* creator = [[QCloudAuthentationV5Creator alloc]
        initWithCredential:credential];
    continueBlock(creator, nil);
}

// 서명을 얻는 메소드 게이트입니다. 임시 키를 얻고 서명을 계산하는 과정을 보여줍니다.
// 서명 계산 과정을 사용자 정의할 수 있습니다.
- (void) signatureWithFields:(QCloudSignatureFields*)fileds
                     request:(QCloudBizHTTPRequest*)request
                  urlRequest:(NSMutableURLRequest*)urlRequst
                   compelete:(QCloudHTTPAuthentationContinueBlock)continueBlock
{
    [self.credentialFenceQueue performAction:^(QCloudAuthentationCreator *creator, 
        NSError *error) {
        if (error) {
            continueBlock(nil, error);
        } else {
            QCloudSignature* signature =  [creator signatureForData:urlRequst];
            continueBlock(signature, nil);
        }
    }];
}


@end
```

**Swift**

```swift
//AppDelegate.swift
//AppDelegate는 QCloudSignatureProvider와 
//QCloudCredentailFenceQueueDelegate 프로토콜을 따라야 합니다.

class AppDelegate: UIResponder, UIApplicationDelegate,
    QCloudSignatureProvider, QCloudCredentailFenceQueueDelegate {

    var credentialFenceQueue:QCloudCredentailFenceQueue?;

    func application(_ application: UIApplication, 
        didFinishLaunchingWithOptions launchOptions: 
        [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
        let config = QCloudServiceConfiguration.init();

        let endpoint = QCloudCOSXMLEndPoint.init();

        // 사용자의 region으로 대체합니다. 생성된 버킷이 속한 region은 콘솔에서 확인 가능합니다. https://console.cloud.tencent.com/cos5/bucket
        // COS에서 지원되는 모든 region 목록은 다음을 참고하십시오. https://www.qcloud.com/document/product/436/6224
        endpoint.regionName = "COS_REGION";
        // HTTPS 사용
        endpoint.useHTTPS = true;
        config.endpoint = endpoint;
        // 키 제공자: 호스트
        config.signatureProvider = self;

        // COS 서비스 초기화 예시
        QCloudCOSXMLService.registerDefaultCOSXML(with: config);
        QCloudCOSTransferMangerService.registerDefaultCOSTransferManger(
            with: config);

        // 임시 키 스캐폴드 초기화
        self.credentialFenceQueue = QCloudCredentailFenceQueue.init();
        self.credentialFenceQueue?.delegate = self;

        return true
    }

    func fenceQueue(_ queue: QCloudCredentailFenceQueue!, 
        requestCreatorWithContinue continueBlock: 
        QCloudCredentailFenceQueueContinue!) {
        //여기서 동기화하여 백그라운드 서버에서 임시 키를 획득합니다.
        //...

        let credential = QCloudCredential.init();
        // 임시 키 SecretId 
        // sercret_id를 사용자의 SecretId로 대체합니다. CAM 콘솔에 로그인하여 키를 확인하십시오. https://console.cloud.tencent.com/cam/capi
        credential.secretID = "SECRETID";
        // 임시 키 SecretKey
        // sercret_key를 사용자의 SecretKey로 대체합니다. CAM 콘솔에 로그인하여 키를 확인하십시오. https://console.cloud.tencent.com/cam/capi
        credential.secretKey = "SECRETKEY";
        // 임시 키 Token
        // 영구 키를 사용하는 경우 token을 입력할 필요가 없으나, 임시 키를 사용하는 경우 입력해야 합니다. 임시 키 생성 및 사용 가이드는 다음을 참고하십시오. https://cloud.tencent.com/document/product/436/14048
        credential.token = "TOKEN";
        /** 휴대폰 로컬 시간과의 편차가 너무 커서 서명이 부정확해지지 않도록 서버 시간을 서명 시작 시간으로 반환할 것을 권장합니다(매개변수 startTime과 expiredTime의 단위: 초).
        */
        credential.startDate = Date.init(timeIntervalSince1970: TimeInterval(startTime)!) DateFormatter().date(from: "startTime");
        credential.expirationDate = Date.init(timeIntervalSince1970: TimeInterval(expiredTime)!) 

        let auth = QCloudAuthentationV5Creator.init(credential: credential);
        continueBlock(auth,nil);
    }

    // 서명을 얻는 메소드 게이트입니다. 임시 키를 얻고 서명을 계산하는 과정을 보여줍니다.
    // 서명 계산 과정을 사용자 정의할 수 있습니다.
    func signature(with fileds: QCloudSignatureFields!, 
        request: QCloudBizHTTPRequest!, 
        urlRequest urlRequst: NSMutableURLRequest!, 
        compelete continueBlock: QCloudHTTPAuthentationContinueBlock!) {
        self.credentialFenceQueue?.performAction({ (creator, error) in
            if error != nil {
                continueBlock(nil,error!);
            }else{
                let signature = creator?.signature(forData: urlRequst);
                continueBlock(signature,nil);
            }
        })
    }
}
```

>!
> - 버킷의 각 리전에 대한 약칭은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참고하십시오.
> - HTTPS를 통한 데이터 요청을 권장합니다. HTTP 프로토콜을 사용할 경우 iOS 9.0 이상의 시스템에서 실행할 수 있도록 애플리케이션을 위해  HTTP 전송 허용을 활성화해야 합니다. 자세한 가이드는 Apple 공식 홈페이지의 설명 문서 [Preventing Insecure Network Connections](https://developer.apple.com/documentation/security/preventing_insecure_network_connections)를 참고하십시오.
> 


`QCloudServiceConfiguration`이 변경된 경우, 아래 방법을 통해 새로운 인스턴스를 등록할 수 있습니다.

```objective-c
+ (QCloudCOSTransferMangerService*) registerCOSTransferMangerWithConfiguration:(QCloudServiceConfig

```
#### 방법 2: 영구 키로 로컬 디버깅 진행

Tencent Cloud의 영구 키로 개발 단계에 있는 로컬 디버깅을 진행할 수 있습니다. **해당 방법은 키가 유출될 리스크가 있으니 런칭 전 반드시 임시 키로 대체하십시오.**

영구 키를 사용하면 `QCloudCredentailFenceQueueDelegate` 프로토콜을 실행하지 않아도 됩니다.

**Objective-C**

```objective-c
- (void) signatureWithFields:(QCloudSignatureFields*)fileds
                     request:(QCloudBizHTTPRequest*)request
                  urlRequest:(NSMutableURLRequest*)urlRequst
                   compelete:(QCloudHTTPAuthentationContinueBlock)continueBlock
{
    
    QCloudCredential* credential = [QCloudCredential new];
    
    // 영구 키 secretID 
    // sercret_id를 사용자의 SecretId로 대체합니다. CAM 콘솔에 로그인하여 키를 확인하십시오. https://console.cloud.tencent.com/cam/capi
    credential.secretID = @"SECRETID";
    // 영구 키 SecretKey
    // sercret_key를 사용자의 SecretKey로 대체합니다. CAM 콘솔에 로그인하여 키를 확인하십시오. https://console.cloud.tencent.com/cam/capi
    credential.secretKey = @"SECRETKEY"; 
    // 영구 키로 서명 계산
    QCloudAuthentationV5Creator* creator = [[QCloudAuthentationV5Creator alloc] 
        initWithCredential:credential];
    QCloudSignature* signature =  [creator signatureForData:urlRequst];
    continueBlock(signature, nil);
}
```

**Swift**

```swift
func signature(with fileds: QCloudSignatureFields!, 
                request: QCloudBizHTTPRequest!, 
                urlRequest urlRequst: NSMutableURLRequest!, 
                compelete continueBlock: QCloudHTTPAuthentationContinueBlock!) {
    let credential = QCloudCredential.init();
    
    // 영구 키 secretID 
    // sercret_id를 사용자의 SecretId로 대체합니다. CAM 콘솔에 로그인하여 키를 확인하십시오. https://console.cloud.tencent.com/cam/capi
    credential.secretID = "SECRETID";
    // 영구 키 SecretKey
    // sercret_key를 사용자의 SecretKey로 대체합니다. CAM 콘솔에 로그인하여 키를 확인하십시오. https://console.cloud.tencent.com/cam/capi
    credential.secretKey = "SECRETKEY"; 

    // 영구 키로 서명 계산
    let auth = QCloudAuthentationV5Creator.init(credential: credential);
    let signature = auth?.signature(forData: urlRequst)
    continueBlock(signature,nil);
}
```

#### 방법 3: 백그라운드에서 계산된 서명을 요청 라이선스에 사용

서명 과정이 백그라운드에 배치되면 `QCloudCredentailFenceQueueDelegate` 프로토콜을 실행하지 않아도 됩니다.

**Objective-C**

```objective-c
- (void) signatureWithFields:(QCloudSignatureFields*)fileds
                     request:(QCloudBizHTTPRequest*)request
                  urlRequest:(NSMutableURLRequest*)urlRequst
                   compelete:(QCloudHTTPAuthentationContinueBlock)continueBlock
{
    // 서명 만료 시간
    NSDate *expiration = [[[NSDateFormatter alloc] init] 
                            dateFromString:@"expiredTime"];
    QCloudSignature *sign = [[QCloudSignature alloc] initWithSignature:
        @"백그라운드에서 계산된 서명" expiration:expiration];
    continueBlock(signature, nil);
}
```

**Swift**

```swift
func signature(with fileds: QCloudSignatureFields!, 
                request: QCloudBizHTTPRequest!, 
                urlRequest urlRequst: NSMutableURLRequest!, 
                compelete continueBlock: QCloudHTTPAuthentationContinueBlock!) {
    // 서명 만료 시간
    let expiration = DateFormatter().date(from: "expiredTime");
    let sign = QCloudSignature.init(signature: "백그라운드에서 계산된 서명", 
                expiration: expiration);
    continueBlock(signature,nil);
}
```

## 3단계: COS 서비스 액세스

### 객체 업로드

SDK는 로컬 파일과 바이너리 데이터 NSData 업로드를 지원합니다. 아래는 로컬 파일 업로드 예시입니다.

**Objective-C**

```objective-c
QCloudCOSXMLUploadObjectRequest* put = [QCloudCOSXMLUploadObjectRequest new];
// 로컬 파일 경로
NSURL* url = [NSURL fileURLWithPath:@"파일의 URL"];
// BucketName-Appid로 구성된 버킷의 이름. COS 콘솔에서 확인 가능 https://console.cloud.tencent.com/cos5/bucket
put.bucket = @"examplebucket-1250000000";
// 객체 키. 객체의 COS 상의 전체 경로로, 디렉터리가 있을 경우 형식은 "video/xxx/movie.mp4"입니다.
put.object = @"exampleobject";
// 업로드가 필요한 객체 콘텐츠입니다. NSData* 또는 NSURL* 유형의 변수를 전달할 수 있습니다.
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
[put setFinishBlock:^(id outputObject, NSError *error) {
    //outputObject에서 response의 etag 또는 사용자 정의 헤더 등 정보 획득 가능
    NSDictionary * result = (NSDictionary *)outputObject;
}];

[[QCloudCOSTransferMangerService defaultCOSTransferManager] UploadObject:put];
```

>?
>- 전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/TransferUploadObject.m)를 참고하십시오.
>- 업로드 후 같은 Key를 사용해 파일 다운로드 링크를 생성할 수 있습니다. 자세한 사용 방법은 **사전 서명 링크 생성** 문서를 참고하십시오. 문서의 권한이 개인 읽기일 경우, 다운로드 링크에 유효 기간이 있습니다.

**Swift**

```swift
let put:QCloudCOSXMLUploadObjectRequest = QCloudCOSXMLUploadObjectRequest<AnyObject>();
// BucketName-Appid로 구성된 버킷의 이름. COS 콘솔에서 확인 가능 https://console.cloud.tencent.com/cos5/bucket
put.bucket = "examplebucket-1250000000";
// 객체 키. 객체의 COS 상의 전체 경로로, 디렉터리가 있을 경우 형식은 "video/xxx/movie.mp4"입니다.
put.object = "exampleobject";
//업로드가 필요한 객체 콘텐츠입니다. NSData* 또는 NSURL* 유형의 변수를 전달할 수 있습니다.
put.body = NSURL.fileURL(withPath: "Local File Path") as AnyObject;

//업로드 결과 수신
put.setFinish { (result, error) in
    // 업로드 결과 획득
    if error != nil{
        print(error!);
    }else{
        print(result!);
    }
}

//업로드 진행률 수신
put.sendProcessBlock = { (bytesSent, totalBytesSent,
    totalBytesExpectedToSend) in
    //      bytesSent                 발송할 바이트 수(대용량 파일은 여러 번으로 나누어 발송해야 할 수 있습니다.)
    //      totalBytesSent            발송한 바이트 수
    //      totalBytesExpectedToSend  이번 업로드에서 발송할 총 바이트 수(파일 1개의 크기)
};
// 업로드 매개변수 설정
put.initMultipleUploadFinishBlock = {(multipleUploadInitResult, resumeData) in
    //멀티파트 업로드 초기화 완료 후 해당 block을 콜백합니다. 여기에서 resumeData를 획득할 수 있습니다.
    //또한 resumeData를 통해 멀티파트 업로드 요청을 생성할 수 있습니다.
    let resumeUploadRequest = QCloudCOSXMLUploadObjectRequest<AnyObject>
        .init(request: resumeData as Data?);
}

QCloudCOSTransferMangerService.defaultCOSTransferManager().uploadObject(put);
```

>?
>- 전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/TransferUploadObject.swift)를 참고하십시오.
>- 업로드 후 같은 Key를 사용해 파일 다운로드 링크를 생성할 수 있습니다. 자세한 사용 방법은 **사전 서명 링크 생성** 문서를 참고하십시오. 문서의 권한이 개인 읽기일 경우, 다운로드 링크에 유효 기간이 있습니다.

### 객체 다운로드

**Objective-C**

```objective-c
QCloudCOSXMLDownloadObjectRequest * request = [QCloudCOSXMLDownloadObjectRequest new];
    
// BucketName-Appid로 구성된 버킷의 이름. COS 콘솔에서 확인 가능 https://console.cloud.tencent.com/cos5/bucket
request.bucket = @"examplebucket-1250000000";
// 객체 키. 객체의 COS 상의 전체 경로로, 디렉터리가 있을 경우 형식은 "video/xxx/movie.mp4"입니다.
request.object = @"exampleobject";

//다운로드할 경로 URL 설정. 설정 시 파일이 지정된 경로에 다운로드됩니다.
request.downloadingURL = [NSURL fileURLWithPath:@"Local File Path"];

//다운로드 결과 수신
[request setFinishBlock:^(id outputObject, NSError *error) {
    //outputObject는 상응하는 모든 http 헤더를 포함합니다.
    NSDictionary* info = (NSDictionary *) outputObject;
}];

//다운로드 진행률 수신
[request setDownProcessBlock:^(int64_t bytesDownload,
                                int64_t totalBytesDownload,
                                int64_t totalBytesExpectedToDownload) {
    //      bytesDownload                   이번에 다운로드할 바이트 수. 대용량 파일은 여러 번으로 나누어 발송해야 할 수 있습니다.
    //      totalBytesDownload              다운로드한 바이트 수
    //      totalBytesExpectedToDownload    이번 다운로드의 총 바이트 수(파일 1개의 크기)
}];

[[QCloudCOSTransferMangerService defaultCOSTransferManager] DownloadObject:request];
```

>?전체 예시는 [GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Objc/Examples/cases/TransferDownloadObject.m)를 참고하십시오.

**Swift**

```swift
let request : QCloudCOSXMLDownloadObjectRequest = QCloudCOSXMLDownloadObjectRequest();
        
// BucketName-Appid로 구성된 버킷의 이름. COS 콘솔에서 확인 가능 https://console.cloud.tencent.com/cos5/bucket
request.bucket = "examplebucket-1250000000";
// 객체 키
request.object = "exampleobject";

//다운로드할 경로 URL 설정. 설정 시 파일이 지정된 경로에 다운로드됩니다.
request.downloadingURL = NSURL.fileURL(withPath: "Local File Path") as URL?;

//다운로드 진행률 수신
request.sendProcessBlock = { (bytesDownload, totalBytesDownload,
    totalBytesExpectedToDownload) in
    //      bytesDownload                   이번에 다운로드할 바이트 수. 대용량 파일은 여러 번으로 나누어 발송해야 할 수 있습니다.
    //      totalBytesDownload              다운로드한 바이트 수
    //      totalBytesExpectedToDownload    이번 다운로드의 총 바이트 수(파일 1개의 크기)
}

//다운로드 결과 수신
request.finishBlock = { (copyResult, error) in
    if error != nil{
        print(error!);
    }else{
        print(copyResult!);
    }
}

QCloudCOSTransferMangerService.defaultCOSTransferManager().downloadObject(request);
```

>?전체 예시는[GitHub](https://github.com/tencentyun/cos-snippets/tree/master/iOS/Swift/Examples/cases/TransferDownloadObject.swift)를 참고하십시오.
