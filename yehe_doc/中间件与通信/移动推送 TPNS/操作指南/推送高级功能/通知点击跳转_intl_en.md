## Use Cases

You can redirect subscribers who tap your notification to the specified in-app page, HTML5 page, or deep link to meet your needs in different use cases.

## Application Scope

| Platform   | Type                                                    |
| ------- | ------------------------------------------------------------ |
| Android | <li>Intent redirect: jumps to the specified in-app page. You can also pass in custom parameters.<li>Open application: directly goes to the application’s homepage<li>URL: opens the browser and accesses the specified webpage<li>In-app activity: jumps to the specified in-app page |
| iOS     | <li>Opens the app by default<li>Implements the business logic based on the delivered custom key and value</li> |

## Android Applications

>! In the SDK, a tap on a message can trigger a click event by default, which opens the target page. If a redirect action is configured in `onNotifactionClickedResult`, it will conflict with the custom redirect rule specified in the console or API, and the custom redirect rule will fail.
>

### Configuring SDK

To use Intent redirect, first configure the page to be redirected to in the client application’s `AndroidManifest` file.

If you want to redirect to the page specified by `AboutActivity`, use the following sample code:
```xml
<activity
    android:name="com.qq.xg.AboutActivity"
    android:theme="@android:style/Theme.NoTitleBar.Fullscreen" >
    
    <!-- Other intent-filter -->
    <!-- <intent-filter> ... </intent-filter> -->
    
    <!-- AndroidManifest supports configuring multiple intent-filters for an Android component. Please add the custom redirection configuration in a separate intent-filter. -->
    <intent-filter>
        <action android:name="android.intent.action.VIEW" />
        <category android:name="android.intent.category.DEFAULT"/>
        <!-- Customize the content of the data block to specify your complete scheme. -->
        <!-- According to your configuration, a URL in the `scheme name://host name/path name` format will be formed. -->
        <!-- To avoid conflicts with the redirection destination pages of other apps, you are advised to use fields that can uniquely identify the app for configuration, such as those with the app name or app package name. -->
        <data
              android:scheme="Scheme name"
              android:host="Host name"
              android:path="/Path name" />
    </intent-filter>
</activity>
```

### Using the console

#### Intent redirect (recommended)

To set the Intent redirect in the [TPNS console](https://console.cloud.tencent.com/tpns), go to **Task List** > **Create Push** > **Advanced Settings** > **Open Location** and enter the following information:

![](https://main.qcloudimg.com/raw/7555576dd7bea459eb7f27e8a0f48d19.png)

#### Open app

Tapping on the notification that is pushed via the console will open the application by default.

#### URL redirect

To set the URL redirect in the [TPNS console](https://console.cloud.tencent.com/tpns), go to **Advanced Settings** > **Open Location** and enter the following information:

![](https://main.qcloudimg.com/raw/0977d856b016ffbc7799644dc5f9af53.png)

#### In-app activity redirect

This method will be disused, so we don’t recommend using it. Go to **Advanced Settings** > **Open Location** in the console and enter the following information:

![](https://main.qcloudimg.com/raw/0d72df984a153f05a31c246e5dd6c8d9.png)



### Using RESTful APIs

Add the `action` and `action_type` fields under `body.message.android` of the push message body.

| Field | Type | Parent Project | Default Value | Required | Description |
| ----------- | ------- | ------- | ------ | ---- | ------------------------------------------------------------ |
| action         | Object  | Android | 1    | No | This sets the action after the notification bar is tapped; the default action is to open an application. |
| action_type | Integer | Action  | 1     | No   | One-tap action. Valid values: <li>`1`: opens activity or app</li><li>`2`: opens browser</li><li>3: opens Intent (recommended; for more information, see [Configuring SDK](#sdk-.E9.85.8D.E7.BD.AE))</li> |

#### Intent redirect (recommended)

Below is a sample of a complete message:
```json
{
  "audience_type": "token",
  "token_list": [
      "04xxx993"
  ],
   "message_type": "notify",
    "message":{
    "title": "xxx",
    "content": "xxx",
    "android": {
      "action": {
            "action_type": 3, // Action type. `1`: opens activity or app; `2`: opens browser; `3`: opens Intent          
            "intent": "xgscheme://com.tpns.push/notify_detail" // The SDK must be version 1.0.9 or later. Configure the data tag in the client's Intent and set the scheme attribute
        }
      }
   }	
}
```

If you want to pass in custom parameters such as `param1` and `param2`, use the sample code below:
```json
{
  "audience_type": "token",
  "token_list": [
      "04xxx993"
  ],
   "message_type": "notify",
    "message":{
    "title": "xxx",
    "content": "xxx",
    "android": {
      "action": {
            "action_type": 3, // Action type. `1`: opens activity or app; `2`: opens browser; `3`: opens Intent          
            "intent": "xgscheme://com.tpns.push/notify_detail?param1=aa&param2=bb" // The SDK must be version 1.0.9 or later. Configure the data tag in the client's Intent and set the scheme attribute
        }
      }
   }
}
```

>? If the client requires more parameters for other responses, refer to [Getting parameters on the client](#zhongduan).
>

#### Open app

Below is a sample of a complete message:

```json
{
  "audience_type": "token",
  "token_list": [
      "04xxx993"
  ],
   "message_type": "notify",
    "message":{
    "title": "xxx",
    "content": "xxx",
    "android": {
      "action": {
           "action_type": 1 // Action type. `1`: opens activity or app; `2`: opens browser; `3`: opens Intent  
        }
      }
   }	
}
```

#### URL redirect

Below is a sample of a complete message:
```json
{
  "audience_type": "token",
  "token_list": [
      "04xxx993"
  ],
   "message_type": "notify",
    "message":{
    "title": "xxx",
    "content": "xxx",
    "android": {
      "action": {
           "action_type": 2, // Action type. `1`: opens activity or app; `2`: opens browser; `3`: opens Intent          
           "browser": {
                "url": "http://tpns.qq.com", // Only HTTP and HTTPS URLs are supported
                "confirm": 1 // Whether user's confirmation is required
            }
        }
      }
   }
}
```

#### Opening the in-app activity

Below is a sample of a complete message:

```json
{
  "audience_type": "token",
  "token_list": [
      "04xxx993"
  ],
   "message_type": "notify",
    "message":{
    "title": "xxx",
    "content": "xxx",
    "android": {
      "action": {
           "action_type": 1, // Action type. `1`: opens activity or app; `2`: opens browser; `3`: opens Intent        
           "activity": "com.x.y.MainActivity",
           "aty_attr": {// Activity attribute, only for action_type=1
               "if": 0, // Intent's Flag attribute
               "pf": 0  // PendingIntent's Flag attribute
				}
			}
		}
	}
}
```

<span id="zhongduan"></span>


### Getting parameters on the client
1. In the `onCreate` method of the page you specify for redirect, add the following intent URI code:
```
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_temp);

    // ...

    // Obtain the intent URI code in `onCreate`
    Uri uri = getIntent().getData();
    Log.i(TAG, "onCreate get data uri: " + uri);
    if (uri != null) {                
        String url = uri.toString();
        String p1= uri.getQueryParameter("param1");
        String p2= uri.getQueryParameter("param2");
    }

    // ...
}
```
2. If your activity page is the application's resident page (for example, `launchMode` is set to `singleTop` or `singleTask`), the intent content for tap-to-redirect will be triggered by the `onNewIntent` method of the activity page. Please add the following to the `onNewIntent` method to get the intent URI code:
``` java
@Override
protected void onNewIntent(Intent intent) {
    super.onNewIntent(intent);

    // ...

    // Get the intent URI code in `onNewIntent`
    Uri uri = intent.getData();
    Log.i(TAG, "onNewIntent get data uri: " + uri);
    if (uri != null) {
        String url = uri.toString();
        String p1= uri.getQueryParameter("param1");
        String p2= uri.getQueryParameter("param2");
    }

    // ...
}
```
3. If the parameters passed in contain special characters, you can use URLEncode to encode the parameter values when creating the push and use URLDecode to decode them at the terminal. The following is a sample:
```java
Uri uri = getIntent().getData();
if (uri != null) {
    String p1 = uri.getQueryParameter("param1");
    String value1 = "";
    try {
        // The value of the custom parameter `param1` contains special characters. You can use URLEncode to encode it when creating the push and use URLDecode to decode it when obtaining it.
        value1 = URLDecoder.decode(p1, "UTF-8");
    } catch (UnsupportedEncodingException e) {
        Log.w("TPNS", "URLDecode param failed: " + e.toString());
    }
    // The custom parameter `param2` is not encoded with URLEncode and can be obtained directly.
    String value2 = uri.getQueryParameter("param2");
    Log.i("TPNS" , "value1 = " + value1);
}
```


## iOS Applications

You can pass in custom parameters in the notification for delivery, and implement the redirect or other business logic by parsing the parameters obtained on the client.

### Using the console

To set parameters in the [TPNS console](https://console.cloud.tencent.com/tpns), go to **Advanced Settings** > **Extra Parameter(s)** and enter the following information:
![](https://main.qcloudimg.com/raw/a77ffabd8cb2d4907bd7b597a11cfc97.png)

### Using RESTful APIs

Add the following `custom_content` field under `body.message.ios` of the push message body.

| Field | Type | Parent Project | Default Value | Required | Description |
| -------------- | ------ | ------ | ------ | ---- | ------------------------------------------ |
| custom_content  | String  | ios    | Empty    | No    | Custom parameter for delivery, which must be serialized to a JSON string.                                |

Below is a sample of a complete message:
```
{
	"audience_type": "token",
	"environment": "dev",
	"token_list": [
		"0250df875c93c555dd3a2ba536b54fc1xxxx"
	],
	"message_type": "notify",
	"message": {
		"title": "xxx",
		"content": "xxxxxxxxx",
		"ios":{
			"aps": {
				"alert": {
					"subtitle": "xxx"
				}
			},
			"custom_content": "{\"key\":\"value\"}"
		}
	}
}
```


### Getting parameters on the client

If you use iOS SDK integration, you can obtain custom parameters using click callback. This callback applies to the notification messages of the app in foreground, background, and shutdown status.

```objective-c
/// Unified message click callback
/// @param response will be `UNNotificationResponse` for iOS 10+/macOS 10.14+, or `NSDictionary` for earlier versions.
/// @note TPNS SDK1.2.7.1+
- (void)xgPushDidReceiveNotificationResponse:(nonnull id)response withCompletionHandler:(nonnull void (^)(void))completionHandler {
    NSLog(@"[XGDemo] click notification");
    if ([response isKindOfClass:[UNNotificationResponse class]]) {
        /// Getting messages on iOS 10 or later versions
        NSLog(@"notification dic: %@", ((UNNotificationResponse *)response).notification.request.content.userInfo);
    } else if ([response isKindOfClass:[NSDictionary class]]) {
        /// Getting messages on iOS versions earlier than 10
        NSLog(@"notification dic: %@", response);
    }
    completionHandler();
}
```

If you use Flutter plugin integration, use the following APIs in the `runner->AppDelegate->didFinishLaunchingWithOptions` method at cold startup to get parameters:
```objective-c
	- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions 
	{
			// Get the message content.
			NSDictionary *remoteNotification = [launchOptions objectForKey:UIApplicationLaunchOptionsRemoteNotificationKey];
			// Perform logical processing according to the message content.
	}
```
