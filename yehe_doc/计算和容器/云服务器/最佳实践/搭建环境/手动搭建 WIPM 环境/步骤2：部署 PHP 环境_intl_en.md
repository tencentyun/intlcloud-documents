## Scenario

This document uses a CVM running Windows Server 2012 R2 as an example to describe how to configure PHP 5.3 and earlier versions or versions later than 5.3 in a Windows CVM.


## Prerequisites

- You have logged in to the Windows CVM and added and installed the IIS role in the CVM. For more information, see [Step 1: Installing and Configuring IIS](https://intl.cloud.tencent.com/document/product/213/2755).
- You have obtained the public IP address of the Windows CVM. For more information, see [Obtaining the Public IP Address of an Instance](https://intl.cloud.tencent.com/document/product/213/17940).

## Directions

<span id="jump1"></span>
### Installing PHP 5.3 or earlier

>! The [PHP official website](http://windows.php.net/download/) no longer provides the installation packages for versions earlier than PHP 5.2. If you require a version earlier than PHP 5.2, search for and download it from the CVM. Alternatively, download it locally and then upload the installation package to the CVM. For more information on how to upload files to a Windows CVM, see [Uploading Files Through MSTSC to a Windows CVM from Windows](https://intl.cloud.tencent.com/document/product/213/2761). The following procedure uses PHP 5.2.13 as an example.
> 
1. Open the PHP installation package in the CVM.
2. Click **Next**.
3. On the "Web Server Setup" page, select **IIS FastCGI** and click **Next**, as shown in the following figure:
![](https://main.qcloudimg.com/raw/c5fc89547b020e6ec943732d16186a7b.png).
4. Complete PHP installation as prompted.
5. Create a PHP file such as `hello.php` in `C:/inetpub/wwwroot`.
6. In the created `hello.php` file, add the following code and save the file.
```
	<?php
	echo "<title>Test Page</title>";
	echo "hello world";
	?>
```
7. On the desktop, open the browser and visit `http://<Public IP address of the Windows CVM>/hello.php` and check whether the environment is successfully configured.
If the page shown below appears, the configuration was successful.
![](https://main.qcloudimg.com/raw/0cdefc8707c4402e9ae5f9e6fa523ae1.png)

<span id="jump"></span>
### Installing a version later than PHP 5.3

Versions later than PHP 5.3 do not have an installation package and are installed by using a zip file or debug pack. The following demonstrates how to install PHP in a Windows Server 2012 R2 environment by using a zip file.

#### Downloading software

1. In the CVM, go to the [PHP official website](http://windows.php.net/download/) and download the compressed PHP installation package, as shown in the following figure:
>! To run PHP under IIS, you must select the x86 installation package for Non Thread Safe. If your server is running Windows Server 32-bit (x86), replace IIS with Apache and select the x86 installation package for Thread Safe.
>
![](https://main.qcloudimg.com/raw/b54dcb237ae24673cd592561ffc91bc0.png)
2. Based on the name of the downloaded PHP installation package, download and install the Visual C++ Redistributable installation package.
The following table lists the Visual C++ Redistributable installation packages that need to be downloaded and installed for the PHP installation package.
<table>
<tr><th>PHP Installation Package Name</th><th>Download Address of the Visual C++ Redistributable Installation Package</th></tr>
<tr><td>php-x.x.x-nts-Win32-VC16-x86.zip</td><td><a href="https://visualstudio.microsoft.com/zh-hans/downloads/">Microsoft Visual C++ Redistributable for Visual Studio 2019</a>(x86)</td></tr>
<tr><td>php-x.x.x-nts-Win32-VC15-x86.zip</td><td><a href="https://visualstudio.microsoft.com/zh-hans/vs/older-downloads/">Microsoft Visual C++ Redistributable for Visual Studio 2017</a>(x86)</td></tr>
<tr><td>php-x.x.x-nts-Win32-VC14-x86.zip</td><td><a href="https://www.microsoft.com/zh-cn/download/details.aspx?id=48145">Microsoft Visual C++ Redistributable for Visual Studio 2015</a>(x86)</td></tr>
</table>
For example, if the name of the downloaded PHP installation package is <code>PHP-7.1.30-nts-Win32-VC14-x86.zip</code>, download and install the Microsoft Visual C++ Redistributable for Visual Studio 2015 installation package (x86).

#### Installation and configuration
1. Decompress the downloaded PHP installation package, for example, to `C:\PHP`.
2. Copy the `php.ini-production` file in `C:\PHP` and change the file extension to `.ini`, that is, rename it to `php.ini`, as shown in the following figure:
![](https://main.qcloudimg.com/raw/52d9a2098fe73c8ddb41366b9732a000.png)
3. On the desktop, click <img src="https://main.qcloudimg.com/raw/f779581f1ce3edfead8c725ce1504009.png" style="margin: 0;"></img> to open **Server Manager**, as shown in the following figure:
4. In the left sidebar, click **IIS**.
5. In the right IIS management window, right-click the server name in the **Server** column and choose **Internet Information Services (IIS) Manager**, as shown in the following figure:
![](https://main.qcloudimg.com/raw/55e0b4c86de284050e5d810e92650337.png)
6. In the "Internet Information Service (IIS) Manager" window, click the server name in the left sidebar to go to the server homepage, as shown in the following figure:
For example, click the 10_141_9_72 server name to go to the 10_141_9_72 homepage.
![](https://main.qcloudimg.com/raw/ab0f2306624452d4a3ab9fd5389d5b1d.png)
7. On the **10_141_9_72 homepage**, double-click **Handler Mappings** to go to the "Handler Mappings" page, as shown in the following figure:
![](https://main.qcloudimg.com/raw/916a9cc9ce1270dbbfe6ddbb58f937e7.png)
8. In the **Actions** column on the right, click **Add Module Mapping** to open the "Add Module Mapping" window.
9. In the "Add Module Mapping" window, enter the following information and click **OK**, as shown in the following figure:
![](https://main.qcloudimg.com/raw/a4d139682fc14204acd77ac3d1ea10eb.png)
The main parameters include:
 - Request path: enter `*.php`.
 - Module: select "FastCgiModule".
 - Executable (optional): select the php-cgi.exe file in the PHP installation package, that is, `C:\PHP\php-cgi.exe`.
 - Name: enter a custom name, such as FastCGI.
10. In the window that appears, click **OK**. 
11. Click the 10_141_9_72 server name in the left sidebar to return to the 10_141_9_72 homepage.
12. On the **10_141_9_72 homepage**, double-click **Default Document** to go to the default document management page, as shown in the following figure:
![](https://main.qcloudimg.com/raw/6a896eeb929ae0104b1792e08bd895a6.png)
13. In the **Actions** column on the right, click **Add** to open the "Add Default Document" window.
14. In the "Add Default Document" window, set **Name** to `index.php` and click **OK**, as shown in the following figure:
![](https://main.qcloudimg.com/raw/2d09af5d86755dd481b13efb0b3619a2.png)
15. Click the 10_141_9_72 server name in the left sidebar to return to the 10_141_9_72 homepage.
16. On the **10_141_9_72 homepage**, double-click **FastCGI Settings** to open the FastCGI setting management page, as shown in the following figure:
![](https://main.qcloudimg.com/raw/2a0693d3b837804b546fc690b4fb5cee.png)
17. On the FastCGI setting management page, select the FastCGI application and click **Edit**, as shown in the following figure:
![](https://main.qcloudimg.com/raw/2038fa0df5c08820dc028fb3635fcda4.png)
18. In the "Edit FastCGI Application" window, set **Monitor changes to file** to the `php.ini` file path, as shown in the following figure:
![](https://main.qcloudimg.com/raw/b1aa458607934a5331b51e22762d0dec.png)
19. In `C:\inetpub\wwwroot`, create a PHP file, such as `index.php`.
20. In the created `index.php` file, add the following code and save the file.
```
<?php
phpinfo();
?>
```
21. On the desktop, open the browser and visit `http://localhost/index.php` to check whether the environment is configured successfully.
If the page shown below appears, the configuration was successful.
![](https://main.qcloudimg.com/raw/ccd08fd9af6afe4ee2c3bf38f9e581b9.png)

