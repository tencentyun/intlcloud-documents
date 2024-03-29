## 注意事项
- 为避免误删除操作，凭据管理系统使用计划删除机制，即**对删除操作强制执行0 - 30天等待期**，并确认删除后等待0 - 30天再进行删除。
- 凭据删除后将**无法恢复**，此凭据下的所有凭据内容也将**无法调用**。

## 操作步骤
1. 登录 [凭据管理系统控制台](https://console.cloud.tencent.com/ssm/index)，在左侧导航栏中，单击【凭据列表】，在凭据列表左上方可以切换不同地区，根据需求可以查看其他地区的凭据列表。
2. 在凭据列表中，选择需要计划删除的凭据，若凭据是启用状态，请先对凭据进行禁用操作，然后在计划删除操作栏中，单击【计划删除】。
![](https://main.qcloudimg.com/raw/7e9f544403c810ae419d461789b6a96d.png)
3. 输入计划删除天数，单击【确定】，凭据将按计划删除。
![](https://main.qcloudimg.com/raw/e651915d58d03adde3b2f1789d91497f.png)
>!若选择等待期为“0”天，凭据将立即删除。

5. 在1 - 30天等待期内，您可以对计划删除的凭据进行取消删除操作。若需取消删除凭据，可以在右侧计划删除操作栏，单击【取消删除】，即可取消删除凭据。确认取消删除后，凭据密钥重置为“启用”状态，可对该凭据进行禁用、修改、删除等操作。
![](https://main.qcloudimg.com/raw/dbdf66930566eadc7f44fe9785ec519a.png)
