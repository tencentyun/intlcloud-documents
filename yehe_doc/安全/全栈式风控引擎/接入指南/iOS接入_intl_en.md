## iOS
An SDK for iOS is provided for your mobile application. You can integrate it in the following steps:

## 1. **Integrate the SDK**

<aside>
💡 Currently, the SDK is compatible with applications on iOS 9 and above and supports manual integration on both simulators and real devices.

</aside>

**Use CocoaPods** 

- **Step 1**. If you don't have a Podfile, create one.

```markdown
 $ pod init
```

- **Step 2**. Add the Shield SDK to the Podfile.

```markdown
target 'MyApp' do
use_frameworks!

# Pods for MyApp
pod 'ShieldFraud'
end
```

- **Step 3**. Install a pod.

```markdown
 $ pod install
```
You should see the following output:
```markdown
Analyzing dependencies
Downloading dependencies
Installing ShieldFraud (1.5.10)
Generating Pods project
Integrating client project

[!] Please close any current Xcode sessions and use `MyApp.xcworkspace` for this project from now on.
Sending stats
Pod installation complete!
There is 1 dependency from the Podfile and 1 total pod installed.
```

- **Step 4**. Update to the latest SDK version with the following command.

```markdown
 $ pod update
```

- **Step 5**. Open your project in Xcode with the `MyApp.xcworkspace` file instead of the `MyApp.xcodeproj` file.

<aside>
💡  If your project uses Objective-C, set `Always Embed Swift Standard Libraries` to `YES` in build settings.

</aside>

### Manual import

- Click here to download the SDK.

[RiskAssessment.zip](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/06298141-dc1c-4d94-9157-92b5ff2fe651/RiskAssessment.zip)

- Decompress the SDK and add it to your Xcode project directory.
- Right-Click the directory you want to add to and click **Add Files to the current filename** to add the decompressed file.
- Check whether the file is added successfully. To do so, select the target of the project, click **Build Phases**, and check whether the SDK file exists in the **Link Binary With Libraries** directory. If not, click the **+** icon in this directory to add the decompressed SDK file with the .a extension.

<aside>
💡 If your project uses Swift, you need to create a bridging header file for bridging, as this SDK is built by Object-C. Pay attention to the naming convention, which is `TargetName-Bridging-Header`.

</aside>

- After creating the bridging header file, add the decompressed .h header file to it.
- Select **Targets** > **Build Settings**, select all, and search for the header. Enter the relative path of the bridging header file `TargetName-Bridging-Header` in **Objective-C Bridging Header** in the **Swift Compiler** > **General** directory.
- If command + right click cannot locate the .h header file, select the target of the project, click **Build Phases**, click **+** in the **Compile Sources** directory to add the .h header file

<aside>
💡 Solution to the `building for iOS Simulator, but linking in object file built for iOS, file` error reported by Xcode12 in a simulator

</aside>

This problem is a compatibility issue and currently should only appear on Macs with the M1 chip. As the M1 chip itself is on the ARM architecture, the simulator naturally supports the ARM architecture.

- Select **Targets** > **Build Settings**, select all, add `Any iOS Simulator SDk ----- arm64` under **Excluded Architectures** in the **Architectures** directory.

## 2. Initialize the SDK

<aside>
💡  You need to get the `APP_ID`, `SECRET_ID`, and `SECRET_KEY` of your Tencent Cloud account to initialize the SDK. It should be initialized only once, and an exception will be reported if it is initialized multiple times.

</aside>

- **Objective-C**

```markdown
#import "RiskAssessmentLib.h"

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions: (NSDictionary *)launchOptions
{
 [RiskAssessmentLib setConfig:APP_ID SECRET_ID:SECRET_ID SECRET_KEY:SECRET_KEY];
  return YES;
}

```

- swfit

```markdown
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: 
	[UIApplication.LaunchOptionsKey: Any]?) -> Bool {
		RiskAssessmentLib.setConfig(APP_ID, secret_ID: SECRET_ID, secret_KEY: SECRET_KEY);
		return true
}
```

## 3. Get the device result

You can retrieve the device result as needed at specific user checkpoints or activities, such as account registration, login, or checkout. This is to ensure that there is enough time to generate the device fingerprint.

- Objective-c

```objectivec
[[RiskAssessmentLib RA] getDeviceResult:^(NSDictionary * _Nonnull result) {

       //do something with the result

    } failure:^(NSError * _Nullable error) {

       // log error

}];
```

- Swift

```swift
RiskAssessmentLib.ra().getDeviceResult { (result) in

		//do something with the result
	
            } failure: { (Error) in

                // log error
            }
```

- **Sample device result response**

```objectivec
Response = {
        Data = {
            Code = 0;
            Message = OK;
            UUid = "3d28f277-cd99-4567-a986-663d5a3be5b3";
            Value = {
                RiskLevel = review;
                RiskType = "<null>";
            };
        };
        RequestId = "28180b2d-3cb0-4498-a426-7472a935496e";
    };
```

If the above data is displayed, the call is successful.

## 4. **Submit to App Store**

<aside>
💡 As the framework is added manually (without CocoaPods), the `x86_64` and `i386` architectures must be pruned before submission to App Store.

</aside>

- Locate the current .a file, click **Show in Finder** to display it in Finder, drag it to the terminal to display the path of the static library, and enter the folder where the static library is located in the terminal.
- View the architectures supported by the static library.

```markdown
lipo -info RiskAssessmentLib.a
```

 Sample: Architectures in the fat file: RiskAssessmentLib.a are: armv7 i386 x86_64 arm64

- Prune `x86_64` and `i386` architectures.

```markdown
lipo -remove i386 RiskAssessmentLib.a -o RiskAssessmentLib.a

lipo -remove x86_64 RiskAssessmentLib.a -o RiskAssessmentLib.a
```

View the supported architecture again

Sample: Architectures in the fat file: RiskAssessmentLib.a are: armv7  arm64
