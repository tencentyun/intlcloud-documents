Tencent Push Notification Service (TPNS) is a professional mobile application push platform that can deliver tens of billions of notifications and messages within seconds. It supports both Android and iOS systems. You can embed SDK, API calls, or web-based visuals to send pushes to specific users, improving user activity and engagement. Real-time push effect data are also available.



## Feature Overview

The SDK for Android provided by TPNS contains APIs for clients to implement message pushing. It is mainly used to:

- Provide two types of push (notification and message) for easy use.
- Bind accounts, tags, and devices, so you can push messages to specific user groups and have more varied push methods;
- Report the number of clicks, i.e., how many times a message is clicked by users.
- Provide the multi-vendor channel integration feature for you to integrate push services from multiple vendors.


## SDK Description

The following files can be extracted from the package downloaded from the official website:
![](https://main.qcloudimg.com/raw/591f29cd6788b791c5e599707d0a4602.png)

#### Five extracted folders in root directory

- `Demo` folder: contains the TPNS official demo. You can refer to it for relevant configurations.
- `flyme-notification-res` folder: contains resource files for the Meizu channel, which are used to enable compatibility with Meizu phones on lower versions. For users of Meizu phones on Flyme 6.0 or below, the corresponding files should be copied to the `res` directory of the application.
- `libs` folder: contains the jar and so files of TPNS push.
- `Other-Platform-SO` folder: contains the so files for other less commonly used CPU architectures.
- `Other-Push-jar`: contains the jar packages encapsulated by TPNS for Huawei, Meizu, Mi, OPPO, Vivo, and FCM channels.

#### libs directory description
![](https://main.qcloudimg.com/raw/11b427ff202da51706d87e78a2cc6258.png)
- android-support-v4.jar: compatible package provided by Google, which is compatible with Android1.6 and above.
- jg-filter-sdk-1.1.jar: jar package for KingKong scan, which is required for any products that uses a Tencent SDK.
- tpns-baseapi-sdk-x.x.x.x.jar: certain underlying common APIs provided by TPNS push.
- tpns-core-sdk-1.2.2.0.jar: core module code of the TPNS SDK, which contains all the classes, APIs, and components used externally.
- tpns-mqttchannel-sdk-1.2.2.0.jar: MTQQ-based communication feature implemented at upper layers of TPNS. The persistent connection is made independent in one process.
- tpns-mqttv3-sdk-1.2.2.0.jar: MQTT protocol package modified by TPNS, which provides the multi-vendor channel integration feature for you to integrate push services from multiple vendors.


## Flow Description

### Device registration flow

The device registration flow is as shown below. For specific API methods, please see the [API documentation](https://intl.cloud.tencent.com/document/product/1024/30715).
![](https://main.qcloudimg.com/raw/e795ce8ea14a01e064ba69a98cf43c5a.png)



### Device unregistration flow

The device unregistration flow is as shown below. For specific API methods, please see the [API documentation](https://intl.cloud.tencent.com/document/product/1024/30715).
![](https://main.qcloudimg.com/raw/55ffc2d38b879f247ec7980d4ee44ef1.png)


### Account flow

The account flow is as shown below. For specific API methods, please see the [API documentation](https://intl.cloud.tencent.com/document/product/1024/30715).
![](https://main.qcloudimg.com/raw/3034b127932ecaa57ac1bb3adb91a9ec.png)



### Tag flow

The tag flow is as shown below. For specific API methods, please see the [API documentation](https://intl.cloud.tencent.com/document/product/1024/30715).
![](https://main.qcloudimg.com/raw/1dfe940d69878cc1c22a1466b8954d23.png)

### User attribute flow

The user attribute flow is as shown below. For specific API methods, please see the [API documentation](https://intl.cloud.tencent.com/document/product/1024/30715).
![](https://main.qcloudimg.com/raw/8941cba3ed40b4ff02d957e6c2332d64.png)
