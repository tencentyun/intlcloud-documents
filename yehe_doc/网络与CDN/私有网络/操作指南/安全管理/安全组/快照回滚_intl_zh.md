如安全组配置了快照策略，则安全组规则将按照设定的快照策略进行规则的备份。当需要将安全组规则恢复到备份的某个规则状态时，可执行快照回滚操作。

## 前提条件
安全组配置[ 快照策略](https://www.tencentcloud.com/document/product/215/46787)，且至少完成了一次快照备份。

## 操作步骤
1. 登录 [安全组控制台](https://console.cloud.tencent.com/vpc/securitygroup?rid=1&rid=1)，进入安全组管理页面。
2. 在安全组管理页面，单击需要回滚规则的安全组 ID，进入安全组详情界面。
3. 单击**快照回滚**页签，界面将按时间展示所有快照记录，默认展示7天内容，可自定义设置查询快照记录的时间区间。
>?如果备份记录较多，建议一次性查询不要超过三个月，否则可能导致系统响应较慢。
>
![](https://staticintl.cloudcachetci.com/yehe/backend-news/Jkdx790_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230330101859.png)
4. 单击**导出**可导出该次快照记录的安全组出入站规则信息，分别保存在**出站规则**和**入站规则**文件中。
5. 单击**恢复**，进入恢复安全组界面，同时展示安全组规则预览及规则比对内容。
>?
>+ 图中 + 号标识的是快照备份记录中相比当前安全组规则新增的规则条目，-为删除的条目。注意，当前比对界面，是以此刻选择比对预览的时刻为准，如在此期间进行规则变更，比对校验可能不准确。
>+ 恢复安全组时，若其来源中包含参数模板规则及嵌套安全组，参数模板内规则以及安全组关联实例以当前状态为准。
>+ 安全组恢复操作等同导入，恢复后将以覆盖方式取代当前所有规则，请谨慎操作。
>
6. 确认无误后单击**确定**完成安全组规则的回滚。
