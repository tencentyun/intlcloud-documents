For the sake of compression performance and ratio, backup files and log files (binlog files) of TencentDB for MariaDB are compressed with LZ4 (Extremely Fast Compression Algorithm). You can use LZ4 for decompression. As common decompression tools do not support this format, this document specifically describes how to use this tool.


## Windows
### Downloading the tool
[Tool download address](https://wiki-jjb-1254408587.cos.ap-chengdu.myqcloud.com/lz4_win64_v1_9_2.zip)

### Installing the tool
Double-click and decompress the zip file to get `LZ4installv1.4.exe`. Double-click it for installation as prompted.
The check box in the last step can be ignored if the tool is only used to decompress TencentDB files.

### Decompressing a file
Right-click the LZ4 file to be decompressed and select **Decode with LZ4**.

## Linux
### Installing the tool
There is an LZ4 component in the yum repository of CVM. Log in to your CVM instance and run the following command to install it.
`$ yum install lz4`
If a screen similar to the one below is returned after you run **lz4**, the installation is successful:
![](https://main.qcloudimg.com/raw/820a98757f5a5ccb84180f2289c88ddf.png)

### Decompressing a file
Run the following command to decompress a file:
`$ lz4 -d xxx.lz4`
