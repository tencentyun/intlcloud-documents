## 操作场景

容器实例 EKSCI 提供日志采集能力，支持将集群内容器标准输出日志、容器日志文件日志发送至 [日志服务 CLS](https://www.tencentcloud.com/products/cls)，适用于需要对 EKSCI 内服务日志进行存储和分析的用户。

## 前提条件
 准备一个 CLS 的日志主题作为日志上报终端，日志上报后在该日志主题下查看并检索日志。若无合适的日志主题，请参见 [创建日志主题](https://intl.cloud.tencent.com/document/product/614/31592)。

## 操作步骤

### 创建容器实例时开启日志采集

>?日志采集需要在创建容器实例时开启。

1. 登录 [容器实例控制台](https://console.cloud.tencent.com/tke2/eksci)，单击新建实例。
2. 根据实际需求，设置容器实例的参数，操作详情请参见 [创建容器实例](https://intl.cloud.tencent.com/document/product/457/47857)。完成后，单击下一步。
3. 在“其他配置”页中开启日志采集。
首次开启日志采集功能，需要进行授权，会默认为您的账号绑定角色 TKE_QCSLinkedRoleInEKSLog，该角色配置的预设策略为 QcloudAccessForTKELinkedRoleInEKSLog，该角色会具备日志上传等权限。开启后，选择以下参数：

	- 选择日志集及日志主题。
	- 选择容器，配置采集路径，支持“stdout”（表示标准输出）和绝对路径，支持 `*` 通配，多个采集路径以 `,` 分割。
<dx-alert infotype="notice" title="">
如果开启日志采集的同时需要使用角色授权的能力，为实例绑定的角色必须具备 “cls:pushLog” 写权限，详细请参考 [角色授权](https://intl.cloud.tencent.com/document/product/457/47857)。容器实例只能绑定一个角色。
</dx-alert>

		


### 查看采集的日志

1. 登录 [日志服务控制台](https://console.cloud.tencent.com/cls)，选择左侧**检索分析**。
2. 进入“检索分析”页面，选择地域、需要查看日志的日志集和日志主题。
3. 单击**索引配置**，在基础配置弹窗中为集群开启全文索引。
4. 输入检索分析语句，选择时间范围，单击检索分析可检索分析日志。如下图所示：
![](https://staticintl.cloudcachetci.com/yehe/backend-news/3YR7537_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221226163615.png)

## 常见问题

### 未查看到日志该如何处理？

若已确定有日志上报，但是未查看到日志，请检查以下问题：
1. 检查 [访问管理控制台](https://console.cloud.tencent.com/cam/role) 中是否有 TKE_QCSLinkedRoleInEKSLog 角色。
2. 检查日志主题是否开启了全文索引。
3. 若已开启角色授权，检查绑定的角色是否有上报日志的权限，具体配置请看角色授权。
4. 检查绑定的角色所选的载体是否是 CVM。

如果您的问题仍未解决，请通过 [提交工单](https://console.intl.cloud.tencent.com/workorder/category) 联系我们。
