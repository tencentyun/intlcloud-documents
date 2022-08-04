容器服务 TKE 计划于2022年7月27至29日、8月1日至4日的10:00 -- 23:00 对监控组件进行版本升级，本次升级修复了 tke-monitor-agent 组件上的部分已知问题。本次变更对业务无影响，若您不希望执行此次变更，可通过[提交工单](https://console.intl.cloud.tencent.com/workorder/category)联系我们。

变更内容：

1）修复：pod的CPU 利用率（占request） 、pod的CPU利用率（占limit） 为负数的情况；

2）修复数据源配置：gpu指标数据源配置错误，影响gpu场景下gpu指标的拉取

3）修复节点cpu利用率、节点内存利用率 指标上报问题
