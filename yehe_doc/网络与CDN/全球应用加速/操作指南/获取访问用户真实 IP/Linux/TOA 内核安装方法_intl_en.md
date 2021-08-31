## How to install CentOS TOA Kernel
### Installing with rpm package
Download one of the following rpm packages:
- CentOS 6 TOA package ([click here to download](http://toakernel-1253438722.cossh.myqcloud.com/kernel-2.6.32-220.23.1.el6.toa.x86_64.rpm)).
- CentOS 7 TOA package ([click here to download](http://toakernel-1253438722.cossh.myqcloud.com/kernel-3.10.0-693.el7.centos.toa.x86_64.rpm)).  

After download and installation, restart the system to complete the process.
You can also create a rpm package as follows:
1. Install kernel-2.6.32-220.23.1.el6.src.rpm:
```
rpm -hiv kernel-2.6.32-220.23.1.el6.src.rpm
```
2. Generate a kernel source code directory:
```
rpmbuild -bp ~/rpmbuild/SPECS/kernel.spec
```
3. Copy the source code directory:
```
cd ~/rpmbuild/BUILD/kernel-2.6.32-220.23.1.el6/
cp -a linux-2.6.32-220.23.1.el6.x86_64/ linux-2.6.32-220.23.1.el6.x86_64_new
```
4. Attach the following toa patch to the copied source code directory:
```
cd ~/rpmbuild/BUILD/kernel-2.6.32-220.23.1.el6/linux-2.6.32-220.23.1.el6.x86_64_new/
patch -p1 < /usr/local/src/linux-2.6.32-220.23.1.el6.x86_64.rs/toa-2.6.32-220.23.1.el6.patch
```
5. Edit `.config` and copy it to the `SOURCE` directory:
```
sed -i 's/CONFIG_IPV6=m/CONFIG_IPV6=y/g' .config
echo -e '\n# toa\nCONFIG_TOA=m' >> .config
cp .config ~/rpmbuild/SOURCES/config-x86_64-generic
```
6. Delete `.config` from the original source code:
```
cd ~/rpmbuild/BUILD/kernel-2.6.32-220.23.1.el6/linux-2.6.32-220.23.1.el6.x86_64
rm -rf .config
```
7. Generate the final patch:
```
cd ~/rpmbuild/BUILD/kernel-2.6.32-220.23.1.el6/
diff -uNr linux-2.6.32-220.23.1.el6.x86_64 linux-2.6.32-220.23.1.el6.x86_64_new/ >
~/rpmbuild/SOURCES/toa.patch
```
8. Edit `kernel.spec`:
`vim ~/rpmbuild/SPECS/kernel.spec`
Add the following lines to `ApplyOptionPath` (you can also modify the names of custom kernel packages such as `buildid`):
```
Patch999999: toa.patch
ApplyOptionalPatch toa.patch
```
9. Create a rpm package:
```
rpmbuild -bb --with baseonly --without kabichk --with firmware --without debuginfo --target=x86_64 ~/rpmbuild/SPECS/kernel.spec
```
10. Install the kernel rpm package:
```
rpm -hiv kernel-xxxx.rpm --force
```
11. Restart the system, load the TOA module, and complete the installation.

### Installing with source code
If the operating system version you need is above CentOS 6, you can download and compile the source code to obtain the corresponding installation package. The steps are as follows:
1. Download the source package with toa patch ([click here to download](http://kb.linuxvirtualserver.org/images/3/34/Linux-2.6.32-220.23.1.el6.x86_64.rs.src.tar.gz)).
2. Decompress it.
3. Edit `.config` and change `CONFIG_IPV6=M` to `CONFIG_IPV6=y`.
4. Edit ` Makefile` to add custom descriptions.
5. Run `make -jn` (n is the number of threads).
6. Run `make modules_install`.
7. Run `make install`.
8. Modify `/boot/grub/menu.lst` and change `default` to the newly installed kernel (title starts at 0).
9. Run `Reboot` to restart the system and toa kernel is loaded.
10. Run `lsmod | grep toa` to check whether toa module is loaded, if not, run the `modprobe toa` command.

## How to Install Ubuntu TOA kernel
Click the link below to download the kernel and headers package:
- Kernel package ([click here to download](http://toakernel-1253438722.cossh.myqcloud.com/linux-image-4.4.87.toa_1.0_amd64.deb)) 
- Kernel headers package ([click here to download](http://toakernel-1253438722.cossh.myqcloud.com/linux-headers-4.4.87.toa_1.0_amd64.deb)) 

Headers package is optional and can be installed if relevant development is needed. Please install kernel package first by following the steps below:
1. Run the following command to install the kernel package:  
```
dpkg -i linux-image-4.4.87.toa_1.0_amd64.deb
```
2. Restart the server after the installation is completed.
3. Run `lsmod | grep toa` to check whether toa module is loaded, if not, run the `modprobe toa` command:
```
echo “modprobe toa” >> /etc/rc.d/rc.local
```

## How to install Debian TOA kernel
Click the link below to download the kernel and headers package:
- Kernel package ([click here to download](http://toakernel-1253438722.cossh.myqcloud.com/linux-image-3.16.43.toa_1.0_amd64.deb))
- Kernel headers package ([click here to download](http://toakernel-1253438722.cossh.myqcloud.com/linux-headers-3.16.43.toa_1.0_amd64.deb))

Headers package is optional and can be installed if relevant development is needed. Please install kernel package first by following the steps below:
1. Run the following command to install the kernel package:  
```
dpkg -i linux-image-4.4.87.toa_1.0_amd64.deb
```
2. Restart the server after the installation is completed.
3. Run `lsmod | grep toa` to check whether toa module is loaded, if not, run the `modprobe toa` command:
```
echo “modprobe toa” >> /etc/rc.d/rc.local
```
