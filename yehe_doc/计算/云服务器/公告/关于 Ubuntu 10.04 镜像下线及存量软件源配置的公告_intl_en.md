Ubuntu has officially ceased providing maintenance for Ubuntu 10.04 LTS, and therefore Tencent Cloud has also deactivated public images of Ubuntu 10.04.

Directory trees for Ubuntu 10.04 LTS have been deleted from the latest official source repository. To ensure consistency with the official source repository, the Tencent Cloud software repository will no longer support Ubuntu 10.04 LTS under the official source directory tree. Accordingly, we recommend that you upgrade your images to a later version.

For existing users who hope to continue to use the software source of Ubuntu 10.04, we provide support for them in the following ways:

## Method 1: Manually Updating the Configuration File
To improve the user experience, the Tencent Cloud software repository pulls the official archive source `http://old-releases.ubuntu.com/ubuntu/` of Ubuntu 10.04 LTS (http://old-releases.ubuntu.com/ubuntu/) for users. Users can use the repository as usual by manually modifying the configuration file:

Open the apt source configuration file `vi/etc/apt/sources.list` and modify the following code snippets:

```
deb-src http://mirrors.tencentyun.com/old-archives/ubuntu lucid main restricted universe multiverse
deb-src http://mirrors.tencentyun.com/old-archives/ubuntu lucid-updates main restricted universe multiverse
deb-src http://mirrors.tencentyun.com/old-archives/ubuntu lucid-security main restricted universe multiverse
deb-src http://mirrors.tencentyun.com/old-archives/ubuntu lucid-backports main restricted universe multiverse
deb http://mirrors.tencentyun.com/old-archives/ubuntu lucid main restricted universe multiverse
deb http://mirrors.tencentyun.com/old-archives/ubuntu lucid-updates main restricted universe multiverse
deb http://mirrors.tencentyun.com/old-archives/ubuntu lucid-security main restricted universe multiverse
deb http://mirrors.tencentyun.com/old-archives/ubuntu lucid-backports main restricted universe multiverse
```

## Method 2: Running the Automated Script
Use the script [old-archive.run](http://ubuntu10-10016717.cos.myqcloud.com/old-archive.run) provided by Tencent Cloud for configuration. To do this, download the file to the CVM with Ubuntu 10.04 and run the following commands:

```
chmod +x old-archive.run
./old-archive.run
```