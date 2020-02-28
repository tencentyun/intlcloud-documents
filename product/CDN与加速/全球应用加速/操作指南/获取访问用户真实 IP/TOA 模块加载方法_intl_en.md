Download and decompress the TOA package corresponding to the version of Linux OS on Tencent Cloud:
-   [CentOS 7.2 64](http://toamodule-1253438722.file.myqcloud.com/CentOS%207.2%2064.zip)
-   [CentOS 7.3 64](http://toamodule-1253438722.file.myqcloud.com/CentOS%207.3%2064.zip)
-   [CentOS 7.4 64](http://toamodule-1253438722.file.myqcloud.com/CentOS%207.4%2064.zip)
-   [Debian 8.2 64](http://toamodule-1253438722.file.myqcloud.com/Debian%208.2%2064.zip)
-   [Debian 9.0 64](http://toamodule-1253438722.file.myqcloud.com/Debian%209.0%2064.zip) 
-   [SUSE Linux Enterprise Server 11 SP3 64](http://toamodule-1253438722.file.myqcloud.com/SUSE%20Linux%20Enterprise%20Server%2011%20SP3%2064.zip)
-   [SUSE Linux Enterprise Server 12 64](http://toamodule-1253438722.file.myqcloud.com/SUSE%20Linux%20Enterprise%20Server%2012%2064.zip)
-   [Ubuntu Server 14.04.1 LTS 64](http://toamodule-1253438722.file.myqcloud.com/Ubuntu%20Server%2014.04.1%20LTS%2064.zip)
-   [Ubuntu Server 16.04.1 LTS 64](http://toamodule-1253438722.file.myqcloud.com/Ubuntu%20Server%2016.04.1%20LTS%2064.zip) 


1. After decompression is completed, run the `cd` command to access the decompressed folder and run the module loading command:
```
insmod toa.ko
``` 
2. Run the following command to check whether loading is successful:
```
lsmod | grep toa
```
3. If yes, load the `toa.ko` file in the startup script (ko file needs to be reloaded if the server is restarted).


If you cannot find from the list above an installation package corresponding to your OS version, please download and compile the source package of the general version for Linux OS. This version supports most Linux distributions such as CentOS 6.9, CentOS 7, and Ubuntu 14.04.
1. Get the source package.
```
wget http://toamodule-1253438722.file.myqcloud.com/tencenttoa.zip
```
2. Compile the file.
```
yum install gcc
yum install kernel-headers
yum install kernel-devel
```
3. Load the `toa.ko` file.
```
tar -zxvf linux_toa.tar.gz
cd toa
make
mv toa.ko /lib/modules/`uname -r`/kernel/net/netfilter/ipvs/toa.ko
insmod /lib/modules/`uname -r`/kernel/net/netfilter/ipvs/toa.ko
```
