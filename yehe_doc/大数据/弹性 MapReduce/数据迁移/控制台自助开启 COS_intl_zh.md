## 适用场景
已创建但未开启 COS 的集群，因业务需要需开启 COS 时。

## 操作说明
### 步骤一：查看 COS 访问密钥
在 [密钥管理](https://console.cloud.tencent.com/cam/capi) 获取 SecretId 和 SecretKey。
![](https://main.qcloudimg.com/raw/7de96fc8624694cfdd8ef24b450d53c8.png)

### 步骤二：获取存储桶内文件下载路径
在 [对象存储控制台](https://console.cloud.tencent.com/cos5/bucket) 创建一个新存储桶或选择一个已有的存储桶，进入存储桶文件管理页。
>这里新建或已有存储桶访问权限，强烈建议选择私有读写，这样数据安全性高，详细信息请参见 [设置访问权限](https://intl.cloud.tencent.com/document/product/436/13315)。
>
EMR 控制台自助开启 COS 时需要提供一个测试验证地址，用于检测 SecretId 和 SecretKey 的正确性，因此应该保证填写的 SecretId 和 SecretKey 对应账号下存在至少一个可下载的真实文件。

例如，存储桶根目录下有一个`t1.txt`文件，可将该文件的对象地址填写到测试验证地址处。进入存储桶文件列表，单击某一文件的【详情】进入文件详情页，复制文件【对象地址】。
![](https://main.qcloudimg.com/raw/8a308284db105fa01c701ebfdd474454.png)![](https://main.qcloudimg.com/raw/83f7e2e435ddfd10246de4865fc3258c.png)

### 步骤三：在集群中设置 COS
>!COS 桶和集群必须要在同一个地域。

1. 进入 [EMR 控制台](https://console.cloud.tencent.com/emr)，在【集群列表】中选择具体的集群 ID/名称进入集群详情页。
![](https://main.qcloudimg.com/raw/c1555c479499b401cf8f55d346fd3297.png)
2. 在【实例信息】>【基础配置】中，单击【COS 访问】中【设置】。
![](https://main.qcloudimg.com/raw/110d1ee209f59db7079ecbbe8ef9cfa0.png)
3. 在弹出框中填写前两步获取的 SecretId、SecretKey 和测试验证地址，然后单击【确认】。
![](https://main.qcloudimg.com/raw/9fa2354b0c282d1f00893d75ebad2bd6.png)

### 步骤四：测试
在 master 节点命令行执行以下命令查看存储桶文件。
```
[root@172 ~]# su hadoop
[hadoop@172 root]$ hadoop fs -ls cosn://{bucket-name}/
Found 8 items
-rw-rw-rw-   1 hadoop hadoop       1366 2019-07-17 18:51 cosn://{bucket-name}/README.txt
drwxrwxrwx   - hadoop hadoop          0 1970-01-01 08:00 cosn://{bucket-name}/emr
drwxrwxrwx   - hadoop hadoop          0 1970-01-01 08:00 cosn://{bucket-name}/flume
drwxrwxrwx   - hadoop hadoop          0 1970-01-01 08:00 cosn://{bucket-name}/hive
-rw-rw-rw-   1 hadoop hadoop   95169691 2019-06-25 20:28 cosn://{bucket-name}/spark-test.jar
drwxrwxrwx   - hadoop hadoop          0 1970-01-01 08:00 cosn://{bucket-name}/test
drwxrwxrwx   - hadoop hadoop          0 1970-01-01 08:00 cosn://{bucket-name}/test2
drwxrwxrwx   - hadoop hadoop          0 1970-01-01 08:00 cosn://{bucket-name}/usr
```
