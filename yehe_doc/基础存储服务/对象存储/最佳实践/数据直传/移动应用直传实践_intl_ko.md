## 소개

본 문서에서는 Tencent Cloud COS를 기반으로 모바일 애플리케이션에서의 파일 다이렉트 업로드 기능을 신속히 구현하는 방법을 소개합니다. 서버에서 복잡한 조작을 할 필요 없이 액세스 키를 생성 및 관리하는 것만으로도 파일 데이터를 Tencent Cloud COS에 저장할 수 있습니다.

## 아키텍처 설명

클라이언트 애플리케이션의 경우, 영구 키를 클라이언트 코드에 입력하면 키 정보가 쉽게 노출될 수 있으며, 사용자 액세스 권한 제어에도 불편이 따릅니다. 영구 키의 유출 방지를 위해 요청 시 임시 키를 사용하고, App에 스토리지 리소스에 대한 임시 액세스 권한을 부여할 것을 권장합니다. 키의 유효기간은 직접 지정할 수 있으며, 기간이 만료되면 키는 자동 무효화됩니다.
COS의 모바일 SDK(Android/IOS)는 임시 키로 권한 부여 요청을 할 수 있습니다. 백그라운드에서 임시 키 서비스를 구축하면 단말 COS로 권한 부여를 위한 요청이 매끄럽게 전달됩니다.
#### 아키텍처
아키텍처 예시는 다음 이미지를 참조하십시오.
![cos로 cam 프레임워크 액세스](https://main.qcloudimg.com/raw/cf0a69ff91770578f70b05873bb1b348.png)
다음을 참고하십시오.
- 사용자 클라이언트: 사용자 휴대폰의 App입니다.
- COS: [Tencent Cloud COS](https://intl.cloud.tencent.com/product/cos), App에서 업로드한 데이터를 보관합니다.
- CAM: [Tencent Cloud CAM](https://intl.cloud.tencent.com/product/cam), COS 임시 키 생성에 쓰입니다.
- 사용자 서버: 사용자의 백그라운드 서버로, 임시 키를 발급하여 애플리케이션 App으로 반환합니다.

## 전제 조건
1. 버킷을 생성합니다.
[COS 콘솔](https://console.cloud.tencent.com/cos/bucket)에서 버킷을 생성합니다. 요구사항에 따라 버킷 권한을 개인 읽기/쓰기 또는 공개 읽기/개인 쓰기로 설정할 수 있습니다. 자세한 단계에 관한 내용은 [버킷 생성](https://intl.cloud.tencent.com/document/product/436/13309)과 [액세스 권한 설정](https://intl.cloud.tencent.com/document/product/436/13315)을 참조하십시오.
2. 영구 키를 받습니다.
임시 키는 영구 키를 통해 생성해야 합니다. [API Keys](https://console.cloud.tencent.com/cam/capi)로 이동하여 SecretId, SecretKey를 획득한 뒤 [계정 정보](https://console.cloud.tencent.com/developer)로 이동하여 APPID를 부여받습니다.
  
	
## 실행 순서	
### 임시 키 서비스 구축

보안 강화를 위해 임시 키로 서명하려면 서버에 임시 키 서비스를 구축하고, API 인터페이스를 클라이언트로 전달해야 합니다. 서비스 구축 단계에 관한 자세한 내용은 [임시 키 생성 및 사용 가이드](https://intl.cloud.tencent.com/document/product/436/14048)를 참조하십시오.

>! 정식 배포에 앞서 서버에 본인 웹 사이트의 권한 인증 기능을 추가하십시오.

#### 적합한 권한 선택

최소 권한의 원칙과 본인의 요구사항에 따라 Policy를 적용하여 임시 키의 권한 범위를 제어할 것을 권장합니다. 서버에서 전달한 완전한 읽기/쓰기 권한을 가진 키가 해킹에 노출되면 다른 사용자의 데이터가 유출될 위험이 있습니다. 설정에 관한 자세한 내용은 [임시 키 생성 및 사용 가이드](https://intl.cloud.tencent.com/document/product/436/14048)를 참조하십시오.

### SDK로 라이선스 서비스 액세스

#### Android

임시 키 서비스를 구축한 뒤 SDK로 라이선스 서비스에 액세스해야 합니다. SDK는 요청한 동시 접속 수를 제어하고, 유효한 키를 로컬에 캐싱합니다. 키가 무효화되면 재요청을 하기 때문에 키를 따로 관리하지 않아도 됩니다.

#### 표준 응답 본문에 의한 권한 부여

STS SDK에서 획득한 JSON 데이터를 임시 키 서비스의 응답 본문으로 할 경우(cossign은 해당 방법 적용), 다음 코드로 COS SDK의 권한 부여 클래스를 생성할 수 있습니다.
```
import android.content.Context;
import com.tencent.cos.xml.*;
import com.tencent.qcloud.core.auth.*;
import com.tencent.qcloud.core.common.*;
import com.tencent.qcloud.core.http.*;
import java.net.*;


Context context = ...;
CosXmlServiceConfig cosXmlServiceConfig = ...;

/**
 * 라이선스 서비스의 url 주소 획득
 */
URL url = null; // 백그라운드의 라이선스 서비스 url 주소
try {
    url = new URL("your_auth_server_url");
} catch (MalformedURLException e) {
    e.printStackTrace();
}

/**
 * {@link QCloudCredentialProvider} 객체 초기화로 SDK에 임시 키 부여
 */
QCloudCredentialProvider credentialProvider = new SessionCredentialProvider(new HttpRequest.Builder<String>()
                .url(url)
                .method("GET")
                .build());
                
CosXmlService cosXmlService = new CosXmlService(context, cosXmlServiceConfig, credentialProvider);                
```
>?이 방법을 적용할 경우, 서명 시작 시간은 휴대폰 로컬 시간이 기준입니다. 휴대폰 로컬 시간이 10분 이상 차이가 난다면 서명 오류가 발생할 수 있습니다. 이런 경우 다음의 사용자 정의 응답 본문으로 권한을 부여하는 것을 권장합니다.

#### 사용자 정의 응답 본문에 의한 권한 부여
사용자 정의한 임시 키 서비스의 HTTP 응답 본문이 단말에서 서버로 반환되는 시간을 서명 시작 시간으로 설정함으로써 사용자 휴대폰의 로컬 시간 오차로 서명 오류가 발생하는 것을 방지하거나 다른 프로토콜로 단말과 서버 간 통신하는 등 보다 효율적인 작업을 원한다면, BasicLifecycleCredentialProvider 클래스를 상속하여 fetchNewCredentials()를 출력합니다.

먼저 MyCredentialProvider 클래스를 정의하십시오.
```java
import android.content.Context;
import com.tencent.cos.xml.*;
import com.tencent.qcloud.core.auth.*;
import com.tencent.qcloud.core.common.*;
import com.tencent.qcloud.core.http.*;
import java.net.*;


public class MyCredentialProvider extends BasicLifecycleCredentialProvider {

    @Override
    protected QCloudLifecycleCredentials fetchNewCredentials() throws QCloudClientException {
       
        // 먼저 임시 키 서버로부터 서명 정보가 담긴 응답 획득
        ....
        
        // 응답을 분석하여 키 정보 획득
        String tmpSecretId = ...;
        String tmpSecretKey = ...;
        String sessionToken = ...;
        long expiredTime = ...;
        
        // 서버 반환 시간을 서명 시작 시간으로 설정
        long beginTime = ...;
         
        // todo something you want
         
        // 최종적으로 임시 키 정보 객체 반환 
        return new SessionQCloudCredentials(tmpSecretId, tmpSecretKey, sessionToken, beginTime, expiredTime);
    }
}
```
본인이 정의한 MyCredentialProvider 인스턴스로 권한 부여를 요청합니다.
```
import android.content.Context;
import com.tencent.cos.xml.*;
import com.tencent.qcloud.core.auth.*;
import com.tencent.qcloud.core.common.*;
import com.tencent.qcloud.core.http.*;
import java.net.*;

Context context = ...;
CosXmlServiceConfig cosXmlServiceConfig = ...;
        
/**
 * {@link QCloudCredentialProvider} 객체 초기화로 SDK에 임시 키 부여
 */
QCloudCredentialProvider credentialProvider = new MyCredentialProvider();

CosXmlService cosXmlService = new CosXmlService(context, cosXmlServiceConfig, credentialProvider);   
```


Android에서 COS로 파일을 업로드 및 다운로드하는 방법은 Android SDK의 [시작하기](https://intl.cloud.tencent.com/document/product/436/12159)를 참조하십시오.

#### iOS

임시 서명을 간편하게 획득하고 관리할 수 있는 QCloudCredentailFenceQueue를 제공합니다. QCloudCredentailFenceQueue로 서명을 획득할 경우, 모든 서명이 완료된 뒤 서명 요청이 실행되는 동기화 클래스 CyclicBarrier를 지원하여 스스로 비동기화를 관리하는 과정이 생략됩니다.

QCloudCredentailFenceQueue를 적용할 경우, 먼저 인스턴스 하나를 생성해야 합니다.

```
 //AppDelegate.m
//AppDelegate는 QCloudCredentailFenceQueueDelegate 프로토콜 따름
//
- (BOOL)application:(UIApplication * )application didFinishLaunchingWithOptions:(NSDictionary * )launchOptions {
    // init step
    self.credentialFenceQueue = [QCloudCredentailFenceQueue new];
    self.credentialFenceQueue.delegate = self;
    return YES;
}

```

QCloudCredentailFenceQueue의 클래스를 호출하려면 QCloudCredentailFenceQueueDelegate를 따르고, 프로토콜에 정의된 방법을 실행합니다.

```
- (void) fenceQueue:(QCloudCredentailFenceQueue * )queue requestCreatorWithContinue:(QCloudCredentailFenceQueueContinue)continueBlock
```

QCloudCredentailFenceQueue로 서명을 획득할 경우, 프로토콜에서 정의한 방법으로 서명 매개변수를 확보하여 유효한 서명을 생성한 뒤에야 SDK 내의 모든 서명 요청이 실행됩니다. 다음 예시를 참조하십시오.
```
- (void)fenceQueue:(QCloudCredentailFenceQueue *)queue requestCreatorWithContinue:(QCloudCredentailFenceQueueContinue)continueBlock {
    QCloudHTTPRequest* request = [QCloudHTTPRequest new];
    request.requestData.serverURL = @“your sign service url”;//요청한 URL
    
    [request setConfigureBlock:^(QCloudRequestSerializer *requestSerializer, QCloudResponseSerializer *responseSerializer) {
        requestSerializer.serializerBlocks = @[QCloudURLFuseWithURLEncodeParamters];
        responseSerializer.serializerBlocks = @[QCloudAcceptRespnseCodeBlock([NSSet setWithObjects:@(200), nil],nil),//반환 코드가 200이 아닌 경우, 오류 반환
                                                QCloudResponseJSONSerilizerBlock];//JSON 형식에 따라 반환 데이터 분석
    }];
    
    [request setFinishBlock:^(id response, NSError *error) {
        if (error) {
            error = [NSError errorWithDomain:@"com.tac.test" code:-1111 userInfo:@{NSLocalizedDescriptionKey:@"임시 키 미획득"}];
            continueBlock(nil, error);
        } else {
            QCloudCredential* crendential = [[QCloudCredential alloc] init];
            crendential.secretID = response[@"data"][@"credentials"][@"tmpSecretId"];
            crendential.secretKey = response[@"data"][@"credentials"][@"tmpSecretKey"];
            credential.startDate =[NSDate dateWithTimeIntervalSince1970:@"반환된 서버 시간"]
            crendential.experationDate = [NSDate dateWithTimeIntervalSinceNow:[response[@"data"][@"expiredTime"] intValue]];
            crendential.token = response[@"data"][@"credentials"][@"sessionToken"];;
            QCloudAuthentationV5Creator* creator = [[QCloudAuthentationV5Creator alloc] initWithCredential:crendential];
            continueBlock(creator, nil);
            
        }
    }];
    [[QCloudHTTPSessionManager shareClient] performRequest:request];
}
```

iOS에서 COS로 파일을 업로드 및 다운로드하는 방법은 iOS SDK의 [시작하기](https://intl.cloud.tencent.com/document/product/436/11280)를 참조하십시오.


### 체험

#### Android 

[여기](https://cos-terminal-resource-1253960454.cos.ap-shanghai.myqcloud.com/cos-transfer-practice.apk)를 클릭하거나 Android 휴대폰 브라우저 App으로 아래의 QR코드를 스캔하면 체험용 demo를 다운로드할 수 있습니다.
![](https://main.qcloudimg.com/raw/8b19785ec487d3e89711063bf80716a6.png)



#### iOS
iOS의 전체 코드에 관한 내용은 [COS iOS Demo](https://github.com/tencentyun/qcloud-sdk-ios-samples)를 참조하십시오.

QCloudCOSXMLDemo/QCloudCOSXMLDemo/key.json 파일에 APPID, secretID, secretKey 매개변수 값을 입력한 뒤 다음 명령어를 실행합니다.


```plaintext
pod install
```
>? APPID, secretID, secretKey는 [API Keys](https://console.cloud.tencent.com/cam/capi) 페이지에서 받을 수 있습니다.

명령어를 실행한 뒤 QCloudCOSXMLDemo.xcworkspace를 열면 Demo 체험으로 이동할 수 있습니다.
