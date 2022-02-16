## Operation Scenarios
This document describes how to manipulate TcaplusDB Protobuf API on Windows x64.

## Runtime Environment
- OS: Microsoft Windows x86\_64
- Compilation environment: Microsoft Visual Studio 2015 (VC14.0)

## Directions
### Downloading program package
1. Download the dependency package and TcaplusDB Protobuf API program package. For more information, please see [SDK Download](https://intl.cloud.tencent.com/document/product/1016/30285).
2. Decompress the packages. The program package structure is as shown below:
```
Tcaplus_PbAPI_3.32.0.171987_Win64Vc14MT_Release_20180413
|-- cfg                                                 # Configuration directory
|-- docs                                                # Documentation directory
|   `-- tcaplus
|-- include                                             # Dependency header file directory
|   `-- tcaplus_pb_api
|-- lib                                                 # Library directory
|    |-- Debug
|    `-- Release
|-- examples                                            # Sample directory
   `-- tcaplus
       |-- C++_common_for_pb2                           # Directory of sample common header files
       |-- C++_pb2_asyncmode_simpletable                # Sample simple PB table in async mode
       |-- C++_pb2_coroutine_simpletable                # Sample simple PB table in coroutine mode
```

### Preparing environment
1. Please make sure that you have enabled the TcaplusDB service in the [TcaplusDB Console](https://console.cloud.tencent.com/tcaplusdb/app) and obtained the corresponding application information (such as the `AppId`, `ZoneId`, and `AppKey`).
2. Decompress the dependency package and install the dependencies. This document uses the `TSF4G_BASE-2.7.28.164975_Win64Vc14Mt_Release.zip` dependency package as an example. You should download an appropriate dependency package [here](https://intl.cloud.tencent.com/document/product/1016/30285#windows-.E5.B9.B3.E5.8F.B0.E4.BE.9D.E8.B5.96.E5.8C.85.E4.B8.8B.E8.BD.BD) as needed.
Supposing the root path for installation is `D:\Tencent\tsf4gMT`, relevant files will be installed under the `D:\Tencent\tsf4gMT\win64vc14MT` path.
3. Compile and install `Porotbuf-3.5.1`.
  - [Source code address](https://github.com/google/protobuf/releases/) 
  - [Compilation and Installation Guide](https://github.com/google/protobuf/tree/master/cmake) 
  - Suppose the installation path is `D:\protobuf-3.5.1`
4. Compile and install `OpenSSL-1.1.0f`.
  - [Source code address](https://www.openssl.org/source/) 
  - [Compilation and Installation Guide](https://wiki.openssl.org/index.php/Compilation_and_Installation) 
  - Suppose the installation path is `D:\openssl-1.1.0f`
5. Set environment variables.
  - `TSF4G_HOME="D:\Tencent\tsf4gMT"`
  - `PROTOBUF_HOME="D:\protobuf-3.5.1"`
  - `OPENSSL_HOME="D:\openssl-1.1.0f"`

### Constructing
1. Decompress the TcaplusDB PB API installation package.
2. Set the `App` information in the `examples/tcaplus/C++_common_for_pb2/common.h` file.
  - DIR_URL_ARRAY: Tcapdir access point address list
  - DIR_URL_COUNT: number of Tcapdir access point addresses
  - TABLE_NAME: table name. Before using this feature, you need to use the `table_test.xml` file in the `examples` directory to create a `TABLE_NAME` table
  - APP_ID: business ID
  - ZONE_ID: regional business server ID
  - SIGNATURE: business password
 ```C
 //examples/tcaplus/C++_common_for_pb2/common.h
  /******************User-defined****************************/
  // Tcapdir access point address list
  static const char DIR_URL_ARRAY[][TCAPLUS_MAX_STRING_LENGTH] =
  {
  	"tcp://10.xx.xx.21:9999"
  };
  // Number of Tcapdir access point addresses
  static const int32_t DIR_URL_COUNT = 1;
  // Table name
  static const char * TABLE_NAME = "tb_online";
  // Business ID
  static const int32_t APP_ID = 4;
  // Regional business server ID
  static const int32_t ZONE_ID = 1;
  // Business password
  static const char * SIGNATURE = "8e24269ba91fxxxa7e89b1cbb77368e";
  /******************User-defined******************************/
  ```
3. Use `examples\tcaplus\C++_pb2_coroutine_simpletable\SingleOperation\set` as an example.
```
set/
|-- main.cpp                              # Sample code of main function
|-- readme.txt
|-- table_test.proto                        # .proto table definition file for Tcaplus. The table needs to be created in advance
|-- pb_co_set.sln                           # VisualStudio solution file of the project
|-- pb_co_set.vcxproj                       # VisualStudio project file of the project
|-- proto_generate.cmd                      # .proto file compilation script
`-- tlogconf.xml
```
  1. First, make sure that you have successfully created a table in the target application by using `table_test.proto`.
  2. Run the `proto_generate.cmd` script and generate the dependent files under the current path.
    * `table_test.pb.cc`
    * `table_test.pb.h`
  3. Open the project file `pb_co_set.sln` in Microsoft Visual Studio 2015.
  4. Generate the solution.
  5. If no errors occur, an executable file `pb_co_set.exe` will be generated under the `examples\tcaplus\C++_pb2_coroutine_simpletable\SingleOperation\set/x64` path.


### Testing
1. Copy the `pb_co_set.exe` and `tlogconf.xml` files into the same directory.
2. Switch to the `administrator` role and use `cmd.exe` or `powershell.exe` to run the executable file `pb_co_set.exe`.
3. Check the output.
4. For detailed running information, please check the log file `tcaplus_pb.log`.
5. To run the `*_crypto` sample code, please make sure that the `libcrypto-1_1-x64.dll` file is in the OpenSSL compilation directory under the system path.
![Output](https://main.qcloudimg.com/raw/40627a3a2dff8a4a4aeea57cda2bb8bb.png)


## TcaplusDB PB API Command List

TcaplusDB PB API provides various types of operations and supports async and coroutine modes. You can find the corresponding usage in the sample code. The list of TcaplusDB PB API commands are as shown below:

| Command | Description |
| ------------------------------- | ------------ |
| SET | Sets record by specifying all its primary keys. If the record already exists, an overwrite operation will be performed; otherwise, an insert operation will be performed. |
| GET | Queries record by specifying all its primary keys in TcaplusDB PB table. If the record does not exist, an error will be returned. |
| ADD | Inserts record by specifying all its primary keys. If the record already exists, an error will be returned. |
| DELETE | Deletes record by specifying all its primary keys. If the record does not exist, an error will be returned. |
| BATCHGET | Queries multiple records by specifying multiple set of primary keys in TcaplusDB PB table. |
| TRAVERSE | Traverses TcaplusDB PB table. Multiple records will be returned. |
| FIELDGET | Queries record by specifying all its primary keys in TcaplusDB PB table. This operation queries and transfers only the values of specified fields, which reduces the network transfer traffic. If the record does not exist, an error will be returned. |
| FIELDSET | Sets specified fields by specifying all primary keys of record. Only the values of specified fields will be transferred, which reduces the network traffic. If the data record already exists, an update operation will be performed; otherwise, an error will be returned. |
| FIELDINC | Auto-increments specified fields by specifying all primary keys of record. This command supports only fields in `int32`, `int64`, `uint32`, and `uint64` types. It is similar to `FIELDSET`. |
| GETBYPARTKEY | Queries multiple eligible data entries by specifying certain primary keys. The specified primary key set must have an index created when the table is created; otherwise, an error will be returned. |
