### Method 1: Download source code and load the module

1. Download and decompress the TOA package corresponding to the version of Linux OS on Tencent Cloud.
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
		- [SUSE Linux Enterprise Server 12 SP3 64](https://gaap-1251337138.file.myqcloud.com/SUSE%20Linux%20Enterprise%20Server%2012%20SP3%2064%E4%BD%8D.rar)
	- **ubuntu**
		- [Ubuntu Server 14.04.1 LTS 64](https://gaap-1251337138.file.myqcloud.com/Ubuntu%20Server%2014.04.1%20LTS%2064.rar)
		- [Ubuntu Server 16.04.1 LTS 64](https://gaap-1251337138.file.myqcloud.com/Ubuntu%20Server%2016.04.1%20LTS%2064.rar)
		- [Ubuntu Server 18.04.1 LTS 64](https://gaap-1251337138.file.myqcloud.com/Ubuntu%20Server%2018.04.1%20LTS%2064.rar)
		- [Ubuntu Server 20.04.1 LTS 64](https://gaap-1251337138.file.myqcloud.com/Ubuntu%20Server%2020.04.1%20LTS%2064.rar)
2. After decompression is completed, run the `cd` command to access the decompressed folder and run the module loading command:
```
insmod toa.ko
```
3. Run the following command to check whether the loading is successful:
```
lsmod | grep toa
```
![](https://qcloudimg.tencent-cloud.cn/raw/1282241c425616a4ad4aa343ca5d4ee4.png)
4. After it is loaded, load the `toa.ko` file in the startup script (the `toa.ko` file needs to be reloaded if the server is restarted).
```
echo "insmod   xxxxx /toa.ko" >> /etc/rc.local
```
5. (Optional) To disable TOA temporarily, run the command `rmmod path/module name`.
```
rmmod toa.ko
```
6. (Optional) If TOA is no longer needed, run the following command to uninstall it.
```
rmmod toa
```
7. (Optional) Run the following command to check whether the module is uninstalled. If you see the message "TOA unloaded", the uninstallation is successful.
```
dmesg -T
```

### Method 2: Compile and load the module

If there is no installation package provided for your OS version, you can download the source package of the Linux general version and then compile it to obtain an installation package. The following is the example for CentOS.

1. Obtain the source package.
   - Source package for CentOS 7 and above versions
```
wget "http://thunder-pro-mainland-1258348367.cos.ap-guangzhou.myqcloud.com/gaap-toa%E6%BA%90%E7%A0%81(centos7%E4%BB%A5%E4%B8%8A).zip"
```
   - Source package for versions below CentOS 7
```
wget "http://thunder-pro-mainland-1258348367.cos.ap-guangzhou.myqcloud.com/gaap-toa%E6%BA%90%E7%A0%81(centos7%E4%BB%A5%E4%B8%8B).zip"
```
2. Install the build environment.
```
yum install gcc 
yum install make
yum install kernel-headers kernel-devel –y
```
3. Decompress the source package.
```
tar zxf toa_kernel_*.tar.gz
```
4. Enter the TOA directory.
```
cd toa
```
5. Compile make.
```
make
```
6. Move and load the module.
```
mv toa.ko /lib/modules/`uname -r`/kernel/net/netfilter/ipvs/toa.ko

insmod /lib/modules/`uname 
¬-r`/kernel/net/netfilter/ipvs/toa.ko
```
7. Check whether the module is loaded successfully.
```
lsmod | grep toa
```
