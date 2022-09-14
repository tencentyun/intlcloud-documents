## Overview 

COSFS allows you to mount COS buckets to a local file system to directly manipulate COS objects. It has the following features:
- Most features of the POSIX file system, such as reading/writing files, operations on directories/links, permission management, and UID/GID management.
- Multipart upload of large files.
- Data verification through MD5.
- Data upload to COS through [COS Migration](https://intl.cloud.tencent.com/document/product/436/15392) or [COSCMD](https://intl.cloud.tencent.com/document/product/436/10976).

## Limitations
**COSFS is built on S3FS. As the disk is required for COSFS read and write operations, COSFS is only suitable for simple management of mounted files but does not support all features of a local file system. Moreover, it cannot be used as a substitute for Cloud Block Storage (CBS) or Cloud File Storage (CFS).** To use COSFS, note that:

- Randomly writing data or appending data to a file may lead to the redownload/reupload of the entire file. To avoid this, you can use a CVM instance in the same region as the bucket to accelerate the upload and download.
- When a COS bucket is mounted to multiple clients, you need to coordinate the behaviors of these clients, for example, to prevent them from simultaneously writing data to the same file.
- `Rename` operation on a file/folder is not atomic.
- For metadata operations such as `list directory`, COSFS performs unsatisfactorily as it requires remote access to the COS server.
- COSFS does not support hard links and is not suitable for high-concurrency reads/writes.
- Mounting and unmounting files cannot be performed on the same mount target at the same time. You can use the `cd` command to switch to another directory and then mount and unmount files at the mount target.

## Operating Environment
Ubuntu, CentOS, SUSE, and macOS.


## Installation
You can install COSFS with an installation package or by compiling the source code.


### Option 1: Install with an installation package
>? This installation method is supported only for Ubuntu and CentOS.
>

#### Ubuntu

1. Download the appropriate installation package based on your system version. Currently, Ubuntu 14.04, 16.04, 18.04, and 20.04 are supported.
Download from GitHub:
```plaintext
#Ubuntu 14.04
sudo wget https://github.com/tencentyun/cosfs/releases/download/v1.0.20/cosfs_1.0.20-ubuntu14.04_amd64.deb
#Ubuntu 16.04
sudo wget https://github.com/tencentyun/cosfs/releases/download/v1.0.20/cosfs_1.0.20-ubuntu16.04_amd64.deb
#Ubuntu 18.04
sudo wget https://github.com/tencentyun/cosfs/releases/download/v1.0.20/cosfs_1.0.20-ubuntu18.04_amd64.deb
#Ubuntu 20.04
sudo wget https://github.com/tencentyun/cosfs/releases/download/v1.0.20/cosfs_1.0.20-ubuntu20.04_amd64.deb
```
Download from CDN:
[cosfs_1.0.20-ubuntu14.04_amd64.deb](https://cos-sdk-archive-1253960454.file.myqcloud.com/cosfs/v1.0.20/cosfs_1.0.20-ubuntu14.04_amd64.deb)
[cosfs_1.0.20-ubuntu16.04_amd64.deb](https://cos-sdk-archive-1253960454.file.myqcloud.com/cosfs/v1.0.20/cosfs_1.0.20-ubuntu16.04_amd64.deb)
[cosfs_1.0.20-ubuntu18.04_amd64.deb](https://cos-sdk-archive-1253960454.file.myqcloud.com/cosfs/v1.0.20/cosfs_1.0.20-ubuntu18.04_amd64.deb)
[cosfs_1.0.20-ubuntu18.04_amd64.deb](https://cos-sdk-archive-1253960454.file.myqcloud.com/cosfs/v1.0.20/cosfs_1.0.20-ubuntu20.04_amd64.deb)

2. Install the package. The following takes Ubuntu 16.04 as an example.
```shell
sudo dpkg -i cosfs_1.0.20-ubuntu16.04_amd64.deb
```

#### CentOS

1. Install dependencies.
```plaintext
sudo yum install libxml2-devel libcurl-devel -y
```
2. Download the appropriate installation package based on your system version. Currently, CentOS 6.5 and 7.0 are supported.
Download from GitHub:
```plaintext
#CentOS 6.5
sudo wget https://github.com/tencentyun/cosfs/releases/download/v1.0.20/cosfs-1.0.20-centos6.5.x86_64.rpm
#CentOS 7.0
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

### Option 2: Install by compiling the source code

>? This installation method is supported for Ubuntu, CentOS, SUSE, and macOS.
>


#### 1. Install the dependency software 
The compilation and installation of COSFS depend on software packages such as `automake`, `git`, `libcurl-devel`, `libxml2-devel`, `fuse-devel`, `make`, and `openssl-devel`. The following describes how to install dependency software on Ubuntu, CentOS, SUSE, and macOS:

- Install dependency software on Ubuntu:
```shell
sudo apt-get install automake autotools-dev g++ git libcurl4-gnutls-dev libfuse-dev libssl-dev libxml2-dev make pkg-config fuse
```
- Install dependency software on CentOS:
```shell
sudo yum install automake gcc-c++ git libcurl-devel libxml2-devel fuse-devel make openssl-devel fuse
```
- Install dependency software on SUSE:
```shell
sudo zypper install gcc-c++ automake make libcurl-devel libxml2-devel openssl-devel pkg-config
```
- Install dependency software on macOS:
```shell
brew install automake git curl libxml2 make pkg-config openssl 
brew install cask osxfuse
```

#### 2. Get the source code 

Download the COSFS source code from [GitHub](https://github.com/tencentyun/cosfs) to a specified directory. The following uses `/usr/cosfs` as an example. You can use another directory as needed.
```shell
sudo git clone https://github.com/tencentyun/cosfs /usr/cosfs
```


#### 3. Compile and install COSFS 
Open the installation directory and run the following command to compile and install COSFS:
```shell
cd /usr/cosfs
sudo ./autogen.sh
sudo ./configure
sudo make
sudo make install
cosfs --version  # View the COSFS version number.
```

#### 4. Troubleshoot `configure` issues

Messages displayed during the `configure` operation vary by OS. If your FUSE version is earlier than 2.8.4, the following error message will be displayed:
```shell
checking for common_lib_checking... configure: error: Package requirements (fuse >= 2.8.4 libcurl >= 7.0 libxml-2.0 >= 2.6) were not met:
  Requested 'fuse >= 2.8.4' but version of fuse is 2.8.3 
```
In this case, you need to manually install FUSE 2.8.4 or later as follows:
```shell
sudo yum -y remove fuse-devel
sudo wget https://github.com/libfuse/libfuse/releases/download/fuse_2_9_4/fuse-2.9.4.tar.gz
tar -zxvf fuse-2.9.4.tar.gz
cd fuse-2.9.4
sudo ./configure
sudo make
sudo make install
export PKG_CONFIG_PATH=/usr/lib/pkgconfig:/usr/lib64/pkgconfig/:/usr/local/lib/pkgconfig
modprobe fuse   # Mount FUSE's kernel module.
echo "/usr/local/lib" >> /etc/ld.so.conf
ldconfig   # Update the dynamic link library.
pkg-config --modversion fuse  # View the FUSE version number. If "2.9.4" is displayed, FUSE 2.9.4 is installed successfully. 
```
- Install FUSE 2.8.4 or later on the SUSE system manually as follows:
>! During installation, you need to comment out the content of line 222 in `example/fusexmp.c` by using `/*content*/`; otherwise, an error will be reported when you use Make.
>
```shell
zypper remove fuse libfuse2
sudo wget https://github.com/libfuse/libfuse/releases/download/fuse_2_9_4/fuse-2.9.4.tar.gz
tar -zxvf fuse-2.9.4.tar.gz
cd fuse-2.9.4
sudo ./configure
sudo make 
sudo make install
export PKG_CONFIG_PATH=/usr/lib/pkgconfig:/usr/lib64/pkgconfig/:/usr/local/lib/pkgconfig
modprobe fuse   # Mount FUSE's kernel module.
echo "/usr/local/lib" >> /etc/ld.so.conf
ldconfig   # Update the dynamic link library.
pkg-config --modversion fuse  # View the FUSE version number. If "2.9.4" is displayed, FUSE 2.9.4 is installed successfully. 
```
- When the `configure` operation is performed on macOS, the following may be displayed:
```shell
configure: error: Package requirements (fuse >= 2.7.3 libcurl >= 7.0 libxml-2.0 >2.6 libcrypto >= 0.9) were not met
No package 'libcrypto' found
```
 In this case, you need to set the `PKG_CONFIG_PATH` variable so that the pkg-config tool can find OpenSSL. The command is as follows:
```shell
brew info openssl 
export PKG_CONFIG_PATH=/usr/local/opt/openssl/lib/pkgconfig # You may need to modify this command based on the message displayed for the previous command.
```


## Directions

### 1. Configure the key file
Write the bucket information in the `/etc/passwd-cosfs` file, including the bucket name (in `BucketName-APPID` format), &lt;SecretId&gt;, and &lt;SecretKey&gt;, and separate them by colon. To avoid compromising your key, set permissions for the key file to 640. Run the following command to configure the `/etc/passwd-cosfs` key file:
```shell
sudo su  # Switch to the root account to modify the `/etc/passwd-cosfs` file. Skip this step if you have already logged in with the root account
echo <BucketName-APPID>:<SecretId>:<SecretKey> > /etc/passwd-cosfs
chmod 640 /etc/passwd-cosfs
```

>? You need to replace the content enclosed in &lt;&gt; with the actual information.
>- &lt;BucketName-APPID&gt; indicates the name of the bucket. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312).
>- &lt;SecretId&gt; and &lt;SecretKey&gt; are information of the key, which can be created and obtained on the [Manage API Key](https://console.cloud.tencent.com/cam/capi) page in the CAM console.
>- You can configure the key in `$HOME/.passwd-cosfs`. You can also run `-opasswd_file=[path]` to specify the directory of the key file and then set permissions of the key file to 600.
> 

**Example:**

```shell
echo examplebucket-1250000000:AKIDHTVVaVR6e3****:PdkhT9e2rZCfy6**** > /etc/passwd-cosfs
chmod 640 /etc/passwd-cosfs
```

>! If your COSFS version is 1.0.5 or earlier, the configuration file format is &lt;BucketName>:&lt;SecretId>:&lt;SecretKey>.
>


### 2. Run the tool
Run the following command to mount the bucket configured in the key file to a specified directory:

```shell
cosfs <BucketName-APPID> <MountPoint> -ourl=http://cos.<Region>.myqcloud.com -odbglevel=info -oallow_other
```
Here:
- &lt;MountPoint&gt; is the mount target, such as `/mnt`.
- &lt;Region&gt; is the abbreviation for the region, such as `ap-guangzhou` and `eu-frankfurt`. For region abbreviations, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224).
- `-odbglevel` specifies the log level. Valid values: `crit`, `error`, `warn`, `info`, `debug`. Default value: `crit`.
- `-oallow_other` allows other users to access the mount target.

**Example:**

```shell
mkdir -p /mnt/cosfs
cosfs examplebucket-1250000000 /mnt/cosfs -ourl=http://cos.ap-guangzhou.myqcloud.com -odbglevel=info -onoxattr -oallow_other
```

>!
>- To improve the performance, COSFS uses the system disk by default for the temporary cache of uploaded and downloaded files and releases space after files are closed. When many concurrent files are opened or large files are read or written, COSFS uses the disk space as much as possible to improve the performance. By default, only 100 MB of free disk space is reserved for other applications. You can use the `oensure_diskfree=[size]` option to set the size of available disk space in MB reserved by COSFS. For example, `-oensure_diskfree=1024` indicates that COSFS will reserve 1,024 MB of free space.
>- If your COSFS version is 1.0.5 or earlier, use the following mount command: cosfs &lt;APPID>:&lt;BucketName> &lt;MountPoint> -ourl=&lt;CosDomainName> -oallow_other.
>


### 3. Unmount a bucket

Unmount a bucket as follows:

```shell
Option 1: Run `fusermount -u /mnt` to unmount a FUSE file system. 
Option 2: Run `umount -l /mnt`. The unmount operation will be performed when no program is using any file in the file system.
Option 3: Run `umount /mnt`. If any program is using a file in the file system during the unmount, an error will be reported.
```

## Common Mount Options

#### -omultipart_size=[size]
Specifies the size in MB of each part for the multipart upload. It is 10 MB by default. Up to 10,000 parts are allowed for a file in a multipart upload. If the file is larger than 100 GB (10 MB \* 10000), you need to adjust this parameter accordingly.

#### -oallow_other
Allows other users to access the folder to which the bucket is mounted.

#### -odel_cache
By default, to ensure the optimal performance, COSFS does not clear local cached data after the bucket is unmounted. To make COSFS automatically clear cached data upon exit, add this option during mounting.

####  -onoxattr
Disables the getattr/setxattr feature. For COSFS earlier than v1.0.9, you cannot set or obtain extended attributes. If the `use_xattr` option is used during mounting, files may fail to be copied to the bucket.

#### -opasswd_file=[path]
Specifies the path for the COSFS key file. You need to set the permission for the key file to 600.

#### -odbglevel=[dbg|info|warn|err|crit]

Sets the log level for COSFS. Valid values: `info`, `dbg`, `warn`, `err`, `crit`. We recommend you set it to `info` in the production environment or `dbg` in the debugging environment. If you don't clear system logs regularly, or numerous logs will be generated due to a huge access request volume, you can set it to `err` or `crit`.

#### -oumask=[perm]

Revokes the permission granted to a specified type of users to manipulate files in the mount destination directory. For example, `-oumask=755` changes the permission for the mount destination directory to 022.

#### -ouid=[uid]
Allows the user with ID [uid] to access all files in the mount destination directory without being restricted by the file permission bits.
You can obtain the uid of a user by using the ID command `id -u username`. For example, you can run `id -u user_00` to get the uid of user_00.

#### -oensure_diskfree=[size]

To improve the performance, COSFS uses the system disk by default for the temporary cache of uploaded and downloaded files and releases space after files are closed. When many concurrent files are opened or large files are read or written, COSFS uses the disk space as much as possible to improve the performance. By default, only 100 MB of free disk space is reserved for other applications. You can use the `oensure_diskfree=[size]` option to set the size of available disk space in MB reserved by COSFS. For example, `-oensure_diskfree=1024` indicates that COSFS will reserve 1,024 MB of free space.


## FAQs
If you have any questions about COSFS, see [COSFS](https://intl.cloud.tencent.com/document/product/436/30587).
