# Demo Test

## Downloading the Demo

1. The demo project can be downloaded [here](http://ixg.qq.com/ctr_index/download) in the TPNS SDK documentation.

2. Register a test app at TPNS' website. The app name can be anything, but the package name must be com.qq.xgdemo. Then, get the AccessID and Accesskey of the registered app.

![](https://main.qcloudimg.com/raw/ced8a570f4750b2cec2b27ad72ee3763.png)

2. Import the demo project in the SDK to the corresponding development tool. Modify the node in the project where TPNS ID and key are configured.

**[AndroidStudioDemo]**

Configure the ACCESSID and ACCESSKEY obtained by registering the test app to the ```manifestPlaceholders``` node in the ```build.gradle``` file under the app module in the demo project. See the figure below:

![](https://main.qcloudimg.com/raw/eda8be7a6d13961b5711ef03194b1041.png)

**[Eclipse]**

Configure the AccessID and Accesskey obtained by registering the test app to the ```<mata-data>``` node in  ```AndroidManifest.xml``` in the demo project. See the figure below:

![](https://main.qcloudimg.com/raw/66093813f952a1c412bcd2b1daf45d6d.png)

## Running the Demo

Filter the TPNS log (with the tag "TPush") in the log console, and the following log entries indicate that TPNS is successfully registered:

```xml
10-09 20:08:46.922 24290-24303/com.qq.xgdemo I/XINGE: [TPush] get RegisterEntity:RegisterEntity [accessId=2100250470, accessKey=null, token=5874b7465d9eead746bd9374559e010b0d1c0bc4, packageName=com.qq.xgdemo, state=0, timestamp=1507550766, xgSDKVersion=3.11, appVersion=1.0]
10-09 20:08:47.232 24290-24360/com.qq.xgdemo D/TPush: The registration succeeded, and the device token is: 5874b7465d9eead746bd9374559e010b0d1c0bc4
```
## Push Testing

Get the device token in the log and launch the TPNS console to create a push:

![](https://main.qcloudimg.com/raw/b8c721a2d3dc3d92ffe9c7fe326ce727.png)
