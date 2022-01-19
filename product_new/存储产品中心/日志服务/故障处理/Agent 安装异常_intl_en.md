For details about how to install and use LogListener, see [LogListener Installation Guide](https://intl.cloud.tencent.com/document/product/614/17414). <!-- and [LogListener mechanism]()-->

## Possible causes

Loglistener may not be installed correctly for the following reasons:
1. The kernel version only supports 64-bit.
2. The installation method is incorrect.
3. The latest features rely on a later version of LogListener.


## Directions

1. Check the kernel version.
The executable file in the bin directory under the LogListener installation directory only supports Linux 64-bit kernel. Execute the command **uname -a** to check whether the kernel version is x86_64.
2. Check the installation command.
Be sure to perform operations according to the [LogListener Installation Guide](https://intl.cloud.tencent.com/document/product/614/17414).
3. Check the LogListener version.
Some of new CLS features may be available only for the latest version of Loglistener. In this case, please download and install the latest version. For step-by-step directions, see [LogListener Installation Guide](https://intl.cloud.tencent.com/document/product/614/17414).
4. Verify the LogListener installation.
Check for process and heartbeat of LogListener and check whether it can properly obtain collection configuration of users. To do this, please see [LogListener Diagnostic Tool](https://intl.cloud.tencent.com/document/product/614/17414#loglistener-.E5.B8.B8.E7.94.A8.E6.93.8D.E4.BD.9C).
