

单击**设置-服务设置**菜单，可开启配置审计服务并设置需监控的资源范围。

### 开启配置审计

您可以在**监控管理**页面**开启**或**关闭**配置审计。首次开通配置审计服务，需授权创建配置审计服务相关角色（Config_QCSLinkedRoleInConfigRecorder)，并选择需监控的资源类型，当前配置审计支持的资源类型请参阅[支持的资源类型](https://www.tencentcloud.com/document/product/1164/51495)。
![](https://qcloudimg.tencent-cloud.cn/raw/10e01aa95fc41cfd197cdb4e0826f167.png)

### 关闭配置审计

如您不再需要使用配置审计，可点击**关闭**停止使用。关闭后，配置审计将不再监控并更新资源配置变更，配置审计中已存储的资源配置数据、已创建的规则和已得到的合规结果将被清空且不可恢复。历史已投递至COS存储桶的数据不受影响。
![](https://qcloudimg.tencent-cloud.cn/raw/9241ff9d66f29a8eccfb323afe744785.png)
![](https://qcloudimg.tencent-cloud.cn/raw/0f336c6bbcaa7e89fd86cd678aeac182.png)

### 修改监控范围

如您已开启配置审计，可点击**修改**，变更监控的资源类型。修改监控范围会导致资源列表新增资源及相应时间线的更新，以及您账号下已有规则，合规包的重新审计，预计将有10-15分钟的时间窗口，请耐心等待。
![](https://qcloudimg.tencent-cloud.cn/raw/426809d3709636e224c065aa3862438a.png)
![](https://qcloudimg.tencent-cloud.cn/raw/32633468f031071a2d40ee3dded2e00e.png)

