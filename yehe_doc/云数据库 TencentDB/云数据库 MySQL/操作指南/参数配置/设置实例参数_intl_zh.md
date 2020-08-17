您可以通过 [MySQL 控制台](https://console.cloud.tencent.com/cdb) 或者 [API](https://intl.cloud.tencent.com/document/product/236/15860) 查看和修改部分参数，并可以在控制台查询参数修改记录。

## 修改参数值
>!
>- 如果修改的参数需要重启实例才生效，系统会提示您是否重启，建议您在业务低峰期操作，并确保应用程序具有重连机制。
>- 参数的修改未提交前，可单击参数旁边的<img src="https://main.qcloudimg.com/raw/81fc2494e8b61ff36a63d23cccb61cd1.png"  style="margin:0;">或修改页面的【取消】取消修改。

### 批量修改参数
1. 登录 [MySQL 控制台](https://console.cloud.tencent.com/cdb)，在实例列表，单击实例名或操作列的【管理】，进入实例管理页面。
2. 选择【数据库管理】>【参数设置】页，单击【批量修改参数】。
![](https://main.qcloudimg.com/raw/3ec389dafa09276ae66b00a71445d9d3.png)
3. 在“参数运行值”列，选择需要修改的参数进行修改，确认无误后，单击【确认修改】。
![](https://main.qcloudimg.com/raw/5307fbeef4b1fccef478ab7fd57b3167.png)
4. 在弹出的对话框，勾选同意，单击【确定】。

### 修改单个参数
1. 登录 [MySQL 控制台](https://console.cloud.tencent.com/cdb)，在实例列表，单击实例名或操作列的【管理】，进入实例管理页面。
2. 选择【数据库管理】>【参数设置】页，选择目标参数所在行，在“参数运行值”列，单击<img src="https://main.qcloudimg.com/raw/788902e3f8c335cf17de420f7181c2a8.png"  style="margin:0;">修改参数值。
![](https://main.qcloudimg.com/raw/4687ed705274b76ec92c43b7f9d448ab.png)
3. 根据“参数可修改值”列的提示，输入目标参数值，单击<img src="https://main.qcloudimg.com/raw/1f4c7f2e0744bc601efb5d9fb04a7a04.png"  style="margin:0;">保存，单击<img src="https://main.qcloudimg.com/raw/2106cb4b9337a1a2fff5908581d2a908.png"  style="margin:0;">可取消操作。
![](https://main.qcloudimg.com/raw/41c7d73d4c5d404a112f54c3a63da726.png)
4. 在弹出的对话框，单击【确定】。

### 自定义时间修改参数
1. 登录 [MySQL 控制台](https://console.cloud.tencent.com/cdb)，在实例列表，单击实例名或操作列的【管理】，进入实例管理页面。
2. 选择【数据库管理】>【参数设置】页，单击【批量修改参数】或在“参数运行值”列单击<img src="https://main.qcloudimg.com/raw/788902e3f8c335cf17de420f7181c2a8.png"  style="margin:0;">修改单个参数值。  
3. 选择需要修改的参数进行修改，确认无误后，单击【确认修改】或单击<img src="https://main.qcloudimg.com/raw/1f4c7f2e0744bc601efb5d9fb04a7a04.png"  style="margin:0;">保存 。
4. 在弹出的对话框中，选择参数“执行方式”，单击【确定】。
>?若选择【维护时间内】，所选实例的参数变更任务会在实例的 [维护时间](https://intl.cloud.tencent.com/document/product/236/10929) 内执行并生效。
>


### 取消参数修改任务
批量修改参数或修改单个参数任务提交后，如需取消修改参数，可在任务执行前（即任务状态为“等待执行”），在左侧导航【[任务列表](https://console.cloud.tencent.com/mysql/task)】页，单击“操作”列的【撤销】，取消参数修改任务。

### 从参数模板导入
1. 登录 [MySQL 控制台](https://console.cloud.tencent.com/cdb)，在实例列表，单击实例名或操作列的【管理】，进入实例管理页面。
2. 选择【数据库管理】>【参数设置】页，单击【从模板导入】。
![](https://main.qcloudimg.com/raw/bd7a2fd3dc89895f1a3bd779d0fe8bbc.png)
3. 在弹出的对话框，选择参数模板，单击【导入并覆盖原有参数】。
![](https://main.qcloudimg.com/raw/2f649840f16befabea6259f9b4c7f47c.png)

### 导入参数
1. 登录 [MySQL 控制台](https://console.cloud.tencent.com/cdb)，在实例列表，单击实例名或操作列的【管理】，进入实例管理页面。
2. 选择【数据库管理】>【参数设置】页，单击【导入参数】。
![](https://main.qcloudimg.com/raw/52d6f069bbce29c933254593d59c0236.png)
3. 在弹出的对话框，选择文件上传后，单击【导入并覆盖原有参数】。
![](https://main.qcloudimg.com/raw/42fb6ef8936131a3bc776e492478e745.png)
	
## 查看参数修改记录
1. 登录 [MySQL 控制台](https://console.cloud.tencent.com/cdb)，在实例列表，单击实例名或操作列的【管理】，进入实例管理页面。
2. 选择【数据库管理】>【参数设置】页，单击右侧的【最近修改记录】。
![](https://main.qcloudimg.com/raw/6d6318fce61fc78c6ff3611479ae5714.png)
3. 在最近参数修改记录页，可查看近期参数修改记录。
![](https://main.qcloudimg.com/raw/4c616b40d058f114e8f75c4021c02648.png)

## 后续操作
- 相关重要参数的配置建议，请参见 [参数配置建议](https://intl.cloud.tencent.com/document/product/236/38056)。
