
<span id="config"></span>
## Configuring the License
You need to call the following methods to configure the license before calling Call SDK APIs:
- **iOS**
 We recommend adding the following in `[AppDelegate application:didFinishLaunchingWithOptions:]`: 
```
[TXLiveBase setLicenceURL:LicenceUrl key:Key];
```
-  **Android**
 We recommend adding the following in the application:
```
TXLiveBase.getInstance().setLicence(context, LicenceUrl, Key);
```

## Viewing License Information
After the license is successfully configured (you need to wait for a while and the time depends on your network condition), you can call the following methods to view information of the license:

- **iOS**
```
NSLog(@"%@", [TXLiveBase getLicenceInfo]);
```
- **Android**
```
TXLiveBase.getInstance().getLicenceInfo();
```

 
