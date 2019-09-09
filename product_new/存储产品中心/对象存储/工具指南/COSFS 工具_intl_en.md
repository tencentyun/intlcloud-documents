

## Description 

COSFS allows you to mount COS buckets locally and work with the objects in Tencent Cloud COS in the same way as you do with a local file system. COSFS supports the following features:
- Most features of the POSIX file system, such as reading/writing files, operations on directories/links, permission management, and uid/gid management.
- Multipart upload of large files.
- Data verification with MD5.
- Upload local data to COS ([COS Migration](https://cloud.tencent.com/document/product/436/15392) or [COSCMD](https://cloud.tencent.com/document/product/436/10976) is recommended).

## Limitations
**Built on S3FS, COSFS is only suitable for simple management of mounted files, and does not support some features of a local file system. It cannot replace Cloud Block Storage (CBS) or Cloud File Storage (CFS) for the reason of performance.** Please note:

- Randomly writing data or appending data to a file may rewrite the entire file. To avoid this, you can use a CVM in a same region as the bucket to accelerate the upload and download of the file.
- When a COS bucket is mounted to multiple clients, you need to coordinate the behaviors of these clients, for example, to prevent the clients from simultaneously writing data to the same file.
- `Rename` operation on a file/folder is not atomic.
- For metadata operations such as `list directory`, COSFS has a limited performance, because remote access to the COS server is required.
- COSFS does not support hard link, and is inapplicable to the scenarios involving high-concurrency read/write operations.
- Mounting and unmounting files cannot be performed on the same mounting point at the same time. You can use the `cd` command to switch to another directory and then mount and unmount the files at the mounting point.

## Installation and Usage 
### Operating Systems 
Ubuntu, CentOS, SUSE, and macOS.

### Installation

#### 1. Obtain the source code 
Download the [COSFS Source Code](https://github.com/tencentyun/cosfs) from the GitHub to a specified directory, for example, `/usr/cosfs`.
```shell
git clone https://github.com/tencentyun/cosfs /usr/cosfs
```

#### 2. Install the dependency software 
The compilation and installation of COSFS depend on the software packages such as automake, git, libcurl-devel, libxml2-devel, fuse-devel, make, and openssl-devel. The following describes how to install dependency software on Ubuntu, CentOS, SUSE, and macOS:

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
#### 3. Compile and install COSFS 
Open the installation directory, and execute the following command to compile and install COSFS:
```shell
cd /usr/cosfs
./autogen.sh
./configure
make
sudo make install
cosfs --version  #View the cosfs version number
```

During the "configure" operation, a message is displayed, which varies with different operating systems:
- On a system where the fuse version is earlier than 2.8.4, the following error message is displayed during the "configure" operation:
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
modprobe fuse   #Mount the fuse's kernel module
echo "/usr/local/lib" >> /etc/ld.so.conf
ldconfig   #Update the dynamic link library
pkg-config --modversion fuse  #View the fuse version number. If "2.9.4" is displayed, fuse 2.9.4 is installed successfully. 
```
Install fuse 2.8.4 or above on the SUSE system, as shown below:
>During installation, you need to comment out the content of line 222 in the example/fusexmp.c file by using `/*content*/`. Otherwise, an error message is displayed when "make" is executed.

	```shell
	zypper remove fuse libfuse2
	wget https://github.com/libfuse/libfuse/releases/download/fuse_2_9_4/fuse-2.9.4.tar.gz
	tar -zxvf fuse-2.9.4.tar.gz
	cd fuse-2.9.4
	./configure
	make 
	make install
	export PKG_CONFIG_PATH=/usr/lib/pkgconfig:/usr/lib64/pkgconfig/:/usr/local/lib/pkgconfig
	modprobe fuse   #Mount the fuse's kernel module
	echo "/usr/local/lib" >> /etc/ld.so.conf
	ldconfig   #Update the dynamic link library
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

### Usage of COSFS

#### 1. Configure the key file
In the /etc/passwd-cosfs file, write the bucket name (such as &lt;BucketName-APPID&gt;), and &lt;SecretId&gt; and &lt;SecretKey&gt; for the bucket. The three items are separated with half-width colons (:). In addition, to prevent key leakage, you need to set the permission for the key file to 640. The command used to configure the /etc/passwd-cosfs key file is as follows:
```shell
echo <BucketName-APPID>:<SecretId>:<SecretKey> > /etc/passwd-cosfs
chmod 640 /etc/passwd-cosfs
```
>Replace &lt;BucketName-APPID&gt;, &lt;SecretId&gt;, and &lt;SecretKey&gt; with the information of your bucket.
>For the bucket naming conventions, see [Bucket Naming Conventions](https://cloud.tencent.com/document/product/436/13312#.E5.91.BD.E5.90.8D.E8.A7.84.E8.8C.83). Go to [Cloud API Key Management](https://console.cloud.tencent.com/cam/capi) in the CAM Console to obtain &lt;SecretId&gt; and &lt;SecretKey&gt;. In addition, you may store the keys in the **$HOME/.passwd-cosfs** file, or specify a path for the key file using **-opasswd_file=[path]**. In this case, you need to set the permission for the key file to 600.

**Sample:**

```shell
echo examplebucket-1250000000:AKIDHTVVaVR6e3:PdkhT9e2rZCfy6 > /etc/passwd-cosfs
chmod 640 /etc/passwd-cosfs
```

#### 2. Run the tool
After the configuration of key file, mount the bucket to the specified directory using the following command:

```shell
cosfs <BucketName-APPID> <MountPoint> -ourl=<CosDomainName> -odbglevel=info
```
Where:
- &lt;MountPoint&gt; is the local directory to which you want to mount the bucket (e.g. /mnt).
- &lt;CosDomainName&gt; is the access domain name for the bucket and is in a form of `http://cos.<Region>.myqcloud.com` (applicable to XML APIs and should not contain the bucket name). &lt;Region&gt; is the region name in short, for example, ap-guangzhou and eu-frankfurt. For more information, see [Regions and Endpoints](https://cloud.tencent.com/document/product/436/6224).
- -odbglevel specifies the log level.

**Sample:**

```shell
mkdir -p /mnt/cosfs
cosfs examplebucket-1250000000 /mnt/cosfs -ourl=http://cos.ap-guangzhou.myqcloud.com -odbglevel=info -onoxattr
```

>The mounting command for the COSFS earlier than v1.0.5 is as follows:
```shell
cosfs <APPID>:<BucketName> <MountPoint> -ourl=<CosDomainName>
```
The configuration file for the COSFS earlier than v1.0.5 is in the following format:
```shell
<BucketName>:<SecretId>:<SecretKey>
```

#### 3. Unmount a bucket

Unmount a bucket using the following commands:

```shell
fusermount -u /mnt or umount -l /mnt
```

## Common Mounting Options

#### -omultipart_size=[size]
Specifies the size (in MB) of each part for multipart upload. It is 10 MB by default. A maximum of 10000 parts for a single file are allowed for a multipart upload. If the file size exceeds 100 GB (10 MB \* 10000), you need to adjust this parameter accordingly.

#### -oallow_other
Allows other users to access the folder to which the bucket is mounted.

#### -odel_cache
By default, to ensure optimal performance, the COSFS does not clear local cached data after a bucket is unmounted. To enable the COSFS to automatically clear cached data upon its exit, you can add this option during mounting.

####  -onoxattr
Disables getattr/setxattr. For the COSFS earlier than 1.0.9, you cannot set or obtain extended attributes. If the use_xattr option is used during mounting, the files may fail to be copied to the bucket.

#### -ouse_cache=[path]
Caches files to a cache directory. "path" is the path of the local cache directory. This option accelerates the reading and writing of a cached file after the file has been read and written once. If the files need not to be cached locally or the capacity of the local disk is limited, you can ignore this option.

#### -opasswd_file=[path]
Specifies the path for the COSFS key file. You need to set the permission for the key file to 600.

#### -odbglevel=[info|dbg]

Sets the level of the COSFS log record to “info” (in a production environment) or “dbg” (during debugging).

#### -oumask=[perm]

Removes the permission of a specified type of users to operate files in the mounting destination directory. For example, when -oumask=755, the permission for the mounting destination directory is changed to 022.

#### -ouid=[uid]
Allows the user whose id is [uid] to access all the files in the mounting destination directory without being restricted by the file permission bits.
You can obtain the uid of a user using the id command `id -u username`. For example, you can execute `id -u user_00` to obtain the uid of user_00.

#### -oensure_diskfree=[size]
Specifies that when the available space of the disk used to store cached files is less than [size] MB, the COSFS minimizes the use of the disk space (in MB) during running. During upload and download, the COSFS caches files in the disk. When a large file is uploaded, if this parameter is not specified, the disk storing cached files will be fully occupied. If the -ouse_cache=[path] parameter is specified, the cached file is stored in the "path" directory, otherwise it is stored in the "/tmp" directory.

## FAQs
For any questions about COSFS, see [FAQs about COSFS](https://cloud.tencent.com/document/product/436/30743).
