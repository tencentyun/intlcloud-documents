## Scenario

[USB/IP](http://usbip.sourceforge.net/) is an open-source project and has been incorporated in the kernel. In a Linux environment, you can use USB/IP to remotely share USB devices. This document uses the following environment versions as examples to describe how to use USB/IP to share USB devices.
USB client: CVM with CentOS 7.6
USB server: local PC with Debian

## Notes
The USB/IP installation method and kernel module name vary by Linux OS versions. Check whether your current Linux OS supports the USB/IP feature.


## Directions

### Configuring the USB server

1. On the local PC, run the following commands in sequence to install USB/IP and load related kernel modules:
```
sudo apt-get install usbip
sudo modprobe usbip-core
sudo modprobe vhci-hcd
sudo modprobe usbip_host
```
2. Insert a USB device and run the following command to view available USB devices:
```
usbip list --local
```
For example, if a Feitian USB key is inserted to the local PC, the following result is returned:
```
busid 1-1.3(096e:031b)
Feitian Technologies, Inc.: unknown product(096e:031b)
```
3. Record the busid value and run the following commands in sequence to enable listening, specify the USB/IP port, and share the USB device:
```
sudo usbipd -D [--tcp-port PORT]
sudo usbip bind -b [busid]
```
For example, if the specified USB/IP port is port 3240 (default USB/IP port) and busid is `1-1.3`, run the following commands:
```
sudo usbipd -D
sudo usbip bind -b 1-1.3
```
(Optional) 4. Run the following command to create an SSH tunnel and use port listening:
> Skip this step if the local PC has a public IP address.
>
```
ssh -Nf -R specified USB/IP port:localhost:specified USB/IP port root@your_host
```
`your_host` indicates the CVM IP address.
For example, if the USB/IP port is port 3240 and the CVM IP address is 192.168.15.24, run the following command:
```
ssh -Nf -R 3240:localhost:3240 root@192.168.15.24
```


### Configuring the USB client

> The following uses a local PC without a public IP as an example. If your local PC has a public IP, replace `127.0.0.1` in the following steps with the public IP of your local PC.
>

1. [Log into Linux instance using standard login method (recommended)](https://intl.cloud.tencent.com/document/product/213/5436).
2. Run the following commands in sequence to download the USB/IP source:
```
rpm --import https://www.elrepo.org/RPM-GPG-KEY-elrepo.org
rpm -ivh http://www.elrepo.org/elrepo-release-7.0-3.el7.elrepo.noarch.rpm
```
3. Run the following commands in sequence to install USB/IP:
```
yum -y install kmod-usbip usbip-utils
modprobe usbip-core
modprobe vhci-hcd
modprobe usbip-host
```
4. Run the following command to query available USB devices of the CVM:
```
usbip list --remote 127.0.0.1
```
For example, if the Feitian USB key information is located, the following result is returned:
```
Exportable USB devices
======================
-127.0.0.1 1-1.3: Feitian Technologies, Inc.: unknown product(096e:031b):/sys/devices/platform/scb/fd500000.pcie/pci0000:00/0000:00:00.0/0000:01:00.0/usb1/1-1/1-1.3:(Defined at Interface level)(00/00/00)
```
5. Run the following command to bind the USB device to the CVM:
```
usbip attach --remote=127.0.0.1 --busid=1-1.3
```
6. Run the following command to query the USB device list:
```
lsusb
```
If information similar to the following is returned, the USB device has been shared.
```
Bus 002 Device 002:ID096e:031b Feitian Technologies, Inc.
Bus 002 Device 001:ID1d6b:0002 Linux Foundation 2.0 root hub
Bus 001 Device 001:ID1d6b:0001 Linux Foundation 1.1 root hub
```
