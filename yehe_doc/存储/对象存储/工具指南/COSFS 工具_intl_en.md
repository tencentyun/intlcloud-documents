## Feature Description 

COSFS allows you to mount COS buckets to local and work with the COS objects as you do with a local file system. COSFS supports the following features:
- Most features of the POSIX file system, such as reading/writing files, operations on directories/links, permission management, and uid/gid management.
- Multipart upload of large files.
- Data verification with MD5.
- Upload data to COS using [COS Migration](https://intl.cloud.tencent.com/document/product/436/15392) or [COSCMD](https://intl.cloud.tencent.com/document/product/436/10976).

## Limitations
**COSFS is built on S3FS. As the disk is required for COSFS′s read and write operations, COSFS is only suitable for simple management of the mounted files and does not support all features of a local file system. Besides, it cannot outperform Cloud Block Storage (CBS) or Cloud File Storage (CFS).** To use COSFS, note that:

- Randomly writing data or appending data to a file may lead to the re-download/re-upload of the entire file. To avoid this, you can use a CVM in the same region as the bucket to accelerate the upload and download.
- When a COS bucket is mounted to multiple clients, you need to coordinate the behaviors of these clients, for example, to prevent the clients from simultaneously writing data to the same file.
- `Rename` operation on a file/folder is not atomic.
- For metadata operations such as `list directory`, COSFS performs unsatisfactorily as it requires remote access to the COS server.
- COSFS does not support hard links and is inapplicable to high-concurrency reads/writes.
- Mounting and unmounting files cannot be performed on the same mounting point at the same time. You can use the `cd` command to switch to another directory and then mount and unmount the files at the mounting point.

## Operating Environments
Mainstream Ubuntu, CentOS, SUSE, and macOS


## Installation
You can install COSFS with an installation package or by compiling the source code.


### Method 1: Install with an installation package
>? This installation method supports only mainstream Ubuntu and CentOS.
>

#### Ubuntu

1. Download the appropriate installation package according to your system version. Currently, Ubuntu 14.04, 16.04, 18.04, and 20.04 are supported.
```plaintext
#Ubuntu14.04
wget https://github.com/tencentyun/cosfs/releases/download/v1.0.19/cosfs_1.0.19-ubuntu14.04_amd64.deb
#Ubuntu16.04
wget https://github.com/tencentyun/cosfs/releases/download/v1.0.19/cosfs_1.0.19-ubuntu16.04_amd64.deb
#Ubuntu18.04
wget https://github.com/tencentyun/cosfs/releases/download/v1.0.19/cosfs_1.0.19-ubuntu18.04_amd64.deb
#Ubuntu20.04
wget https://github.com/tencentyun/cosfs/releases/download/v1.0.19/cosfs_1.0.19-ubuntu20.04_amd64.deb
```
2. Install the package. The following takes Ubuntu 16.04 as an example.
```shell
sudo dpkg -i cosfs_1.0.19-ubuntu16.04_amd64.deb
```

#### CentOS

1. Install dependencies.
```plaintext
sudo yum install libxml2-devel libcurl-devel -y
```
2. Download the appropriate installation package according to your system version. Currently, CentOS 6.5 and 7.0 are supported.
```plaintext
#CentOS6.5
wget https://github.com/tencentyun/cosfs/releases/download/v1.0.19/cosfs-1.0.19-centos6.5.x86_64.rpm
#CentOS7.0
wget https://github.com/tencentyun/cosfs/releases/download/v1.0.19/cosfs-1.0.19-centos7.0.x86_64.rpm
```
3. Install the package. The following takes CentOS 7.0 as an example.
```shell
sudo rpm -ivh cosfs-1.0.19-centos7.0.x86_64.rpm
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
brew cask install osxfuse
```

#### 2. Obtain the source code 

Download the [COSFS Source Code](https://github.com/tencentyun/cosfs) from GitHub to a specified directory. The following uses `/usr/cosfs` as an example. You can use another directory as needed.
```shell
git clone https://github.com/tencentyun/cosfs /usr/cosfs
```


#### 3. Compile and install COSFS 
Open the installation directory, and execute the following command to compile and install COSFS:
```shell
cd /usr/cosfs
./autogen.sh
./configure
make
sudo make install
cosfs --version  #View the COSFS version number
```

#### 4. Troubleshooting configure issues

Messages displayed during the `configure` operation vary depending on the OS. If your FUSE version is earlier than 2.8.4, the following error message will be displayed:
```shell
checking for common_lib_checking... configure: error: Package requirements (fuse >= 2.8.4 libcurl >= 7.0 libxml-2.0 >= 2.6) were not met:
  Requested 'fuse >= 2.8.4' but version of fuse is 2.8.3 
```
In this case, you need to manually install fuse 2.8.4 or above as shown below:
```shell
yum -y remove fuse-devel
wget https://github.com/libfuse/libfuse/releases/download/fuse_2_9_4/fuse-2.9.4.tar.gz
tar -zxvf fuse-2.9.4.tar.gz
cd fuse-2.9.4
./configure
make
make install
export PKG_CONFIG_PATH=/usr/lib/pkgconfig:/usr/lib64/pkgconfig/:/usr/local/lib/pkgconfig
modprobe fuse   # Mount FUSE's kernel module.
echo "/usr/local/lib" >> /etc/ld.so.conf
ldconfig   # Update the dynamic-link library.
pkg-config --modversion fuse  #View the fuse version number. If "2.9.4" is displayed, fuse 2.9.4 is installed successfully. 
```
- Install FUSE 2.8.4 or later on the SUSE system manually, as shown below:
>! During installatioDuring installation, you need to comment out the content of line 222 in `example/fusexmp.c` by using `/*content*/`. Otherwise, an error will be reported when you use Make.
>
```shell
zypper remove fuse libfuse2
wget https://github.com/libfuse/libfuse/releases/download/fuse_2_9_4/fuse-2.9.4.tar.gz
tar -zxvf fuse-2.9.4.tar.gz
cd fuse-2.9.4
./configure
make 
make install
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


## Directions

### 1. Configure the key file
Write the bucket information in the `/etc/passwd-cosfs` file, including the bucket name (in `BucketName-APPID` format) &lt;SecretId&gt;, as well as &lt;SecretKey&gt;, and use colons (:) to separate them. To avoid compromising your key, you need to set permissions for the key file to 640. You can run the following command to configure the `/etc/passwd-cosfs` key file:
```shell
sudo su  # Switch to the root account to modify the /etc/passwd-cosfs file. Skip this step if you have already logged in with the root account
echo <BucketName-APPID>:<SecretId>:<SecretKey> > /etc/passwd-cosfs
chmod 640 /etc/passwd-cosfs
```

>?You need to replace the content enclosed in &lt;&gt; with the actual information.
>- &lt;BucketName-APPID&gt; indicates the name of the bucket. For more information, please see [Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312).
>- &lt;SecretId&gt; and &lt;SecretKey&gt; are information about the key, which can be obtained and created at [Manage API Key](https://console.cloud.tencent.com/cam/capi) in the CAM console.
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
You can run the following command to mount the bucket configured in the key file to a specified directory:

```shell
cosfs <BucketName-APPID> <MountPoint> -ourl=http://cos.<Region>.myqcloud.com -odbglevel=info -oallow_other
```
Where:
- &lt;MountPoint&gt; is the mount point, for example, `/mnt`.
- &lt;Region&gt; is the abbreviation for the region, such as `ap-guangzhou` and `eu-frankfurt`. For more information about region abbreviations, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224).
- `-odbglevel` specifies the log level. The default value is `crit`. Available options are `crit`, `error`, `warn`, `info`, and `debug`.
- `-oallow_other` allows other users to access the mount point.

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

Sets the log level for COSFS. Valid values are `info`, `dbg`, `warn`, `err`, and `crit`. You are advised to set it to `info` in the production environment, and `dbg` for debugging. If you do not clear system logs regularly, or numerous logs will be generated due to a huge access volume, you can set it to `err` or `crit`.

#### -oumask=[perm]

Removes the permission of a specified type of users to operate files in the mounting destination directory. For example, when -oumask=755, the permission for the mounting destination directory is changed to 022.

#### -ouid=[uid]
Allows the user whose id is [uid] to access all the files in the mounting destination directory without being restricted by the file permission bits.
You can obtain the uid of a user using the id command `id -u username`. For example, you can execute `id -u user_00` to obtain the uid of user_00.

#### -oensure_diskfree=[size]

To improve performance, COSFS uses the system disk by default for the temporary cache of uploaded and downloaded files and releases space after files are closed. When a large number of concurrent files are opened or large files are read or written, COSFS uses hard disk space as much as possible to improve performance. By default, only 100 MB of free hard disk space is reserved for other applications. You can use the `oensure_diskfree=[size]` option to set the size of available hard disk space in MB reserved by COSFS. For example, `-oensure_diskfree=1024` indicates that COSFS will reserve 1024 MB of free space.


## FAQs
If you have any questions about COSFS, please see [COSFS FAQs](https://intl.cloud.tencent.com/document/product/436/30587).
