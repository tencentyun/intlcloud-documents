[](id:config)
## Configuring a License
Before calling the SDK APIs, you need to configure the license by following steps below 
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
After the license is successfully configured, you can call the below commands to view the license information. Please note that it may take awhile for the configuration to be completed.

- **iOS**
```
NSLog(@"%@", [TXLiveBase getLicenceInfo]);
```
- **Android**
```
TXLiveBase.getInstance().getLicenceInfo();
```

 
