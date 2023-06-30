## 操作场景
本文介绍通过**登录实例**或**轻量应用服务器控制台**两种查看自动化助手命令执行状态的方法，您可按需选择方式查看命令的执行状态信息。命令的所有执行状态信息，请参见 [命令执行状态](https://intl.cloud.tencent.com/document/product/1147/46034)。

## 操作步骤
### 方法1：登录实例查看
1. 登录实例。
2. 执行以下命令，获取 agent 运行日志。
```
cd /usr/local/qcloud/tat_agent/log/
```
对比 [命令执行状态](https://intl.cloud.tencent.com/document/product/1147/46034)，获取当前的命令执行状态信息。

### 方法2：通过控制台查看
1. 登录 [轻量应用服务器控制台](https://console.cloud.tencent.com/lighthouse/instance/index)。
2. 在服务器列表中，找到并进入目标实例的详情页。
3. 选择【执行命令】页签，并单击命令所在行右侧的【查看执行详情】。如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/38cf0f7f70473987e19d8897422c2366.png)
4. 即可在弹出的“命令执行详情”窗口中，对比 [命令执行状态](https://intl.cloud.tencent.com/document/product/1147/46034)，获取当前的命令执行状态信息。
