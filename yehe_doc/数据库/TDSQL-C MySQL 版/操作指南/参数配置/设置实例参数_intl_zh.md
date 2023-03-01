您可以通过控制台查看参数及对参数的修改记录，也可以根据业务需要调整部分参数值，本文为您介绍通过控制台修改参数的相关操作。

## 注意事项
- 为保证实例的稳定，控制台仅开放部分参数的修改，控制台的参数配置页面展示的参数即为可以修改的参数。
- 如果修改的参数需要重启实例才生效，系统会提示您是否重启，建议您在业务低峰期操作，并确保应用程序具有重连机制。
- 参数任务：修改参数任务详情可通过任务列表查询。
 - 	如参数任务暂未执行，可撤销。
 - 	如该集群存在参数修改任务，在未完成时，再次修改参数会导致修改失败。
- 全局参数需要在读写实例上进行修改，修改后将应用至集群下的所有实例。非全局参数可以在集群下的实例上单独设置并生效。

## 修改单个参数
1. 登录 [TDSQL-C MySQL 版控制台](https://console.cloud.tencent.com/cynosdb)，在集群列表，找到目标集群，单击集群 ID，进入集群管理页面。
2. 在集群管理页面，选择参数设置页，选择需要修改参数的实例 ID（全局参数需要在读写实例进行设置，设置后对集群整体生效，非全局参数可以在任一实例单独设置）。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/gUCb301_29.png)
>!TDSQL-C MySQL 版对参数新增了**是否全局参数**字段，方便您快速区分哪些参数对集群整体生效，哪些参数可以对不同实例设置不同参数值。全局参数设置的参数值将对集群下所有实例生效，非全局参数的参数值设置后只会对当前实例生效，但您可以将该值同步至其他实例。
3. 在参数列表找到目标参数所在行，在**参数运行值**列，单击<img src="https://main.qcloudimg.com/raw/788902e3f8c335cf17de420f7181c2a8.png"  style="margin:0;">修改参数值。
>?您也可通过参数设置页右侧检索框搜索参数名快速找到需要修改的参数。
>![](https://staticintl.cloudcachetci.com/yehe/backend-news/UMvB145_30.png)
4. 根据参数可修改值列的提示，输入目标参数值，单击![](https://qcloudimg.tencent-cloud.cn/raw/e8e0e48e149000b81beb9aa8401b144f.png)保存，单击![](https://qcloudimg.tencent-cloud.cn/raw/63fbddc988994f6de30f39c9f3916295.png)可取消操作。
>?若参数值前显示![](https://qcloudimg.tencent-cloud.cn/raw/69a6a4c89f58c07672271750d8e8766e.png)图标，表明当前参数支持整型和公式化两种设置方式。公式化设置后参数值将随 cpu /内存等规格自动调整（公式仅支持修改数值变量，详情请参考 [参数公式](https://www.tencentcloud.com/document/product/1098/53398)）。
>![](https://staticintl.cloudcachetci.com/yehe/backend-news/9daX674_34.png)
>![](https://staticintl.cloudcachetci.com/yehe/backend-news/uuds530_35.png)
>
>5. 单击<img src="https://main.qcloudimg.com/raw/1f4c7f2e0744bc601efb5d9fb04a7a04.png"  style="margin:0;">后，在弹出的对话框确认无误后，选择执行时间，单击**确定**。
>执行时间：
 - 选择立即执行时，则会在确认后，立即触发修改。
 - 选择维护时间内修改时，则会在实例的维护时间内进行修改。修改维护窗口期可参考 [设置实例维护时间](https://www.tencentcloud.com/document/product/1098/53399)。
>!参数修改确认时，系统会提示您是否会重启数据库实例，您可选择立即执行或维护时间内执行。
修改非重启项界面如下：
![](https://staticintl.cloudcachetci.com/yehe/backend-news/w499822_36.png)
修改重启项提示如下：
![](https://staticintl.cloudcachetci.com/yehe/backend-news/RNEF143_37.png)
若修改参数包含非全局参数，将提示您是否将该参数同步应用至其他实例，您可选择不同步，单独对当前实例设置该参数值。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/Q59z995_38.png)
或者在下拉框中选择要同步设置的实例 ID，选中后，该非全局参数值将同步应用至选中的实例。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/QkGh313_39.png)

## 批量修改参数
1. 登录 [TDSQL-C MySQL 版控制台](https://console.cloud.tencent.com/cynosdb)，在集群列表，找到目标集群，单击集群 ID，进入集群管理页面。
2. 在集群管理页面，选择参数设置页，选择需要修改参数的实例 ID（全局参数需要在读写实例进行设置，设置后对集群整体生效，非全局参数可以在任一实例单独设置）。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/VeMi479_40.png)
3. 单击**修改参数**。
4. 在参数运行值列，选择需要修改的参数进行修改，确认无误后，单击**确认**。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/DyFx836_41.png)
5. 在弹出的对话框，系统会提示您是否会重启数据库实例，若存在非全局参数，可以选择应用至其他实例，确认无误后，选择立即执行或维护时间内执行，然后单击**确定**。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/9AQK630_42.png)

## 通过导入参数模板修改参数
1. 登录 [TDSQL-C MySQL 版控制台](https://console.cloud.tencent.com/cynosdb)，在集群列表，找到需要的集群，单击集群 ID，进入集群管理页面。
2. 在集群管理页面，选择参数设置页，选择目标实例 ID，单击**从模板导入**。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/cKvt608_43.png)
3. 在弹出的对话框，选择参数模板，单击**确定**。
4. 确认参数后，单击左上角的**确认**。
5. 在弹出的对话框，系统会提示您是否会重启数据库实例，若存在非全局参数，可以选择应用至其他实例，确认无误后，选择立即执行或维护时间内执行，然后单击**确定**。

## 通过导入参数配置文件修改参数
>!参数配置文件不支持导入公式。
>
1. 登录 [TDSQL-C MySQL 版控制台](https://console.cloud.tencent.com/cynosdb)，在集群列表，找到需要的集群，单击集群 ID，进入集群管理页面。
2. 在集群管理页面，选择参数设置页，选择目标实例 ID，单击**导入参数**。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/gBsx463_44.png)
3. 在弹出的对话框，选择参数文件上传后，单击**导入并覆盖原有参数**。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/9npU904_45.png)
4. 确认参数后，单击左上角的**确认**。
5. 在弹出的对话框，系统会提示您是否会重启数据库实例，若存在非全局参数，可以选择应用至其他实例，确认无误后，选择立即执行或维护时间内执行，然后单击**确定**。

## 导出参数配置文件
>!当前导出参数配置文件时，公式化参数值将自动转换为整数值导出。
>
1. 登录 [TDSQL-C MySQL 版控制台](https://console.cloud.tencent.com/cynosdb)，在集群列表，找到需要的集群，单击集群 ID，进入集群管理页面。
2. 在集群管理页面，选择参数设置页，选择目标实例 ID，单击**导出参数**，导出文件直接会保存到本地。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/2GQF750_46.png)

## 查询参数修改记录
1. 登录 [TDSQL-C MySQL 版控制台](https://console.cloud.tencent.com/cynosdb)，在集群列表，找到需要的集群，单击集群 ID，进入集群管理页面。
2. 在集群管理页面，选择**参数设置**页，在右侧单击**最近修改记录**。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/YFzt052_47.png)
3. 在跳转的页面，您可在右侧选择需要查看最近修改记录的实例 ID，然后查看其参数修改记录，可查看的字段信息包括（参数名称、修改前参数值、修改后参数值、修改状态、修改时间）。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/K9g2267_48.png)
