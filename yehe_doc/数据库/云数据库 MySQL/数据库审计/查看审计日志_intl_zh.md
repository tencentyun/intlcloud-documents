本文为您介绍如何查看数据库审计日志及相关审计日志列表的字段。

>?
>- 2023年07月12日发布了新版审计日志页面，审计日志搜索字段“扫描行数”为新增字段，在此日期之前的存量审计日志，此字段数据会显示为“-”，对应下载的文件和 API 展示为“-1”。
>- 审计日志字段“执行时间”、“CPU 时间”在控制台和下载的审计日志文件里的单位统一调整为微秒。
>- 搜索审计日志时，对多个搜索项进行分隔的字符由**逗号**更换为**换行符**。

## 前提条件
已 [开通审计服务](https://www.tencentcloud.com/document/product/236/52086)。
## 查看审计日志
>?审计日志展示时间扩展到毫秒，便于对 SQL 进行更精确的排序和问题分析。
>

1. 登录 [MySQL 控制台](https://console.cloud.tencent.com/dls/mysql)。
2. 在左侧导航栏选择**数据库审计**。
3. 在上方选择**地域**后，在**审计实例**页，单击**审计状态**选择**已开启**选项过滤已开启审计的实例。
4. 在**审计实例**列表里找到**目标实例**（也可在搜索框通过资源属性筛选快速查找），在其操作列单击**查看审计日志**，跳转至**审计日志**页查看对应日志。

### 工具列表
- 在**审计实例筛选框**，可选择切换已开启审计服务的其他审计实例。
- 在**时间框**，选择时间段，可查看所选时间段内相关审计日志。
   >?搜索时间段支持选取存在数据的任意时间段进行搜索，最多展示符合条件的前60000条记录。
   > 
- 在**搜索框**，选择搜索项（SQL 命令详情、客户端 IP、用户账号、数据库名、SQL 类型、错误码、执行时间（微秒）、锁等待时间（微秒）、IO 等待时间（微秒）、事务持续时间（微秒）、CPU 时间（微秒）、线程 ID、扫描行数、影响行数、返回行数等）进行搜索，可查看相关审计结果，多个搜索项使用换行符分隔。
<table><thead><tr><th>搜索项</th><th>匹配项</th><th>说明</th></tr></thead><tbody>
<tr>
<td>SQL 命令详情</td>
<td>包含<br>不包含</td>
<td><li>输入 SQL 命令详情，多个关键字使用换行符进行分隔。</li><li>SQL 命令详情搜索不区分大小写。</li><li>当匹配类型为包含/不包含时，仅支持分词维度模糊搜索，不支持通配符模糊搜索。<br>例：SQL 命令详情为 SELECT * FROM test_db LIMIT 1; 可以通过“SELECT”、“select * from”、“*”、“SELECT * FROM test_db LIMIT 1;”、“from Test_DB”等分词关键词进行搜索；无法通过 “SEL”、“sel”、“test” 等通配关键词进行搜索。</li></td>
</tr>
<tr>
<td>客户端 IP</td>
<td>包含<br>不包含<br>等于<br>不等于</td>
<td>输入客户端 IP，多个关键字使用换行符进行分隔；IP 地址支持使用 * 作为条件进行筛选。如搜索客户端 IP: 9.223.23.2*，则匹配以9.223.23.2 开头的 IP 地址。</td>
</tr>
<tr>
<td>用户账号</td>
<td>包含<br>不包含<br>等于<br>不等于</td>
<td>输入用户账号，多个关键字使用换行符进行分隔。</td>
</tr>
<tr>
<td>数据库名</td>
<td>包含<br>不包含<br>等于<br>不等于</td>
<td>输入数据库名，多个关键字使用换行符进行分隔。</td>
</tr>
<tr>
<td>SQL 类型</td>
<td>等于<br>不等于</td>
<td>下拉选择 SQL 类型（ALTER、CHANGEUSER、CREATE、DELETE、DROP、EXECUTE、INSERT、LOGOUT、OTHER、REPLACE、SELECT、SET、UPDATE），支持多选。</td>
</tr>
<tr>
<td>错误码</td>
<td>等于<br>不等于</td>
<td>输入错误码，多个关键字使用换行符进行分隔。</td>
</tr>
<tr>
<td>执行时间（微秒）</td>
<td>区间格式</td>
<td>输入执行时间，格式为 M-N，如10-100或20-200。</td>
</tr>
<tr>
<td>锁等待时间（微秒）</td>
<td>区间格式</td>
<td>输入锁等待时间，格式为 M-N，如10-100或20-200。</td>
</tr>
<tr>
<td>IO 等待时间（微秒）</td>
<td>区间格式</td>
<td>输入 IO 等待时间，格式为 M-N，如10-100或20-200。</td>
</tr>
<tr>
<td>事务持续时间（微秒）</td>
<td>区间格式</td>
<td>输入事务持续时间，格式为 M-N，如10-100或20-200。</td>
</tr>
<tr>
<td>CPU 时间（微秒）</td>
<td>区间格式</td>
<td>输入 CPU 时间，格式为 M-N，如10-100或20-200。</td>
</tr>
<tr>
<td>线程 ID</td>
<td>等于<br>不等于</td>
<td>输入线程 ID，多个关键字使用换行符进行分隔。</td>
</tr>
<tr>
<td>扫描行数</td>
<td>区间格式</td>
<td>输入扫描行数，格式为 M-N，如10-100或20-200。</td>
</tr>
<tr>
<td>影响行数</td>
<td>区间格式</td>
<td>输入影响行数，格式为 M-N，如10-100或20-200。</td>
</tr>
<tr>
<td>返回行数</td>
<td>区间格式</td>
<td>输入返回行数，格式为 M-N，如10-100或20-200。</td>
</tr>
</tbody></table>

### 日志列表
- 在列表的 **SQL 类型** 中，使用 SQL 类型进行过滤时，支持选择多个 SQL 类型进行过滤。
- **返回行数**字段代表执行 SQL 返回的具体行数，主要用于对 SELECT 类型 SQL 影响的判断。

## 审计字段
云数据库 MySQL 的审计日志中支持如下字段。用户可以在**审计日志**页面单击右上角下载图标，下载完成后单击文件列表的图标，在跳转页面复制下载地址进行下载，即可获取完整的 SQL 审计日志。

>!
>- 目前日志文件下载仅提供腾讯云内网地址，请通过同一地域的腾讯云服务器进行下载（例如：北京区的数据库实例审计日志请通过北京区的 CVM 下载）。
>- 日志文件有效期为 24 小时，请及时下载。
>- 每一个数据库实例的日志文件不得超过 30 个，请下载后及时删除清理。
>- 若状态显示失败，可能是由于日志过多导致，请缩短时间窗口分批下载。

<table><thead>
<tr><th>序号</th>
<th>字段名</th>
<th>备注</th></tr></thead><tbody>
<tr>
<td rowspan="1" colSpan="1" >1</td>
<td rowspan="1" colSpan="1" >时间</td>
<td rowspan="1" colSpan="1" >-</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >2</td>
<td rowspan="1" colSpan="1" >客户端 IP</td>
<td rowspan="1" colSpan="1" >-</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >3</td>
<td rowspan="1" colSpan="1" >数据库名</td>
<td rowspan="1" colSpan="1" >-</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >4</td>
<td rowspan="1" colSpan="1" >用户账号</td>
<td rowspan="1" colSpan="1" >-</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >5</td>
<td rowspan="1" colSpan="1" >SQL 类型</td>
<td rowspan="1" colSpan="1" >-</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >6</td>
<td rowspan="1" colSpan="1" >SQL 命令详情</td>
<td rowspan="1" colSpan="1" >-</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >7</td>
<td rowspan="1" colSpan="1" >错误码</td>
<td rowspan="1" colSpan="1" >0表示成功</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >8</td>
<td rowspan="1" colSpan="1" >线程 ID</td>
<td rowspan="1" colSpan="1" >-</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >9</td>
<td rowspan="1" colSpan="1" >扫描行数</td>
<td rowspan="1" colSpan="1" >-</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >10</td>
<td rowspan="1" colSpan="1" >返回行数</td>
<td rowspan="1" colSpan="1" >-</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >11</td>
<td rowspan="1" colSpan="1" >影响行数</td>
<td rowspan="1" colSpan="1" >-</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >12</td>
<td rowspan="1" colSpan="1" >执行时间（微秒）</td>
<td rowspan="1" colSpan="1" >-</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >13</td>
<td rowspan="1" colSpan="1" >CPU 时间（微秒）</td>
<td rowspan="1" colSpan="1" >-</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >14</td>
<td rowspan="1" colSpan="1" >锁等待时间（微秒）</td>
<td rowspan="1" colSpan="1" >-</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >15</td>
<td rowspan="1" colSpan="1" >IO 等待时间（微秒）</td>
<td rowspan="1" colSpan="1" >-</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >16</td>
<td rowspan="1" colSpan="1" >事务持续时间（微秒）</td>
<td rowspan="1" colSpan="1" >-</td>
</tr>
</tbody></table>

## SQL 语句类型与 SQL 语句映射对象关系
<table><thead>
<tr>
<th rowspan="1" colSpan="1" >序号</th>
<th rowspan="1" colSpan="1" >SQL 语句类型</th>
<th rowspan="1" colSpan="1" >SQL 语句映射对象</th>
</tr></thead><tbody>
<tr>
<td rowspan="1" colSpan="1" >1</td>
<td rowspan="1" colSpan="1" >OTHER</td>
<td rowspan="1" colSpan="1" >除下述 SQL 语句类型外的所有 SQL 语句类型。</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >2</td>
<td rowspan="1" colSpan="1" >SELECT</td>
<td rowspan="1" colSpan="1" >SQLCOM_SELECT</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >3</td>
<td rowspan="1" colSpan="1" >INSERT</td>
<td rowspan="1" colSpan="1" >SQLCOM_INSERT，SQLCOM_INSERT_SELECT</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >4</td>
<td rowspan="1" colSpan="1" >UPDATE</td>
<td rowspan="1" colSpan="1" >SQLCOM_UPDATE，SQLCOM_UPDATE_MULTI</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >5</td>
<td rowspan="1" colSpan="1" >DELETE</td>
<td rowspan="1" colSpan="1" >SQLCOM_DELETE，SQLCOM_DELETE_MULTI，SQLCOM_TRUNCATE</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >6</td>
<td rowspan="1" colSpan="1" >CREATE</td>
<td rowspan="1" colSpan="1" >SQLCOM_CREATE_TABLE，SQLCOM_CREATE_INDEX，SQLCOM_CREATE_DB，SQLCOM_CREATE_FUNCTION，SQLCOM_CREATE_USER，SQLCOM_CREATE_PROCEDURE，SQLCOM_CREATE_SPFUNCTION，SQLCOM_CREATE_VIEW，SQLCOM_CREATE_TRIGGER，SQLCOM_CREATE_SERVER，SQLCOM_CREATE_EVENT，SQLCOM_CREATE_ROLE，SQLCOM_CREATE_RESOURCE_GROUP，SQLCOM_CREATE_SRS</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >7</td>
<td rowspan="1" colSpan="1" >DROP</td>
<td rowspan="1" colSpan="1" >SQLCOM_DROP_TABLE，SQLCOM_DROP_INDEX，SQLCOM_DROP_DB，SQLCOM_DROP_FUNCTION，SQLCOM_DROP_USER，SQLCOM_DROP_PROCEDURE，SQLCOM_DROP_VIEW，SQLCOM_DROP_TRIGGER，SQLCOM_DROP_SERVER，SQLCOM_DROP_EVENT，SQLCOM_DROP_ROLE，SQLCOM_DROP_RESOURCE_GROUP，SQLCOM_DROP_SRS</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >8</td>
<td rowspan="1" colSpan="1" >ALTER</td>
<td rowspan="1" colSpan="1" >SQLCOM_ALTER_TABLE，SQLCOM_ALTER_DB，SQLCOM_ALTER_PROCEDURE，SQLCOM_ALTER_FUNCTION，SQLCOM_ALTER_TABLESPACE，SQLCOM_ALTER_SERVER，SQLCOM_ALTER_EVENT，SQLCOM_ALTER_USER，SQLCOM_ALTER_INSTANCE，SQLCOM_ALTER_USER_DEFAULT_ROLE，SQLCOM_ALTER_RESOURCE_GROUP</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >9</td>
<td rowspan="1" colSpan="1" >REPLACE</td>
<td rowspan="1" colSpan="1" >SQLCOM_REPLACE，SQLCOM_REPLACE_SELECT</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >10</td>
<td rowspan="1" colSpan="1" >SET</td>
<td rowspan="1" colSpan="1" >SQLCOM_SET_OPTION，SQLCOM_RESET，SQLCOM_SET_PASSWORD，SQLCOM_SET_ROLE，SQLCOM_SET_RESOURCE_GROUP</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >11</td>
<td rowspan="1" colSpan="1" >EXECUTE</td>
<td rowspan="1" colSpan="1" >SQLCOM_EXECUTE</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >12</td>
<td rowspan="1" colSpan="1" >LOGIN</td>
<td rowspan="1" colSpan="1" >登入数据库行为，不受审计规则约束</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >13</td>
<td rowspan="1" colSpan="1" >LOGOUT</td>
<td rowspan="1" colSpan="1" >登出数据库行为，不受审计规则约束</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >14</td>
<td rowspan="1" colSpan="1" >CHANGEUSER</td>
<td rowspan="1" colSpan="1" >更改用户行为，不受审计规则约束</td>
</tr>
</tbody></table>


