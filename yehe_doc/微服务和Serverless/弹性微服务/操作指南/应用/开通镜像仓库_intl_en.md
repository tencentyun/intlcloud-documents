
## Overview

This document describes how to create a Personal Edition image repository in the TKE console to receive container images built or pushed by TEM.



## Directions

1. Log in to the TKE console and enter the **Image Repositories** >**[Personal Edition](https://console.cloud.tencent.com/tke2/registry/user/self?rid=1)** page. If you are accessing this service for the first time, the initialization page will be displayed.
![](https://main.qcloudimg.com/raw/27260978f7b766e018a5a885ff6b5242.png)
2. Select the region of the application environment.
3. Set a password for your personal container image repository, which can be used to log in to the repository through `docker login`.
4. After the personal image repository is activated, you can return to the [TEM console](https://console.cloud.tencent.com/tem) to create an application.
	- If you select **Image** > **Auto Create** for package upload, the image you upload will be pushed to the namespace created by TEM.
	- If you select **JAR** or **WAR** for package upload, TEM will automatically build a container image for you and push it to the namespace created by TEM.
	

![](https://main.qcloudimg.com/raw/c30fb85a7d311421a07ca336c8ac9f6a.png)


