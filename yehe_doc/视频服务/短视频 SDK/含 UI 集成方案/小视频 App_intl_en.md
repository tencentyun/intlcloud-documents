## Client

You can use Xcode or Android Studio to compile and debug the UGSV demo app's source code as follows. The execution effect is as shown below:
<img src="https://qcloudimg.tencent-cloud.cn/raw/667b7b4917c41cc549f4c24b9075c99a.png" width="800"/>

### Step 1. Download the app source code
Download the UGSV demo app's source code [here](https://intl.cloud.tencent.com/document/product/1069/37914).

### Step 2. Apply for the SDK license
For more information, see [License Application](https://intl.cloud.tencent.com/document/product/1069/38041).

### Step 3. Prepare the debugging environment
- **iOS**
	- Xcode 9 or later
	- iOS 12 or later
- **Android**
	- Android SDK Tools: android-sdk_26.0.2
		- minSdkVersion: 21
		- targetSdkVersion: 26

### Step 4. Compile and run
Click **Build** in Xcode or Android Studio to compile and run the source code. Tencent's test server address `http://demo.vod2.myqcloud.com/lite/` is configured in the source code, so you can quickly run the UGSV app in the debugging environment.


## Backend
The UGSV demo app depends on two backend services:
- **VOD**
VOD offers video storage and online delivery capabilities for the UGSV demo app. The basic edition of the UGSV license comes with the VOD plan and a free tier of traffic.
- **CVM**
The UGSV demo app requires a simple business server to provide capabilities such as signup, login, video list storage, and video upload signature. You can set up the server in a CVM instance and modify the logic as needed.

If you use the default server address `http://demo.vod2.myqcloud.com/lite/` in the UGSV demo app's source code, both the VOD service and list server are provided by Tencent Cloud. However, they can be used only for debugging and trial as there is a limit on the concurrent requests.
You can also set up your own backend server as follows:

### Step 1. Activate VOD
1. Log in to the [VOD console](https://console.cloud.tencent.com/vod) to activate the VOD service, which can provide video storage and online playback capabilities for the UGSV demo app.
2. In [**Callback Settings**](https://console.cloud.tencent.com/vod/callback) in the VOD console, set the callback mode to **Reliable Callback** and select **Callback on video upload completion** in **Callback Event Configuration**. The settings will take effect in about ten minutes.
![](https://qcloudimg.tencent-cloud.cn/raw/a1c7b0e5e7928bea1cc5f928c2d947d1.png)

### Step 2. Get the TencentCloud API key.
When the UGSV demo app uploads a video, it requires a Tencent Cloud key, i.e., `SecretId` and `SecretKey`, which need to be obtained from the Tencent Cloud console and configured on the business server.
1. Log in to the console and select **Products** > **Cloud Access Management**> [**Manage API Key**](https://console.cloud.tencent.com/cam/capi) to enter the **Manage API Key** page.
2. Get the TencentCloud API key. If you haven't created a key, click **Create Key** to create a pair of `SecretId` and `SecretKey`.[](id:step2_2)
![](https://qcloudimg.tencent-cloud.cn/raw/1fea6406ce16024b76ec44a6b3611251.png)

### Step 3. Deploy the backend code on the CVM instance
1. **Create a CVM instance in the [CVM console](https://console.cloud.tencent.com/cvm).**  
   ![](https://qcloudimg.tencent-cloud.cn/raw/ae4f7b90516fab3df6ad232ca2496bfe.png)
2. **Select** Custom Configuration and **enter the image marketplace to select an image.**
   ![](https://qcloudimg.tencent-cloud.cn/raw/2ba675d61f2b9afb1caf02f345109910.png)
   ![](https://qcloudimg.tencent-cloud.cn/raw/7fe72e44b822b69505967bfbae49d82d.png)
3. **Configure the disk, network, and CVM access password. Keep the password secure. Then, configure a security group.**
   ![](https://qcloudimg.tencent-cloud.cn/raw/372019bf38705fd788af995d25e83f1f.png)
4. **Log in to the created CVM instance.**[](id:step3_4)
   You can click **Log In** in the **Operation** column of the instance to access the instance through Tencent Cloud's web shell or use **PuTTY** or **SecureCRT** to log in to it over SSH.
5. **Modify the CVM instance configuration information.**
   Set `appId`, `SecretId`, and `SecretKey` in the following script to the `APPID`, `SecretId`, and `SecretKey` obtained in [step 2](#step2_2). Then, log in to the CVM instance and directly run the modified script in the instance.
    5.1 Modify and copy the following configuration locally. Then, log in to the CVM instance and paste and run the code in the console.
 ```
  echo '{
      "dbconfig":{
          "host":"127.0.0.1",
          "user":"litvideo",
          "password":"litvideo",
          "database":"db_litvideo",
          "port":3306,
          "supportBigNumbers": true,
          "connectionLimit":10
      },
      "tencentyunaccount":{
          "appid":"Your AppId",
          "SubAppId":"",
          "SecretId": "Your SecretId",
          "SecretKey": "Your SecretKey",
          "bucket":"xiaoshipin",
          "region":"ap-guangzhou"
      },
      "server":{
          "ip":"0.0.0.0",
          "port":8001,
          "reliablecb":true
      }
  }' > /home/ubuntu/vod-xiaoshipin-server/conf/localconfig.json
 ```
  5.2. In the instance, run the following command to directly start the service. The default port for starting the service is `8001`.
  - Start the service:
 ```
  cd /home/ubuntu/vod-xiaoshipin-server/;pm2 start app.js --name 'litvideo';
 ```
  - To stop or restart the service, run the following commands:
    Restart the service:
```
  pm2 restart litvideo;
```
   Stop the service:
 ```
  pm2 delete litvideo;
 ```
  5.3 View the CVM instance's public IP in [step 4](#step3_4) and enter `http://IP` in the browser to check whether the service has started successfully.

### Step 4. Replace the backend address in the terminal source code
- **iOS**: After decompressing the source code package, change the `kHttpServerAddr` in the `iOS/Demo/XiaoShiPin/TCConstants.h` file to the public IP address of your CVM instance.
- **Android**: After decompressing the source code package, change the `APP_SVR_URL` in the `XiaoShiPin_Professional_Android/Demo/ugckit/src/main/java/com/tencent/qcloud/ugckit/UGCKitConstants.java` file to the public IP address of your CVM instance.

>! If no certificate is configured for the CVM instance, then HTTP, not HTTPS, must be used in the CVM address.

At this point, the server mode of the UGSV demo app has been configured, and you can run the app to try out its features.
