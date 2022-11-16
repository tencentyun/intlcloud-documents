## 라이브 스트리밍 및 비디오 재생 License

### 설정 방법

미디어 SDK의 API를 호출하기 전에 아래 단계에 따라 License를 구성하십시오.
- **iOS**
 `[AppDelegate application:didFinishLaunchingWithOptions:]`에 다음을 추가하는 것이 좋습니다. 
```
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    NSString * const licenceURL = @"<획득한 licenseUrl>";
    NSString * const licenceKey = @"<획득한 key>";

    // V2TXLivePremier는 헤더 파일 "V2TXLivePremier.h"에 있습니다
    [V2TXLivePremier setLicence:licenceURL key:licenceKey];
    [V2TXLivePremier setObserver:self];
    NSLog(@"SDK Version = %@", [V2TXLivePremier getSDKVersionStr]);
    return YES;
}

#pragma mark - V2TXLivePremierObserver
- (void)onLicenceLoaded:(int)result Reason:(NSString *)reason {
    NSLog(@"onLicenceLoaded: result:%d reason:%@", result, reason);
}
@end
```
-  **Android**
 application에 아래 코드를 추가하는 것이 좋습니다.
```
public class MApplication extends Application {

@Override
public void onCreate() {
    super.onCreate();
    String licenceURL = ""; // 획득한 licence url
    String licenceKey = ""; // 획득한 licence key
    V2TXLivePremier.setLicence(this, licenceURL, licenceKey);
    V2TXLivePremier.setObserver(new V2TXLivePremierObserver() {
            @Override
            public void onLicenceLoaded(int result, String reason) {
                Log.i(TAG, "onLicenceLoaded: result:" + result + ", reason:" + reason);
            }
        });
}
```

### License 정보 보기
License가 성공적으로 구성되면 아래 API를 호출하여 License 정보를 볼 수 있습니다. 구성이 적용되는 데 시간이 걸릴 수 있습니다. 정확한 소요 시간은 네트워크 상태에 따라 다릅니다.

- **iOS:**
```
NSLog(@"%@", [TXLiveBase getLicenceInfo]);
```
- **Android:**
```
TXLiveBase.getInstance().getLicenceInfo();
```

 

## UGSV License

### 설정 방법

SDK 관련 인터페이스를 호출하기 전에 아래와 같은 방법을 호출하여 License를 설정합니다.
- **iOS**
 `[AppDelegate application:didFinishLaunchingWithOptions:]`에 다음을 추가하는 것이 좋습니다. 
```
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    NSString * const licenceURL = @"<획득한 licenseUrl>";
    NSString * const licenceKey = @"<획득한 key>";

    //TXUGCBase는 헤더 파일 "TXUGCBase.h"에 있습니다
    [TXUGCBase setLicenceURL:licenceURL key:licenceKey]; 
    NSLog(@"SDK Version = %@", [TXUGCBase getSDKVersionStr]);
    return YES;
}

- (void)onLicenceLoaded:(int)result Reason:(NSString *)reason {
    NSLog(@"onLicenceLoaded: result:%d reason:%@", result, reason);
}
@end
```
-  **Android**
 application에 다음을 추가하는 것이 좋습니다.
```
public class MApplication extends Application {

    @Override
    public void onCreate() {
        super.onCreate();
        String licenceURL = ""; // 획득한 licence url
        String licenceKey = ""; // 획득한 licence key
        TXUGCBase.getInstance().setLicence(this, licenceURL, licenceKey);
        TXUGCBase.setListener(new TXUGCBaseListener() {
            @Override
            public void onLicenceLoaded(int result, String reason) {
                Log.i(TAG, "onLicenceLoaded: result:" + result + ", reason:" + reason);
            }
        });
    }
}
```

>? 라이브 스트리밍 License, UGSV License 및 비디오 재생 License의 licenceURL이 동일한 경우 License 정보를 한 번만 구성하면 됩니다. [TRTC 콘솔](https://console.tencentcloud.com/trtc/license), [CSS 콘솔](https://console.tencentcloud.com/live/license) 또는 [VOD 콘솔](https://console.tencentcloud.com/vod/license)에 로그인하여 무료 체험 License를 신청하거나 [공식 License를 구매](https://buy.tencentcloud.com/license)할 수 있습니다.

### License 정보 보기

License 설정 완료 후 잠시 기다리면(네트워크 환경에 따라 다름) 아래와 같은 방법으로 호출하여 License 정보를 확인할 수 있습니다.

- **iOS:**
```
NSLog(@"%@", [TXUGCBase getLicenceInfo]);
```
- **Android:**
```
TXUGCBase.getInstance().getLicenceInfo(context);
```