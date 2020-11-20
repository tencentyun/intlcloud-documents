# TcaplusDB Java RESTful API 使用说明
[TOC]

# 1. 背景
为满足用户使用Java操作TcaplusDB表，基于RESTful API封装了一个Java SDK。本文档主要介绍基于此Java RESTful API来操作TcaplusDB PB表(基于protobuf协议)。
# 2. 前置条件
## 2.1. CVM环境
- 申请一台腾讯云CVM实例,　建议配置: 1C2G, Centos7。__注意：申请的CVM实例需要和所申请的TcaplusDB表同属一个VPC网络环境。__
- 通过[SDK下载](https://intl.cloud.tencent.com/document/product/1016/30285) Java RESTful API SDK安装包。

## 2.2 Java环境
SDK依赖Java 1.8以上环境，如果CVM操作系统为CentOS 7或Red Hat 7以上版本， 执行`yum install -y java`即可。
## 2.3.TcaplusDB表格
创建TcaplusDB测试表，示例表为[`game_players.proto`](https://tcaplusdb-sdk-1301716906.cos.ap-shanghai.myqcloud.com/3.36.0.192960/game_players.proto)

## 2.4 接口说明
目前SDK示例支持8个接口，详情如下:

|接口名|接口用途|
|---|---|
|addRecord|增加一条TcaplusDB记录, 记录必须包含所有主键字段值|
|getRecord|查询一条TcaplusDB记录，必须指定主键字段查询|
|setRecord|更新一条TcaplusDB记录，必须指定主键字段更新，若记录不存在则插入一条新记录|
|deleteRecord|删除一条TcaplusDB记录，必须指定主键字段删除|
|fieldSetRecord|更新指定字段，必须指定主键字段更新|
|fieldGetRecord|获取指定字段，必须指定主键字段获取|
|fieldIncRecord|更新指定字段，只针对数值类型字段，自增或自减场景，必须指定主键字段更新|
|partkeyGetRecord|根据指定的索引名和对应的索引字段值获取相应TcaplusDB记录(1条或多条),必须指定对应的索引字段值|


# 3. 使用步骤
上传整个SDK包`tcaplusdb-restapi-java-sdk-1.0-assembly.zip`到CVM目录，解压后目录名`tcaplusdb-restapi-java-sdk-1.0`。
## 3.1 配置准备
配置文件在`tcaplusdb-restapi-java-sdk-1.0/conf/config.properties`。配置内容如下：
```
#replace with your table endpoint
endpoint=http://10.0.0.16

#replace with your table access id
access_id=60

#replace with your table access password
access_password=Tcaplus2019

#replace with your table group id
table_group_id=1

#replace with your table name
table_name=game_players

#optional, configure the returning fields for GetRecord API, multiple fields with comma delimeter
get_select_fields=

#required, configure the returing fields for FieldGetRecord API
field_get_select_fields=game_server_id,is_online

#optional, configure the returning fields for PartkeyGetRecord API
part_key_get_select_fields=game_server_id,is_online

#required, configure the updating fields for FieldSetRecord API
field_set_fields=game_server_id,pay.amount

#required, configure the index keys for PartkeyGetRecord API
part_key_index_keys=player_id,player_name

#required, configure the index name for PartkeyGetRecord API
part_key_index_name=index_1

#optional, configure the limit number of records per request to return for PartkeyGetRecord API, value range: >0
part_key_limit = 10

#optional, configure the offset position to return for PartkeyGetRecord API, value range: >=0
part_key_offset = 0
```

## 3.2 数据准备
示例为每个RESTful API接口单独准备测试数据，以json文件方式放在`tcaplusdb-restapi-java-sdk-1.0/conf`目录。

|文件名|文件说明|
|---|---|
|add_data.json|用于addRecord示例接口，增加一条记录|
|set_data.json|用于updateRecord示例接口，更新一条记录字段值|
|delete_data.json|用于deleteRecord示例接口，删除记录的主键值|
|get_data.json|用于getRecord示例接口，获取记录的主键值|
|field_get_data.json|用于fieldGetRecord示例接口，获取部分字段的值|
|field_set_data.json|用于fieldSetRecord示例接口，更新部分字段的值|
|field_inc_data.json|用于fieldIncRecord示例接口，增加部分字段的值，针对数值类型字段|
|partkey_get_data.json|用于partkeyGetRecord示例接口，根据索引获取记录值|

## 3.3 脚本执行
主要执行脚本在`tcaplusdb-restapi-java-sdk-1.0/bin/run.sh`。执行方法如下:
```
#增加一条记录
sh bin/run.sh add
#获取一条记录
sh bin/run.sh get
#更新一条记录
sh bin/run.sh set
#删除一条记录
sh bin/run.sh delete
#更新部分字段
sh bin/run.sh field_set
#获取部分字段
sh bin/run.sh field_get
#更新部分字段值（数据类型)
sh bin/run.sh field_inc
#根据索引获取一条记录
sh bin/run.sh partkey_get

```

# 4 接口数据说明
## 4.1 addRecord接口
此接口增加一条记录，插入的数据格式为JSON格式，示例数据如下所示:
```
{"player_id":1,"player_name":"test","player_email":"test@email.com", "game_server_id":2,"login_timestamp":[],"logout_timestamp":[],"is_online":true,"pay":{"pay_id":1,"amount":20,"method":3}}
```
## 4.2 getRecord接口
查询一条记录，指定记录的主键字段，数据格式为JSON, 示例数据如下所示:
```
{"player_id":1,"player_name":"test","player_email":"test@email.com"}
```

查询接口还支持指定要返回的字段列表，在配置文件`config.properties`中定义了`get_select_fields`配置项，用于指定要返回的字段名，如果配置为空则默认返回记录所有字段，如果不为空则返回指定的字段的值。

## 4.3 setRecord接口
更新一条记录，更新记录必须包含主键字段，数据格式为JSON，示例数据如下所示:
```
{"player_id":1,"player_name":"test","player_email":"test@email.com", "game_server_id":2,"login_timestamp":[],"logout_timestamp":[],"is_online":false,"pay":{"pay_id":1,"amount":30,"method":3}}
```

## 4.4 deleteRecord接口
删除一条记录，输入数据必须包含主键字段，数据格式为JSON, 示例数据如下所示:
```
{"player_id":1,"player_name":"test","player_email":"test@email.com"}
```

## 4.5 fieldSetRecord接口
更新部分字段值，输入数据必须包含主键字段，数据格式为JSON, 示例数据如下所示：
```
{"player_id":1,"player_name":"test","player_email":"test@email.com", "game_server_id":3,"is_online":false, "login_timestamp":[],"logout_timestamp":[],"pay":{"pay_id":1,"amount":40,"method":3}}
```
同时还需要指定更新的部分字段名，在配置文件`config.properties`中定义了`field_set_fields`这个配置项，指定对应的字段名即可，用逗号隔开，__不能为空__。

## 4.6 fieldGetRecord接口
获取部分字段值，输入数据必须包含主键字段，数据格式为JSON，示例数据如下所示：
```
{"player_id":1,"player_name":"test","player_email":"test@email.com"}
```
同时还需要指定要获取的部分字段名，在配置文件`config.properties`中定义了`field_get_select_fields`这个配置项,　指定需要返回的字段值，__不能为空__。

## 4.7 fieldIncRecord接口
更新部分字段值，与fieldSetRecord接口所不同的是，此接口只支持更新数值类型的字段值，如增加或减少相应值，输入数据必须包含主键字段和要更新数值字段，数据格式为JSON，示例数据如下所示：
```
{"player_id":1,"player_name":"test","player_email":"test@email.com", "pay":{"amount":50}}
```
假设pay.amount的初始值为100, 请求传参值为50, 则最终pay.amount的值为150。
## 4.8 partkeyGetRecord接口
根据指定索引获取对应记录，可能对应多条记录，支持返回指定字段的值，输入数据必须包含索引字段，数据格式为JSON，示例数据如下所示：
```
{"player_id":1,"player_name":"test","player_email":"test@email.com"}
```
同时还必须指定对应的索引名和索引字段名，在配置文件`config.properties`中定义：`part_key_index_name`表示索引名，`part_key_index_keys`表示索引字段名, __这两个配置项不能为空__。
如果要返回指定字段，支持在配置文件中配置`part_key_get_select_fields`来指定要返回的字段，可以为空。

对于此接口，1个请求返回的最大包大小为`256KB`, limit的设置依赖于单条记录大小。推荐设置策略：
* __单条记录小于256KB__：Limit 参考设置为256KB/[单条记录大小], 如记录大小为10KB，则limit推荐设置20-25左右。
* __单条记录大于等于256KB__: Limit设置为1, 即一次请求只返回一条记录。

对于设置Limit和Offset的场景，如果要根据索引键获取全量的数据，则需要依据响应包中返回的`TotalNum和RemainNum`标识来判断数据是否获取完全。

设置Limit和Offset的场景演示可按如下步骤进行:
```
#step1, 准备批量演示数据，参考conf/batch_add_data.json.设置Limit值和Offset值
part_key_limit = 2
part_key_offset = 0

#step2, 批量增加演示数据，用batch_add命令,增加3条记录
sh bin/run.sh batch_add

#step3, 调用partkey_get命令，会执行partkeyGetRecord两次：一次不带Limit和Offset, 一次带Limit和Offset,观察两次执行的结果差异。
sh bin/run.sh partkey_get

#step4, 不带limit和offset的响应数据如下,总共4条数据

{"MultiRecords":[{"RecordVersion":3,"Record":{"game_server_id":3,"is_online":true,"player_email":"test@email.com","player_id":1,"player_name":"test"}},{"RecordVersion":1,"Record":{"game_server_id":3,"is_online":true,"player_email":"test1@email.com","player_id":1,"player_name":"test"}},{"RecordVersion":1,"Record":{"game_server_id":4,"is_online":true,"player_email":"test2@email.com","player_id":1,"player_name":"test"}},{"RecordVersion":1,"Record":{"game_server_id":5,"is_online":true,"player_email":"test3@email.com","player_id":1,"player_name":"test"}}],"TotalNum":4,"RemainNum":0,"ErrorCode":0,"ErrorMsg":"Succeed"}

#step5, 带limit和offset的响应数据如下,只返回2条和limit配置值一致

{"MultiRecords":[{"RecordVersion":3,"Record":{"game_server_id":3,"is_online":true,"player_email":"test@email.com","player_id":1,"player_name":"test"}},{"RecordVersion":1,"Record":{"game_server_id":3,"is_online":true,"player_email":"test1@email.com","player_id":1,"player_name":"test"}}],"TotalNum":4,"RemainNum":2,"ErrorCode":0,"ErrorMsg":"Succeed"}

```

