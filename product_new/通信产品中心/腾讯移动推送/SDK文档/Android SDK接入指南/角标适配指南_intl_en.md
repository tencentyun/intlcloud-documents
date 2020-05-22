For Android phones, the opened badge capabilities vary by vendor. TPNS' support for push badge is as detailed below for your reference:

## Overview
| Vendor | Support for Display of Badge/Red Dot | Configuration Required | Badge/Red Dot Display Rule |
|-----|------------------------------|--------------------|-----------------------|
| Huawei | Badge | Yes | For more information, please see the Huawei phone badge adaptation guide below |
| Mi | Badge | No | It is compliant with the default system logic. The number of notifications in the notification bar is detected, and the badge number will increase/decrease by one accordingly |
| Meizu | Red dot | No | It is compliant with the default system logic, and only the red dot can be displayed. If there is a notification, a red dot will be displayed, and vice versa |
| OPPO | Red dot | No | You can manually enable the display of red dot in notification settings, which is compliant with the default system logic. If there is a notification, a red dot will be displayed, and vice versa; <br>Display of the notification number is available only to specified applications such as QQ and WeChat. If you need to use it, please apply for permission. No adaption instructions are provided currently</br> |
| Vivo | Neither | No | This feature is available only to specified applications such as QQ and WeChat. If you need to use it, please apply for permission. No adaption instructions are provided currently |



## Huawei Phone Badge Adaptation Guide

### Use limits
Badge display is supported for Huawei phones on EMUI 8.0 or above.
Limited by the openness of Huawei phone badge capabilities, the badge feature varies by push scenario as detailed below. Please use the Huawei phone badge feature as instructed.

| Push Form | Badge Capability | Implementation Method |
|:-:|:--:|:--:|
| Notification through Huawei channel | The badge number automatically increases by one or does not change when a push message is received | This feature can be set in the console or through the push API keyword |
| Notification through TPNS channel | When the user clicks or dismisses a notification pushed through TPNS channel, the badge number can automatically decrease by one, which is not supported for notifications pushed through the Huawei channel | This feature can be adapted through the TPNS SDK with no additional settings required |
| Passthrough message | You can process the increase/decrease logic by yourself | An open API of the TPNS SDK can be called to implement this feature |



### Implementation method
#### Applying for permission to set in-app badge
To implement the correct badge modification effect, please first apply for the Huawei phone badge read/write permission for your application by adding the following permission configuration under the `manifest` tag in the application's `AndroidManifest.xml` file:

```xml
<uses-permission android:name="com.huawei.android.launcher.permission.CHANGE_BADGE "/>
```
#### Setting notification delivery badge
You can implement the badge for push message delivery in the notification bar on the push page in the console or through the REST API. You need to enable the Huawei channel in the console and enter the `Activity` class of the application entry corresponding to the homescreen icon in parameter configurations, such as `com.test.badge.MainActivity`; otherwise, the badge settings will not take effect. The settings are as shown below:
![](https://main.qcloudimg.com/raw/815a22b60155a70557bdd0d0bc4c63a5.png)

#### Setting badge rules
**Method 1:** set on the push page in the console
![](https://main.qcloudimg.com/raw/2db6d9f0905649cd7d094a25b7745f71.png)
**Method 2:** set through the `Push` API
  In the push message body, add the `badge_type` field with the following attributes under `body.message.android`:
	
| Parameter Name | Type | Parent Project | Required | Default Value | Description |
 | :--:|:--:|:--:|:--:|:--:|:---:|
 | badge_type|int|android| No | -1 | Notification badge, which takes effect only for Huawei devices. Valid values: -2: automatically increase by one, -1: unchanged |
	
Sample message body:
```json
  {
      "audience_type": "token",
      "expire_time": 3600,
      "message_type": "notify",
      "message": {
          "android": {
              "badge_type": -2,
              "clearable": 1,
              "ring": 1,
              "ring_raw": "xtcallmusic",
              "vibrate": 1,
              "lights": 1,
              "action": {
                  "action_type": 1,
                  "activity": "com.qq.xg4all.JumpActivity",
                  "aty_attr": {
                  "if": 0,
                  "pf": 0
              }
              }
          },
          "title": "android test",
          "content": "android test 21"
      },
      "token_list": [
        "01f6ac091755a79015b4a30c9c4c7ddba1ea"
      ],
      "multi_pkg": true,
      "platform": "android",
  }
```

#### Setting passthrough message badge

You can implement the badge number increase/decrease logic of TPNS passthrough messages by calling the corresponding API provided in the SDK v1.1.6.0 or above.
You can get passthrough message content by inheriting ```com.tencent.android.tpush.XGPushBaseReceiver``` and implementing the callback API ```onTextMessage(Context context, XGPushTextMessage message)```. You can call the following API in this callback method to increase the badge number by one:
```java
/**
     * Huawei phone badge modification API
     *
     * @param context   Application context
     * @param changeNum   Changed number, which is incremental during modification; for example, if the badge number 5 and the input parameter is 1, it will be increased to 6
     *		Valid values: 1: the badge number increases by one; -1: the badge number decreases by one
     */
XGPushConfig.changeHuaweiBadgeNum(Context context, int changeNum);
```

Example: when a passthrough message is received, call `XGPushConfig.changeHuaweiBadgeNum(context, 1)` to increase the badge number by one; when the message badge needs to be dismissed, call `XGPushConfig.changeHuaweiBadgeNum(context, -1)` to decrease the badge number by one.


#### Resetting badge number
As the badge number set for notifications through the Huawei channel cannot automatically decrease by one to respond to user's click/dismissal event, you are recommended to call the following API to reset the application badge number upon application start or at other appropriate times:

```java
/*
     * Resetting Huawei phone badge number
     * You are recommended to reset the badge number upon application start or at other appropriate times
     * @param context   Application context
     */
XGPushConfig.resetHuaweiBadgeNum(Context context)
```




