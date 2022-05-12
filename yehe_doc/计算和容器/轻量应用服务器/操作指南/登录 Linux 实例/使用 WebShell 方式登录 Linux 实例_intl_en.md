## Overview
WebShell is a login method recommended by Tencent Cloud. You can use it to directly log in to a Linux instance quickly. It has the following strengths:
- Supports copy and paste.
- Supports scrolling with mouse wheel.
- Supports Chinese input.


<dx-alert infotype="explain" title="">
- When you create a Linux Lighthouse instance, it will be bound to a key by default. The username of the key is `lighthouse`, which has the root privileges.
- When you use WebShell to log in to a Linux instance, the system will use the key of the `lighthouse` username for login by default.
</dx-alert>



## Supported Systems
Windows, Linux, or Mac OS.

## Prerequisites

- Before login, confirm that the firewall of the instance has passed port 22 (which has been enabled by default when the instance was created).

## Directions

1. Log in to the [Lighthouse console](https://console.cloud.tencent.com/lighthouse/instance/index).
2. Find the target instance in the server list and select a login method as desired.
 - Click **Log in** in the instance card in the server list.
![](https://qcloudimg.tencent-cloud.cn/raw/11148d430192dcc14bb2f55d039d32d5.png)
 - Click the instance card to enter the instance details page and click **Log In** in **Remote Login** or in the top-right corner of the page.
![](https://qcloudimg.tencent-cloud.cn/raw/492865c871113a6fdc0cc23766c67eae.png)
 - For an instance created by using an [application image](https://intl.cloud.tencent.com/document/product/1103/41261), you can select **Pre-installed application** on the instance details page and then click **Log In** in **Pre-installed software** or in the top-right corner of the page.
![](https://qcloudimg.tencent-cloud.cn/raw/e57fd4363e3fbad62f902def7a2e8a21.png)
After successful login, you can set up low-load lightweight applications with a moderate number of access requests, such as small and middle-sized websites, web applications, blogs, forums, mini programs, mini games, ecommerce, cloud storage, image hosting, and cloud-based development, testing, and learning environments.

## Related Operations
### Enabling/Disabling WebShell-based quick login


<dx-alert infotype="explain" title="">
After a Lighthouse instance is created successfully, the WebShell-based quick login feature will be enabled by default. You can disable or enable it again in the following steps:
</dx-alert>


1. Log in to the [Lighthouse console](https://console.cloud.tencent.com/lighthouse/instance/index).
2. Find the target instance in the server list and enter the instance details page.
3. In **Quick login** in **Remote login**, you can **enable** or **disable** WebShell-based quick login as needed:
 - **Close**: If you don't need to use quick login, you can disable it.
<dx-alert infotype="notice" title="">
- After quick login is disabled, you can still use the local SSH client to remotely log in to the instance. You can also enable quick login again.
- After quick login is disabled, the public key (stored under the `lighthouse` user of the operating system by default) of the default system key won't be deleted at the same time. You can delete the public key by yourself. However, if it is deleted, quick login will not take effect after being enabled again.
</dx-alert>
 - **Enable**: After quick login is enabled, you can use the default system key to quickly log in to the instance through WebShell in a browser.
<dx-alert infotype="notice" title="">
Confirm that the public key (stored under the `lighthouse` user of the operating system by default) of the default system private key is not deleted; otherwise, the quick login feature won't work after being enabled.
</dx-alert>



