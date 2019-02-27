[//]: # (chinagitpath:XXXXX)

## Scenario
This document describes how to work with Tcaplus Protobuf API on the Windows(x64) system.
## Running Environment

Operating system - Microsoft Windows x86\_64
Compiling environment - Microsoft Visual Studio 2015 (VC14.0)

## Procedure
### Download the package

1. Download the dependency package and the Tcaplus Protobuf API package: [Download SDK](https://intl.cloud.tencent.com/document/product/596/31925).
2. Decompress the package. The structure of the package is shown below.
```
Tcaplus_PbAPI_3.32.0.171987_Win64Vc14MT_Release_20180413
|-- cfg                                                 # Configuration directory
|-- docs                                                # Document directory
|   `-- tcaplus
|-- include                                             # Dependent header file directory
|   `-- tcaplus_pb_api
|-- lib                                                 # Library directory
|    |-- Debug
|    `-- Release
|-- examples                                            # Example directory
   `-- tcaplus
       |-- C++_common_for_pb2                           # Sample common header file directory
       |-- C++_pb2_asyncmode_simpletable                # Example of pb simple table in async mode
       |-- C++_pb2_coroutine_simpletable                # Example of pb simple table in coroutine mode
```



### Preparations

1. Make sure that you have activated the game service on [Tencent Cloud TcaplusDB](https://intl.cloud.tencent.com/product/tcaplus) and obtained the corresponding App information (such as AppID, ZoneID, and AppKey).
2. Decompress `TSF4G_BASE-2.7.28.164975_Win64Vc14Mt_Release.zip` and install the file.
  * Assuming that the root path of the installation is `D:\Tencent\tsf4gMT`, the relevant files will be installed in `D:\Tencent\tsf4gMT\win64vc14MT`.
3. Compile and install `Porotbuf-3.5.1`.
  * Source code URL: https://github.com/google/protobuf/releases/
  * Compilation and installation instructions: https://github.com/google/protobuf/tree/master/cmake
  * Assume that the installation path is `D:\protobuf-3.5.1`.
4. Compile and install `OpenSSL-1.1.0f`.
  * Source code URL: https://www.openssl.org/source/
  * Compilation and installation instructions: https://wiki.openssl.org/index.php/Compilation_and_Installation
  * Assume that the installation path is `D:\openssl-1.1.0f`.
5. Set the environment variables.
  * `TSF4G_HOME="D:\Tencent\tsf4gMT"`
  * `PROTOBUF_HOME="D:\protobuf-3.5.1"`
  * `OPENSSL_HOME="D:\openssl-1.1.0f"`

### Building

1. Decompress the Tcaplus Pb API installer package.
2. Set the App information in `examples/tcaplus/C++_common_for_pb2/common.h`.
  * List of Tcapdir access point URLs - `DIR_URL_ARRAY`
  * Number of Tcapdir access point URLs - `DIR_URL_COUNT`
  * User table name (you need to create a table using the table_test.xml file in the example directory before using the API) - `TABLE_NAME`
  * App ID - `APP_ID`
  * App zone ID - `ZONE_ID`
  * App key - `SIGNATURE`

  ```C
  //examples/tcaplus/C++_common_for_pb2/common.h

  /******************Custom****************************/
  // List of Tcapdir access point URLs
  static const char DIR_URL_ARRAY[][TCAPLUS_MAX_STRING_LENGTH] =
  {
  	"tcp://10.125.32.21:9999"
  };
  // Number of Tcapdir access point URLs
  static const int32_t DIR_URL_COUNT = 1;
  // Table name
  static const char * TABLE_NAME = "tb_online";
  // App ID
  static const int32_t APP_ID = 4;
  // App zone ID
  static const int32_t ZONE_ID = 1;
  // App key
  static const char * SIGNATURE = "8e24269ba91f433ca7e89b1cbb77368e";
  /******************Custom******************************/
  ```

3. Take `examples\tcaplus\C++_pb2_coroutine_simpletable\SingleOperation\set` as an example.
```
set/
|-- main.cpp                              # Sample primary function code
|-- readme.txt
|-- table_test.proto                        # The proto file defined using T table that should be created first
|-- pb_co_set.sln                           # Project VisualSudio's solution file
|-- pb_co_set.vcxproj                       # Project VisualSudio's project file
|-- proto_generate.cmd                      # Script used to compile the proto file
`-- tlogconf.xml
```
  * First, confirm that the table has been successfully created in the target App using `table_test.proto`.
  * Run the `proto_generate.cmd` script to generate dependent files in the current path.
    * `table_test.pb.cc`
    * `table_test.pb.h`
  * Open the project file `pb_co_set.sln` in Microsoft Visual Studio 2015.
  * Generate a solution.
  * If no error occurs, the executable file `pb_co_set.exe` will be generated in `examples\tcaplus\C++_pb2_coroutine_simpletable\SingleOperation\set/x64`.


### Test

1. Copy `pb_co_set.exe` and `tlogconf.xml` files to the same directory.
2. Switch to `administrator` and use cmd.exe or powershell.exe to run the executable file `pb_co_set.exe`.
3. Review the output.
4. For detailed running information, see the log file `tcaplus_pb.log`.
5. To run the `*_crypto` example, make sure that the `libcrypto-1_1-x64.dll` file is copied to the system's Path directory. The file can be found in the openssl compiling directory.
![Output](https://main.qcloudimg.com/raw/40627a3a2dff8a4a4aeea57cda2bb8bb.png)


## Tcaplus Pb API Command List

Tcaplus Pb API supports various types of operations in both async and coroutine modes. You can find the corresponding usage method in the example. Here is the Tcaplus Pb API command list.

| Command | Description |
| ------------------------------- | ------------ |
| SET | Specifies all primary keys of a record to set this record. If the record exists, an overwrite operation will be performed, otherwise an insert operation will be performed. |
| GET | Specifies all primary keys of a record to query this record from a Tcaplus pb table. If no data record exists, an error is returned. |
| ADD | Specifies all primary keys of a record to insert this record. If the record exists, an error is returned. |
| DELETE | Specifies all primary keys of a record to delete this record. If data does not exist, an error is returned. |
| BATCHGET | Specifies multiple primary keys to query multiple records from a Tcaplus pb table. |
| TRAVERSE | Traverses a Tcaplus pb table and multiple records are returned. |
| FIELDGET | Specifies all primary keys of a record to query this record from a Tcaplus pb table. This operation only supports querying and transferring the values of specified fields to minimize the traffic in network transmission. If no record exists, an error is returned. |
| FIELDSET | Specifies all primary keys of a record to modify this record. Only the values of specified fields are transferred to minimize the network traffic. If the data record exists, it will be updated; otherwise, an error is returned. |
| FIELDINC | Specifies all primary keys of a record to perform auto-increment on specified fields. This command word only supports int32, int64, uint32 and uint64 fields. It has the same feature as FIELDSET. |
| GETBYPARTKEY | Specifies partial primary keys to query multiple records that meet the condition. An index must be created for the primary key set when you create a table; otherwise, an error is returned. |











