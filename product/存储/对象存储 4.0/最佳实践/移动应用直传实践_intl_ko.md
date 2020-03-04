## 배경

본 문서에서는 Tencent Cloud COS에 기초하여 하나의 앱에서 파일의 직접 전송 기능을 빠르게 구현하는 방법을 소개합니다. 서버에서 접근 키를 생성하고 관리하기만 하면 디테일에 신경 쓸 필요가 없으며 파일 데이터는 모두 Tencent Cloud COS에 저장됩니다.

## 아키텍처

pc에서 영구 키를 클라이언트 코드에 입력할 경우 귀하의 키 정보가 유출되기 쉽고 이용자 접근 권한을 제어하기 불편합니다. 당사는 요청 시 임시 키를 휴대할 것을 권장하며 귀하는 App에 임시 권한을 부여함으로써 귀하의 스토리지 리소스에 접근할 수 있으나 귀하의 영구 키는 유출되지 않습니다. 키의 유효 기간은 사용자가 직접 지정할 수 있고 만료될 경우 자동으로 무효됩니다.

COS의 모바일 SDK(Android/IOS)는 모두 임시 키를 통한 권한 요청을 효과적으로 지원합니다. 귀하는 백 엔드에서 하나의 임시 키 서비스를 수립하기만 하면 스무드하게 단말 COS 요청을 권한 부여할 수 있습니다.

### 아키텍처 그림
전체 아키텍처 그림은 아래와 같습니다.
![cos로 cam에 액세스하는 아키텍처 그림](http://mc.qcloudimg.com/static/img/b1e187a9ec129ffc766c07a733ef4dd6/image.jpg)

그 중:

- 사용자 클라이언트: 즉 사용자의 핸드폰 App.
- COS: [Tencent Cloud COS](https://cloud.tencent.com/product/cos), App에 업로드한 데이터의 저장을 책임집니다.
- CAM: [Tencent Cloud CAM](https://cloud.tencent.com/product/cam), COS 임시 키의 생성에 사용됩니다.
- 응용프로그램 서버: 사용자 자체의 백 엔드 서버로서 임시 키를 획득하고 응용프로그램 App에 반환할 때 사용됩니다.

## 준비

### 버킷 생성

[COS 콘솔](https://console.cloud.tencent.com/cos5/bucket)에서 하나의 Bucket을 생성합니다. 자체의 수요에 따라 bucket 권한을 비공개 읽기/쓰기 권한 또는 공개 읽기 및 비공개 쓰기 권한으로 설정합니다.

### 영구 키 획득

임시 키는 영구 키를 통해서 생성 가능합니다. [API 키 콘솔](https://console.cloud.tencent.com/cam/capi)에 로그인하여 획득하십시오. 아래 사항을 포함합니다.

- SecretId
- SecretKey
- AppID

## 임시 키 서비스 구축

보안성을 고려하여 서명에 임시 키가 필요합니다. 서버에서 임시 키 서비스를 구툭하려면 API를 클라이언트에 제공하여 사용됩니다. 자세한 절차는 [임시 키 생성 및 사용 가이드](https://cloud.tencent.com/document/product/436/14048)를 참조하십시오.

>! 공식적으로 배포할 때 서버에 사용자의 웹사이트 자체의 권한 인증을 한 단계 더 추가하십시오.

### 적합한 권한 선택

최소 권한 원칙에 의해 자체의 수요에 따라 정책을 통해 임시 키의 권한 범위를 제어할 것을 권장합니다. 서버는 하나의 전체 읽기/쓰기 권한의 키를 제공하며 일단 공격을 받기만 하면 기타 사용자의 데이터를 유출할 가능성이 존재합니다. 자세한 구성 방법은 [임시 키 생성 및 사용 가이드](https://cloud.tencent.com/document/product/436/14048)를 참조하십시오.

## SDK 액세스 권한 부여 서비스

### Android

임시 키 서비스를 구축한 후 SDK를 권한 부여 서비스에 접속시켜야 합니다. SDK는 요청한 동시 발생 수를 제어하고 유효한 키를 로컬에 캐시하며 키가 무효된 후 다시 요청하는 등을 책임지므로 귀하는 획득한 키를 자체로 관리할 필요가 없습니다.

#### 표준 응답 본문 권한 부여

STS SDK에서 획득한 JSON 데이터를 임시 응답 본문으로 사용하였다면(cossign은 이러한 방식을 채택하였음), 다음 코드를 사용하여 COS SDK에서 권한 부여 클래스를 생성할 수 있습니다.

```
CosXmlServiceConfig cosXmlServiceConfig = ...;

/**
 * 권한부여 서비스의 url 주소 획드
 */
URL url = null; // 백 엔드 권한 부여 서비스의 url 주소
try {
    url = new URL("your_auth_server_url");
} catch (MalformedURLException e) {
    e.printStackTrace();
}

/**
 * {@link QCloudCredentialProvider} 객체를 초기화하여 SDK에 임시 키를 제공합니다.
 */
QCloudCredentialProvider credentialProvider = new SessionCredentialProvider(new HttpRequest.Builder<String>()
                .url(url)
                .method("GET")
                .build());

CosXmlService cosXmlService = new CosXmlService(this, cosXmlServiceConfig, credentialProvider);                
```
>!?이러한 방식에서 서명 시작 시간은 휴대폰 현지 시간이기 때문에 휴대폰 현지 시간 편차가 너무 크면(10분 이상), 서명 오류를 초래할 수 있습니다. 이럴 때 다음 사용자 지정 응답 본문 권한 부여를 사용할 수 있습니다.

#### 사용자 지정 응답 본문 권한 부여

더 큰 유연성을 얻고자 할 경우 예를 들어 임시 키 서비스의 HTTP 응답 본문을 사용자가 지정하여 단말에 서버 시간을 반환하여 서명의 시작 시간으로 합니다. 사용자 핸드폰이 로컬 시간과의 과도한 편차로 인한 서명 오류를 방지하고자 하는 경우 또는 기타 프로토콜을 사용하여 단말과 서버 사이의 통신을 진행하고자 할 경우 `BasicLifecycleCredentialProvider` 클래스를 계승하여 해당 `fetchNewCredentials()`를 구현할 수 있습니다.

우선 하나의 `MyCredentialProvider` 클래스를 정의하십시오.

```java
public class MyCredentialProvider extends BasicLifecycleCredentialProvider {

    @Override
    protected QCloudLifecycleCredentials fetchNewCredentials() throws QCloudClientException {

        // 우선 임시 키 서버에서 서명 정보를 포함한 응답을 획득합니다
        ....

        // 다음 응답 내용을 해석하고 키 정보를 획득합니다
        String tmpSecretId = ...;
        String tmpSecretKey = ...;
        String sessionToken = ...;
        long expiredTime = ...;

        // 서버 시간을 반환하여 서명의 시작 시간으로 합니다
        long beginTime = ...;

        // todo something you want

        // 마지막으로 임시 키 정보 객체를 반환합니다
        return new SessionQCloudCredentials(tmpSecretId, tmpSecretKey, sessionToken, beginTime, expiredTime);
    }
}
```
정의한 `MyCredentialProvider` 인스턴스를 사용하여 요청을 권한 부여합니다.

```
CosXmlServiceConfig cosXmlServiceConfig = ...;

/**
 * {@link QCloudCredentialProvider} 객체를 초기화하여 SDK에 임시 키를 제공합니다.
 */
QCloudCredentialProvider credentialProvider = new MyCredentialProvider();

CosXmlService cosXmlService = new CosXmlService(this, cosXmlServiceConfig, credentialProvider);   
```

완전한 예제 코드는 [Android COS Transfer](https://github.com/tencentyun/qcloud-sdk-android-samples/tree/master/COSTransfer)를 참조하십시오.

Android 시스템에서 COS에 파일을 업로드하고 다운로드하는 데 관한 자세한 사항은 [Android SDK 시작 가이드](https://cloud.tencent.com/document/product/436/12159)를 참조하십시오.

### iOS

당사는 QCloudCredentailFenceQueue를 제공하여 임시 서명의 획득 및 관리에 도움이 됩니다. QCloudCredentailFenceQueue는 허들 메커니즘을 제공합니다. 다시 말하면 귀하가 QCloudCredentailFenceQueue를 사용하여 서명을 획득할 경우 서명을 획득해야 하는 모든 요청은 서명 완료 후 재실행되므로 자체 관리의 비동기화 과정을 생략하였습니다.

QCloudCredentailFenceQueue 사용 시 우선 하나의 인스턴스를 생성해야 합니다.

```
 //AppDelegate.m
//AppDelegate는 QCloudCredentailFenceQueueDelegate 프로토콜에 따라야 합니다
//
- (BOOL)application:(UIApplication * )application didFinishLaunchingWithOptions:(NSDictionary * )launchOptions {
    // init step
    self.credentialFenceQueue = [QCloudCredentailFenceQueue new];
    self.credentialFenceQueue.delegate = self;
    return YES;
}

```

다음 QCloudCredentailFenceQueue 클래스의 호출은 QCloudCredentailFenceQueueDelegate를 따라야 하며 프로토콜 내 정의를 구현하는 방법은 아래와 같습니다.

```
 - (void) fenceQueue:(QCloudCredentailFenceQueue * )queue requestCreatorWithContinue:(QCloudCredentailFenceQueueContinue)continueBlock
```

QCloudCredentailFenceQueue로 서명 획득 시 모든 서명이 필요한 SDK의 요청은 모두 해당 프로토콜 정의의 방법 내에서 서명이 필요한 매개변수를 획득하고 유효한 서명을 생성한 후 실행됩니다. 아래 예시를 참조하십시오.

```
- (void)fenceQueue:(QCloudCredentailFenceQueue *)queue requestCreatorWithContinue:(QCloudCredentailFenceQueueContinue)continueBlock {
    QCloudHTTPRequest* request = [QCloudHTTPRequest new];
    request.requestData.serverURL = @“your sign service url”;//요청한 URL

    [request setConfigureBlock:^(QCloudRequestSerializer *requestSerializer, QCloudResponseSerializer *responseSerializer) {
        requestSerializer.serializerBlocks = @[QCloudURLFuseWithURLEncodeParamters];
        responseSerializer.serializerBlocks = @[QCloudAcceptRespnseCodeBlock([NSSet setWithObjects:@(200), nil],nil),//오류 코드가 200을 초과할 때 오류를 반환합니다
                                                QCloudResponseJSONSerilizerBlock];//JSON 포맷에 따라 반환하는 데이터를 분석합니다
    }];

    [request setFinishBlock:^(id response, NSError *error) {
        if (error) {
            error = [NSError errorWithDomain:@"com.tac.test" code:-1111 userInfo:@{NSLocalizedDescriptionKey:@"임시 키를 획득하지 못했습니다"}];
            continueBlock(nil, error);
        } else {
            QCloudCredential* crendential = [[QCloudCredential alloc] init];
            crendential.secretID = response[@"data"][@"credentials"][@"tmpSecretId"];
            crendential.secretKey = response[@"data"][@"credentials"][@"tmpSecretKey"];
            credential.startDate =[NSDate dateWithTimeIntervalSince1970:@"반환한 서버 시간"]
            crendential.experationDate = [NSDate dateWithTimeIntervalSinceNow:[response[@"data"][@"expiredTime"] intValue]];
            crendential.token = response[@"data"][@"credentials"][@"sessionToken"];;
            QCloudAuthentationV5Creator* creator = [[QCloudAuthentationV5Creator alloc] initWithCredential:crendential];
            continueBlock(creator, nil);

        }
    }];
    [[QCloudHTTPSessionManager shareClient] performRequest:request];
}
```

iOS 시스템에서 COS에 파일을 업로드하고 다운로드하는 데 관한 자세한 사항은 [iOS SDK 시작 가이드]()를 참조하십시오.


## 체험하기

### Android

<<<<<<< HEAD
[여기](https://cos-terminal-resource-1253960454.cos.ap-shanghai.myqcloud.com/cos-transfer-practice.apk)를 클릭하거나 Android 핸드폰으로 QR코드를 스캔하여 demo를 직접적으로 다운로드하고 체험해 보세요.
=======
[여기](https://cos-terminal-resource-1253960454.cos.ap-shanghai.myqcloud.com/cos-transfer-practice.apk)를 클릭하거나 Android 핸드폰으로 QR코드를 스캔하여 demo를 직접적으로 다운로드하고 체험해 보세요.
>>>>>>> parent of b3f10c0cd1... Revert "Merge branch 'master' of https://github.com/tencentyun/qcloud-documents"

![](https://cos-terminal-resource-1253960454.cos.ap-shanghai.myqcloud.com/cos-transfer-practice-download.png)

완전한 코드는 [COS Android Demo](https://github.com/tencentyun/qcloud-sdk-android-samples/tree/master/COSTransferPractice)를 참조하십시오.

### iOS

iOS의 완전한 사례 프로젝트는 [COS iOS Demo](https://github.com/tencentyun/qcloud-sdk-ios-samples/tree/master/OOTB-XML)를 참조하십시오.

QCloudCOSXMLDemo/QCloudCOSXMLDemo/TestCommonDefine.h 파일을 수정하고 AppID 및 앞에서 배포 완료한 임시 키를 획득할 수 있는 주소를 입력한 다음 아래 명령을 실행하십시오.

```sh
pod install
```

명령을 실행한 후 QCloudCOSXMLDemo.xcworkspace를 열면 바로 Demo를 체험할 수 있습니다.
