
### MariaDB 的备份功能支持实时备份吗？
目前暂不支持实时备份。

### MariaDB 如何解压备份并恢复到一个自建实例？
详细操作请参见 [通过备份文件恢复实例](https://intl.cloud.tencent.com/document/product/237/4190)。

### MariaDB 的备份方式有哪些？
支持全量备份和增量备份方式，详细介绍请参见 [备份方式](https://intl.cloud.tencent.com/document/product/237/8487)。

### 如何解压 MariaDB 的备份和日志文件？
MariaDB 的备份文件和日志文件（binlog 文件）采用 LZ4（Extremely Fast Compression algorithm）工具进行压缩，您可以选用 LZ4 工具进行解压。
解压操作请参见 [解压备份和日志文件](https://intl.cloud.tencent.com/document/product/237/2088)。

