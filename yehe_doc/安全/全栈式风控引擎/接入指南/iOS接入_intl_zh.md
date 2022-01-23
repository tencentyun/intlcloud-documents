## IOS
为您的移动应用提供了ios sdk , 开始使用有以下步骤：

## 1.**集成SDK**

目前支持 iOS 9 及更高版本的应用程序兼容，手动集成，支持模拟器和真机。


**使用 CocoaPods** 

- **第 1 步**：如果您没有现有的 Podfile，则创建一个。

```markdown
 $ pod init
```

- **第 2 步**：将 SHIELD SDK 添加到 Podfile。

```markdown
target 'MyApp' do
use_frameworks!

# Pods for MyApp
pod 'ShieldFraud'
end
```

- **第 3 步**：安装 pod。

```markdown
 $ pod install
```
您应该看到以下输出：
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

- **第4步**：使用以下命令更新到最新的SDK版本：

```markdown
 $ pod update
```

- **第5步**：使用`MyApp.xcworkspace`文件在 Xcode 中打开您的项目，而不是`MyApp.xcodeproj`文件。

如果您的项目使用的是 Objective-C，请在构建设置中将`Always Embed Swift Standard Libraries` 设置成 YES。

**手动导入**

- 点击此下方下载sdk：

[RiskAssessment.zip](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/06298141-dc1c-4d94-9157-92b5ff2fe651/RiskAssessment.zip)

- 解压缩 SDK 并将其添加到您的 Xcode 项目目录中。
- 选定你需要添加的目录点击鼠标右键，点击Add Files to "当前文件名"后，将解压出来的文件添加进去。
- 查看是否添加成功，选中工程的target，点击Build Phases，查看Link Binary With Libraries目录下是否有该SDK文件，若无则点击此目录下的“+”号添加解压出的.a后缀名的sdk文件。

如果您的项目使用的是swift，则需要创建桥接文件进行桥接，因为此sdk是由Object-c构建的,注意命名规则为`TargetName-Bridging-Header`。


- 创建好桥接头文件后在桥接文件中添加解压出的.h头文件。
- 选择 Targets -> Build Settings -> 选择all并搜索header, 在Swift Compiler - General 目录下的Objective-C Bridging Header中填写桥接头文件`TargetName-Bridging-Header`的相对路径。
- 若commoand + 鼠标右键定位不到.h头文件，这选中工程的target，点击Build Phases，在Compile Sources目录下点击“+”添加.h头文件。

Xcode12 运行模拟器报building for iOS Simulator, but linking in object file built for iOS, file错误解决方案。


这个问题目前应该只出现在M1芯片的Mac上，一个兼容性问题，因为M1芯片的Mac本身就是arm架构，所以模拟器自然也支持arm架构。

- 选择 Targets -> Build Settings -> 选择all, 在Architectures目录下的 Excluded ArchiteCtures下添加Any iOS Simulator SDk ----- arm64。

## 2.初始化SDK

您需要获取到您腾讯云账号的 APP_ID，SECRET_ID，SECRET_KEY来初始化SDK, SD只被初始化一次，如果多次初始化会抛出异常。

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

## 3.获取设备结果

您可以在特定用户检查点或活动（例如帐户注册、登录或结帐）中按需检索设备结果。这是为了确保有足够的时间来生成设备指纹。

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

- **设备结果响应示例**

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

若显示以上数据的话，恭喜您调用成功。

## 4.**提交到 App Store**

框架是手动添加的（没有 CocoaPods），则在提交到 App Store 之前必须修剪`x86_64`和`i386`架构。

- 定位到当前.a文件，点击show in Finder在Finder中显示，将.a文件拖动至终端，显示该静态库所在路径，在终端进入静态库所在文件夹。
- 查看静态库支持架构。

```markdown
lipo -info RiskAssessmentLib.a
```

 示例显示：Architectures in the fat file: RiskAssessmentLib.a are: armv7 i386 x86_64 arm64

- 修剪`x86_64`和`i386`架构。

```markdown
lipo -remove i386 RiskAssessmentLib.a -o RiskAssessmentLib.a

lipo -remove x86_64 RiskAssessmentLib.a -o RiskAssessmentLib.a
```

再次查看支持架构

示例显示：Architectures in the fat file: RiskAssessmentLib.a are: armv7  arm64
