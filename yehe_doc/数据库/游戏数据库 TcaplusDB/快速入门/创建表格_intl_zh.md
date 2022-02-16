## 操作场景
本文为您介绍如何通过 TcaplusDB 控制台创建数据表格。

## 前提条件
- 已创建 TcaplusDB [集群](https://intl.cloud.tencent.com/document/product/1016/32714) 和 [表格组](https://intl.cloud.tencent.com/document/product/1016/32716)。
- 已根据 [表描述文件示例](https://intl.cloud.tencent.com/document/product/1016/36560) 准备好表格文件。

## 操作步骤
1. 登录 [TcaplusDB 控制台](https://console.cloud.tencent.com/tcaplusdb/table)，在左侧导航选择**表格列表**页，单击**新建表格**。
2. 在新建表格页面，配置表格信息。
 - **集群、表格组**：选择目标集群和表格组。
 - **表格文件**：从本地上传或从已经上传过的历史文件中选择表定义文件，用户可以同时选择新上传和已上传的历史文件来创建表格，不能上传或选择同名文件。可参考 ProtoBuf 协议的示例表格文件 [game_players.proto](
https://tcaplusdb-sdk-1301716906.cos.ap-shanghai.myqcloud.com/3.36.0.192960/game_players.proto)。
 - **备注**：输入表格备注信息。
   ![](https://main.qcloudimg.com/raw/5621a15042a9d73b4364fe19b9a9268b.png)
3. 单击**下一步**，系统将校验用户选定的表格定义文件，
 - 校验不通过，将返回错误，请根据错误提示修改文件后重新上传。
 - 校验通过，将显示文件中定义的表格元信息，请继续执行下一步。
4. 在配置表格页，勾选要创建的表格，输入容量、预留读和预留写参数，系统将自动计算表格每日的花费价格。
![](https://main.qcloudimg.com/raw/32aa5c8a292df17249a62e88b6fca4e6.png)
5. 确认表格信息无误后，单击**创建**，系统返回创建成功提示。
![](https://main.qcloudimg.com/raw/7a39640da609a65df7040fc9c1d7be3d.png)
