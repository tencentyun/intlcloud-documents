## Overview
Some Tencent Cloud CentOS 7 public images have Python 2-pip 8.1.2 installed by default. However, this version of pip does not allow users to select compatible package versions to install. Instead, it defaults to installing the latest packages. Unfortunately, the latest versions of pip and some commonly used application tools like NumPy do not support Python 2. As a result, when running a command to upgrade pip (pip install pip --upgrade) or installing specific application tools, compatibility issues may arise. To resolve this issue, Tencent Cloud has updated pip in some public images of the CentOS 7 series.

## Update Content and Scope
The table below lists the CentOS 7 public images with updated pip. By default, these public images have Python 2 installed, which comes with [pip 20.3.4](https://pypi.org/project/pip/20.3.4/) instead of pip 8.1.2.
<dx-alert infotype="explain" title="">
The upgrade has been performed in stages and finished on December 12, 2022. Instances purchased after the upgrade of a corresponding public image are automatically updated, while instances purchased prior to the upgrade are not. To update these instances, refer to the manual upgrade instructions.
</dx-alert>

| Image Tag | Image ID |
|---------|---------|
| CentOS 7.9, 64-bit | img-180g963d |
| CentOS 7.6, 64-bit | img-9qabwvbn |
| CentOS 7.9, 64-bit + SG1-pv1.5 | img-all2luul |
| CentOS 7.9, 64-bit + SG1-pv1.6 | img-ojhiw86l |
| CentOS 7.4 (arm64) | img-k4xgkxa5 |

## Directions
### Upgrading pip
You can run the following command to view the pip version of your instance:
```plaintext
pip --version
```
If the version of pip2 of your instance is earlier than pip 9.0, errors may occur when you upgrade pip or install application tools. To avoid this issue, you can run the following command to perform the upgrade to pip 20.3.4 first:
```plaintext
pip2 install --upgrade pip==20.3.4
```
### Installing pip2
You can run the following command to install the latest version of pip2:
```plaintext
wget https://bootstrap.pypa.io/pip/2.7/get-pip.py
python2 ./get-pip.py -i http://mirrors.tencentyun.com/pypi/simple --trusted-host mirrors.tencentyun.com
```
If you have any questions about the product, [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category).
