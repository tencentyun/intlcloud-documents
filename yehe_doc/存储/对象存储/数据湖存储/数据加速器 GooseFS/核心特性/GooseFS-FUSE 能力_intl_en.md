GooseFS-FUSE can mount a GooseFS system to a local file system on a Unix machine. Using this feature, some standard command-line tools (such as ls, cat, and echo) can directly access data in the GooseFS system. More importantly, applications implemented in different languages, such as C, C++, Python, Ruby, Perl, and Java, can use standard POSIX APIs (such as open, write, and read) to read and write GooseFS without any client-side integration and setup of GooseFS.

GooseFS-FUSE is based on the [FUSE](http://fuse.sourceforge.net/) project and supports most file system operations. However, due to the inherent properties of GooseFS, such as its one-time, immutable file data model, the mounted file system does not fully conform to POSIX standards and has some limitations. Therefore, read [Limitations](#limit) first to see what this feature does and what its limitations are.

## Installation Requirements

- JDK 1.8 or later
- Linux system: [libfuse](https://github.com/libfuse/libfuse) 2.9.3 or later (Version 2.8.3 can be used, but there will be some alerts.)
- MAC system: [osxfuse](https://osxfuse.github.io/) 3.7.1 or later

## Usage

### Mounting GooseFS-FUSE

After configuring and starting the GooseFS cluster, start Shell on the node where you want to mount GooseFS, go to the `$GOOSEFS_HOME` directory, and run the following command:
```
$ integration/fuse/bin/goosefs-fuse mount mount_point [GooseFS_path]
```
This command starts a background Java process that mounts the corresponding GooseFS path to the path specified by `<mount_point>`. For example, mount the GooseFS path `/people` to the `/mnt/people` directory on the local file system.
```
$ integration/fuse/bin/goosefs-fuse mount /mnt/people /people
Starting goosefs-fuse on local host.
goosefs-fuse mounted at /mnt/people. See /lib/GooseFS/logs/fuse.log for logs
```
If `GooseFS_path` is not specified, GooseFS-FUSE is mounted to the GooseFS root directory (/) by default. You can run this command multiple times to mount GooseFS to different local directories. All GooseFS-FUSE clients will share the `$GOOSEFS_HOME\logs\fuse.log` log file. This log file is useful for troubleshooting.
>! `<mount_point>` must be an empty folder in the local file system, and the user that starts the GooseFS-FUSE process must have the read/write permission on the mount target.
>


### Unmounting GooseFS-FUSE

To unmount GooseFS-FUSE, you need to start Shell on the node, go to the `$GOOSEFS_HOME` directory and run the following command:
```
$ integration/fuse/bin/goosefs-fuse umount mount_point
```
This command ends the Java background process of GooseFS-FUSE and unmount the file system. The following is an example:
```
$ integration/fuse/bin/goosefs-fuse umount /mnt/people
Unmount fuse at /mnt/people (PID: 97626).
```
By default, if any read/write operation is not completed, the unmount operation will wait a maximum of 120 seconds. If the read/write operation does not complete after 120 seconds, the FUSE process will be forcibly ended, which will cause the current file read/write to fail. You can add the `-s` parameter to prevent the FUSE process from being forcibly ended, for example:
```
$ ${GOOSEFS_HOME}/integration/fuse/bin/goosefs-fuse unmount -s /mnt/people
```

### Checking whether GooseFS-FUSE is running

List all mount targets, start Shell on the node, go to the `$GOOSEFS_HOME` directory, and run the following command:
```
$ integration/fuse/bin/goosefs-fuse stat
```
This command will output information including `pid`, `mount_point` and `GooseFS_path`.

The following is an example of the output format:
```
$ pid    mount_point     GooseFS_path
80846  /mnt/people     /people
80847  /mnt/sales       /sales
```
 

### GooseFS-FUSE directory structure

![](https://qcloudimg.tencent-cloud.cn/raw/1711edcd1e0789aed28f6a295dfe5361.png)

The structure of the `conf` directory is as follows:
- masters: master server IP configuration file
- workers: worker server IP configuration file
- goosefs-site.properties: GooseFS configuration file
- libexec: library file on which GooseFS-FUSE depends to run
- goosefs-fuse-1.4.0: GooseFS-FUSE JAR package to run in the background
- log: log directory

## Configuration Options

GooseFS-FUSE performs operations based on the standard GooseFS-core-client-fs. If you want it to perform operations like other applications, you can customize the behavior of GooseFS-core-client-fs.

You can edit the `$GOOSEFS_HOME/conf/goosefs-site.properties` configuration file to modify the client options.
>! All modifications must be completed before GooseFS-FUSE is started.
>

<span id=limit></span>

## Limitations

Currently, GooseFS-FUSE supports most basic file system operations. However, due to some inherent features of GooseFS, you need to be aware of the following:
- Files cannot be written randomly and additionally.
- Files can be written sequentially only once and cannot be modified. If you want to modify a file, first delete the file and then recreate it or open the file with the `O_TRUNC` identifier and set its length to `0`.
- Files being written in the mount point cannot be read.
- The file length cannot be truncated.
- Commands related to soft/hard link are not supported. GooseFS does not have the concepts of hard link or soft link, so it does not support commands related to them, such as `ln`. In addition, information about hard links is not shown in the output of `ll`.
- When Cloud Object Storage (COS) is used as the underlying storage, the `Rename` operation is nonatomic. 
-  Only when the `GooseFS.security.group.mapping.class` option of GooseFS is set to the value of `ShellBasedUnixGroupsMapping`, the user and group information of a file corresponds to the user group of a Unix system. Otherwise, the `chown` and `chgrp` operations do not take effect, and `ll` returns the information of the user and group that started the GooseFS-FUSE process.

## Performance Considerations

Due to the combination of FUSE and JNR, the performance of mounting file systems is relatively lower compared to using native file system APIs directly.

Most of the performance problems are due to the fact that there are several copies in the memory each time a read or write operation is performed, and FUSE sets the maximum granularity of write operations to 128 KB. Performance can be greatly improved with the FUSE write-backs cache policy introduced by Kernel 3.15 (however, the libfuse 2.x userspace library currently does not support this feature).

## GooseFS-FUSE Parameters

The following are GooseFS-FUSE related parameters:

| **Parameter**                                    | **Default Value**   | **Description**                                                     |
| ------------------------------------------- | ------------ | ------------------------------------------------------------ |
| goosefs.fuse.cached.paths.max               | 500          |   Defines the size of the internal GooseFS-FUSE cache, which maintains the most common conversions between local file system paths and Alluxio file URIs.                                                           |
| goosefs.fuse.debug.enabled                  | false        | Allows FUSE debugging output, which is redirected to the `fuse.out` log file in the directory specified by `goosefs.logs.dir`. |
| goosefs.fuse.fs.name                        | goosefs-fuse | Descriptive name used by FUSE to mount a file system.                           |
| goosefs.fuse.jnifuse.enabled                | true         |   Use the JNI-FUSE library for higher performance. If the JNI-FUSE library is disabled, JNR-FUSE will be used.                                                           |
| goosefs.fuse.shared.caching.reader.enabled  | false        |  (Experimental) Use a shared gRPC data reader to achieve higher performance in multi-process file reading by using GooseFS JNI-FUSE. Block data will be cached on the client, so the FUSE process requires more memory.                                                            |
| goosefs.fuse.logging.threshold              | 10s          |  Record FUSE API calls when the time taken exceeds the threshold.                                                            |
| goosefs.fuse.maxwrite.bytes                 | 131072       | Granularity (in bytes) of FUSE write operations. Note that 128 KB is currently the upper limit for the Linux kernel limit. |
| goosefs.fuse.user.group.translation.enabled | false        | Whether to convert GooseFS users and groups to the corresponding Unix users and groups in the FUSE API. When set to `false`, the users and groups of all FUSE files are displayed as the users and groups that mount the GooseFS-FUSE thread. |

## FAQs

#### Missing libfuse library file
You need to install libfuse before mounting GooseFS-Fuse.
![](https://qcloudimg.tencent-cloud.cn/raw/7a535eed0fac0da06f530fb04ca9702b.png)
- **Option 1**
Installation command:
```
yum install fuse-devel
```
Check whether the installation is successful:
```
find / -name libfuse.so*
```
- **Option 2**
Update the old version libfuse.so.2.9.2. The procedure is as follows:
>? If libfuse is installed in CentOS 7, libfuse.so.2.9.2 is installed by default.
>
Download the [libfuse source code](https://github.com/libfuse/libfuse/releases/tag/fuse-2.9.7) and compile and generate libfuse.so.2.9.7.
```
tar -zxvf fuse-2.9.7.tar.gz
cd fuse-2.9.7/ && ./configure && make && make install
echo -e '\n/usr/local/lib' >> /etc/ld.so.conf
ldconfig
```
Install libfuse.so.2.9.7 to replace the old version:
 1. Run the following command to find the links of the libfuse.so.2.9.2 library:
```
find / -name libfuse.so*
```
 2. Run the following command to copy libfuse.so.2.9.7 to the location of the old version libfuse.so.2.9.2 library:
```
cp /usr/local/lib/libfuse.so.2.9.7 /usr/lib64/
```
 3. Run the following commands to delete all links of the old version libfuse.so library:
```
rm -f /usr/lib64/libfuse.so
rm -f /usr/lib64/libfuse.so.2
```
 4. Run the following commands to build libfuse.so.2.9.7 library links similar to those of the old version library.
```
ln -s /usr/lib64/libfuse.so.2.9.7 /usr/lib64/libfuse.so
ln -s /usr/lib64/libfuse.so.2.9.7 /usr/lib64/libfuse.so.2
```

#### “Write error in swap file” error during editing a file in the mounting point by using VIM
You can change the VIM configuration to use VIM 7.4 or earlier for editing files in the GooseFS-Fuse mounting point. The VIM swap file is used to retain the modifications so that VIM can restore unsaved modifications based on the swap file if the machine crashes or restarts. The above error is due to a random write operation to a VIM swap file, while GooseFS does not support it. Solution: You can run the `:set noswapfile` command to terminate swap file generation or add `set noswapfile` to the configuration file (“~/.vimrc”).
