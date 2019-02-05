[//]: # (chinagitpath:XXXXX)

## Scenario
This document describes how to install and use TcaplusDB Pb in the Linux environment.
## Running Environment
Linux 2.6 and 32/64-bit Suse.

## Prerequisites
### Installing Protobuf
Protobuf needs to be installed before installing and using TcaplusDB Pb. If you have installed Protobuf, skip this section.
Protobuf, a mixed-language data standard developed by Google, provides a lightweight and structured data storage format. The TcaplusDB system supports defining data tables using the Protobuf definition file (.proto). Before using the TcaplusDB Pb APIs, you need to install Protobuf on the GameSvr server. It is recommended to use the source code for Protobuf installation. The installation method is as follows:
1. Prepare the GameSvr environment.
You need to prepare a GameSvr with the CentOS 6-x86_64 or the CentOS 7-x86_64 operating system. To compile and build Protobuf, you need to install the following software:
 - autoconf
 - automake
 - libtool
 - curl (used to download gmock)
 - make
 - g++
 - unzip

2. Download the Protobuf (syntax = "proto2") source code installer package.
[Download SDK](https://github.com/protocolbuffers/protobuf/releases).
3. Decompress the source code installer package and enter the root directory of the source code. You can perform the following command lines to do this.
```
tar -xzvf protobuf-2.6.1.tar.gz
cd ./protobuf-2.6.1
```
4. Configure and specify the installation path prefix. It is recommended to install it in /usr/local/protobuf. You can perform the following command lines to do this.
```
./configure --prefix=/usr/local/protobuf
```
5. Compile and install it. You can perform the following command lines to do this.
```
make
make check
make install
```
6. Test. Use the "protoc" command to check if the installation is successful. You can perform the following command lines to do this.
```
protoc -version
```
Once installed, you will see the following:
![](https://mc.qcloudimg.com/static/img/0c9e3f1f45df121b214f07b8961c1c09/1.jpg)

## Procedure
### Downloading SDK
Click to [Download SDK](https://mc.qcloudimg.com/static/archive/5455997ec0076386ac96536d71f0a1ce/TcaplusPbApi3.18.0.152096.x86_64_release_20170712.tar.gz).

### Installing SDK
``` tar –xzf<installer package path> -C <installation directory> ```

### Verification
After installation, the root directory structure is shown as follows:

| Directory/File | Description |
|---------|---------|
| include/tcaplus_service/ | Header files of Tcaplus service API |
| lib/libtcaplusserviceapi.a | Library files of Tcaplus service API |
| include/tcaplus_service/protobuf/ | Header files of Protobuf API |
| lib/libtcaplusprotobufapi.a | Library files of Tcaplus Protobuf API |
| examples/tcaplus/ProtoBuf | Application examples of Tcaplus Protobuf API |

### Run example to access TcaplusDB
For the development of the corresponding data access logic in GameSvr, see APIs in example.

1. Decompress the TcaplusDB Pb API release package.
```
tar -xzvf TcaplusPbApi3.18.0.152096.x86_64_release_20170712.tar.gz
```
2. Configure TcaplusDB system connection information.
	i. Enter the following code on the command line to enter the directory:   
```
cd TcaplusPbApi3.18.0.152096.x86_64_release_20170712/release/x86_64/examples/tcaplus/C++_common_for_pb2
```

	ii. Enter vi common.h on the command line to modify the common.h header file, and modify the following content in the image based on your business.
	**DIR_URL_ARRAY:** tcapdir address and port.
	**DIR_URL_COUNT:** tcapdir count.
	**TABLE_NAME:** Destination table to be accessed.
	**APP_ID:** AppId to be accessed.
	**ZONE_ID:** deployment unit ZoneId.
	**SIGNATURE:** AppKey.

3. Modify the environment configuration file.
The TcaplusPbApi3.18.0.152096.x86_64_release_20170712/release/x86_64/examples/tcaplus directory shows examples of calling API calls asynchronously and by coroutines. The following shows how to call the Set API by coroutines:
Enter the following code on the command line to enter the directory:
```
cd TcaplusPbApi3.18.0.152096.x86_64_release_20170712/release/x86_64/examples/tcaplus/C++_pb2_coroutine_simpletable/SingleOperation/set
```
All codes for the Set example by coroutines are displayed in this directory. Modify the envcfg.env file, set the PROTOBUF_HOME environment variable to the installation path of the native protobuf (the specified prefix), and set the TCAPLUS_HOME environment variable to the absolute path of the release/x86_64 directory under the Tcaplus Pb API package, as shown below:
![](https://mc.qcloudimg.com/static/img/093250c857a6c77847fd14bd037dc7e9/image.png)
4. Set environment variables.
Set in the code directory:
```
source envcfg.env
bash conv.sh
```
5. Compile a binary program.
Run the `make` command to compile the example binary. After compiling, a mytest executable file is generated.
![](https://mc.qcloudimg.com/static/img/9b4dd73cf2d3b93721d9782a76804d7f/mytest.png)
6. Run a binary program.
Enter `./mytest` on the command line to run the binary program. The running result will be displayed in the standard output of the command line. If you encounter an error, check the tcaplus_pb.log file in the code directory.

