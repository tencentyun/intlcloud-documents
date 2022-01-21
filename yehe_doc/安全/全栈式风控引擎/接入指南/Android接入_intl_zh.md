## Android
为您的移动应用提供了Android sdk , 开始使用有以下步骤
## 1.集成SDK

<aside>
💡 目前支持Android API 级别 15 及更高级别的应用程序 、模拟器，手动集成

</aside>

### 手动集成

- 点击此下方下载sdk

[RiskAssessment.rar](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b393d6f5-3882-4e09-bf49-930b51e0af6e/RiskAssessment.rar)

- 将`aar`文件添加到您的 libs 文件夹中。
- 在您的应用程序中`build.gradle`，添加以下代码

```java
android {
	........
	sourceSets {
        main {
            jniLibs.srcDirs = ['libs']
        }
   }
}

dependencies {
    implementation files('libs/RiskAssessment.aar')
}
```

- 将项目与 gradle 文件同步

## 2.初始化SDK

<aside>
💡 SDK 初始化应`onCreate()`在您的`Application`子类中配置，以确保成功生成和处理设备指纹, 您需要获取到您腾讯云账号的 APP_ID, SECRET_ID，SECRET_KEY来初始化SDK, SDK只被初始化一次，如果多次初始化会抛出异常。

</aside>

```java
RiskAssessment.initRiskAssessment(this,APP_ID,SECRET_ID,SECRET_KEY);
```

## 3.获取设备结果

<aside>
💡 您可以在特定用户检查点或活动（例如帐户注册、登录或结帐）中按需检索设备结果。这是为了确保有足够的时间来生成设备指纹。
  要按需检索设备结果，请调用：

</aside>

```java
RiskAssessment.getInstance().setRiskAssessmentStateListener(new RiskAssessment.RiskAssessmentStateListener() {
            @Override
            public void isReady() {
                JSONObject result= RiskAssessment.getInstance().getDeviceResult();
                if(result!= null){
		//do something with device result
                } else {
                    ShieldException error = RiskAssessment.getError();
		//do error handling
                }
            }
 });
```

setRiskAssessmentStateListener(new RiskAssessment.RiskAssessmentStateListener()检查 DeviceResult 是否准备好被检索。getDeviceResult()检索最新的 DeviceResult。如果在评估完成之前调用此函数，则这可能返回 null。getError启用对不成功的 DeviceResult 检索的故障排除。

**示例设备结果响应**

```java
{
	"Response":{
		"Data":{
			"UUid":"21f71983-6a4c-4b1c-a5a3-4b79a08bacc1",
			"Code":0,
			"Message":"OK",
			"Value":{
				"RiskLevel":"pass",
				"RiskType":null
				}
		},
	"RequestId":"250f67d3-0f14-4955-bc64-5c5b5d2ebc60"
	}
}
```

若显示以上数据的话，恭喜您调用成功。
