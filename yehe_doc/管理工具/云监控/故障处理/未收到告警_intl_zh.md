
本文档为您介绍未收到告警的排查方法和解决方案。

## 未收到告警原因

| 未收到告警原因                 | 解决方法                                                  |
| ------------------------------ | --------------------------------------------------------- |
| 告警策略未启用                 | 参考 [ 排查步骤一](#step1)  开启告警策略                  |
| **未配置或未验证告警通知渠道** | 参考 [排查步骤二](#step2)  排查并开启或验证告警渠道       |
| 接收组未配置用户               | 参考 [排查步骤三](#step3) 排查并配置用户                  |
| 未达到告警触发条件             | 参考 [排查步骤四 ](#step4) 排查并确认是否达到告警触发条件 |

## 排查步骤

<span id="step1"></span>

### 步骤一：查看告警策略是否启用

1. 进入 [云监控控制台—告警策略](https://console.cloud.tencent.com/monitor/policylist)。
2. 查看对应的告警策略是否开启。
	- 如下图策略1，告警启停按钮为灰色则说明未开启告警策略，单击灰色按钮 > 【确认】开启即可。
	- 如下图策略2，告警启停按钮为蓝色则说明告警策略已开启，请按照其它步骤继续排查。
![](https://main.qcloudimg.com/raw/dc74145f7bd40e64d22715f9b00bde9c.png)

<span id="step2"></span>

### 步骤二：查看告警渠道是否配置/验证

1. 登录 [访问管理控制台](https://console.cloud.tencent.com/cam)。
2. 在用户列表中单击对应的用户名称，进入用户详情页。
	- 告警渠道未配置：如下图所示则说明告警渠道未配置，请单击【![](https://main.qcloudimg.com/raw/e6ecaf9389ae90463b6acefca2f30cb7.png)】进行配置，配置完后参考下文【告警渠道未验证】进行验证。
![](https://main.qcloudimg.com/raw/093bf3503c1760e7263c7c18c9cb3ab4.png)
	- 告警渠道未验证：如下图所示则说明告警渠道未验证，请单击认证。
	![](https://main.qcloudimg.com/raw/75b6b6a123c3530bc8f306dc6160094b.png)
		 发送成功后请前往各渠道进行认证。
	- 短信认证：请前往您的手机短信点击相关链接进行认证。
	- 邮箱认证：请登录您的邮箱点击相关链接进行认证。



 <span id="step3"></span>
### 步骤三：查看告警接收组是否配置用户

1. 进入 [云监控控制台—告警策略](https://console.cloud.tencent.com/monitor/policylist)。
2. 找到对应的告警策略，单击策略名称，进入告警策略管理页。
3. 查看告警接收对象是否包含未收到告警的用户。若出现“未设置”或没有此用户，请参考  [创建告警接收组](https://intl.cloud.tencent.com/zh/document/product/248/38908) 添加用户到告警接收组。
![](https://main.qcloudimg.com/raw/00155e489f2b870c94341cec6ca67839.png)


<span id="step4"></span>

### 步骤四：查看是否达到告警触发条件

#### 查看指标告警是否到达触发条件

例如：设置指标为 CPU 利用率 、比较关系为 > 、阈值为80% 、统计周期为5分钟 、持续周期为2个周期。 表示：每5分钟收集一次 CPU 利用率数据，若某台云服务器的 CPU 利用率**连续三次**大于80%则触发告警。 以此类推，设置持续周期为 N，则需要指标监控数据 N+1 次达到阈值才会产生告警。

您可以登录 [云监控控制台](https://console.cloud.tencent.com/monitor)，选择对应的云产品，单击【![img](https://main.qcloudimg.com/raw/913709c7fa409d62518bf58e23c95446.png)】查看指标监控数据，通过时间筛选器确认指标监控数据是否达到触发告警条件，未达到则不发送告警通知。

如下图所示：查看云服务器 CPU 利用率。 
![img](https://main.qcloudimg.com/raw/e9d82c8be76f1c84bc8921a63f01813b.png)

#### 查看事件告警是否达到触发条件

1. 进入 [云监控控制台—产品事件](https://console.cloud.tencent.com/monitor/event/product) 。
2. 查看是否有事件告警记录，若无则说明未触达事件告警条件，不发送告警通知。
 ![img](https://main.qcloudimg.com/raw/271f446c313ae08f29bb9491edd8f7fc.png)

若通过以上步骤仍未解决问题，请 [提交工单](https://console.cloud.tencent.com/workorder/category) 联系工作人员为您处理。 
