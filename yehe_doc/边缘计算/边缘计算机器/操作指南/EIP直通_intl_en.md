## Overview
When you create an ECM instance, EIP direct access is configured by default. If your ECM instance is not configured with EIP direct access, you can run the EIP direct access script for configuration. This document describes how to configure an EIP direct access script for an ECM instance and how to restore the script if you delete it by mistake. 

## Notes

- Currently, you can configure EIP direct access only for Linux instances.
- The EIP direct access script must run on CentOS 6 or above or Ubuntu.

## Prerequisites

- You have created an ECM instance and obtained its public IP.
- You have obtained the instance admin account and password.
- Both the private IP and EIP of the Linux instance are on the primary ENI (eth0).
If the public IP bound to the primary ENI is not an EIP, you need to convert it to an EIP first.

## Directions

<span id="downloadEIPscript"></span>
### Downloading EIP direct access script

As EIP direct access will interrupt network connection, you need to select a method to save the EIP direct access script to the ECM instance first.
- **Method 1: upload the script for EIP direct access**
 1. Download the EIP direct access script to the local PC.
 Click [here](https://eip-direct-1254277469.cos.ap-guangzhou.myqcloud.com/eip_direct.sh) to download it.
 2. Upload the downloaded script to the ECM instance requiring EIP direct access.
- **Method 2: use the command directly** 
Log in to the ECM instance and run the following command to download the EIP direct access script:
```
wget https://eip-direct-1254277469.cos.ap-guangzhou.myqcloud.com/eip_direct.sh
```

### Running EIP direct access script

1. [Log in to a Linux instance](https://intl.cloud.tencent.com/document/product/1119/43412).
2. Run the following command to grant the execution permission:
```
chmod +x eip_direct.sh
```
3. Run the following command to run the script:
```
./eip_direct.sh install XX.XX.XX.XX
```
Here, `XX.XX.XX.XX` is the EIP address, which is optional. You can also directly run `./eip_direct.sh install` without entering the address.


## Appendix
If you delete the EIP direct access script by mistake, you can restore it as follows:
1. Upload/Download the EIP direct access script to the ECM instance.
For more information, see [Downloading EIP direct access script](#downloadEIPscript).
2. Log in to the instance and run the following command to restart it:
```
reboot
```

