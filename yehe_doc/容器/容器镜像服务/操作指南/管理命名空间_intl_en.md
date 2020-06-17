
## Scenario
In Tencent Container Registry (TCR), a namespace is used to manage multiple associated image repositories and Helm charts. It does not directly store container images or Helm charts, but can map to teams, product projects, or individuals in an enterprise.

TCR Enterprise Edition instances are exclusive for an enterprise. Therefore, you do not need to worry that a namespace may be occupied by other users when creating the namespace. However, if you create a namespace in a TCR Personal Edition instance, the name of the namespace must be different from that of any existing namespaces. This document describes how to create and manage a namespace in a TCR Enterprise Edition instance.


## Prerequisites

Before creating and managing a namespace in a TCR Enterprise Edition instance, complete the following tasks:
- [Create an Enterprise Edition instance](https://intl.cloud.tencent.com/document/product/1051/35486).
- If you are using a sub-account, grant the sub-account operation permissions for the corresponding instance in advance. For more information, see Examples of Enterprise Edition Authorization Schemes.

## Procedure
### Creating a namespace
1. Log in to the [TCR console](https://console.cloud.tencent.com/tcr) and select **Namespace** in the left sidebar.
2. On the "Namespace" page, you can view the namespace list of the current instance. To change the instance, select the desired instance name from the **Instance Name** drop-down list at the top of the page.
3. Click **Create**. In the "Create a Namespace" window, configure the name and access level of the namespace, as shown in the figure below.

 - **Associated Instance**: currently selected instance, to which the created namespace belongs.
 - **Name**: name of the namespace. It is a string of 2-30 characters. The name can only contain lowercase letters, number, and separators, which are periods (.), underscores (_), and hyphens (-). It cannot start or end with a separator or contain several consecutive separators. We recommend that you set this parameter to the name of an enterprise team or product project. You can also set this parameter to a personal name and use this namespace for personal testing.
 - **Access Level**: you can select either "Private" or "Public". The default value is "Private".
 If you set this parameter to "Public", all image repositories and Helm charts in the namespace are public repositories. If anonymous access is also enabled for this instance (which is enabled by default), any clients in the whitelist can pull images and Helm charts without having to log in. You can modify **Access Level** after the namespace is created.
4. Click **Confirm** to create the namespace.
After the namespace is created, you can view the namespace on the "Namespace" page. Then, you can perform the following operations to manage the namespace. See the figure below.


### Changing the access level
 In the "Access Level" area of a specified namespace, click <img src="https://main.qcloudimg.com/raw/5ba06490364505efc4d698e3adb1064e.png" style="margin:-6px 0px"> in front of "Public" or "Private" to change the public or private attribute of the namespace.
 > After the access level is changed, all the image repositories and Helm charts in the namespace immediately inherit this attribute. **Do not change a private namespace to a public namespace unless necessary.**
 >
 - <img src="https://main.qcloudimg.com/raw/5ba06490364505efc4d698e3adb1064e.png" style="margin:-6px 0px">: the access level of the namespace is private.
 - <img src="https://main.qcloudimg.com/raw/d31873587cb976e1429768b2dc2b0e16.png" style="margin:-6px 0px">: the access level of the namespace is public.

### Changing the security scan mode
Click <img src="https://main.qcloudimg.com/raw/5ba06490364505efc4d698e3adb1064e.png" style="margin:-6px 0px"> under "Security Scan" of a specified namespace to change the security scan mode for container images in this namespace. You can set the security scan mode to **Manual** or **Automatic**.
> Changing the security scan mode does not affect existing security scan results.
>
- <img src="https://main.qcloudimg.com/raw/5ba06490364505efc4d698e3adb1064e.png" style="margin:-6px 0px">: the security scan mode is set to **Manual**. To perform a security scan on a specified container image and view the result, go to the "Image Repository" page, select this image, and click **Scan** on the **Tag Management** tab.
- <img src="https://main.qcloudimg.com/raw/d31873587cb976e1429768b2dc2b0e16.png" style="margin:-6px 0px">: the security scan mode is set to **Automatic**. An automatic security scan is triggered when a new image is pushed to any image repository in the current namespace.

### Deleting a namespace
To delete a namespace, select a namespace and click **Delete** next to the namespace. To prevent important data from being deleted by mistake, a namespace that still contains image repositories or Helm charts cannot be deleted.
