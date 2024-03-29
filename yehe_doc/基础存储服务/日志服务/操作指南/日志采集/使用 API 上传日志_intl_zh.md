## 功能描述

本接口用于将日志写入到指定的日志主题。

日志服务提供以下两种模式：

<dx-tabs>
::: 负载均衡模式
系统根据当前日志主题下所有可读写的分区，遵循负载均衡原则自动分配写入的目标分区。该模式适合消费不保序的场景。

#### 示例

```shell
POST /structuredlog?topic_id=xxxxxxxx-xxxx-xxxx-xxxx HTTP/1.1
Host: <Region>.cls.tencentyun.com
Authorization: <AuthorizationString>
Content-Type: application/x-protobuf

<LogGroupList 的 PB 格式打包内容>
```

#### 内外网域名

日志服务请求域名区分内外网形式：
- 内网域名格式形如`${region}.cls.tencentyun.com` ，内网域名仅对同地域访问生效，即云服务器或云产品通过内网域名访问相同地域的日志服务。
- 外网域名格式形如`${region}.cls.tencentcs.com`，访问源端接入 Internet 网后，正常情况均能访问日志服务外网域名。

`region`字段是日志服务区域简称，例如北京区域填写`ap-beijing`，完整区域列表格式参考 [地域列表](https://intl.cloud.tencent.com/document/product/614/18940)。

```
ap-beijing - 北京
ap-shanghai - 上海
ap-guangzhou - 广州
ap-chengdu - 成都
...
```
:::
::: 哈希路由模式
系统根据携带的哈希值（x-cls-hashkey）将数据写入到符合范围要求的目标分区。例如，可以将某个日志源端通过 hashkey 与某个主题分区强绑定，这样可以保证数据在该分区上写入和消费是严格保序的。

#### 示例

```shell
POST /structuredlog?topic_id=xxxxxxxx-xxxx-xxxx-xxxx HTTP/1.1
Host: <Region>.cls.tencentyun.com
Authorization: <AuthorizationString>
Content-Type: application/x-protobuf
x-cls-hashkey: xxxxxxxxxxxxxxxxxxxxxxxx

<LogGroupList 的 PB 格式打包内容>
```

>? PB 描述文件格式以及编译步骤，请参阅 [PB 编译示例](#pb-.E7.BC.96.E8.AF.91.E7.A4.BA.E4.BE.8B)。
>

:::
</dx-tabs>

此外日志服务还为用户提供以下两种不同的日志上传模式：

<dx-tabs>
::: 压缩上传模式
使用压缩上传模式时，用户日志将在采集端先以 lz4 格式压缩，之后再将压缩完成后的日志数据上传到日志存储端。通过使用压缩上传模式，用户可以减少日志上传流量（日志写流量），从而节省费用。

#### 示例

```shell
POST /structuredlog?topic_id=xxxxxxxx-xxxx-xxxx-xxxx HTTP/1.1
Host: <Region>.cls.tencentyun.com
Authorization: <AuthorizationString>
Content-Type: application/x-protobuf
x-cls-compress-type:lz4

<LogGroupList 的 PB 格式压缩包内容>
```

:::
::: 非压缩上传模式
使用非压缩上传模式时，用户日志将以原始大小上传，相比于压缩上传模式，非压缩模式将会产生更高的日志写流量费用。

#### 示例

```shell
POST /structuredlog?topic_id=xxxxxxxx-xxxx-xxxx-xxxx HTTP/1.1
Host: <Region>.cls.tencentyun.com
Authorization: <AuthorizationString>
Content-Type: application/x-protobuf

<LogGroupList 的 PB 格式打包内容>
```

:::
</dx-tabs>

## 请求

#### 请求行

```shell
POST /structuredlog
```

#### 请求头

x-cls-hashkey 请求头表示日志根据 hashkey 路由写入到 CLS 对应范围的主题分区，以保证写入到的每个主题分区是严格有序的，便于消费时有序消费。

| 字段名        | 类型   | 位置   | 是否必须 | 含义                                |
| ------------- | ------ | ------ | -------- | ----------------------------------- |
| x-cls-hashkey | string | header | 否       | 根据 hashkey 写入相应范围的主题分区 |


#### 请求参数

| 字段名       | 类型    | 位置  | 必须 | 含义                                                         |
| ------------ | ------- | ----- | ---- | ------------------------------------------------------------ |
| topic_id     | string  | query | 是   | 日志主题 ID ，表示数据上传的目标日志主题，可在 [日志主题列表](https://console.cloud.tencent.com/cls/logset/desc) 查看日志主题 ID |
| logGroupList | message | pb    | 是   | logGroup 列表，封装好的日志组列表内容，建议 logGroup 数量不要超过5个                           |

LogGroup 说明：

| 字段名      | 是否必选 | 含义                                                         |
| ----------- | -------- | ------------------------------------------------------------ |
| logs        | 是       | 日志数组，表示有多个 Log 组成的集合，一个 Log 表示一条日志，一个 LogGroup 中 Log 个数不能超过10000 |
| contextFlow | 否       | 保持上下文的 UID，该字段目前暂无效用                         |
| filename    | 否       | 日志文件名                                                   |
| source      | 否       | 日志来源，一般使用机器 IP 作为标识                           |
| logTags     | 否       | 日志的标签列表                                               |

Log 说明：

| 字段名   | 是否必选 | 含义                                                         |
| -------- | -------- | ------------------------------------------------------------ |
| time     | 是       | 日志时间（Unix 格式时间戳），支持秒、毫秒，建议采用毫秒 |
| contents | 否       | key-value 格式的日志内容，表示一条日志里的多个 key-value 组合 |

Content 说明：

| 字段名 | 是否必选 | 含义                                                         |
| ------ | -------- | ------------------------------------------------------------ |
| key    | 是       | 单条日志里某个字段组的 key 值，不能以`_`开头                 |
| value  | 是       | 单条日志某个字段组的 value 值，单条日志 value 不能超过1MB，LogGroup 中所有 value 总和不能超过5MB |

LogTag 说明：

| 字段名 | 是否必选 | 含义                         |
| ------ | -------- | ---------------------------- |
| key    | 是       | 自定义的标签 key              |
| value  | 是       | 自定义的标签 key 对应的 value 值 |

## 响应

#### 响应示例

```shell
HTTP/1.1 200 OK
Content-Length: 0
```

#### 响应头

除公共响应头部外，无特殊响应头部。

#### 响应参数

无。

## 错误码

参见 [错误码](https://intl.cloud.tencent.com/document/product/614/12402)。

## PB 编译示例

本示例将说明如何使用官方 protoc 编译工具将 PB 描述文件 编译生成为 C++ 语言可调用的上传日志接口。

> ?目前 protoc 官方支持 Java、C++、Python 等语言的编译，详情请参见 [protoc](https://github.com/protocolbuffers/protobuf)。

#### 1. 安装 Protocol Buffer

下载 [Protocol Buffer](https://main.qcloudimg.com/raw/d7810aaf8b3073fbbc9d4049c21532aa/protobuf-2.6.1.tar.gz) ，解压并安装。示例版本为 protobuf 2.6.1，环境为 Centos 7.3 系统。
解压`protobuf-2.6.1.tar.gz`压缩包至`/usr/local`目录并进入该目录，执行命令如下：
```sh
[root@VM_0_8_centos]# tar -zxvf protobuf-2.6.1.tar.gz -C /usr/local/ && cd /usr/local/protobuf-2.6.1
```
开始编译和安装，配置环境变量，执行命令如下：
```sh
[root@VM_0_8_centos protobuf-2.6.1]# ./configure 
[root@VM_0_8_centos protobuf-2.6.1]# make && make install
[root@VM_0_8_centos protobuf-2.6.1]# export PATH=$PATH:/usr/local/protobuf-2.6.1/bin
```
编译成功后，您可以使用以下命令查看版本：
```sh
[root@VM_0_8_centos protobuf-2.6.1]# protoc --version
liprotoc 2.6.1
```



#### 2. 创建 PB 描述文件

PB 描述文件是通信双方约定的数据交换格式，上传日志时须将规定的协议格式编译成对应语言版本的调用接口，然后添加到工程代码里，详情请参见 [protoc](https://github.com/protocolbuffers/protobuf) 。

以日志服务所规定的 PB 数据格式内容为准， 在本地创建 PB 消息描述文件 cls.proto。

> !PB 描述文件内容不可更改，且文件名须以`.proto`结尾。

cls.proto 内容（PB 描述文件）如下：

```
package cls;

message Log
{
    message Content
    {
        required string key   = 1; // 每组字段的 key
        required string value = 2; // 每组字段的 value
    }
    required int64   time     = 1; // 时间戳，UNIX时间格式
    repeated Content contents = 2; // 一条日志里的多个kv组合
}

message LogTag
{
    required string key       = 1;
    required string value     = 2;
}

message LogGroup
{
    repeated Log    logs        = 1; // 多条日志合成的日志数组
    optional string contextFlow = 2; // 目前暂无效用
    optional string filename    = 3; // 日志文件名
    optional string source      = 4; // 日志来源，一般使用机器IP
    repeated LogTag logTags     = 5;
}

message LogGroupList
{
    repeated LogGroup logGroupList = 1; // 日志组列表
}

```

#### 3. 编译生成

此例中，使用 proto 编译器生成 C++ 语言的文件，在 cls.proto 文件的同一目录下，执行如下编译命令：

```
protoc --cpp_out=./ ./cls.proto 

```

>? `--cpp_out=./ `表示编译成 cpp 格式并输出当前目录下，`./cls.proto`表示位于当前目录下的 cls.proto 描述文件。
>

编译成功后，会输出对应语言的代码文件。此例会生成 cls.pb.h 头文件和 cls.pb.cc 代码实现文件，如下所示：

```
[root@VM_0_8_centos protobuf-2.6.1]# protoc --cpp_out=./ ./cls.proto
[root@VM_0_8_centos protobuf-2.6.1]# ls
cls.pb.cc cls.pb.h cls.proto
```

#### 4. 调用

将生成的 cls.pb.h 头文件引入代码中，调用接口进行数据格式封装。
