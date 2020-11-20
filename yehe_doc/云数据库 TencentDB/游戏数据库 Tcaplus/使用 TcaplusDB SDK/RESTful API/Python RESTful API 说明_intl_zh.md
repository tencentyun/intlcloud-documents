# TcaplusDB RESTful API Python SDK
[TOC]
## 1. 使用准备

本SDK是基于RESTful API封装的一个Python语言SDK, 用于进行TcaplusDB表的增删查改操作。

### 1.1 CVM环境
- 申请一个CVM实例，参考配置: Centos7, 1c2g。CVM所在的VPC网络需要和TcaplusDB表所在VPC网络保持一致。
- 通过[SDK下载](https://intl.cloud.tencent.com/document/product/1016/30285) Python RESTful API SDK安装包。

### 1.2 TcaplusDB表创建
本示例所用的TcaplusDB表基于Google protobuf协议定义，示例表为[`game_players.proto`](https://tcaplusdb-sdk-1301716906.cos.ap-shanghai.myqcloud.com/3.36.0.192960/game_players.proto)。

## 2. 接口使用步骤

1. 通过指定endpoint, access_id, access_passwd参数创建TcaplusRestClient的对象client
2. 通过client对象的SetTargetTable方法指定想要访问的目标表
3. 调用接口函数，发送数据访问请求

		```
		#创建TcaplusRestClient对象
		#endpoint: restful API, such as http://x.x.x.x:80
		client = TcaplusRestClient(endpoint, access_id, access_passwd)

		#SetTargetTable指定想要访问的目标表
		client.SetTargetTable(table_group_id=1, table_name='game_players')

		#发送数据访问请求，以AddRecord为例
		record = {'player_id': 10805514, 'player_name': 'Calvin', 'player_email': 'calvin@test.com', 'game_server_id': 10,
						'login_timestamp': ['2019-12-12 15:00:00'], 'logout_timestamp': ['2019-12-12 16:00:00'], 'is_online': False, 'pay': {'pay_id': 10101, 'amount': 1000, 'method': 1}}
		status, resp = client.AddRecord(record, custom_headers=None, return_values=None, table_group_id=None, table_name=None)
		```

4. 用户通过SetTargetTable方法指定目标表后，可以通过GetTargetTable方法获取目标表
```
table_group_id, table_name = client.GetTargetTable()
```
5. 也可以通过接口的table_group_id和table_name参数直接指定目标表，通过这种方式不会改变SetTargetTable函数设置的目标表
```
status, resp = client.AddRecord(record, custom_headers=None, return_values=None, table_group_id=1, table_name='game_players')
```

## 3. 接口列表

### 3.1 GetRecord 记录查询
根据主键字段查询表记录，一次返回一条。
```
@param keys (必须) - 查询目标记录的主键字段(Primary key)字典
@param select_fields (可选) - 返回结果中所包含的非主键字段名数组, 嵌套字段可以通过点分路径的方式指定
@param custom_headers (可选) - 用户需要指定的http header
@param table_group_id (可选) - 表所在集群表格组id
@param table_name (可选) - 目标表table_name

def GetRecord(self, keys, select_fields=[], custom_headers=None, table_group_id=None, table_name=None)
```
### 3.2 AddRecord 插入记录
插入一条表记录，如果记录存在则报错。
			```
			@param record (必须) - 待插入的目标记录json对象
			@param custom_headers (可选) - 用户需要指定的http header
			@param table_group_id (可选) - 表所在集群表格组id
			@param table_name (可选) - 目标表table_name

			def AddRecord(self, record, custom_headers=None, return_values=None, table_group_id=None, table_name=None)
			```

### 3.3 SetRecord 设置记录
依据主键更新或插入一条记录，如果记录已存在则更新记录相关值，如果记录不存在则插入新的记录。
```
@param record (必须) - 待设置的目标记录json对象，该操作包含插入和修改的语义
@param custom_headers (可选) - 用户需要指定的http header
@param table_group_id (可选) - 表所在集群表格组id
@param table_name (可选) - 目标表table_name

def SetRecord(self, record, custom_headers=None, return_values=None, table_group_id=None, table_name=None)
```
### 3.4 DeleteRecord 删除记录
根据主键删除一条记录。
```
@param record (必须) - 待删除的目标记录json对象，可以只需要设置主键字段
@param custom_headers (可选) - 用户需要指定的http header
@param table_group_id (可选) - 表所在集群表格组id
@param table_name (可选) - 目标表table_name

def DeleteRecord(self, record, custom_headers=None, return_values=None, table_group_id=None, table_name=None)
```
### 3.5 FieldGetRecord 指定字段查询
根据主键获取部分字段值，指定需要返回的字段列表(必须为非主键字段)，嵌套字段以点分方式表示，如:　pay.amount。
```
@param keys (必须) - 查询目标记录的主键字段(Primary key)字典
@param select_fields (必须) - 返回结果中所包含的非主键字段名数组, 嵌套字段可以通过点分路径的方式指定
@param custom_headers (可选) - 用户需要指定的http header
@param table_group_id (可选) - 表所在集群表格组id
@param table_name (可选) - 目标表table_name

def FieldGetRecord(self, keys, select_fields, custom_headers=None, table_group_id=None, table_name=None)
```

### 3.6 FieldSetRecord 指定字段设置
根据主键更新部分字段的值，指定需要更新的字段列表(必须为非主键字段), 嵌套字段以点分方式表示，如: pay.amount。
```
@param record (必须) - 待设置的目标记录json对象，该操作包含插入和修改的语义
@param field_path (必须) - 待设置的字段名(路径)数组, 嵌套字段可以通过点分路径的方式指定
@param custom_headers (可选) - 用户需要指定的http header
@param table_group_id (可选) - 表所在集群表格组id
@param table_name (可选) - 目标表table_name

def FieldSetRecord(self, record, field_path, custom_headers=None, return_values=None, table_group_id=None, table_name=None)
```

### 3.7 FieldIncRecord 指定字段自增/自减
根据主键更新数值类型字段的值，自增或自减。如pay.method原始值为200, 请求值为50，则最终pay.method值为250，如果请求值为负数-50, 则最终pay.method值为150。__注意__: 这里如果是`自减`，那么请求传入的自减字段的类型必须为有符号数值类型如int32,int64。
```
@param record (必须) - 待自增、自减的记录，必须保证记录中包含主键，待自增、自减的记录必须是整数类型
@param custom_headers (可选) - 用户需要指定的http header
@param table_group_id (可选) - 表所在集群表格组id
@param table_name (可选) - 目标表table_name

def FieldIncRecord(self, record, custom_headers=None, return_values=None, table_group_id=None, table_name=None)
```

### 3.8 PartkeyGetRecord 索引查询
根据表定义的索引进行数据查询，返回一条或多条索引键匹配的记录。支持指定字段列表返回。支持指定limit和offset来控制每个请求返回的包大小。
```
@param index_keys (必须) - 查询目标记录的索引键字典
@param index_name (必须) - 查询的索引名称
@param select_fields (可选) - 返回结果中所包含的非主键字段名数组, 嵌套字段可以通过点分路径的方式指定
@param custom_headers (可选) - 用户需要指定的http header
@param table_group_id (可选) - 表所在集群表格组id
@param table_name (可选) - 目标表table_name
@param limit (可选) -限制返回的记录条数
@param offset (可选) -设定返回记录数的起始偏移量

def PartkeyGetRecord(self, index_keys, index_name, select_fields=[], custom_headers=None, table_group_id=None, table_name=None, limit=None, offset=None)
```
对于该接口，1个请求返回的最大包大小为`256KB`, limit的设置依赖于单条记录大小。推荐设置策略：
* __单条记录小于256KB__：Limit 参考设置为256KB/[单条记录大小], 如记录大小为10KB，则limit推荐设置20-25左右。
* __单条记录大于等于256KB__: Limit设置为1, 即一次请求只返回一条记录。

下面是关于设置limit和offset以及不设置的响应包情况:
```
#索引键情况
{'player_id': 39775502, 'player_name': 'Sara'}

#请求不设置limit和offset，响应包如下
{u'ErrorCode': 0, u'ErrorMsg': u'Succeed', u'MultiRecords': [{u'RecordVersion': 1, u'Record': {u'logout_timestamp': [u'2019-12-12 16:00:00'], u'player_name': u'Sara', u'login_timestamp': [u'2019-12-12 15:00:00'], u'pay': {u'amount': 100, u'pay_id': 1, u'method': 1}, u'game_server_id': 1, u'player_email': u'sara@test.com', u'is_online': True, u'player_id': 39775502}}, {u'RecordVersion': 1, u'Record': {u'logout_timestamp': [u'2019-12-12 16:10:00'], u'player_name': u'Sara', u'login_timestamp': [u'2019-12-12 15:10:00'], u'pay': {u'amount': 200, u'pay_id': 2}, u'game_server_id': 2, u'player_email': u'sara@163.com', u'is_online': True, u'player_id': 39775502}}, {u'RecordVersion': 1, u'Record': {u'logout_timestamp': [u'2019-12-12 16:20:00'], u'player_name': u'Sara', u'login_timestamp': [u'2019-12-12 15:20:00'], u'pay': {u'amount': 300, u'pay_id': 3, u'method': 1}, u'game_server_id': 3, u'player_email': u'sara@gmail.com', u'is_online': True, u'player_id': 39775502}}], u'RemainNum': 0, u'TotalNum': 3}

#请求设置limit和offset, 其中limit设置为2，响应包如下
{u'ErrorCode': 0, u'ErrorMsg': u'Succeed', u'MultiRecords': [{u'RecordVersion': 1, u'Record': {u'logout_timestamp': [u'2019-12-12 16:00:00'], u'player_name': u'Sara', u'login_timestamp': [u'2019-12-12 15:00:00'], u'pay': {u'amount': 100, u'pay_id': 1, u'method': 1}, u'game_server_id': 1, u'player_email': u'sara@test.com', u'is_online': True, u'player_id': 39775502}}, {u'RecordVersion': 1, u'Record': {u'logout_timestamp': [u'2019-12-12 16:10:00'], u'player_name': u'Sara', u'login_timestamp': [u'2019-12-12 15:10:00'], u'pay': {u'amount': 200, u'pay_id': 2}, u'game_server_id': 2, u'player_email': u'sara@163.com', u'is_online': True, u'player_id': 39775502}}], u'RemainNum': 1, u'TotalNum': 3}
```

从上面响应包来看，设置了limit和offset的结果返回的条数和设定的limit的大小保持一致。
如果用户想获取全量的索引数据，则可根据响应包中的`RemainNum`和`TotalNum`这两个标识来判断数据是否获取完全。




