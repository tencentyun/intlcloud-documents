This document describes how to install Python for different operating systems.

## Using an Installation Package

### 1. Download a package
Go to the [Python website](https://www.python.org/downloads/) to download an installation package according to your OS.

>! Python has dropped support for Python 2 since January 1, 2020. Therefore, you are advised to install Python 3.

### 2. Install the package
Install the downloaded package as instructed.

>? If you use Windows, check **Add Python to environment variables**.
> ![](https://main.qcloudimg.com/raw/bd52e448e3ba0e8171b5a37b31caadb8.png)

### 3. Verify the installation
Run the following command in Terminal to view the Python version:
```shell
python -V
```
If the Python version is displayed, Python has been installed successfully.

>? If you use Windows, you may need to restart your computer after the installation.

### 4. Configure environment variables
In Windows, if “not recognized as an internal or external command” is reported in Terminal after the command above is run, right-click the **Computer** icon, click **Properties** > **Advanced system settings** > **Environment Variables**, and in the **System variables** area, click **New** to add the Python installation path:


## Using a Package Manager

### macOS
Install [HomeBrew](https://brew.sh/index_zh-cn) and use it to install Python:
```shell
brew install python
```

### Ubuntu
Use the built-in Advanced Packaging Tool (APT) to install Python:
```shell
sudo apt-get install python
```

### CentOS
Use the built-in Yellowdog Updater, Modified (YUM) to install Python:
```shell
sudo yum install -y python
```
