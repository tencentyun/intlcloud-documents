Download and decompress the TOA package corresponding to the version of Linux OS on Tencent Cloud:
- **arm64**
	- [kernel-4.18.0 ](https://gaap-1251337138.file.myqcloud.com/kernel-4.18.0.rar)
- **centos**
	- [CentOS 6.5 64](https://gaap-1251337138.file.myqcloud.com/CentOS%206.5%2064.rar)
	- [CentOS 7.2 64](https://gaap-1251337138.file.myqcloud.com/CentOS%207.2%2064.rar)
	- [CentOS 7.3 64](https://gaap-1251337138.file.myqcloud.com/CentOS%207.3%2064.rar)
	- [CentOS 7.4 64](https://gaap-1251337138.file.myqcloud.com/CentOS%207.4%2064.rar)
	- [CentOS 7.5 64](https://gaap-1251337138.file.myqcloud.com/CentOS%207.5%2064.rar)
	- [CentOS 7.6 64](https://gaap-1251337138.file.myqcloud.com/CentOS%207.6%2064.rar)
	- [CentOS 7.7 64](https://gaap-1251337138.file.myqcloud.com/CentOS%207.7%2064.rar)
	- [CentOS 7.8 64](https://gaap-1251337138.file.myqcloud.com/CentOS%207.8%2064.rar)
	- [CentOS 7.9 64](https://gaap-1251337138.file.myqcloud.com/CentOS%207.9%2064.rar)
	- [CentOS 8.0 64](https://gaap-1251337138.file.myqcloud.com/CentOS%208.0%2064.rar)
	- [CentOS 8.2 64](https://gaap-1251337138.file.myqcloud.com/CentOS%208.2%2064.rar)
- **debian**
	- [Debian 8.2 64](https://gaap-1251337138.file.myqcloud.com/Debian%208.2%2064.rar)
	- [Debian 9.0 64](https://gaap-1251337138.file.myqcloud.com/Debian%209.0%2064.rar)
	- [Debian 10.2 64](https://gaap-1251337138.file.myqcloud.com/Debian%2010.2%2064.rar)
- **suse linux**
	- [SUSE Linux Enterprise Server 11 SP3 64](http://toamodule-1253438722.file.myqcloud.com/SUSE%20Linux%20Enterprise%20Server%2011%20SP3%2064.zip)
	- [SUSE Linux Enterprise Server 12 64](http://toamodule-1253438722.file.myqcloud.com/SUSE%20Linux%20Enterprise%20Server%2012%2064.zip)
	- [SUSE Linux Enterprise Server 12 SP3 64](https://gaap-1251337138.file.myqcloud.com/SUSE%20Linux%20Enterprise%20Server%2012%20SP3%2064位.rar)
- **ubuntu**
	- [Ubuntu Server 14.04.1 LTS 64](https://gaap-1251337138.file.myqcloud.com/Ubuntu%20Server%2014.04.1%20LTS%2064.rar)
	- [Ubuntu Server 16.04.1 LTS 64](https://gaap-1251337138.file.myqcloud.com/Ubuntu%20Server%2016.04.1%20LTS%2064.rar)
	- [Ubuntu Server 18.04.1 LTS 64](https://gaap-1251337138.file.myqcloud.com/Ubuntu%20Server%2018.04.1%20LTS%2064.rar)
	- [Ubuntu Server 20.04.1 LTS 64](https://gaap-1251337138.file.myqcloud.com/Ubuntu%20Server%2020.04.1%20LTS%2064.rar)




1. After decompression is completed, run the `cd` command to access the decompressed folder and run the module loading command:
```
insmod toa.ko
```
2. Run the following command to check whether loading is successful:
```
lsmod | grep toa
```
3. If yes, load the `toa.ko` file in the startup script (the `toa.ko` file needs to be reloaded if the server is restarted).

If you cannot find an installation package corresponding to your OS version from the list above, please download and compile the source package of the general version for Linux OS. This version supports most Linux distributions such as CentOS 6.9, CentOS 7, and Ubuntu 14.04.
1. Obtain the source package.
	- Source package for CentOS 7 and above versions
```
wget "http://thunder-pro-mainland-1258348367.cos.ap-guangzhou.myqcloud.com/gaap-toa%E6%BA%90%E7%A0%81(centos7%E4%BB%A5%E4%B8%8A).zip"
```
	- Source package for versions below CentOS 7
```
wget "http://thunder-pro-mainland-1258348367.cos.ap-guangzhou.myqcloud.com/gaap-toa%E6%BA%90%E7%A0%81(centos7%E4%BB%A5%E4%B8%8B).zip"
```
2. Compile the source package to generate the TOA module file.
```
yum install gcc
yum install kernel-headers
yum install kernel-devel
unzip gaap-toa*.zip //Decompress the source package above
cd gaap-toa* //Access the corresponding directory
make
```
3. Load the TOA module file.
```
mv toa.ko /lib/modules/`uname -r`/kernel/net/netfilter/ipvs/toa.ko
insmod /lib/modules/`uname -r`/kernel/net/netfilter/ipvs/toa.ko
```

If the compilation error is reported, the error may be caused by the inconsistency between the installed kernel version and the version `uname -r` displays. In the directory `/lib/modules/`, check the kernel version actually installed, modify the `uname -r` in `Makefile` to the actual kernel version, and compile the file again.
