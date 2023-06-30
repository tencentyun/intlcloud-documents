
## Overview
In Tencent Container Registry (TCR) Enterprise Edition, a namespace is used to manage multiple associated image repositories and Helm charts. It does not directly store container images or Helm charts, but can map to teams, product projects, or individuals in an enterprise.

TCR Enterprise Edition instances are exclusive for an enterprise. Therefore, you do not need to worry that a namespace may be occupied by other users when creating the namespace. However, if you create a namespace in a TCR Personal Edition instance, the name of the namespace must be different from that of any existing namespaces. This document describes how to create and manage a namespace in a TCR Enterprise Edition instance.


## Prerequisites

Before creating and managing a namespace in a TCR Enterprise Edition instance, complete the following preparations:
- [Purchasing Instances](https://intl.cloud.tencent.com/document/product/1051/39088).
- If you are using a sub-account, you must have granted the sub-account required permissions for the instance. For more information, see [Example of Authorization Solution of the Enterprise Edition](https://intl.cloud.tencent.com/document/product/1051/37248).

## Directions
### Creating a namespace
1. Log in to the [TCR console](https://console.cloud.tencent.com/tcr) and select **Namespace** on the left sidebar.
2. On the **Namespace** page, you can view the namespace list of the current instance. To change the instance, select the desired instance name from the **Instance** drop-down list at the top of the page.
3. Click **Create**. In the **Create a Namespace** window, configure the name and access level of the namespace as shown below:
![](https://main.qcloudimg.com/raw/48fbf6c0aeafc5614e67fde1bbc0c531.png)
 - **Associated Instance**: the currently selected instance, to which the created namespace belongs.
 - **Name**: the namespace name. It is a string of 2-30 characters. The name can only contain lowercase letters, number, and separators, which are periods (.), underscores (_), and hyphens (-). It cannot start or end with a separator or contain several consecutive separators. We recommend that you set this parameter to the name of an enterprise team or product project. You can also set this parameter to a personal name and use this namespace for personal testing. The namespace names must be unique in an instance.
 - **Access Level:** you can select **Private** or **Public**. The default value is **Private**.
 If you set this parameter to "Public", all image repositories and Helm charts in the namespace are public repositories. If anonymous access is also enabled for this instance (which is enabled by default), any clients in the allowlist can pull images and Helm charts without having to log in. You can modify **Access Level** after the namespace is created.
4. Click **OK**.
5. After the namespace is created, you can view the namespace on the "Namespace" page. Then, you can perform the following operations to manage the namespace, as shown in the figure below.
![](https://main.qcloudimg.com/raw/f9e8a249b7d79068cea2a83d1cdb44fa.png)


### Changing the access level
1. Click the namespace that you want to change the access level and go to its "Basic Information" page.
2. On the "Basic Information" page, click <img src="https://main.qcloudimg.com/raw/8f25ce6088a7b046c4cae311b8a5293e.png" style="margin:-2px 0px"> next to the **Access Level**. Change the public or private attribute of the namespace in the pop-up window.
 >!After the access level is changed, all the image repositories and Helm charts in the namespace immediately inherit this attribute. **Do not change a private namespace to a public namespace unless necessary**.
 >

### Changing the security scan mode
1. Click the namespace that you want to change the access level and go to its "Basic Information" page.
2. Click <img src="https://main.qcloudimg.com/raw/8f25ce6088a7b046c4cae311b8a5293e.png" style="margin:-2px 0px"> next to the **Security Scan** to change the security scan mode for container images in this namespace. You can set the security scan mode to **Manually Scan** or **Auto-scan**.
>!Changing the security scan mode does not affect the existing security scan results.
>
 - **Manually Scan**: to perform a security scan on a specified container image and view the result, you need to go to the **Image Repository** page, select the image, and click **Scan** on the **Tag Management** tab.
 - **Auto-scan**: an automatic security scan is triggered when a new image is pushed to any image repository in the current namespace.


### Configuring deployment security
An Enterprise Edition instance can block the deployment of high-risk images. For more information, see [High-Risk Image Deployment Blocking]().

### Deleting a namespace
To delete a namespace, select it and click **Delete** next to it. To prevent important data from being deleted by mistake, a namespace that still contains image repositories or Helm charts cannot be deleted.
