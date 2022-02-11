
您可以通过 [TDSQL-C 控制台](https://console.cloud.tencent.com/cynosdb) 查看和修改部分参数，并可以在控制台查询参数修改记录。

## 注意事项
- 为保证实例的稳定，控制台仅开放部分参数的修改，控制台的参数配置页面展示的参数即为用户可以修改的参数。
- 如果修改的参数需要重启实例才生效，系统会提示您是否重启，建议您在业务低峰期操作，并确保应用程序具有重连机制。
- 设置参数时，当前不支持自定义公式输入。
- 如果希望恢复为默认公式，清空输入的参数内容并应用。

## 通过参数列表修改参数
### [批量修改参数](id:plxgcs)
1. 登录 [TDSQL-C 控制台](https://console.cloud.tencent.com/cynosdb)，在集群列表，找到需要的集群，单击集群 ID，进入集群管理页面。
2. 在集群管理页面，选择**参数设置**页，单击**修改参数**。
![](https://qcloudimg.tencent-cloud.cn/raw/4ba02fd67412019812d35d2b8a8053fb.png)
3. 在**参数运行值**列，选择需要修改的参数进行修改，确认无误后，单击**确认**。
![](https://qcloudimg.tencent-cloud.cn/raw/eee113fe6f3229f26bad7791964da616.png)
4. 在弹出的对话框，确认无误后，单击**确定**。

### [修改单个参数](id:xgdgcs)
1. 登录 [TDSQL-C 控制台](https://console.cloud.tencent.com/cynosdb)，在集群列表，找到需要的集群，单击集群 ID，进入集群管理页面。
2. 在集群管理页面，选择**参数设置**页，选择目标参数所在行，在**参数运行值**列，单击<img src="https://main.qcloudimg.com/raw/788902e3f8c335cf17de420f7181c2a8.png"  style="margin:0;">修改参数值。
3. 根据**参数可修改值**列的提示，输入目标参数值，单击<img src="https://main.qcloudimg.com/raw/1f4c7f2e0744bc601efb5d9fb04a7a04.png"  style="margin:0;">保存，单击<img src="https://main.qcloudimg.com/raw/2106cb4b9337a1a2fff5908581d2a908.png"  style="margin:0;">可取消操作。
![](https://qcloudimg.tencent-cloud.cn/raw/2a3bd2fa1ca1341f7526f04b1102c7fb.png)
4. 在弹出的对话框，确认无误后，单击**确定**。

## 通过导入参数模板修改参数
1. 登录 [TDSQL-C 控制台](https://console.cloud.tencent.com/cynosdb)，在集群列表，找到需要的集群，单击集群 ID，进入集群管理页面。
2. 在集群管理页面，选择**参数设置**页，单击**从模板导入**。
![](https://qcloudimg.tencent-cloud.cn/raw/eb5e72ef067744d50e1d744e31572998.png)
3. 在弹出的对话框，选择参数模板，单击**确定**。
4. 确认参数后，单击左上角的**确认**。
5. 在弹出的对话框，确认无误后，单击**确定**。


## 通过导入参数配置文件修改参数
1. 登录 [TDSQL-C 控制台](https://console.cloud.tencent.com/cynosdb)，在集群列表，找到需要的集群，单击集群 ID，进入集群管理页面。
2. 在集群管理页面，选择**参数设置**页，单击**导入参数**。
![](https://qcloudimg.tencent-cloud.cn/raw/9c4a1bbea12fc43cbe434e5f3388d20c.png)
3. 在弹出的对话框，选择参数文件上传后，单击**导入并覆盖原有参数**。
![](https://qcloudimg.tencent-cloud.cn/raw/877033e022af7ccde30d689c6a0cd5a1.png)
4. 确认参数后，单击左上角的**确认**。
5. 在弹出的对话框，确认无误后，单击**确定**。

## 导出参数配置文件
1. 登录 [TDSQL-C 控制台](https://console.cloud.tencent.com/cynosdb)，在集群列表，找到需要的集群，单击集群 ID，进入集群管理页面。
2. 在集群管理页面，选择**参数设置**页，单击**导出参数**导出参数配置文件。

## 导出参数配置为参数模板
1. 登录 [TDSQL-C 控制台](https://console.cloud.tencent.com/cynosdb)，在集群列表，找到需要的集群，单击集群 ID，进入集群管理页面。
2. 在集群管理页面，选择**参数设置**页，单击**另存为模板**，可将现有参数配置存储为参数模板。

## 后续操作
- 您可以使用数据库参数模板来批量管理数据库的参数配置，请参见 [使用参数模板](https://intl.cloud.tencent.com/document/product/1098/44601)。
- 相关重要参数的配置建议，请参见 [参数配置建议](https://intl.cloud.tencent.com/document/product/1098/44600)。

