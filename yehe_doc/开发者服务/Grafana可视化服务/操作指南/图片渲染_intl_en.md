TCMG is preconfigured with a remote image rendering server, so you can use the image rendering capabilities without performing any additional operations. This document lists common use cases of image rendering.

## Prerequisites
1. Log in to the [TCMG console](https://console.cloud.tencent.com/monitor/grafana).
2. In the instance list, find the target instance and click the **Grafana icon <img src="https://main.qcloudimg.com/raw/978c842f0c093a31df8d5240dd01016d.png" width="2%">**.
3. Enter your Grafana account and password and click any dashboard in Grafana.



## Sharing Dashboard

1. On any dashboard, click **Title** and select **Share** in the pop-up window.
   ![](https://qcloudimg.tencent-cloud.cn/raw/5762b723909024dab95eed1a9eed577d.png)
2. Click **Direct link rendered image** at the bottom of the pop-up window.
   ![](https://qcloudimg.tencent-cloud.cn/raw/49479bdfbb036b8cc69a7adb0f36fd6f.png)
3. Get the address of the dashboard rendered as an image and share it.
   ![](https://qcloudimg.tencent-cloud.cn/raw/324a5b8f710948d446525b8c550a18ad.png)


## Setting Alarm
Similarly, you can select **Include Image** in **Notification settings** to render the alert dashboard as an image as shown below:
	![](https://qcloudimg.tencent-cloud.cn/raw/65eaa9e1ab618bc42c0f634c652ab250.png)

>?Remote image rendering is not supported for dashboards with data sources of the `Browser` type.
