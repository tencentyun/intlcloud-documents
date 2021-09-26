
您可以通过 SQL Server 控制台查看和修改部分参数，并可以在控制台查询参数修改历史。

## 注意事项
- 为保证实例的稳定，控制台仅开放部分参数的修改，控制台的参数配置页面展示的参数即为用户可以修改的参数。
- 如果修改的参数需要重启实例才生效，系统会提示您是否重启，建议您在业务低峰期操作，并确保应用程序具有重连机制。

## 批量修改参数
1. 登录 [SQL Server 控制台](https://console.cloud.tencent.com/sqlserver)，在实例列表，单击实例 ID 或“操作”列的【管理】，进入实例管理页面。
2. 在实例管理页面，选择【参数配置】>【参数设置】页，单击【批量修改参数】。
![](https://main.qcloudimg.com/raw/eb99fc02ef937bcf284cde55c65defc7.png)
3. 在“当前运行参数值”列，选择需要修改的参数进行修改，确认无误后，单击【确定】。
![](https://main.qcloudimg.com/raw/56e48d579e473235848479d9c0bfd809.png)
4. 在弹出的对话框，选择参数任务的“执行方式”，单击【确定】。
>?
>- 若选择【立即执行】，所选实例的参数变更任务会立即执行并生效。
>- 若选择【维护时间内】，所选实例的参数变更任务会在实例的 [维护时间](https://intl.cloud.tencent.com/document/product/238/35785) 内执行并生效。
> 
![](https://main.qcloudimg.com/raw/09cd7df6181f175a265a3c0c29a71b25.png)

## 修改单个参数
1. 登录 [SQL Server 控制台](https://console.cloud.tencent.com/sqlserver) ，在实例列表，单击实例 ID，进入实例管理页面。
2. 在实例管理页面，选择【参数配置】>【参数设置】页，选择目标参数所在行，在“当前运行参数值”列，单击![img](https://main.qcloudimg.com/raw/788902e3f8c335cf17de420f7181c2a8.png)修改参数值。
![](https://main.qcloudimg.com/raw/840cd20adf065b0fa30adefed997a640.png)
3. 根据“参数值”列的提示，输入目标参数值，单击![img](https://main.qcloudimg.com/raw/1f4c7f2e0744bc601efb5d9fb04a7a04.png)保存，单击![img](https://main.qcloudimg.com/raw/2106cb4b9337a1a2fff5908581d2a908.png)可取消操作。
![](https://main.qcloudimg.com/raw/896f3db37107b9e3c69d7b3cd1164f55.png)
4. 在弹出的对话框，选择参数任务的“执行方式”，单击【确定】。
>?
>- 若选择【立即执行】，所选实例的参数变更任务会立即执行并生效。
>- 若选择【维护时间内】，所选实例的参数变更任务会在实例的 [维护时间](https://intl.cloud.tencent.com/document/product/238/35785) 内执行并生效。
>
![](https://main.qcloudimg.com/raw/f31ea4d1b771972dbde10e5fab9eb763.png)
