## Feature Description

This API is used to write a log to the specified log topic.

CLS provides the following two modes:

<dx-tabs>
::: Load balancing mode
In this mode, logs will be automatically written to a target partition among all readable/writable partitions under the current log topic based on the load balancing principle. This mode is suitable for scenarios where the sequential consumption is not needed.

#### Sample

```shell
POST /structuredlog?topic_id=xxxxxxxx-xxxx-xxxx-xxxx HTTP/1.1
Host: <Region>.cls.tencentyun.com
Authorization: <AuthorizationString>
Content-Type: application/x-protobuf

<`LogGroupList` content packaged as a PB file>
```

#### Private and public domain names

CLS request domain names divide into private domain names and public domain names:
- A private domain name is in the format of `${region}.cls.tencentyun.com`, which is only valid for access requests from the same region, that is, CVM or Tencent Cloud services access the CLS service in the same region through the private domain name.
- A public domain name is in the format of `${region}.cls.tencentcs.com`. After the access source is connected to the internet, the public domain name of CLS can be accessed under normal circumstances.

The `region` field is the abbreviation of a CLS service region, such as `ap-beijing` for the Beijing region. For the complete region list, see [Available Regions](https://intl.cloud.tencent.com/document/product/614/18940).

```
ap-beijing - Beijing
ap-shanghai - Shanghai
ap-guangzhou - Guangzhou
ap-chengdu - Chengdu
...
```
:::
::: Hash routing mode
In this mode, data will be written to a target partition that meets the range requirements based on the hash value (x-cls-hashkey) carried by data. For example, a log source can be bound to a topic partition through `hashkey`, strictly guaranteeing the sequence of the data written to and consumed in this partition.

#### Sample

```shell
POST /structuredlog?topic_id=xxxxxxxx-xxxx-xxxx-xxxx HTTP/1.1
Host: <Region>.cls.tencentyun.com
Authorization: <AuthorizationString>
Content-Type: application/x-protobuf
x-cls-hashkey: xxxxxxxxxxxxxxxxxxxxxxxx

<`LogGroupList` content packaged as a PB file>
```

>? For more information on the PB description file format and compilation steps, see [PB Compilation Sample](#pb-.E7.BC.96.E8.AF.91.E7.A4.BA.E4.BE.8B).
>

:::
</dx-tabs>

In addition, CLS allows you to upload logs in the following two modes:

<dx-tabs>
::: Uploading compressed logs
In this mode, logs are compressed in LZ4 format for collection, and then uploaded for retention. This mode reduces the log upload traffic (write traffic) and saves costs.

#### Sample

```shell
POST /structuredlog?topic_id=xxxxxxxx-xxxx-xxxx-xxxx HTTP/1.1
Host: <Region>.cls.tencentyun.com
Authorization: <AuthorizationString>
Content-Type: application/x-protobuf
x-cls-compress-type:lz4

<`LogGroupList` content packaged as a PB file>
```

:::
::: Uploading original logs
In this mode, logs are uploaded in their original size, which incurs higher log write traffic fees.

#### Sample

```shell
POST /structuredlog?topic_id=xxxxxxxx-xxxx-xxxx-xxxx HTTP/1.1
Host: <Region>.cls.tencentyun.com
Authorization: <AuthorizationString>
Content-Type: application/x-protobuf

<`LogGroupList` content packaged as a PB file>
```

:::
</dx-tabs>

## Request

#### Request line

```shell
POST /structuredlog
```

#### Request headers

The `x-cls-hashkey` request header indicates that logs are written to the CLS topic partitions with a range corresponding to the hashkey route, strictly guaranteeing the write sequence of logs to each topic partition for sequential consumption.

| Field Name | Type | Location | Required | Description |
| ------------- | ------ | ------ | -------- | ----------------------------------- |
| x-cls-hashkey | string | header | No       | Specifies the topic partition to which the logs will be written based on `hashkey`  |


#### Request parameters

| Field Name | Type | Location | Required | Description |
| ------------ | ------- | ----- | ---- | ------------------------------------------------------------ |
| topic_id     | string  | query | Yes   | ID of the target log topic to which data will be uploaded, which can be viewed on the [log topic](https://console.cloud.tencent.com/cls/logset/desc) page |
| logGroupList | message | pb    | Yes   | The logGroup list, which describes the encapsulated log groups. No more than five `logGroup` values are recommended.                     |

LogGroup description:

| Field Name     | Required | Description                                                         |
| ----------- | -------- | ------------------------------------------------------------ |
| logs        | Yes       | Log array, which is a set consisting of multiple `Log` values. A `Log` indicates a log, and `LogGroup` can contain up to 10,000 `Log` values |
| contextFlow | No       | UID used to maintain context, which does not take effect currently |
| filename    | No       | Log filename                                                   |
| source      | No       | Log source, which is generally the server IP                           |
| logTags     | No       | Tag list of the log                                               |

Log description:

| Field Name | Required | Description |
| -------- | -------- | ------------------------------------------------------------ |
| time | Yes | UNIX timestamp of log time in seconds or milliseconds (recommended) |
| contents | No | Log content in `key-value` format. A log can contain multiple `key-value` pairs. |

Content description:

| Field Name | Required | Description |
| ------ | -------- | ------------------------------------------------------------ |
| key    | Yes       | Key of a field group in one log, which cannot start with `_`.                 |
| value  | Yes       | Value of a field group, which cannot exceed 1 MB in one log. The total value cannot exceed 5 MB in `LogGroup`. |

`LogTag` description:

| Field Name     | Required | Description                                                         |
| ------ | -------- | ---------------------------- |
| key    | Yes       | Key of a custom tag             |
| value  | Yes       | Value corresponding to the custom tag key |

## Response

#### Sample response

```shell
HTTP/1.1 200 OK
Content-Length: 0
```

#### Response headers

No special response headers. Only common headers are used.

#### Response parameters

N/A

## Error Codes

For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/614/12402).

## PB Compilation Sample

This sample describes how to use the protoc compiler to compile the PB description file into a log upload API in C++.

> ?Currently, protoc supports compilation in multiple programming languages such as Java, C++, and Python. For more information, see [protoc](https://github.com/protocolbuffers/protobuf).

#### 1. Install Protocol Buffer

Download [Protocol Buffer](https://main.qcloudimg.com/raw/d7810aaf8b3073fbbc9d4049c21532aa/protobuf-2.6.1.tar.gz), then decompress and install it. This document uses protobuf 2.6.1 running on CentOS 7.3 as an example.
Run the following command to decompress the `protobuf-2.6.1.tar.gz` package to `/usr/local` and access this directory:
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

A PB description file is an agreed-on data exchange format for communication. To upload logs, compile the specified protocol format to an API in the target programming language and add the API to the project code. For more information, see [protoc](https://github.com/protocolbuffers/protobuf).

Create a PB message description file `cls.proto` based on the PB data format content specified by CLS.

> !The PB description file content cannot be modified, and the filename must end with `.proto`.

The content of `cls.proto` (PB description file) is as follows:

```
package cls;

message Log
{
    message Content
    {
        required string key   = 1; // Key of each field group
        required string value = 2; // Value of each field group
    }
    required int64   time     = 1; // Unix timestamp
    repeated Content contents = 2; // Multiple `key-value` pairs in one log
}

message LogTag
{
    required string key       = 1;
    required string value     = 2;
}

message LogGroup
{
    repeated Log    logs        = 1; // Log array consisting of multiple logs
    optional string contextFlow = 2; // This parameter does not take effect currently
    optional string filename    = 3; // Log filename
    optional string source      = 4; // Log source, which is generally the server IP
    repeated LogTag logTags     = 5;
}

message LogGroupList
{
    repeated LogGroup logGroupList = 1; // Log group list
}

```

#### 3. Compile and generate the API

This sample uses the proto compiler to generate a C++ file in the same directory as the `cls.proto` file. Run the following compilation commands:

```
protoc --cpp_out=./ ./cls.proto 

```

>? `--cpp_out=./ ` indicates that the file will be compiled in cpp format and output to the current directory. `./cls.proto` indicates the `cls.proto` description file in the current directory.
>

After the compilation succeeds, the code file in the corresponding programming language will be generated. This sample generates the `cls.pb.h` header file and `cls.pb.cc` code implementation file.

```
[root@VM_0_8_centos protobuf-2.6.1]# protoc --cpp_out=./ ./cls.proto
[root@VM_0_8_centos protobuf-2.6.1]# ls
cls.pb.cc cls.pb.h cls.proto
```

#### 4. Call

Import the generated `cls.pb.h` header file into the code and call the API for data format encapsulation.
