## 操作场景 
本文为您介绍如何通过 TcaplusDB 控制台修改表格。如果您希望修改表的结构定义，在新的定义满足 TcaplusDB 改表规则的条件下，可以通过修改表格功能实现。

## 前提条件
已创建表格，请参见 [创建表格](https://intl.cloud.tencent.com/document/product/1016/32715)。

## 操作步骤
1. 进入 [表格列表](https://console.cloud.tencent.com/tcaplusdb/table) 页，选择所需表格，在“操作”列选择【更多】>【修改】，或勾选多个表格，单击上方的【批量修改】。
2. 在弹出的修改对话框中，上传或选择新的表定义文件，并单击【比较差异】。
> 
>- 主键字段不能删除。
>- 主键字段名和字段类型不能改变。
>- 不能增加主键字段。
>- 普通字段有 required 标识的不能删除。
>- 同标识号的字段名称和字段类型不能改变。
>- 增加的普通字段名要符合命名规则 。
>
![](https://main.qcloudimg.com/raw/407bf6c819bf9b60d4ebd18928904a6b.png)
3. 在弹出的对话框，可查看比对结果，如果用户的新表定义不满足 TcaplusDB 的改表规则，将在此提示。
![](https://main.qcloudimg.com/raw/087642d98430e6e1d066ae5dfc202f1a.png)
4. 单击对比预览列的【预览】，可查看新旧表结构对比。
![](https://main.qcloudimg.com/raw/997d4e6cd91e2815a8534f44e2ee10de.png)
5. 确认无误后，单击【确定】，提交改表请求，修改成功将返回提示。
![](https://main.qcloudimg.com/raw/53fc68f54fcbaf6726874e9af3c26463.png)
   修改后，可在表格配置页面查看新表的结构。
   
