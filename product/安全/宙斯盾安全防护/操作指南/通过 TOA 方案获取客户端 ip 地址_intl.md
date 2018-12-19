After the business request is forwarded through layer 4 of the protective IP, the source IP address that the business server sees after receiving the message is the egress IP address of the protective IP. In order to enable the server to obtain the actual IP address of the client, you can use the following TOA scheme. On the Linux server of the business service, install the corresponding TOA kernel package and reboot the server. Then the service side can obtain the actual IP address of the client.

## How TOA Works
After forwarded, the data packet will undergo SNAT and DNAT at the same time, and its source and destination addresses will be modified.
In the TCP protocol, in order to pass the client IP to the server, the client's IP and port are placed in the custom tcp option field when forwarding.
		
    #define TCPOPT_ADDR	200  
    #define TCPOLEN_ADDR 8	/* |opcode|size|ip+port| = 1 + 1 + 6 */

    /*
    *insert client ip in tcp option, now only support IPV4,
    *must be 4 bytes alignment.
    */
    struct ip_vs_tcpo_addr {
    __u8 opcode;
    __u8 opsize;
    __u16 port;
    __u32 addr;
    }; 
The Linux kernel's state transits from `SYN_REVC` to `TCP_ESTABLISHED` after the listening socket receives the ACK packet of three-way handshake. At this point, the kernel will call the `tcp_v4_syn_recv_sock` function. The Hook function `tcp_v4_syn_recv_sock_toa ` first calls the original ` tcp_v4_syn_recv_sock ` function, then calls the `get_toa_data` function to extract the TOA OPTION from the TCP OPTION and stores it in the `sk_user_data` field.

Then, `inet_getname_toa hook inet_getname` is used. When getting the source IP address and port, the original `inet_getname` function is called first, and then it is judged whether `sk_user_data` is empty. If data is present there, the real IP and port are extracted from it to replace the return of `inet_getname`.

The client program calls getpeername in user mode, and the returned IP and port are the client's original IP.

## Kernel Package Installation Steps
### CentOS 6.x/7.x
Installation steps

1. Download the installation package;
 (1) [Download CentOS 6.x](http://toakernel-1253438722.cossh.myqcloud.com/kernel-2.6.32-220.23.1.el6.toa.x86_64.rpm)
 (2) [Download CentOS 7.x](http://toakernel-1253438722.cossh.myqcloud.com/kernel-3.10.0-693.el7.centos.toa.x86_64.rpm)
2. Install the package file;
							
			rpm -hiv kernel-2.6.32-220.23.1.el6.toa.x86_64.rpm --force						
3. Reboot the server after the installation is completed;

			reboot
4. Execute the following command to check whether the TOA module is successfully loaded;

			lsmod | grep toa
5. If not, manually start it;
    
			modprobe toa
6. Use the following command to enable automatic loading of the TOA module.

			echo "modprobe toa" >> /etc/rc.d/rc.local
			
### Ubuntu 16.04
Download the installation package:
(1) [Download kernel package](http://toakernel-1253438722.cossh.myqcloud.com/linux-image-4.4.87.toa_1.0_amd64.deb )
(2) [Download kernel header package](http://toakernel-1253438722.cossh.myqcloud.com/linux-headers-4.4.87.toa_1.0_amd64.deb)
Installation steps:

			dpkg -i linux-image-4.4.87.toa_1.0_amd64.deb
The header package is optional. If needed for related development, install it.
After the installation is completed, reboot the server, then execute the ` lsmod | grep toa ` command to check whether the TOA module is loaded, and if not, start it by executing the `modprobe toa` command.
Use the following command to enable loading of the TOA module.
		
		echo "modprobe toa" >> /etc/rc.d/rc.local
		 
### Debian 8

(1) [Download kernel package](http://toakernel-1253438722.cossh.myqcloud.com/linux-image-3.16.43.toa_1.0_amd64.deb)
(2) [Download kernel header package](http://toakernel-1253438722.cossh.myqcloud.com/linux-headers-3.16.43.toa_1.0_amd64.deb)

The installation method is the same as Ubuntu.


Please download the appropriate kernel package according to the type and version of the Linux operating system of your business server and follow the steps below. If there is no kernel package for your operating system, you can install the TOA source code by following the instructions below.

## TOA Source Code Installation Guide

### Source Code Installation

1. Download the source code package containing the [TOA patch](http://kb.linuxvirtualserver.org/images/3/34/Linux-2.6.32-220.23.1.el6.x86_64.rs.src.tar.gz) and click the TOA patch to download the installation package;
2. Decompress it;
3. Edit .config by changing `CONFIG_IPV6=M` to `CONFIG_IPV6=y`;
4. If you need to add some custom descriptions, you can edit Makefile;
5. Execute make -jn (n is the number of threads);
6. Execute `make modules_install`;
7. Execute `make install`;
8. Modify /boot/grub/menu.lst 	by changing default to the newly installed kernel (the title order starts at 0);
9. Reboot and the kernel has TOA;
10. Execute `lsmode | grep toa` to check whether the TOA module is loaded, 	and if not, start it by executing `modprobe toa`.

### Making a Kernel Package

You can make your own rpm package or use the one provided by us.

1. Install kernel-2.6.32-220.23.1.el6.src.rpm; 

			rpm -hiv kernel-2.6.32-220.23.1.el6.src.rpm
2. Generate the kernel source code directory;

			rpmbuild -bp ~/rpmbuild/SPECS/kernel.spec
3. Copy the source code directory;

			cd ~/rpmbuild/BUILD/kernel-2.6.32-220.23.1.el6/ cp -a linux-2.6.32-220.23.1.el6.x86_64/ linux-2.6.32-220.23.1.el6.x86_64_new   
4. Apply the TOA patch to the copied source directory;

			cd ~/rpmbuild/BUILD/kernel-2.6.32-220.23.1.el6/linux-2.6.32-220.23.1.el6.x86_64_new/ 
			patch -p1 < /usr/local/src/linux-2.6.32-220.23.1.el6.x86_64.rs/toa-2.6.32-220.23.1.el6.patch
5. Edit .config and copy it to the SOURCE directory;

			sed -i 's/CONFIG_IPV6=m/CONFIG_IPV6=y/g' .config 
			echo -e '\n# toa\nCONFIG_TOA=m' >> .config
			cp .config ~/rpmbuild/SOURCES/config-x86_64-generic
6. Delete .config from the original source code;

			cd ~/rpmbuild/BUILD/kernel-2.6.32-220.23.1.el6/linux-2.6.32-220.23.1.el6.x86_64 
			rm -rf .config
7. Generate the final patch;
    
			cd ~/rpmbuild/BUILD/kernel-2.6.32-220.23.1.el6/
			diff -uNr linux-2.6.32-220.23.1.el6.x86_64 linux-2.6.32-220.23.1.el6.x86_64_new/ >
			~/rpmbuild/SOURCES/toa.patch
8. Edit kernel.spec;

    vim ~/rpmbuild/SPECS/kernel.spec
Add the following two lines under ApplyOptionPath (you can also modify custom kernel package names such as buildid) 

			Patch999999: toa.patch
    ApplyOptionalPatch toa.patch
9. Make an rpm package;

			rpmbuild -bb --with baseonly --without kabichk --with firmware --without debuginfo --target=x86_64 ~/rpmbuild/SPECS/kernel.spec
10. Install the kernel rpm package;
		 rpm -hiv kernel-xxxx.rpm --force
	 
Reboot to load the TOA module





