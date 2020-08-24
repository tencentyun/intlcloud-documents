## Problem description
When you attempt to [log in to a Windows instance via VNC](https://intl.cloud.tencent.com/document/product/213/32496) or [log in to a Linux instance via VNC](https://intl.cloud.tencent.com/document/product/213/32494), you may not be prompted for a login, but encounter a **black screen** or view only the **blue Windows logo**, as shown below:
![](https://main.qcloudimg.com/raw/b30848087c48d5d5a2f83e08cfb5ca89.png)

## Possible causes
1. Your GPU instance is installed with a graphics driver.
When you log in to a GPU instance via VNC, the VGA device emulated by QEMU is accessed by default to obtain the framebuffer of the operating system for a login. After you install a graphics driver on the GPU instance, the framebuffer is no longer handled by the VGA device. As a result, you cannot log in to the operating system via VNC.
2. The operating system failed to start due to other causes. For example, third-party software that conflicts with the operating system is installed on the GPU instance.

## Solution
1. If the GPU instance is installed with a graphics driver, install a VNC server on the instance so that you can log in to the GPU instance via a local VNC client.
You need to obtain the VNC server and client installation packages by yourself.
2. Check installed third-party software and analyze why the software leads to the login failure.
We recommend that you uninstall the conflicting third-party software or reinstall the operating system.

