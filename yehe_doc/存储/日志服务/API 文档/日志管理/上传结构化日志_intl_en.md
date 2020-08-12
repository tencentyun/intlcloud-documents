## Feature Description

This API is used to write logs to a specified log topic.



CLS provides the following two modes:



#### Load balancing mode

In this mode, the system automatically assigns the target partitions for writing logs among all readable/writable partitions under the current log topic based on the load balancing principle. This mode is suitable for scenarios where the consumption sequence does not need to be guaranteed.

#### Sample

```shell
POST /structuredlog?topic_id=xxxxxxxx-xxxx-xxxx-xxxx HTTP/1.1
Host: <Region>.cls.tencentyun.com
Authorization: <AuthorizationString>
Content-Type: application/x-protobuf

<Packaged content of `LogGroupList` in PB format>
```




#### Hash routing mode

In this mode, the system writes data to target partitions that meet the range requirements based on the carried hash value (`x-cls-hashkey`). For example, a log source can be bound to a topic partition through the `hashkey` so as to strictly guarantee the sequence of the data written to and consumed in this partition.

#### Sample

```shell
POST /structuredlog?topic_id=xxxxxxxx-xxxx-xxxx-xxxx HTTP/1.1
Host: <Region>.cls.tencentyun.com
Authorization: <AuthorizationString>
Content-Type: application/x-protobuf
x-cls-hashkey: xxxxxxxxxxxxxxxxxxxxxxxx

<Packaged content of `LogGroupList` in PB format>
```

>  For more information on the PB description file format and compilation steps, please see [PB Compilation Sample](#pb-.E7.BC.96.E8.AF.91.E7.A4.BA.E4.BE.8B).



In addition, CLS allows you to upload logs in the following two modes:



#### Compressed upload

In compressed upload mode, your logs are compressed on the collector first in lz4 format, and then the compressed log data is uploaded to the log store. In this mode, you can reduce the log upload traffic (log write traffic) to save costs.

#### Sample

```shell
POST /structuredlog?topic_id=xxxxxxxx-xxxx-xxxx-xxxx HTTP/1.1
Host: <Region>.cls.tencentyun.com
Authorization: <AuthorizationString>
Content-Type: application/x-protobuf
x-cls-compress-type:lz4

<Package content of `LogGroupList` in PB format>
```




#### Uncompressed upload

In uncompressed upload mode, logs are uploaded in their original size, which incurs higher log write traffic fees compared with the compressed upload mode.

#### Sample

```shell
POST /structuredlog?topic_id=xxxxxxxx-xxxx-xxxx-xxxx HTTP/1.1
Host: <Region>.cls.tencentyun.com
Authorization: <AuthorizationString>
Content-Type: application/x-protobuf

<Packaged content of `LogGroupList` in PB format>
```

## Request


#### Request line

```shell
POST /structuredlog
```

#### Request header

The `x-cls-hashkey` request header indicates that logs should be written to the corresponding CLS topic partitions according to the `hashkey` route, guaranteeing the strict sequence of logs written to each topic partition for sequential consumption.

| Field Name | Type | Location | Required | Description |
| ------------- | ------ | ------ | -------- | ----------------------------------- |
| x-cls-hashkey | string | header | No       | Logs are written to the corresponding topic partition according to `hashkey` |



#### Request parameters

| Field Name | Type | Location | Required | Description |
| ------------ | ------- | ----- | ---- | ------------------------------------------------------------ |
| topic_id     | string  | query | Yes   | Log topic ID, which identifies the target log topic to which data will be uploaded and can be viewed in the [log topic list](https://console.cloud.tencent.com/cls/logset/desc) |
| logGroupList | message | pb    | Yes   | Log group list, i.e., encapsulated log group list content                           |

`LogGroup` description:

| Field Name | Required | Description |
| ----------- | -------- | ------------------------------------------------------------ |
| logs        | Yes       | Log array, which is a set consisting of multiple `Log` values. A `Log` indicates a log, and `LogGroup` can contain up to 10,000 `Log` values |
| contextFlow | No       | UID used to maintain context, which currently does not take effect                         |
| filename    | No       | Log filename                                                   |
| source      | No       | Log source, which is generally the server IP                           |

`Log` description:

| Field Name | Required | Description |
| -------- | -------- | ------------------------------------------------------------ |
| time | Yes | Unix timestamp for logging in seconds (not recommended), milliseconds, or microseconds |
| contents | No       | Log content in `key-value` format. A log can contain multiple `key-value` pairs |

`Content` description:

| Field Name | Required | Description |
| ------ | -------- | ------------------------------------------------------------ |
| key    | Yes       | Key of field group in log, which cannot start with `_`                 |
| value  | Yes       | Value of field group in log, which cannot exceed 1 MB in one log. `LogGroup` can contain up to 5 MB of `value` in total |

## Response

#### Sample response

```shell
HTTP/1.1 200 OK
Content-Length: 0
```

#### Response header

There are only common response headers but no special response headers.

#### Response parameters

None.

## Error Codes

For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/614/12402).

## PB Compilation Sample

This sample describes how to use the protoc compilation tool to compile the PB description file into a log upload API callable in C++.

> Currently, protoc officially supports compilation in multiple programming languages such as Java, C++, and Python. For more information, please see [protoc](https://github.com/protocolbuffers/protobuf).

#### 1. Install Protocol Buffer

Download [Protocol Buffer](https://main.qcloudimg.com/raw/d7810aaf8b3073fbbc9d4049c21532aa/protobuf-2.6.1.tar.gz), decompress the package, and install the tool. The version used in the sample is protobuf 2.6.1 running on CentOS 7.3.

Run the following command to decompress the `protobuf-2.6.1.tar.gz` package to the `/usr/local` directory and enter the directory:

```sh
[root@VM_0_8_centos]# tar -zxvf protobuf-2.6.1.tar.gz -C /usr/local/ && cd /usr/local/protobuf-2.6.1
```

Run the following commands to start compilation and installation and configure the environment variables:

```sh
[root@VM_0_8_centos protobuf-2.6.1]# ./configure 
[root@VM_0_8_centos protobuf-2.6.1]# make && make install
[root@VM_0_8_centos protobuf-2.6.1]# export PATH=$PATH:/usr/local/protobuf-2.6.1/bin
```

After the compilation succeeds, run the following command to view the version:

```sh
[root@VM_0_8_centos protobuf-2.6.1]# protoc --version
liprotoc 2.6.1
```



#### 2. Create a PB description file

A PB description file is a data exchange format agreed on by both communication parties. When uploading logs, you need to compile the specified protocol format to a callable API in the corresponding programming language and add the API to the project code. For more information, please see [protoc](https://github.com/protocolbuffers/protobuf).

Create a PB message description file `cls.proto` based on the PB data format content specified by CLS.

> The PB description file content cannot be modified, and the filename must end with `.proto`.

The content of `cls.proto` (PB description file) is as follows:

```
package cls;
message Log
{
    message Content
    {
        required string key   = 1; // `key` of each field group
        required string value = 2; // `value` of each field group
    }
    required int64   time     = 1; // Timestamp in Unix time format
    repeated Content contents = 2; // Multiple `kv` pairs in one log
}
message LogGroup
{
    repeated Log    logs        = 1; // Log array consisting of multiple logs
    optional string contextFlow = 2; // This parameter does not take effect currently
    optional string filename    = 3; // Log filename
    optional string source      = 4; // Log source, which is generally the server IP
}
message LogGroupList
{
    repeated LogGroup logGroupList = 1; // Log group list
}

```

#### 3. Compile and generate the API

In this sample, the file in C++ generated with the proto compiler is in the same directory as the `cls.proto` file. Run the following compilation command:

```
protoc --cpp_out=./ ./cls.proto 

```

> `--cpp_out=./ ` indicates that the compiled file is in `cpp` format and output to the current directory. `./cls.proto` indicates the `cls.proto` description file in the current directory.

After the compilation succeeds, the code file in the corresponding programming language will be output. In this sample, the `cls.pb.h` header file and `cls.pb.cc` code implementation file will be generated as shown below:

```
[root@VM_0_8_centos protobuf-2.6.1]# protoc --cpp_out=./ ./cls.proto
[root@VM_0_8_centos protobuf-2.6.1]# ls
cls.pb.cc cls.pb.h cls.proto
```

#### 4. Call

Import the generated `cls.pb.h` header file into the code and call the API for data format encapsulation.