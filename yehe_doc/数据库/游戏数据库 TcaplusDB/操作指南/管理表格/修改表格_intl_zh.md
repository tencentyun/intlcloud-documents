
## 操作场景 
本文为您介绍如何通过 TcaplusDB 控制台修改表格。如果您希望修改表的结构定义，在新的定义满足 TcaplusDB 改表规则的条件下，可以通过修改表格功能实现。

## 前提条件
已创建表格，请参见 [创建表格](https://intl.cloud.tencent.com/document/product/1016/32715)。

## 操作步骤
1. 进入 [表格列表](https://console.cloud.tencent.com/tcaplusdb/table) 页，选择所需表格，在**操作**列选择**更多** > **修改**，或勾选多个表格，单击上方**批量操作**的**表格修改**。
2. 在弹出的修改对话框中，上传或选择新的表定义文件，并单击**比较差异**。
>! 
>- 主键字段不能删除。
>- 主键字段名和字段类型不能改变。
>- 不能增加主键字段。
>- 普通字段有 required 标识的不能删除。
>- 同标识号的字段名称和字段类型不能改变。
>- 增加的普通字段名要符合命名规则 。
>
![](https://qcloudimg.tencent-cloud.cn/raw/e814beb8d7e1e21d537b4b54b7f33c35.png)
3. 在弹出的对话框，可查看比对结果，如果用户的新表定义不满足 TcaplusDB 的改表规则，将在此提示。
![](https://qcloudimg.tencent-cloud.cn/raw/cf146c39e9873ae25823ef1ffdcf0e2c.png)
4. 单击对比预览列的**预览**，可查看新旧表结构对比。
![](https://qcloudimg.tencent-cloud.cn/raw/4a8eb927da13cfd9715c139484c3a09e.png)
5. 确认无误后，单击**修改**，提交改表请求，修改成功将返回提示。
![](C:\Users\v_vwslwu\AppData\Roaming\Typora\typora-user-images\image-20220303203648828.png)
修改后，可在表格配置页面查看新表的结构。
