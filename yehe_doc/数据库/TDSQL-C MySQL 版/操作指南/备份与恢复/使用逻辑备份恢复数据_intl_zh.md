本文为您介绍通过逻辑备份文件进行数据恢复。

## 操作场景
>?为节约存储空间，TDSQL-C MySQL 版的备份文件，都会先经过 qpress 压缩，后经过 xbstream 打包（xbstream 为 Percona 的一种打包/解包工具）。

TDSQL-C MySQL 版支持逻辑备份方式，用户可通过控制台手动备份来生成逻辑备份文件，并下载获取整集群/部分库表的逻辑备份文件，本文为您介绍通过 Linux 平台，使用逻辑备份文件进行数据恢复。

## 操作步骤
### 步骤1：下载备份文件
1. 登录 [TDSQL-C MySQL 版控制台](https://console.cloud.tencent.com/cynosdb)，在集群列表，单击集群 ID 或**操作**列的**管理**，进入集群管理页面。
2. 在集群管理页面，选择**备份管理** > **数据备份列表**， 找到需要下载的备份，在**操作**列单击**下载**。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/9i8N093_33.png)
3. 在弹出的对话框，复制下载地址，并 [登录到 CVM（Linux 系统）](https://www.tencentcloud.com/document/product/213/10517#.E6.AD.A5.E9.AA.A43.EF.BC.9A.E7.99.BB.E5.BD.95.E4.BA.91.E6.9C.8D.E5.8A.A1.E5.99.A8)中，运用 wget 命令进行高速下载。
>?
>- 复制下载地址后 [登录到 CVM（Linux 系统）](https://www.tencentcloud.com/document/product/213/10517#.E6.AD.A5.E9.AA.A43.EF.BC.9A.E7.99.BB.E5.BD.95.E4.BA.91.E6.9C.8D.E5.8A.A1.E5.99.A8)中运用 wget 命令下载。
>  - 如果集群和 CVM 属于同地域，那么无论是跨 VPC 还是同 VPC，都支持运用 wget 命令进行内网高速下载。
>  - 如果集群与 CVM 属于跨地域，将不支持内网高速下载，CVM 必须开启公网 IP 才支持运用 wget 命令进行下载。
>- 您也可以选择**本地下载**直接下载，但耗时较多。
>
wget 命令格式如下：
```
wget -c "<备份文件下载地址>" -O <自定义名称>.xb
```

### 步骤2：解包备份文件
使用 xbstream 解包备份文件。
>? xbstream 工具下载地址请参见 [Percona XtraBackup 官网](https://www.percona.com/downloads/Percona-XtraBackup-2.4/LATEST/)，请选择 Percona XtraBackup 2.4.6 及以上的版本，安装介绍请参见 [Percona XtraBackup 2.4](https://docs.percona.com/percona-xtrabackup/2.4/installation/yum_repo.html)。
>
```
xbstream -x < test0.xb  -P
```
>?`test0.xb` 替换为您的备份文件名。
>
解包结果如下图所示：
![](https://staticintl.cloudcachetci.com/yehe/backend-news/VkG7203_34.png)

### 步骤3：解压备份文件
1. 通过如下命令下载 qpress 工具。
```
wget -d --user-agent="Mozilla/5.0 (Windows NT x.y; rv:10.0) Gecko/20100101 Firefox/10.0" https://docs-tencentdb-1256569818.cos.ap-guangzhou.myqcloud.com/qpress-11-linux-x64.tar
```
>?若 wget 下载提示错误，您可单击 [下载 qpress 工具](https://docs-tencentdb-1256569818.cos.ap-guangzhou.myqcloud.com/qpress-11-linux-x64.tar) 下载到本地后，再将 qpress 工具上传至 Linux 云服务器，请参见 [通过 SCP 上传文件到 Linux 云服务器](https://intl.cloud.tencent.com/document/product/213/2133)。
>
2. 通过如下命令解出 qpress 二进制文件。
```
tar -xf qpress-11-linux-x64.tar -C /usr/local/bin
source /etc/profile
```
3. 使用 qpress 解压备份文件。
```
qpress -d <备份文件>.sql.qp .
```

### 步骤4：导入备份至目标数据库
执行如下命令导入 sql 文件至目标数据库：
```
mysql -u<账户名> -P<端口> -h<目标数据库内网地址> -p < <通过 qpress 实际解压出的 sql 文件>
```
