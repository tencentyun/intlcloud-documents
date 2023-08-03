## 使用场景
腾讯云数据连接器提供丰富的状态管理方案。登录 [腾讯云数据连接器控制台](https://ipaas.tencentcloud.com/login)，单击左侧工具栏**集成工具 > 通用存储**，进入“通用存储”功能，即可管理项目中使用到的存储结构和数据。


## 通用存储管理
“通用存储”主页面为存储管理页面。该页面下可以新建存储，同时查看当前已创建的所有存储列表，包括存储名、存储类型以及针对不同类型的存储可以执行的操作。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/mc2T784_175.png)

## 新增存储
新增存储功能可以帮助您快速创建一个全新的存储类型。只需进行简单的配置即可完成创建工作、需要创建的存储名称以及对应的存储类型。
- 存储名称：请输入25位以内的英文字母或_。
- 存储类型：表结构、哈希结构、列表和字符串四种类型。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/eyYM492_176.png)


### 表结构
#### 编辑结构
用户可以使用该功能进行表结构的维护，包括列信息、索引信息、关系配置。
- **列信息**：表结构的列信息配置支持新增、修改和删除数据表中的列配置，可以快速完成结构编排。当前支持用户编辑列名称、列中数据的类型（支持 String、bool、int、float、decimal、datetime、date 和 time）、值长度（当类型为 string 时）、精度值和小数位（当类型为 decimal 时）、是否为主键以及是否支持自动编号（仅当该列为主键时）。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/s8ZI640_177.png)

- **索引配置**：索引配置用法同 MySQL 的 index 配置，用户可以通过此标签页建立索引，提高 MySQL 的检索速度。当前支持新建、删除索引、配置索引名称、配置索引类型（当前支持 index和 unique 两种类型，具体区别请参考 [DOCUMENTATION](https://dev.mysql.com/doc/refman/8.0/en/create-index.html)）、配置索引所在列（在已维护的列信息列表中选择）。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/y7vA546_178.png)

- **关系配置**：腾讯云数据连接器通用存储同时还支持用户配置外键信息。通过给外键命名、配置外键所在列、选择外键所对应的来源表和来源列信息即可完成配置。如果需要进行外键事件触发配置，则可以通过配置 on delete 和 on update 选项，请参考 [DOCUMENTATION](https://dev.mysql.com/doc/refman/8.0/en/create-index.html)。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/9IWb691_179.png)

#### 更多操作
- **清空表结构**：“清空”操作允许用户清除当前表结构中的所有数据内容。
>!清空动作是高危操作，该操作将会清空本存储内的所有数据，且无法恢复，请谨慎使用。
>
![](https://staticintl.cloudcachetci.com/yehe/backend-news/UhMK740_180.png)
- **复制同结构表**：通过“复制同结构表”功能可以基于现有的数据表结构快速创建一个新的数据表，方便用户进行数据结构的迁移和备份。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/AevH596_181.png)
- **删除**：“删除”操作可以删除本条存储记录。**同样的，此操作被视为高危操作，会对线上数据造成影响，请确认后再进行。**



### 哈希结构
哈希（hash）是根据关键码值（Key value）而直接进行访问的数据结构。它通过把关键码值映射到表中一个位置来访问记录，以加快查找的速度。腾讯云数据连接器允许用户创建，哈希表结构：内容为 key-value 格式的数据。

### 列表
也可称为数组，是有序的元素序列，格式为一组拥有 ID 的数据信息。数组是用于储存多个相同类型数据的集合。

### 字符串
字符串（String）是由数字、字母、下划线组成的一串字符。腾讯云数据连接器通过通用存储功能，可以创建和使用字符串，帮助用户完成快速的复用，简化操作。
