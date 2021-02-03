## Overview
Tencent Container Registry (TCR) Enterprise Edition supports security scanning of managed container images and generating scanning reports, exposing potential security vulnerabilities in container images, and providing suggestions for fixing the vulnerabilities. Container image security is an important part of cloud-native application delivery security. Timely and secure scanning of uploaded container images and blocking application deployment based on the scanning results can effectively reduce the risk of vulnerabilities in the production environment.

The image security scanning feature is a built-in feature of image repositories. Users can actively trigger the security scanning of the container image of a specified version after uploading the container image. Also, they can configure automatic scanning at the namespace level, so that newly pushed images in the namespace will be scanned automatically after upload. The current image security scanning service is based on the open-source Clair solution, and the relevant vulnerability information is from the official CVE vulnerability library and synchronized on a regular basis.

## Prerequisites

Before using the image security scanning feature, you must perform the following operations:
- [Purchasing Instances](https://intl.cloud.tencent.com/document/product/1051/39088).
- If you are using a sub-account, you must grant the sub-account required permissions for the instance. For more information, see [Example of Authorization Solution of the Enterprise Edition](https://intl.cloud.tencent.com/document/product/1051/37248).

## Directions
### Configuring the scanning policy
1. Log in to the [TCR console](https://console.cloud.tencent.com/tcr) and select **Namespace** in the left sidebar.
2. On the "Namespace" page, click the name of the instance for which you want to enable the image security scanning feature to go to the namespace details page.
3. On the "Basic Information" page, set security scanning to **Automatic Scanning**, as shown in the figure below:
![](https://main.qcloudimg.com/raw/115b339d261ccceca8092829dc2fa390.png)

### Manually triggering scanning
#### Step 1: Preparing a container image
Refer to [Managing Image Registry](https://intl.cloud.tencent.com/document/product/1051/35488) to upload a container image and view the image on the version management page of the corresponding image repository.
<span id="step2"></span>
#### Step 2: Triggering image scanning
Select a specific image version in the image repository and click **Scan** to trigger image scanning. Then, the security level becomes "Scanning", as shown in the figure below:
![](https://main.qcloudimg.com/raw/0ffd1a76b8cca60faaec21bd37eee50e.png)


#### Step 3: Viewing the scanning results
After security scanning is completed, the security level area displays the highest level and number of vulnerabilities in the current image. You can view the details of the vulnerabilities, as shown in the figure below:
![](https://main.qcloudimg.com/raw/0d5e243a57ea0130c975fa01fa0a62b0.png)
When viewing the details of vulnerabilities, you can click a vulnerability ID to view the details of the vulnerability so that you can assess its actual impact on business, as shown in the figure below:
![](https://main.qcloudimg.com/raw/8170a2162576bed9b6e7d2d87d64929e.png)

#### Step 4: Re-triggering scanning
As the vulnerability library is updated regularly, you can refer to [Step 2: Triggering image scanning](#step2) to re-trigger the security scanning of the specified image and obtain the latest scanning results.
