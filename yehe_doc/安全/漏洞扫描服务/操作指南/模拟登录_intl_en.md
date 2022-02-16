## Overview
If some or all pages or features of your website can be accessed only after login, we recommend you set a cookie to simulate website login for comprehensive vulnerability scan. Currently, VSS can simulate login by setting a cookie with the value of successful login, and the backend will periodically bring the set cookie to access the website, so as to ensure that the cookie won't expire.
## Directions
### Settings of simulated website login
1. Log in to the [VSS console](https://console.cloud.tencent.com/vss) and click **Asset Management** on the left sidebar to enter the asset management page.
2. On the asset management page, click **Website** and find the asset for which to simulate a login.
3. Click **Set** in the **Simulated Login** column of the target asset, and the **Simulated Login** window will pop up.
![](https://qcloudimg.tencent-cloud.cn/raw/86edc8eb3fb13daae126505c09aaddeb.png)
4. In the **Simulated Login** window, enter the correct cookie value (see [How to get cookie value](#Cookie)) and click **Save**.
![](https://qcloudimg.tencent-cloud.cn/raw/f990d1776773d550eb926766bde258b5.png)
5. The simulated website login is successfully set.


### [How to get cookie value](id:Cookie)
1. Log in to your website in Chrome, access a page that requires login, and press F12 or right-click on the page and select **Inspect**.
2. Select **Network** > **All** in DevTools that appears and refresh the page.
![](https://main.qcloudimg.com/raw/c4bb8a03b0167c989ce6a4837f1340f9.png)
3. Click the first network request.
![](https://main.qcloudimg.com/raw/dc68b9a94aca03731fb0d8819ba860e0.png)
4. Find the **Cookie** item in **Headers** and copy the cookie value.
![](https://main.qcloudimg.com/raw/b96eea46b74b2355e185ec48a3239dee.png)
