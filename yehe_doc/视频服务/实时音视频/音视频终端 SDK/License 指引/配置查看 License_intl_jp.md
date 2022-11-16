## ライブストリーミングおよびビデオ再生License

### 設定方法

SDKに関連するインターフェースを呼び出す前に、次のメソッドを呼び出してLicenseを設定する必要があります。
- **iOS**
 `[AppDelegate application:didFinishLaunchingWithOptions:]`内に以下を追加することをお勧めします。 
```
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    NSString * const licenceURL = @"<取得したlicenseUrl>";
    NSString * const licenceKey = @"<取得したkey>";

    // V2TXLivePremierは"V2TXLivePremier.h"ヘッダーファイル内にあります
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
 applicationに以下を追加することをお勧めします。
```
public class MApplication extends Application {

@Override
public void onCreate() {
    super.onCreate();
    String licenceURL = ""; // 取得したlicence url
    String licenｃeKey = ""; // 取得したlicence key
    V2TXLivePremier.setLicence(this, licenceURL, licenceKey);
    V2TXLivePremier.setObserver(new V2TXLivePremierObserver() {
            @Override
            public void onLicenceLoaded(int result, String reason) {
                Log.i(TAG, "onLicenceLoaded: result:" + result + ", reason:" + reason);
            }
        });
}
```

### 確認方法
License設定に成功後（しばらくかかります。時間の長さはネットワークの状況に応じて異なります）、次のメソッドを呼び出してLicense情報を確認することができます。

- **iOS:**
```
NSLog(@"%@", [TXLiveBase getLicenceInfo]);
```
- **Android:**
```
TXLiveBase.getInstance().getLicenceInfo();
```

 

## UGSV License

### 設定方法

SDKに関連するインターフェースを呼び出す前に、以下に示す方法を呼び出してLicenseの設定を実行します。
- **iOS**
 `[AppDelegate application:didFinishLaunchingWithOptions:]`内に以下を追加することをお勧めします。 
```
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    NSString * const licenceURL = @"<取得したlicenseUrl>";
    NSString * const licenceKey = @"<取得したkey>";

    //TXUGCBaseは"TXUGCBase.h"ヘッダーファイル内にあります
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
 applicationに以下を追加することをお勧めします。
```
public class MApplication extends Application {

    @Override
    public void onCreate() {
        super.onCreate();
        String licenceURL = ""; // 取得したlicence url
        String licenｃeKey = ""; // 取得したlicence key
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

>? ライブストリーミングLicense、UGSV Licenseおよびビデオ再生Licenseは、licenceURLと同様に、設定はグローバルで1回行うだけでよく、重複して設定する必要はありません。[TRTC](https://console.tencentcloud.com/trtc/license)、 [CSS](https://console.tencentcloud.com/live/license)または[VOD](https://console.tencentcloud.com/vod/license)のいずれかの製品のコンソールにログインし、無料のテスト版Licenseの申請または[正式版Licenseの購入](https://buy.tencentcloud.com/license)を行うことができます。

### 確認方法

License設定が成功してから一定時間経つと（ネットワークの状況に応じて異なります）、以下の方法を呼び出してLicense情報を確認することができます。

- **iOS:**
```
NSLog(@"%@", [TXUGCBase getLicenceInfo]);
```
- **Android:**
```
TXUGCBase.getInstance().getLicenceInfo(context);
```