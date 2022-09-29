CAR provides a way to capture the window image of the cloud application for users. If you need to use an adaptive frontend resolution, we recommend you use this mode. You need to provide the application class name and title (the title is the window title during application startup). If the window title isn't customized during development, the window title after `Demo.exe` starts will be `Demo`. If your application is a UE application, enter `UnrealWindow` for the **Class name**.

This document describes how to use WinSpy to capture the application class name and title for the startup parameter configuration.

## Directions
1. Download [WinSpy](https://sourceforge.net/projects/winspyex/files/latest/download) to capture the window attributes.
2. Unzip WinSpy, and open WinSpy32.exe or WinSpy64.exe based on your system type. 
![](https://qcloudimg.tencent-cloud.cn/raw/d35860773c6750e9d7af1559c1e1895c.png) 3. Open the application to capture (such as Google Chrome), click and move the Finder Tool (shown in the red box) to the application window, and release it.
![](https://qcloudimg.tencent-cloud.cn/raw/5ba80671990e21560fbf1c22686eba5d.png)
4. WinSpy captures the window attributes.
	- Title: Window title of your application (such as `CAR - Google Chrome`)
	- Class: Application class name (such as `Chrome_WidgetWin_1`)
![](https://qcloudimg.tencent-cloud.cn/raw/9e224f6b0a97bc6f7a8b44e6eae9b985.png)
5. Modify the startup parameter configuration according to the captured attributes.
![](https://qcloudimg.tencent-cloud.cn/raw/f8b5b84a85fbc7402716cca9ffabb284.png)