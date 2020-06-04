本文介绍如何为云数据库 MySQL 实例创建库和表。

## 相关概念
- **实例**：数据库实例是在腾讯云中独立运行的数据库环境。一个数据库实例可以包含多个由用户创建的数据库，并且可以使用与独立数据库实例相同的工具和应用程序进行访问。
- **数据库**：按照数据结构来组织、存储和管理数据的仓库。

## 创建数据库
1. [登录 phpMyAdmin 控制台](https://intl.cloud.tencent.com/document/product/236/32341)，单击【新建】或者【数据库】，进入创建数据库页面。
![](https://main.qcloudimg.com/raw/e7fab349b3854db1fa15b111a7d99786.png)
2. 输入数据库名称，选择排序规则（默认为 utf8_general_ci），单击【创建】即可完成数据库的创建。
>
>- 数据库名称：长度为1个 - 64个字符，名称在实例内必须唯一。
>- 排序规则：可单击“新建数据库”旁的<img src="https://main.qcloudimg.com/raw/63e8499b6204a9e75179809e80d7867c.png"  style="margin:0;">，跳转至 [MySQL 官方文档](https://dev.mysql.com/doc/refman/5.7/en/create-database.html) 查看详细介绍。
>
![](https://main.qcloudimg.com/raw/b4a4fe5ab5f19ebef146f8a81813ad95.png)
3. 选择需要操作的数据库，单击上方导航栏中的【操作】，即可进入数据库操作页面，在此页面可以对数据库进行【新建数据表】、【删除数据库】等操作，创建完成后还可进行移动、改名、复制等操作。
![](https://main.qcloudimg.com/raw/b1316742957bcfa1846ea93ab19b045b.png)

## 创建数据表
1. [登录 phpMyAdmin 控制台](https://intl.cloud.tencent.com/document/product/236/32341)，选择需要建表的数据库，单击【新建】或者在【新建数据表】栏输入数据表名和选择字段数后单击【执行】。
>表名称：长度为1个 - 64个字符，名称在当前数据内必须唯一。
>
![](https://main.qcloudimg.com/raw/c267998c45afb6bd58218ca08117e7dc.png)
2. 进入数据表创建页面后，若需要添加字段，请在【添加】处输入所需添加的字段数，然后单击【执行】；【结构】栏为各字段信息的填写，【PARTITION definition】栏为分区信息（请参见 [MySQL 分区章节](https://dev.mysql.com/doc/refman/5.6/en/partitioning.html)），填写完信息后单击【保存】，即可完成数据表的创建。
>各字段详细介绍可单击字段旁的<img src="https://main.qcloudimg.com/raw/63e8499b6204a9e75179809e80d7867c.png"  style="margin:0;">查看。
>
![](https://main.qcloudimg.com/raw/a2599ceef079be861cf797c247da3e03.png)
