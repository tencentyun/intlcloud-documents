您可以通过 [MySQL 控制台](https://console.cloud.tencent.com/cdb) 查看和修改部分参数，并可以在控制台查询参数修改记录。

## 注意事项
- 为保证实例的稳定，控制台仅开放部分参数的修改，控制台的参数配置页面展示的参数即为用户可以修改的参数。
- 如果修改的参数需要重启实例才生效，系统会提示您是否重启，建议您在业务低峰期操作，并确保应用程序具有重连机制。

## 通过参数列表修改参数

<span id = "plxgcs"></span>
### 批量修改参数
1. 登录 [MySQL 控制台](https://console.cloud.tencent.com/cdb)，在实例列表，单击实例 ID 或**操作**列的**管理**，进入实例管理页面。
2. 选择**数据库管理**>**参数设置**页，单击**批量修改参数**。
![](https://main.qcloudimg.com/raw/82c535bd50543645831988ca2e9b688e.png)
3. 在**参数运行值**列，选择需要修改的参数进行修改，确认无误后，单击**确认修改**。
![](https://main.qcloudimg.com/raw/5307fbeef4b1fccef478ab7fd57b3167.png)
4. 在弹出的对话框，选择参数任务的**执行方式**，单击**确定**。
>?
>- 若选择**立即执行**，所选实例的参数变更任务会立即执行并生效。
>- 若选择**维护时间内**，所选实例的参数变更任务会在实例的 [维护时间](https://intl.cloud.tencent.com/document/product/236/10929) 内执行并生效。
>

<span id = "xgdgcs"></span>
### 修改单个参数
1. 登录 [MySQL 控制台](https://console.cloud.tencent.com/cdb)，在实例列表，单击实例 ID ，进入实例管理页面。
2. 选择**数据库管理**>**参数设置**页，选择目标参数所在行，在**参数运行值**列，单击<img src="https://main.qcloudimg.com/raw/788902e3f8c335cf17de420f7181c2a8.png"  style="margin:0;">修改参数值。
![](https://main.qcloudimg.com/raw/4687ed705274b76ec92c43b7f9d448ab.png)
3. 根据**参数可修改值**列的提示，输入目标参数值，单击<img src="https://main.qcloudimg.com/raw/1f4c7f2e0744bc601efb5d9fb04a7a04.png"  style="margin:0;">保存，单击<img src="https://main.qcloudimg.com/raw/2106cb4b9337a1a2fff5908581d2a908.png"  style="margin:0;">可取消操作。
![](https://main.qcloudimg.com/raw/41c7d73d4c5d404a112f54c3a63da726.png)
4. 在弹出的对话框，选择参数任务的**执行方式**，单击**确定**。
>?
>- 若选择**立即执行**，所选实例的参数变更任务会立即执行并生效。
>- 若选择**维护时间内**，所选实例的参数变更任务会在实例的 [维护时间](https://intl.cloud.tencent.com/document/product/236/10929) 内执行并生效。
>


## 通过导入参数模板修改参数
### 方式一：通过**参数设置**页面导入
1. 登录 [MySQL 控制台](https://console.cloud.tencent.com/cdb)，在实例列表，单击实例 ID ，进入实例管理页面。
2. 选择**数据库管理**>**参数设置**页，单击**从模板导入**。
![](https://main.qcloudimg.com/raw/bd7a2fd3dc89895f1a3bd779d0fe8bbc.png)
3. 在弹出的对话框，选择参数模板，单击**导入并覆盖原有参数**。
![](https://main.qcloudimg.com/raw/2f649840f16befabea6259f9b4c7f47c.png)
4. 确认参数后，单击**确认修改**。
![](https://main.qcloudimg.com/raw/1673166256bc4d122f5a72c3c703ffab.png)
5. 在弹出的对话框，选择参数任务的**执行方式**，单击**确定**。
>?
>- 若选择**立即执行**，所选实例的参数变更任务会立即执行并生效。
>- 若选择**维护时间内**，所选实例的参数变更任务会在实例的 [维护时间](https://intl.cloud.tencent.com/document/product/236/10929) 内执行并生效。
>


### 方式二：通过**参数模板**页面导入
请参见 [应用参数模板于实例](https://intl.cloud.tencent.com/document/product/236/31906#.E5.BA.94.E7.94.A8.E5.8F.82.E6.95.B0.E6.A8.A1.E6.9D.BF.E4.BA.8E.E5.AE.9E.E4.BE.8B)。

## 通过导入参数配置文件修改参数
1. 登录 [MySQL 控制台](https://console.cloud.tencent.com/cdb)，在实例列表，单击实例 ID ，进入实例管理页面。
2. 选择**数据库管理**>**参数设置**页，单击**导入参数**。
![](https://main.qcloudimg.com/raw/52d6f069bbce29c933254593d59c0236.png)
3. 在弹出的对话框，选择参数文件上传后，单击**导入并覆盖原有参数**。
![](https://main.qcloudimg.com/raw/42fb6ef8936131a3bc776e492478e745.png)
4. 确认参数后，单击**确认修改**。
![](https://main.qcloudimg.com/raw/1673166256bc4d122f5a72c3c703ffab.png)
5. 在弹出的对话框，选择参数任务的**执行方式**，单击**确定**。
>?
>- 若选择**立即执行**，所选实例的参数变更任务会立即执行并生效。
>- 若选择**维护时间内**，所选实例的参数变更任务会在实例的 [维护时间](https://intl.cloud.tencent.com/document/product/236/10929) 内执行并生效。
>


## 导出参数配置文件
1. 登录 [MySQL 控制台](https://console.cloud.tencent.com/cdb)，在实例列表，单击实例 ID ，进入实例管理页面。
2. 选择**数据库管理**>**参数设置**页，单击**导出参数**导出参数配置文件。
![](https://main.qcloudimg.com/raw/6885ffbc45f3154ed203551a309e1848.png)

## 导出参数配置为参数模板
1. 登录 [MySQL 控制台](https://console.cloud.tencent.com/cdb)，在实例列表，单击实例 ID ，进入实例管理页面。
2. 选择**数据库管理**>**参数设置**页，单击**另存为模板**，可将现有参数配置存储为参数模板。
![](https://main.qcloudimg.com/raw/fca4ec16b316948af812db9988d0c92c.png)

## 自定义时间修改参数
执行参数修改的最后一步时，在弹出的对话框，可自定义参数的修改时间。
>?选择**维护时间内**，所选实例的参数变更任务会在实例的 [维护时间](https://intl.cloud.tencent.com/document/product/236/10929) 内执行并生效。
>
![](https://main.qcloudimg.com/raw/00d4892fb614dd285cdec91a4a74cf2d.png)


## 取消参数修改任务
选择**维护时间内**的修改参数任务提交后，如需取消修改参数，可在任务执行前（即任务状态为**等待执行**），在左侧导航**[任务列表](https://console.cloud.tencent.com/mysql/task)**页，单击**操作**列的**撤销**，取消参数修改任务。
![](https://main.qcloudimg.com/raw/566fd9374d0d59b38ceb99d310b782a9.png)


## 查看参数修改记录
1. 登录 [MySQL 控制台](https://console.cloud.tencent.com/cdb)，在实例列表，单击实例 ID ，进入实例管理页面。
2. 选择**数据库管理**>**参数设置**页，单击右侧的**最近修改记录**。
![](https://main.qcloudimg.com/raw/93494ebb3b80a6547f1c6fe7bcbf9c8a.png)
3. 在最近参数修改记录页，可查看近期参数修改记录。


## 后续操作
- 您可以使用数据库参数模板来批量管理数据库的参数配置，请参见 [使用参数模板](https://intl.cloud.tencent.com/document/product/236/31906)。
- 相关重要参数的配置建议，请参见 [参数配置建议](https://intl.cloud.tencent.com/document/product/236/38056)。
