Prometheus 支持您在创建实例后修改数据存储时长。存储时长越长，实例单价越高，您可以参见 [按量计费说明](https://intl.cloud.tencent.com/document/product/1116/43156) 进行合理调整。


## 操作步骤
1. 登录 [ Prometheus 监控服务控制台](https://console.cloud.tencent.com/monitor/prometheus)。
2. 在实例列表中，找到需要被修改的 Prometheus 实例，单击右侧的 **更多** > **实例配置** > **修改存储时长**。
    <img src="https://qcloudimg.tencent-cloud.cn/raw/7ce8ea82777e221f9fba01ecd13ceecd.png" width="100%">
3. 在弹框中选择需要修改的存储时长，单击 **确定** 即可。
    <img src="https://qcloudimg.tencent-cloud.cn/raw/1a2f2354be794dd165256dba0676e223.png" width="80%">
>? 
>- 修改成功后，第二天0点开始，新采集的数据将按照新的存储时长存储和新的计费单价进行计费。
>- 历史数据的存储时长仍按照修改前的存储时长存储。

