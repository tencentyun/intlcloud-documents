This document describes how to install Tencent Cloud Command Line Interface (TCCLI).

## Prerequisites

You have installed the Python environment and pip tool.


<dx-alert infotype="notice" title="">
- Python 2.7 or later is required. For more information, visit the [Python website](https://www.python.org/) and [pip website](https://pypi.org/project/pip/).
- TCCLI depends on the TencentCloudApi Python SDK. If the version of the SDK is earlier than that of TCCLI, the SDK is automatically upgraded during TCCLI installation. Check the latest TCCLI version at [GitHub](https://github.com/TencentCloud/tencentcloud-cli-intl-en).
</dx-alert>

## Directions
You can install TCCLI in the following ways:

<dx-tabs>
::: Using pip (recommended)
1. The installation command is the same on Windows, macOS, and Linux. Open the command line window on your operating system.
2. Run the following command to install TCCLI:
```bash
sudo pip install tccli
```
<dx-alert infotype="notice" title="">
If you upgrade TCCLI from a version earlier than 3.0.252.3, run the following commands:
```bash
sudo pip uninstall tccli jmespath
sudo pip install tccli
```
</dx-alert>
3. After the installation is completed, run the following command to check whether the installation is successful:
```bash
tccli --version
```
:::
::: Using source code
Run the following commands in sequence to download the TCCLI project from [tencentcloud-cli](https://github.com/TencentCloud/tencentcloud-cli) and to install TCCLI by using the `setup.py` script.
```bash
git clone https://github.com/TencentCloud/tencentcloud-cli.git
```
```
cd tencentcloud-cli
```
```
python setup.py install
```
:::
::: Using Homebrew


<dx-alert infotype="notice" title="">
This method applies only to macOS. You need to install Homebrew first. See the installation method at the [Homebrew website](https://brew.sh/).
</dx-alert>



Run the following commands in sequence:
```bash
brew tap tencentcloud/tccli
```
```bash
brew install tccli
```
You can run the following command to upgrade TCCLI:
```bash
brew upgrade
```
:::
</dx-tabs>
