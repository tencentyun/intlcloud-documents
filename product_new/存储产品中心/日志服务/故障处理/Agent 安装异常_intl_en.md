> For details about how to install and use LogListener, see [LogListener Installation Guide](https://intl.cloud.tencent.com/document/product/614/17414) <!-- and [LogListener mechanism]()-->

## Possible causes

Loglistener may not be installed correctly for the following reasons:
1. The kernel version only supports 64-bit.
2. The installation method is incorrect.
3. The latest features rely on a later version of LogListener.


## Directions

1. Check the kernel version.
The executable file in the bin directory under the LogListener installation directory only supports Linux 64-bit kernel. Execute the command **uname -a** to check whether the kernel version is x86_64.
2. Check the installation execution command.
The script file in the Tools directory is a bash script, which does not support the `sh install.sh` execution method. It is recommended that you use `./install.sh` or `bash install.sh`. Be sure to perform the operations according to the [LogListener Installation Guide](https://intl.cloud.tencent.com/document/product/614/17414).
3. Check the LogListener version.
Some of new CLS features may be available only for the latest version of Loglistener. In this case, please download and install the latest version. For step-by-step directions, see [LogListener Installation Guide](https://intl.cloud.tencent.com/document/product/614/17414).
4. Verify whether LogListener is successfully installed.
Check whether LogListener processes are running normally. Enter the installation directory and execute the following command:
```shell
cd loglistener/tools && ./p.sh
```
Normally, the output is as follows:
 ![](https://main.qcloudimg.com/raw/e256cf61689ead123251a8f9f3a753c9.png)
Enter the installation directory and execute the following command to verify whether the configuration items are configured correctly and the network is in good condition.
```shell
cd loglistener/bin && ./check
```
Normally, the output is as follows:
 ![](https://main.qcloudimg.com/raw/e7e85f139feb14b1aaa3353b2bafd5e1.png)
 If the above command is executed without error, LogListener is successfully installed.
