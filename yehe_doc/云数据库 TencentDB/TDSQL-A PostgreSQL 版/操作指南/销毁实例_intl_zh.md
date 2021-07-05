
本文为您介绍如何通过控制台销毁 TDSQL-A PostgreSQL版 实例。

## 操作场景
根据业务需求，您可以在控制台自助销毁实例。自助销毁后，实例的状态一旦变为“已隔离”，隔离7天后彻底销毁，隔离中实例无法恢复。

>!
>- 实例销毁后数据将无法找回，备份文件会同步销毁，无法在云上进行数据恢复。
>- 实例销毁后 IP 资源同时释放。

## 操作步骤
1. 登录 [TDSQL-A  PostgreSQL版 控制台](https://console.cloud.tencent.com/tdsqla/tdapg)，在实例列表选择所需实例，在“操作”列选择【更多】>【销毁】。
![](https://main.qcloudimg.com/raw/3ee36e69b705740ef35a509c74c5dc0b.png)
2. 在弹出的对话框，阅读并勾选“已阅读并同意销毁规则”后，单击【确定】。
![](https://main.qcloudimg.com/raw/a2151f6eacfcaab380f0a00c8ff4eaae.png) 
3. 确定销毁实例后，实例状态变更为“已隔离”。
![](https://main.qcloudimg.com/raw/b32ca16b8211b2b39c645e1cab386fbb.png)
4. 在实例列表选择所需实例，在“操作”列选择【更多】>【立即下线】。
>!执行下线操作后，实例会彻底销毁，数据将无法找回，请提前备份实例数据。
>
![](https://main.qcloudimg.com/raw/c5be91618049e1d48683df416d4dfb11.png)
5. 在弹出的对话框，确认无误后，单击【确定】。
6. 实例下线成功后，实例列表右上角会弹出下线成功提示框。
![](https://main.qcloudimg.com/raw/b7869d46781925c69b0ab86b98c5935a.png)

 
