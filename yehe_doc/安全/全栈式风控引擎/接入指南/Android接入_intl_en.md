## Android
An SDK for Android is provided for your mobile application. You can integrate it in the following steps:
## 1. Integrate the SDK

<aside>
Currently, the SDK is compatible with applications with Android API level 15 and above and supports manual integration on simulators.

</aside>

### Manual integration

- Click here to download the SDK.

[RiskAssessment.rar](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b393d6f5-3882-4e09-bf49-930b51e0af6e/RiskAssessment.rar)

- Add the `aar` file to your `libs` folder.
- In your application's `build.gradle`, add the following code:

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

- Sync the project with the gradle file

## 2. Initialize the SDK

<aside>
SDK initialization should be configured in `onCreate()` in your `Application` subclass to ensure successful generation and processing of the device fingerprint. You need to get the `APP_ID`, `SECRET_ID`, and `SECRET_KEY` of your Tencent Cloud account to initialize the SDK. It should be initialized only once, and an exception will be reported if it is initialized multiple times.

</aside>

```java
RiskAssessment.initRiskAssessment(this,APP_ID,SECRET_ID,SECRET_KEY);
```

## 3. Get the device result

<aside>
You can retrieve the device result as needed at specific user checkpoints or activities, such as account registration, login, or checkout. This is to ensure that there is enough time to generate the device fingerprint.
  To retrieve the device result as needed, call:

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

`setRiskAssessmentStateListener(new RiskAssessment.RiskAssessmentStateListener()` checks whether the `DeviceResult` is ready to be retrieved. `getDeviceResult()` retrieves the latest `DeviceResult`. This function may return null if it is called before the evaluation is completed. `getError` enables the troubleshooting of unsuccessful `DeviceResult` retrievals.

**Sample device result response**

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

If the above data is displayed, the call is successful.
