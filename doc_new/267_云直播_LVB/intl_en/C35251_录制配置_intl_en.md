## Scenario

The recording feature is disabled by default for live push. If you want to set or modify it, you can do so in the recording configuration. Then, associate a specified domain name in domain name management.

## Prerequisites

You have logged in to the [LVB Console](https://console.cloud.tencent.com/live).

## Directions

1. 	Select **Domain Name Management** in the left sidebar and click **Manage** or the push domain name to be configured to enter the domain name management page.
 ![](https://main.qcloudimg.com/raw/75e7ebd2eddd55b1f836ec9cad10aa33.png)
2. 	In the **Template Configuration** tab, you can see the recording configuration information of the domain name.
![](https://main.qcloudimg.com/raw/6e8e04482179d71dea6b51bd474baaaf.png)
3. 	Click **Edit** to select a recording configuration which specifies the corresponding recording template for the playback address under the domain name.
![](https://main.qcloudimg.com/raw/1e38a01e024ab32f67dedeec201eb2aa.png)
For more information about how to configure a recording template, see [Recording Configuration](https://intl.cloud.tencent.com/document/product/267/31070).

> If you want to unbind the recording configuration from the domain name, click **Edit** in **Template Configuration**, deselect the corresponding template, and click **Save**.
>[](https://main.qcloudimg.com/raw/dd741fc787ce82ee445deab349834f3e.png)

## Getting a Recording File
The generated recording file is automatically stored in the VOD system and can be obtained in the following ways:

### VOD Console

Log in to the VOD Console and browse all recording files on the [Video Management](https://console.cloud.tencent.com/video/videomanage) page.

 ![](https://main.qcloudimg.com/raw/e371c4ca2c589c494e53ba7dbd86b0d4.png)

### Recording Event Notification

The recording callback address can be set in the console or through API calls, and you will receive the address in notification messages after the recording file is generated. After that, you can perform business processing according to the callback protocol content for recording.

The event notification mechanism is efficient, reliable, and real-time, so it is recommended to use the callback method to get recording files.

