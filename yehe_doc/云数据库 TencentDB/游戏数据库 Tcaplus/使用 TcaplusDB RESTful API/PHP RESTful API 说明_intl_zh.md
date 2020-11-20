# PHP版本的TcaplusDB RestAPI使用方法
[TOC]
## 1. 使用准备

- 表创建：创建一个示例表，示例表为[`game_players.proto`](https://tcaplusdb-sdk-1301716906.cos.ap-shanghai.myqcloud.com/3.36.0.192960/game_players.proto)。
- CVM实例申请：根据表创建所在的子网区域，申请对应区域的腾讯云CVM实例, 建议配置: Centos7, 1c2g。
- php安装： 新申请实例未安装php, 需要执行yum install php安装默认版本的Php(5.4.16)， php版本要求大于5.3。
- 通过[SDK下载](https://intl.cloud.tencent.com/document/product/1016/30285) PHP RESTful API SDK安装包。


## 2. 使用方法
### 2.1 修改配置
所有基础配置统一放在当前目录下的*config.php*中, 需要根据用户申请的表信息进行相应更改。
* __连接配置__:如url, endpoint, table_group_id, access_id, access_passwd等，修改成对应值, 连接信息获取请参考:[获取访问点信息](https://intl.cloud.tencent.com/document/product/1016/30276)。
* __默认数据源__: 此部分变量都为大写，用于作为demo.php中具体接口函数的数据源，可以统一在这里修改。
### 2.2 接口函数
所有API接口封装成函数统一在*demo.php*中， 总共有8个接口函数，所有接口函数支持从配置中加载数据源进行批量操作，具体函数如下所示：

|接口函数名|接口函数功能|
|---|---|
|GetRecord|获取表记录|
|AddRecord|插入表记录|
|SetRecord|更新表记录|
|DeleteRecord|删除记录|
|FieldGetRecord|获取指定记录属性字段|
|FieldSetRecord|更新指定记录属性字段值|
|FieldIncRecord|更新指定记录属性字段数值，如增加/减少数值类型值|
|PartKeyGetRecord|根据指定索引获取指定记录属性字段值|



## 3. SDK接口列表
### 3.1 add
插入一条表记录，如果记录存在则报错。

```
@param $table_group_id (必须) - 目标表table_group_id
@param $table_name (必须) - 目标表table_name
@param $record (必须) - 待插入的目标记录数组
@param $ReturnValues (可选) - 指定返回的自定义值
@param $resultflag (可选) - 指定返回响应包的内容，取值范围如下：
            0: 应答中仅包含请求成功或失败
            1: 应答中包含与请求一致的值
            2: 应答中包含被修改的数据的所有字段最新值
            3: 应答中包含记录被修改前的值

public function add($table_group_id, $table_name, array $record, $ReturnValues = 'TcaplusDB', $resultflag = 1)
```

### 3.2 get

 根据主键查询一条记录，支持指定要返回的属性字段列表，参考$params["select"]定义。
 ```
@param $table_group_id (必须) 游戏区ID
@param $table_name (必须) 表名
@param $params (必须)
    $params\["select"\] (可选) 查询的字段 数组
    $params \["keys"\] (必须) 查询目标记录的主键字段(Primary key)
    $params \["limit"\] (可选) 返回记录数限制量
    $params \["offset"\] (可选) 返回记录数偏移量

public function get($table_group_id, $table_name, $params)
```

### 3.3 fieldGet
根据主键查询返回指定字段的值，指定字段列表参考:`$param["select"]`, 这个参数必须为非空。
```
@param $table_group_id (必须) 游戏区ID
@param $table_name (必须) 表名
@param  $params (必须)
    $params\["select"\] (必须) 查询的字段 数组
    $params\["keys"\] (必须) 查询目标记录的主键字段(Primary key)
    $params\["limit"\] (可选)  返回记录数限制量
    $params\["offset"\] (可选) 返回记录数偏移量

public function fieldGet($table_group_id, $table_name, $params)

```

### 3.4 partKeyGet
根据表定义的索引查询返回一条或多条记录，支持指定字段列表返回，支持limit和offset参数控制返回包的记录数。
```
@param $table_group_id (必须) 游戏区ID
@param $table_name (必须) 表名
@param  $params (必须)
    $params\["select"\] (可选) 查询的字段 数组
    $params\["index"\] (必须) 查询的索引名称
    $params\["keys"\] (必须) 查询目标记录的主键字段(Primary key)
    $params\["limit"\] (可选)  返回记录数限制量,　默认值-1
    $params\["offset"\] (可选) 返回记录数偏移量

public function partKeyGet($table_group_id, $table_name, $params)
```

对于partkeyGet接口，1个请求返回的最大包大小为`256KB`, limit的设置依赖于单条记录大小。推荐设置策略：
* __单条记录小于256KB__：Limit 参考设置为256KB/[单条记录大小], 如记录大小为10KB，则limit推荐设置20-25左右。
* __单条记录大于等于256KB__: Limit设置为1, 即一次请求只返回一条记录。

关于limit和offset设置的响应示例如下:
```
#请求设置limit=-1, offset=0
{"MultiRecords":[{"RecordVersion":1,"Record":{"pay":{"amount":1000,"pay_id":10101},"player_email":"kosh@test.com","player_id":1,"player_name":"kosh"}},{"RecordVersion":1,"Record":{"pay":{"amount":1000,"pay_id":10101},"player_email":"kosh@163.com","player_id":1,"player_name":"kosh"}},{"RecordVersion":1,"Record":{"pay":{"amount":1000,"pay_id":10101},"player_email":"kosh@gmail.com","player_id":1,"player_name":"kosh"}},{"RecordVersion":1,"Record":{"pay":{"amount":1000,"pay_id":10101},"player_email":"kosh@126.com","player_id":1,"player_name":"kosh"}}],"TotalNum":4,"RemainNum":0,"ErrorCode":0,"ErrorMsg":"Succeed"}

#请求设置limit=2, offset=0
{"MultiRecords":[{"RecordVersion":1,"Record":{"pay":{"amount":1000,"pay_id":10101},"player_email":"kosh@test.com","player_id":1,"player_name":"kosh"}},{"RecordVersion":1,"Record":{"pay":{"amount":1000,"pay_id":10101},"player_email":"kosh@163.com","player_id":1,"player_name":"kosh"}}],"TotalNum":4,"RemainNum":2,"ErrorCode":0,"ErrorMsg":"Succeed"}
```
从上面响应包来看，设置了limit和offset的结果返回的条数和设定的limit的大小保持一致。
如果用户想获取全量的索引数据，则可根据响应包中的`RemainNum`和`TotalNum`这两个标识来判断数据是否获取完全。

### 3.5 set
更新记录或插入记录, 如果记录存在则进行更新，如果记录不存在则进行插入。
```
@param $table_group_id (必须) 游戏区ID
@param $table_name (必须) 表名
@param $record (必须) 待设置的目标记录 该操作包含插入和修改的语义
@param $ReturnValues (可选) 校验字符串, 服务端返回同样的字符串
@param $resultflag (可选) 默认值1，设置响应包的内容模式，取值范围如下:
            0: 应答中仅包含请求成功或失败
            1: 应答中包含与请求一致的值
            2: 应答中包含被修改的数据的所有字段最新值
            3: 应答中包含记录被修改前的值

public function set($table_group_id, $table_name, array $record, $ReturnValues = 'TcaplusDB', $resultflag = 1)
```

### 3.6 fieldSet
根据主键更新指定字段的值，指定更新字段参考: `$field_path`。
```
@param $table_group_id (必须) 游戏区ID
@param $table_name (必须) 表名
@param $record (必须) 待设置的目标记录 该操作包含插入和修改的语义
@param $field_path (必须) - 待设置的字段名(路径)数组, 嵌套字段可以通过点分路径的方式指定
@param $ReturnValues (可选) 校验字符串, 服务端返回同样的字符串
@param $resultflag (可选) 默认值1，设置响应包的内容模式，取值范围如下:
            0: 应答中仅包含请求成功或失败
            1: 应答中包含与请求一致的值
            2: 应答中包含被修改的数据的所有字段最新值
            3: 应答中包含记录被修改前的值

public function fieldSet($table_group_id, $table_name, array $record, $field_path, $ReturnValues = 'TcaplusDB', $resultflag = 1)

```

### 3.7 fieldInc
根据主键更新指定字段的值（自增或自减)，仅针对数值类型字段。如: pay.method原始值为200，请求值若为50，则最终值为250 ; 请求值若为-50,　则最终值为150。__注意__：自减仅针对有符号型字段，如int32,int64。
```
@param $table_group_id (必须) 游戏区ID
@param $table_name (必须) 表名
@param $record (必须)  待自增、自减的记录，必须保证记录中包含主键，待自增、自减的记录必须是整数类型
@param $ReturnValues (可选) 校验字符串, 服务端返回同样的字符串
@param $resultflag (可选), 默认值1，设置响应包的内容模式，取值范围如下:
            0: 应答中仅包含请求成功或失败
            1: 应答中包含与请求一致的值
            2: 应答中包含被修改的数据的所有字段最新值
            3: 应答中包含记录被修改前的值
@param $dataVersion (可选) 版本号
@param $dataVersionCheck (可选) 数据版本检查策略，取值范围:
    1 : 表示版本号一致才能会写入
    2 : 不检测版本号，强制将客户端传入的版本号设置到存储层
    3 : 默认值，不校验版本号，写操作会将存储层数据版本号+1

public function fieldInc($table_group_id, $table_name, array $record, $ReturnValues = 'TcaplusDB', $resultflag = 2, $dataVersion = -1, $dataVersionCheck = 3)

```

### 3.8 delete
删除指定主键的记录。
```
@param $table_group_id (必须) 游戏区ID
@param $table_name (必须) 表名
@param $record (必须)  待删除的目标记录，可以只需要设置主键字段
@param  $ReturnValues (可选) 校验字符串, 服务端返回同样的字符串
@param $resultflag(可选)  默认值1，设置响应包的内容模式，取值范围如下:
            0: 应答中仅包含请求成功或失败
            1: 应答中包含与请求一致的值
            2: 应答中包含被修改的数据的所有字段最新值
            3: 应答中包含记录被修改前的值

public function delete($table_group_id, $table_name, array $record, $ReturnValues = 'TcaplusDB', $resultflag = 1)
```

## 4. demo.php的使用方法

为方便用户快速体验Tcaplusdb sdk功能， 目前所有接口已经封闭成函数统一放在demo.php, 共8个函数，可以按需执行对应的函数，只需要注释其它函数即可，执行命令如下：
```
php -f  "demo.php"
```



## 5. sample目录中接口使用方法
为了方便测试单个接口的功能，这里还把所有sdk接口函数单独成了程序，分别对应demo中的8个接口函数，采用的也是数据源与程序代码分离管理方式。所有接口函数的数据源有两个地方 ，一个是默认的数据源统一在`config.php`中，另一个是每个接口函数自己的数据源在`data`子目录下，用户可以修改该数据文件来执行对应的接口函数，方便需要批量操作时避免在程序代码中定义数据源。如果数据文件不存在则会加载默认数据源。数据源统一采用数据列表方式，支持批量加载。sample中的程序文件执行方法类似：
```
php -f <具体的接口函数文件>
```
