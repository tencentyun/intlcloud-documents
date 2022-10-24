## Live Stream Publishing/Video Playback License

### Configuration

Before you call the APIs of the media SDKs, follow the steps below to configure the license:
- **iOS**
 Add the code below in `[AppDelegate application:didFinishLaunchingWithOptions:]`: 
```
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    NSString * const licenceURL = @"<The license URL obtained>";
    NSString * const licenceKey = @"<The key obtained>";

    // `V2TXLivePremier` is in the header file `V2TXLivePremier.h`.
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
 Add the code below in `application`:
```
public class MApplication extends Application {

@Override
public void onCreate() {
    super.onCreate();
    String licenceURL = ""; // The license URL obtained
    String licenceKey = ""; // The license key obtained
    V2TXLivePremier.setLicence(this, licenceURL, licenceKey);
    V2TXLivePremier.setObserver(new V2TXLivePremierObserver() {
            @Override
            public void onLicenceLoaded(int result, String reason) {
                Log.i(TAG, "onLicenceLoaded: result:" + result + ", reason:" + reason);
            }
        });
}
```

### Viewing license information
After the license is successfully configured, you can call the API below to view the license information. Please note that it may take a while for the configuration to take effect. The exact time needed depends on your network conditions.

- **iOS:**
```
NSLog(@"%@", [TXLiveBase getLicenceInfo]);
```
- **Android:**
```
TXLiveBase.getInstance().getLicenceInfo();
```

 

## UGSV License

### Configuration

Before you call the APIs of the media SDKs, follow the steps below to configure the license:
- **iOS**
 Add the code below in `[AppDelegate application:didFinishLaunchingWithOptions:]`: 
```
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    NSString * const licenceURL = @"<The license URL obtained>";
    NSString * const licenceKey = @"<The key obtained>";

    // `TXUGCBase` is in the header file `TXUGCBase.h`.
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
 We recommend adding the following in the application:
```
public class MApplication extends Application {

    @Override
    public void onCreate() {
        super.onCreate();
        String licenceURL = ""; // The license URL obtained
        String licenceKey = ""; // The license key obtained
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

>? If a live stream publishing license, a UGSV license, and a video playback license have the same license URL, you only need to configure license information once. You can apply for free trial licenses in the [TRTC console](https://console.tencentcloud.com/trtc/license), the [CSS console](https://console.tencentcloud.com/live/license), or the [VOD console](https://console.tencentcloud.com/vod/license), or you can [buy an official license](https://buy.tencentcloud.com/license).

### Viewing license information

After the license is successfully configured, you can call the API below to view the license information. Please note that it may take a while for the configuration to take effect. The exact time needed depends on your network conditions.

- **iOS:**
```
NSLog(@"%@", [TXUGCBase getLicenceInfo]);
```
- **Android:**
```
TXUGCBase.getInstance().getLicenceInfo(context);
```