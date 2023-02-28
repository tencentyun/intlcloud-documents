## Login
### What is a CVD instance?
A CVD instance is a cloud-based virtual desktop that can replace a traditional desktop. A CVD instance consists of an operating system, compute resources, storage space, and software applications. You can perform daily tasks in the instance just like on a traditional desktop.
### How do I access the CVD portal?
You can access the CVD portal URL from any supported device such as Windows PC and Mac. If your browser supports HTML5, for example, Chrome or Firefox, you can quickly open CVD resources in the browser.
### What should I do if I forgot my login password?
Click **Forgot password?** in the login portal and select a reset method based on your account conditions. You can also contact the admin to request a new password, in which case you need to change the password at the next login.
### Why does the system show that my account is locked?
In order to ensure the login security, if your admin has enabled the login verification feature, your account will be locked after consecutive failed login attempts. If the admin has enabled the self-service unlock feature, you can unlock your account by yourself through your email address or security question; otherwise, you need to contact the admin to unlock your account.
### Why can't I log in to my account?
The CVD portal supports multiple login policies. If you encounter login restrictions, contact the admin for help.

### CVD access process for end users
The CVD access process for end users is as follows:
1. As an end user, you will receive an email or SMS reminder. Follow the prompts to activate your account.
2. You need to visit the CVD portal and log in to obtain CVD resources as instructed in [Logging in to the CVD Portal](https://www.tencentcloud.com/document/product/1167/51920).
3. After obtaining the desktop list, you can select an appropriate access method based on your needs as instructed in [Opening CVD](https://www.tencentcloud.com/document/product/1167/51921).

![](https://staticintl.cloudcachetci.com/yehe/backend-news/Y6QX385_PRELIM__%E4%BA%91%E6%A1%8C%E9%9D%A2%E4%BA%A7%E5%93%81%E7%9B%AE%E5%BD%95_%E4%B8%AD%E8%AF%91%E8%8B%B1_EN-US-3.png)

## CVD Access
### What is client access?
Launch the client to open CVD. This method provides the best graphical experience. Make sure that the client has been installed. If the client prompts you to set up an account or enter a user ID, just close the prompt. If the client has already been installed on your computer, skip this step.
### Why can't I access in a browser?
Check your local network connection and make sure that your browser supports HTML5. If the problem persists, it may be because the browser has blocked pop-ups. If this is the case, allow pop-ups and try again.
### Why can't I download the client?
If you click **Download client** but nothing happens, it is because your browser blocks pop-ups. You will receive a message from your browser stating that pop-ups have been blocked. Pop-ups can be allowed or blocked by changing the browser settings.
### I downloaded the client, but why can't I start my cloud desktop on the client?
Make sure that the client has been installed, and then click **Client access** again. The CVD portal will automatically launch the client plugin to open the cloud desktop.
### How long does it take for the desktop to become available after I log in?
If your cloud desktop is already running, you can connect to it almost instantly. If it has been shut down or restarted, you need to start it first or wait for the restart to complete before you can access it.
### What should I do if an error is reported when trying to access my desktop?
The CVD instance may be damaged due to misoperations. You can contact the admin for repair.
### What is browser access?
You can quickly open and use a CVD instance through a web browser that has HTML5 capability, with no need to download and install the client. However, there are some restrictions in this mode; for example, local files uploaded to the cloud desktop are limited to 2 GB, and files downloaded from the cloud desktop to your local device are limited to 250 MB, and you cannot use some device driver mappings.

## CVD Use
### Can I personalize my cloud desktop?
By default, you can change the wallpaper, icons, and shortcut keys of the desktop, and these settings will be saved. The CVD admin controls the permissions that allow you to personalize the desktop.
### How do I transfer files between my local device and the cloud desktop?
You can transfer files between the cloud desktop and your local device by copying and pasting. If you cannot perform this operation, contact the CVD admin and ask them to change the security policy.
### Can I access files on the local device from the cloud desktop?
You can see the local disk in the file explorer in the CVD instance. If you cannot perform this operation, contact the CVD admin and ask them to change the security policy.
### Why can't my cloud desktop recognize USB devices or peripherals such as flash drives?
CVD supports plug-and-play for peripheral devices. If you cannot perform this operation, contact the CVD admin and ask them to adjust the security policy for peripheral devices.
### Does CVD support dual-monitor display?
Yes. In browser access mode, select multi-monitor on the toolbar to use a dual-monitor display. In client access mode, connect the two monitors to the CVD instance.
### Can I access multiple cloud desktops at the same time?
Yes, if you have two or more cloud desktops, you can access and operate all of them at the same time.
### How do I install applications in a cloud desktop?
When using a cloud desktop, you can install applications just as you normally would using application installation packages. You can transfer installation packages to the desktop or download them from the internet. If applications that change the network configuration are involved, please contact Tencent Cloud technical support for assessment.
>?Using network tools such as VPN and firewall may make CVD connections abnormal. Therefore, install and use them with caution.

### Can I access the internet from my cloud desktop?
Internet access is subject to the configuration of the admin. Contact the admin for policy adjustment if necessary.
### Will my temporary data be saved when I disconnect or close the desktop UI?
The CVD instance runs in the cloud and will save your temporary data when you close the connection. You can see the saved temporary data the next time you log in to your cloud desktop.
### Will my temporary data be saved when I shut down or restart the desktop?
When you shut down or restart the desktop, unsaved temporary data will be discarded. Therefore, be sure to save the files before performing such operations.
### Does CVD support devices with high DPI displays?
CVD will adaptively adjust the resolution to match the DPI settings of the local device for an optimal user experience.
### Does CVD support resolution adjustment?
In browser access mode, you can specify the desktop resolution on the toolbar. In client access mode, CVD adaptively adjusts the resolution according to the window size and local device resolution to guarantee an optimal user experience.
### Does CVD support touchscreen devices?
Yes. CVD delivers a good interactive experience on touchscreen devices. You can use two- or three-finger gestures to open the mouse and keyboard.
### How do I view the real-time network quality in CVD?
A network monitoring tool is provided on the toolbar at the bottom-right corner of the desktop, which can display the real-time RTT and latency and remind you of network quality changes of the local device through colors.
### What should I do if a scroll bar is displayed on the desktop when I access CVD from a browser?
Your browser's display settings may limit the size of the virtual desktop window. If this happens, your virtual desktop display may automatically start scrolling when it becomes larger than the window size. Go to your browser settings and configure autofit or autosize.

## Notes
### Default port (80)
CVD communicates with backend management components over port 80, which is occupied by default. When using CVD, avoid using port 80 for applications; otherwise, CVD cannot be connected.
### VPN usage
Be cautious when using VPN and firewall tools in CVD, which may make CVD connections abnormal.
### Network configuration
Do not disable the ENI or change the route in CVD; otherwise, CVD cannot be connected.
### Data saving
Save data regularly when using the cloud desktop to avoid unnecessary losses caused by accidental data loss and corruption.

