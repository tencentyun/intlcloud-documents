## 功能介绍
对于已经使用云监控事件中心产品的存量用户，为了保证使用体验的平滑，事件总线产品已于4月底为您完成云监控侧存量**告警策略**与**推送目标**的自动迁移。

## 使用说明
1. 本次迁移只涉及**事件告警**相关策略，对于指标告警，您可以继续在云监控控制台进行配置与管理。
![](https://qcloudimg.tencent-cloud.cn/raw/c847311f108601a2f0c406c4b58a706f.png)
2. 策略将以产品维度进行迁移，对于单条告警规则，转换逻辑如下图所示，完成迁移后，用户账号下该产品所有资源都将默认配置告警；迁移前迁移后的告警规则数量将保持一致，如果希望对指定资源进行告警，您可以手动调整告警规则，参考 [告警策略配置](https://intl.cloud.tencent.com/document/product/1108/45206)。
![](https://qcloudimg.tencent-cloud.cn/raw/157790efa462957756733e39600e0b29.png)
3. 迁移将同时完成**告警策略**、**推送目标**、**平台事件**迁移，为您给**广州**地域的**云服务事件集**创建对应的事件规则和目标。
