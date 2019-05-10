> For more information about how to install and use CLS Loglistener, see the [Loglistener Installation Guide](https://cloud.tencent.com/document/product/614/17414), and understand the [Loglistener mechanism](https://cloud.tencent.com/document/product/614/17415).

## Possible Cause

The following reasons may prevent the Loglistener from being installed correctly:
1. The kernel version only supports 64-bit.
2. The installation method is incorrect.
3. The latest features rely on a higher version of Loglistener.


## Dealing Steps

1. Check the kernel version.
The executable file in the bin directory under the Loglistener installation directory only supports Linux 64-bit kernel. Execute the command **uname-a** to check whether the kernel version is x86_64.
2. Check the installation execution command.
The script file in the Tools directory is a bash script, which does not support the execution method of `sh install.sh`. It is recommended to use `./install.sh` or `bash install.sh`. Be sure to operate according to [Loglistener Installation Guide](https://cloud.tencent.com/document/product/614/17414).
3. Check the Loglistener version.
The latest features of CLS may rely on the new version of Loglistener. If it is confirmed that the exception is caused by use of new features, download the [latest version of Loglistener](https://main.qcloudimg.com/raw/8656fcadd12ab9689674df09b510b52b/loglistener.2.2.2.tar.gz).
4. Verify whether Loglistener is successfully installed.
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
 If the above command is executed without error, Loglistener is successfully installed.

