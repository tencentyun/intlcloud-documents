腾讯云 EMR 提供 Spark 3.x、2.x 多版本支持 ，软件环境信息如下：
- Spark 默认安装在 master 节点。
- 登录机器后使用命令 `su hadoop` 切换到 Hadoop 用户。
- Spark 软件路径在 `/usr/local/service/spark` 下。
- 相关日志路径在 `/data/emr` 下。

更多详细资料请参考 [社区文档](http://spark.apache.org/docs/2.0.2/)，这里主要介绍基于 Spark 访问腾讯云对象存储相关操作。
