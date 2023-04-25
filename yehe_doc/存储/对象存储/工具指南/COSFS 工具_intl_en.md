## Overview 

COSFS allows you to mount COS buckets to local and work with the COS objects as you do with a local file system. COSFS supports the following features:
- Most features of the POSIX file system, such as reading/writing files, operations on directories/links, permission management, and uid/gid management.
- Multipart upload of large files.
- Data verification with MD5.
- Data upload to COS using [COS Migration](https://www.tencentcloud.com/document/product/436/15392) or [COSCMD](https://www.tencentcloud.com/document/product/436/10976).


## Limitations
COSFS is built on S3FS. As disks are required for COSFS' read and write operations, COSFS is only suitable for simple management of mounted files and does not support all features of a local POSIX file system. Note the following limitations when using the COSFS tool:

- Randomly writing data or appending data to a file may lead to the re-download/re-upload of the entire file. To avoid this, you can use a CVM in the same region as the bucket to accelerate the upload and download.
- When a COS bucket is mounted to multiple clients, you need to coordinate the behaviors of these clients, for example, to prevent the clients from simultaneously writing data to the same file.
- `Rename` operation on a file/folder is not atomic.
- For metadata operations such as `list directory`, COSFS performs unsatisfactorily as it requires remote access to the COS server.
- COSFS does not support hard links and is inapplicable to high-concurrency reads/writes.
- Mounting and unmounting files cannot be performed on the same mount point at the same time. You can use the `cd` command to switch to another directory and then mount and unmount the files at the mount point.
- Regular disk scanning tasks of the server may cause a high CPU utilization of COSFS, which sends a large number of HEAD and LIST requests, incurring a large amount of request fees. For more information, see [FAQs](#faq).

We recommend you use the following tools rather than COSFS:
- GooseFS-Lite: You can access COS using GooseFS-Lite, a lightweight standalone COS Fuse tool with better read/write performance and stability.
- Cloud Storage Gateway (CSG): You can access COS through CSG, which can mount COS buckets to multiple servers as network file systems. Users can use the POSIX file protocol to read and write objects in COS through mount points.
- WinFsp + GitHub + Rclone: You can use these tools to mount COS as a local drive. For more information, see [Mounting COS to Windows Server as Local Drive](https://www.tencentcloud.com/document/product/436/40490).

## Operating Environments
Mainstream Ubuntu, CentOS, SUSE, and macOS


## Installation Methods
You can install COSFS with an installation package or by compiling the source code.


### Method 1: Install with an installation package
>? This installation method supports only mainstream Ubuntu and CentOS.
>

#### Ubuntu

1. Download the appropriate installation package according to your system version. Currently, Ubuntu 14.04, 16.04, 18.04, and 20.04 are supported.
Download from GitHub:
```plaintext
#Ubuntu14.04
sudo wget https://github.com/tencentyun/cosfs/releases/download/v1.0.20/cosfs_1.0.20-ubuntu14.04_amd64.deb
#Ubuntu16.04
sudo wget https://github.com/tencentyun/cosfs/releases/download/v1.0.20/cosfs_1.0.20-ubuntu16.04_amd64.deb
#Ubuntu18.04
sudo wget https://github.com/tencentyun/cosfs/releases/download/v1.0.20/cosfs_1.0.20-ubuntu18.04_amd64.deb
#Ubuntu20.04
sudo wget https://github.com/tencentyun/cosfs/releases/download/v1.0.20/cosfs_1.0.20-ubuntu20.04_amd64.deb
```
Download from CDN:
[cosfs_1.0.20-ubuntu14.04_amd64.deb](https://cos-sdk-archive-1253960454.file.myqcloud.com/cosfs/v1.0.20/cosfs_1.0.20-ubuntu14.04_amd64.deb)
[cosfs_1.0.20-ubuntu16.04_amd64.deb](https://cos-sdk-archive-1253960454.file.myqcloud.com/cosfs/v1.0.20/cosfs_1.0.20-ubuntu16.04_amd64.deb)
[cosfs_1.0.20-ubuntu18.04_amd64.deb](https://cos-sdk-archive-1253960454.file.myqcloud.com/cosfs/v1.0.20/cosfs_1.0.20-ubuntu18.04_amd64.deb)
[cosfs_1.0.20-ubuntu20.04_amd64.deb](https://cos-sdk-archive-1253960454.file.myqcloud.com/cosfs/v1.0.20/cosfs_1.0.20-ubuntu20.04_amd64.deb)

2. Install the package. The following takes Ubuntu 16.04 as an example.
```shell
sudo dpkg -i cosfs_1.0.20-ubuntu16.04_amd64.deb
```

#### CentOS

1. Install dependencies.
```plaintext
sudo yum install libxml2-devel libcurl-devel -y
```
2. Download the appropriate installation package according to your system version. Currently, CentOS 6.5 and 7.0 are supported.
Download from GitHub:
```plaintext
#CentOS6.5
sudo wget https://github.com/tencentyun/cosfs/releases/download/v1.0.20/cosfs-1.0.20-centos6.5.x86_64.rpm
#CentOS7.0
sudo wget https://github.com/tencentyun/cosfs/releases/download/v1.0.20/cosfs-1.0.20-centos7.0.x86_64.rpm
```
Download from CDN:
[cosfs-1.0.20-centos6.5.x86_64.rpm](https://cos-sdk-archive-1253960454.file.myqcloud.com/cosfs/v1.0.20/cosfs-1.0.20-centos6.5.x86_64.rpm)
[cosfs-1.0.20-centos7.0.x86_64.rpm](https://cos-sdk-archive-1253960454.file.myqcloud.com/cosfs/v1.0.20/cosfs-1.0.20-centos7.0.x86_64.rpm)
3. Install the package. The following takes CentOS 7.0 as an example.
```shell
sudo rpm -ivh cosfs-1.0.20-centos7.0.x86_64.rpm
```
>? If the system reports the error `conflicts with file from package fuse-libs-*` during installation, add the `--force` parameter and install the package again.
>

### Method 2: Install by compiling the source code

>? This installation method supports mainstream Ubuntu, CentOS, SUSE, and macOS.
>


#### 1. Install the dependency software 
The compilation and installation of COSFS depend on software packages such as `automake`, `git`, `libcurl-devel`, `libxml2-devel`, `fuse-devel`, `make`, and `openssl-devel`. The following describes how to install dependency software on Ubuntu, CentOS, SUSE, and macOS:

- Install dependency software on the Ubuntu system:
```shell
sudo apt-get install automake autotools-dev g++ git libcurl4-gnutls-dev libfuse-dev libssl-dev libxml2-dev make pkg-config fuse
```
- Install dependency software on the CentOS system:
```shell
sudo yum install automake gcc-c++ git libcurl-devel libxml2-devel fuse-devel make openssl-devel fuse
```
- Install dependency software on the SUSE system:
```shell
sudo zypper install gcc-c++ automake make libcurl-devel libxml2-devel openssl-devel pkg-config
```
- Install dependency software on the macOS system:
```shell
brew install automake git curl libxml2 make pkg-config openssl 
brew install cask osxfuse
```

#### 2. Obtain the source code 

Download the [COSFS Source Code](https://github.com/tencentyun/cosfs) from GitHub to a specified directory. The following uses `/usr/cosfs` as an example. You can use another directory as needed.
```shell
sudo git clone https://github.com/tencentyun/cosfs /usr/cosfs
```


#### 3. Compile and install COSFS 
Open the installation directory, and execute the following command to compile and install COSFS:
```shell
cd /usr/cosfs
sudo ./autogen.sh
sudo ./configure
sudo make
sudo make install
cosfs --version  #View the COSFS version number
```

#### 4. Troubleshoot configure issues

Messages displayed during the `configure` operation vary depending on the OS. If your FUSE version is earlier than 2.8.4, the following error message will be displayed:
```shell
checking for common_lib_checking... configure: error: Package requirements (fuse >= 2.8.4 libcurl >= 7.0 libxml-2.0 >= 2.6) were not met:
  Requested 'fuse >= 2.8.4' but version of fuse is 2.8.3 
```
In this case, you need to manually install fuse 2.8.4 or later as shown below:
```shell
sudo yum -y remove fuse-devel
yum -y remove fuse-devel84%97sudo wget https://github.com/libfuse/libfuse/releases/download/fuse_2_9_4/fuse-2.9.4.tar.gz
tar -zxvf fuse-2.9.4.tar.gz
cd fuse-2.9.4
sudo ./configure
sudo make
sudo make install
export PKG_CONFIG_PATH=/usr/lib/pkgconfig:/usr/lib64/pkgconfig/:/usr/local/lib/pkgconfig
modprobe fuse   # Mount FUSE's kernel module.
echo "/usr/local/lib" >> /etc/ld.so.conf
ldconfig   #Update the dynamic link library
pkg-config --modversion fuse  #View the fuse version number. If "2.9.4" is displayed, fuse 2.9.4 is installed successfully. 
```
- Install fuse 2.8.4 or later on the SUSE system manually, as shown below:
>! During installation, you need to comment out the content of line 222 in `example/fusexmp.c` by using `/*content*/`. Otherwise, an error will be reported when you use Make.
>
```shell
zypper remove fuse libfuse2
yum -y remove fuse-devel84%97sudo wget https://github.com/libfuse/libfuse/releases/download/fuse_2_9_4/fuse-2.9.4.tar.gz
tar -zxvf fuse-2.9.4.tar.gz
cd fuse-2.9.4
sudo ./configure
sudo make 
sudo make install
export PKG_CONFIG_PATH=/usr/lib/pkgconfig:/usr/lib64/pkgconfig/:/usr/local/lib/pkgconfig
modprobe fuse   # Mount FUSE's kernel module.
echo "/usr/local/lib" >> /etc/ld.so.conf
ldconfig   # Update the dynamic-link library.
pkg-config --modversion fuse   #View the fuse version number. If "2.9.4" is displayed, fuse 2.9.4 is installed successfully. 
```
- When the "configure" operation is performed on macOS, the following may be displayed:
```shell
configure: error: Package requirements (fuse >= 2.7.3 libcurl >= 7.0 libxml-2.0 >2.6 libcrypto >= 0.9) were not met
No package 'libcrypto' found
```
 In this case, you need to set the variable PKG_CONFIG_PATH, so that the pkg-config tool can find openssl. The command is as follows:
```shell
brew info openssl 
export PKG_CONFIG_PATH=/usr/local/opt/openssl/lib/pkgconfig #You may need to modify this command based on the message displayed for the previous command.
```


## How to Use

### 1. Configure the key file
Write the bucket information in the `/etc/passwd-cosfs` file, including the bucket name (in `BucketName-APPID` format), &lt;SecretId&gt;, as well as &lt;SecretKey&gt;, and use colons (:) to separate them. To avoid compromising your key, set permissions for the key file to 640. Run the following command to configure the `/etc/passwd-cosfs` key file:
```shell
sudo su  # Switch to the root account to modify the /etc/passwd-cosfs file. Skip this step if you have already logged in with the root account
echo <BucketName-APPID>:<SecretId>:<SecretKey> > /etc/passwd-cosfs
chmod 640 /etc/passwd-cosfs
```

>?You need to replace the content enclosed in &lt;&gt; with the actual information.
>- <BucketName-APPID> indicates the name of the bucket. For more information, see [Bucket Naming Conventions](https://www.tencentcloud.com/document/product/436/13312).
> - <SecretId> and <SecretKey> are key information. We recommend you use a sub-account key and authorize a sub-account by following the [Notes on Principle of Least Privilege](https://www.tencentcloud.com/document/product/436/32972) to reduce risks. For details on how to obtain a sub-account key, see [Access Key](https://www.tencentcloud.com/document/product/598/32675).
>- You can configure the key in `$HOME/.passwd-cosfs`. Alternatively, you can run `-opasswd_file=[path]` to specify the directory of the key file and then set permissions of the key file to 600.
> 

**Example:**

```shell
echo examplebucket-1250000000:AKIDHTVVaVR6e3****:PdkhT9e2rZCfy6**** > /etc/passwd-cosfs
chmod 640 /etc/passwd-cosfs
```

>! If your COSFS version is v1.0.5 or earlier, the configuration file format is &lt;BucketName>:&lt;SecretId>:&lt;SecretKey>.
>


### 2. Run the tool
Run the following command to mount the bucket configured in the key file to a specified directory:

```shell
cosfs <BucketName-APPID> <MountPoint> -ourl=http://cos.<Region>.myqcloud.com -odbglevel=info -oallow_other
```
Parameter description
- &lt;MountPoint&gt; is the mount point, for example, `/mnt`.
- <Region> is the abbreviation for the region, such as `ap-guangzhou` and `eu-frankfurt`. For more information about region abbreviations, see [Regions and Access Endpoints](https://www.tencentcloud.com/document/product/436/6224).
- `-odbglevel` specifies the log level. The default value is `crit`. Available options are `crit`, `error`, `warn`, `info`, and `debug`.
- `-oallow_other` allows other users to access the mount folder.

**Example:**

```shell
mkdir -p /mnt/cosfs
cosfs examplebucket-1250000000 /mnt/cosfs -ourl=http://cos.ap-guangzhou.myqcloud.com -odbglevel=info -onoxattr -oallow_other
```

>!
>- To improve performance, COSFS uses the system disk by default for the temporary cache of uploaded and downloaded files and releases space after files are closed. When a large number of concurrent files are opened or large files are read or written, COSFS uses hard disk space as much as possible to improve performance. By default, only 100 MB of free hard disk space is reserved for other applications. You can use the `oensure_diskfree=[size]` option to set the size of available hard disk space in MB reserved by COSFS. For example, `-oensure_diskfree=1024` indicates that COSFS will reserve 1024 MB of free space.
>- If your COSFS is v1.0.5 or earlier, use the following mount command: `cosfs &lt;APPID>:&lt;BucketName> &lt;MountPoint> -ourl=&lt;CosDomainName> -oallow_other`.
>


### 3. Unmount a bucket

Unmount a bucket using the following commands:

```shell
Method 1: Use `fusermount -u /mnt, fusermount` to unmount a FUSE file system 
Method 2: Use `umount -l /mnt`. The unmount operation will be performed when no program is using any file in the file system.
Method 3: Use `umount /mnt`. If any program is using a file in the file system during the unmount, an error will be reported.
```

## Common Mounting Options

#### -omultipart_size=[size]
Specifies the size (in MB) of each part for the multipart upload. It is 10 MB by default. Up to 10,000 parts are allowed for a file in a multipart upload. If the file is larger than 100 GB (10 MB \* 10000), you need to adjust this parameter accordingly.

#### -oallow_other
Allows other users to access the folder to which the bucket is mounted.

#### -odel_cache
By default, to ensure optimal performance, the COSFS does not clear local cached data after a bucket is unmounted. To enable the COSFS to automatically clear cached data upon its exit, you can add this option during mounting.

####  -onoxattr
Disables getattr/setxattr. For the COSFS earlier than 1.0.9, you cannot set or obtain extended attributes. If the use_xattr option is used during mounting, the files may fail to be copied to the bucket.

#### -opasswd_file=[path]
Specifies the path for the COSFS key file. You need to set the permission for the key file to 600.

#### -odbglevel=[dbg|info|warn|err|crit]

Sets the log level for COSFS. Valid values: `info`, `dbg`, `warn`, `err`, `crit`. You are advised to set it to `info` in the production environment, and `dbg` for debugging. If you do not clear system logs regularly, or numerous logs will be generated due to a huge access volume, you can set it to `err` or `crit`.

#### -oumask=[perm]

Removes the permission of a specified type of users to operate files in the mounting destination directory. For example, when -oumask=755, the permission for the mounting destination directory is changed to 022.

#### -ouid=[uid]
Allows the user whose ID is [uid] to access all the files in the mounting destination directory without being restricted by the file permission bits.
You can obtain the uid of a user using the ID command `id -u username`. For example, you can run `id -u user_00` to obtain the uid of user_00.

#### -oensure_diskfree=[size]

To improve performance, COSFS uses the system disk by default for the temporary cache of uploaded and downloaded files and releases space after files are closed. When a large number of concurrent files are opened or large files are read or written, COSFS uses hard disk space as much as possible to improve performance. By default, only 100 MB of free hard disk space is reserved for other applications. You can use the `oensure_diskfree=[size]` option to set the size of available hard disk space in MB reserved by COSFS. For example, `-oensure_diskfree=1024` indicates that COSFS will reserve 1024 MB of free space.


<span id="faq"></span>
## FAQs

Some FAQs about COSFS are listed below. If you have more questions, see [COSFS FAQs](https://www.tencentcloud.com/document/product/436/30587).

- [What should I do if COSFS has a high CPU utilization, sends a large number of HEAD and LIST requests to COS, and incurs a large amount of request fees during a certain period of time every day?](https://intl.cloud.tencent.com/document/product/436/30587#.E5.AE.89.E8.A3.85-cosfs-rpm-.E5.8C.85.E6.97.B6.EF.BC.8C.E6.8F.90.E7.A4.BA-conflicts-with-file-from-package-fuse-libs-*.EF.BC.8C.E6.80.8E.E4.B9.88.E5.8A.9E.EF.BC.9F)
 
- [Why does it take the ls command so long to return when I run it in a COSFS directory?](https://intl.cloud.tencent.com/document/product/436/30587#.E5.9C.A8-cosfs-.E7.9A.84.E7.9B.AE.E5.BD.95.E4.B8.AD.E6.89.A7.E8.A1.8C-ls-.E5.91.BD.E4.BB.A4.EF.BC.8C.E4.B8.BA.E4.BB.80.E4.B9.88.E5.91.BD.E4.BB.A4.E8.BF.94.E5.9B.9E.E9.9C.80.E8.A6.81.E5.BE.88.E4.B9.85.E7.9A.84.E6.97.B6.E9.97.B4.EF.BC.9F)


