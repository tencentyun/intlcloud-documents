## 操作场景
在使用云函数（SCF）进行函数计算时，会产生大量的函数运行日志。SCF 运行日志已打通腾讯云日志服务（CLS）平台，可实时采集函数运行日志至 CLS 平台。您可在 CLS 平台进行日志的实时检索、投递和消费等更多操作。如下图所示：
![](https://main.qcloudimg.com/raw/ca4e6aefa5b78812d98ea8baaac25238.png)


## 前提条件
在使用 SCF 实时日志服务功能之前，需开通 [日志服务](https://intl.cloud.tencent.com/product/cls)。


## 操作步骤
### 创建日志集和日志主题
登录 [CLS 控制台](https://console.cloud.tencent.com/cls) 并 [创建日志集和日志主题](https://intl.cloud.tencent.com/document/product/614/31592)。本文以在广州创建 `SCF-test` 日志集和日志主题为例。如下图所示：
>日志集地域请选择函数服务所在地域，暂不支持跨地域日志推送。
>
![](https://main.qcloudimg.com/raw/128f3400bc4f8da1a7532bd13fbec8a5.png)

### 配置日志服务
1. 登录 SCF 控制台，选择左侧导航栏中的【[函数服务](https://console.cloud.tencent.com/scf/list)】。
2. 在页面上方选择函数所在地域及命名空间，并在列表中单击需实时采集日志的函数名。
3. 在“函数配置”页面，单击右上角的【编辑】。如下图所示：
![](https://main.qcloudimg.com/raw/28d3fa31668d9280acb7de553050d008.png)
4. 在“日志投递”中，选择已为该函数创建的日志集和日志主题，本文以 `SCF-test` 为例。如下图所示：
![](https://main.qcloudimg.com/raw/984025711efc018826ce93f86f922102.png)
5. 单击【保存】即可成功接入 CLS 平台。

### 开启索引
>如果您需要使用日志检索功能，则需手动开启索引，请参考此步骤开启索引。
>
1. 登录 CLS 控制台，选择左侧导航栏中的【[日志集管理](https://console.cloud.tencent.com/cls/logset)】。
2. 单击已创建的日志集 ID，进入“基本信息”页面。
3. 选择日志主题所在行右侧的【管理】，进入日志主题“基本信息”页面。
4. 在日志主题“基本信息”页面，单击【索引配置】。如下图所示：
![](https://main.qcloudimg.com/raw/dfb2ab52611a37e82873d3b97f33a0a6.png)
5. 单击右上角的【编辑】，开启索引后保存设置。
如需使用更多功能，例如日志实时检索，日志投递和消费等，请参考 [日志服务文档](https://intl.cloud.tencent.com/document/product/614) 并前往 [CLS 控制台](https://console.cloud.tencent.com/cls) 开始使用。


### 实时检索示例
>在使用实时检索功能前，请确保您的函数服务日志已接入 CLS 平台，并且需检索的日志主题已开启索引。
>
1. 登录 CLS 控制台，选择左侧导航栏中的【[日志检索](https://console.cloud.tencent.com/cls/search)】。
2. 在“检索分析”页面选择需检索的日志主题和时间，并在输入框中填写检索语法，本文以 `START` 为例。
检索语法支持关键词检索、模糊检索、范围检索等方式，详情请参考 [语法规则](https://intl.cloud.tencent.com/document/product/614/16981)。
3. 单击【查询分析】即可查看实时日志信息。如下图所示：
![](https://main.qcloudimg.com/raw/e7e49246fb6867a7295480fab166541d.png)
