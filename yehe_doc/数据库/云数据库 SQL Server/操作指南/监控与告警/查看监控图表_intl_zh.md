
为方便用户查看和掌握实例的运行信息，云数据库 SQL Server 提供了丰富的性能监控项与便捷的监控功能（自定义视图、时间对比、合并监控项等）。

本文为您介绍如何通过控制台查看监控图表信息。
>?单个实例的表数量超过100万后，可能会影响数据库监控，请合理规范表的数量，控制单个实例表数量不超过100万。

## 支持监控的实例类型
云数据库 SQL Server 支持主实例、只读实例的监控，并为每个实例提供独立的监控视图供查询。

## [查看监控信息](id:ckjkxx)
1. 登录 [SQL Server 控制台](https://console.cloud.tencent.com/sqlserver)。
2. 在上方选择地域，找到所需实例，单击实例 ID 或**操作**列的**管理**，进入实例管理页。
![](https://qcloudimg.tencent-cloud.cn/raw/273f3f073d2dd195dae0926ab52dd708.png)
3. 在实例管理页，选择**系统监控**页，可对各项监控指标进行查阅。
![](https://qcloudimg.tencent-cloud.cn/raw/72fe5eadb03993db12e0a8b6a45eca43.png)
>?您也可以在实例列表，找到需要查看监控的实例，单击其监控图标快捷查看该实例的监控情况。
>![](https://qcloudimg.tencent-cloud.cn/raw/f23fd5341d823616580cf13619e381ee.png)

## 全屏显示图表
您可以将单个指标进行全屏显示，方便更清晰的预览指标数据。
1. 在 [系统监控](#ckjkxx) 页，通过单击对应指标右侧的![](https://qcloudimg.tencent-cloud.cn/raw/5ad2d8ff9f3dfcf99cc82d10f0c718ae.png)图标，可全屏显示该指标情况。
2. 全屏显示预览数据后，可单击右上角的X，关闭全屏显示窗口。
![](https://qcloudimg.tencent-cloud.cn/raw/67c8af1dce72f488fb5d7f542dc2cf32.png)

## 数据导出
您可以将需要的指标数据单个导出。
在 [系统监控](#ckjkxx) 页，通过单击对应指标右侧的![](https://qcloudimg.tencent-cloud.cn/raw/96ac56f01426b5d7af37b10f181bf85a.png)图标，可选择导出该指标的数据或者图片到本地。
![](https://qcloudimg.tencent-cloud.cn/raw/998d0541294395dd8d7dad5fe517d9e9.png)

## 选择监控时间范围
您可以通过选择或自定义时间范围，对该时间段的监控情况进行查询。
1. 在 [系统监控](#ckjkxx) 页，单击时间框。
![](https://qcloudimg.tencent-cloud.cn/raw/0179ccba669135a7b2f3e79d904bd862.png)
2. 在弹窗里可选择查看时间为5分钟，30分钟，1小时，3小时，12小时，24小时，2天，7天，30天，今天，昨天，或者在日历上选择查看的起止日期和选择该起止日期的时间范围，选择好后单击**确定**。
![](https://qcloudimg.tencent-cloud.cn/raw/ace670b8815b5dfc66d8edb0c01bc54f.png)

## 添加时间对比
您可以通过添加时间对比，对比多个时间范围的监控数据。
1. 在 [系统监控](#ckjkxx) 页，选择时间窗口后面单击添加时间。
![](https://qcloudimg.tencent-cloud.cn/raw/46d924db19663714642e4e0a751bf002.png)
2. 在下拉选项中，选择同比，环比或者自定义时间，单击**确定**。
![](https://qcloudimg.tencent-cloud.cn/raw/25a57c04d50e2de1b210acaa31ddb981.png)

## 监控粒度
您可以在所选时间周期内查看不同时间粒度下实例监控的情况。
在 [系统监控](#ckjkxx) 页，选择时间周期后，单击时间粒度后的下拉键，选择需要查看的粒度。
![](https://qcloudimg.tencent-cloud.cn/raw/7ca17555648846fea1da31495d4e3989.png)

**时间周期和图表颗粒度对照表**

| 时间周期 | 支持查看统计粒度 |
|---------|---------|
| 5分钟 | 10秒、1分钟 |
| 30分钟、1小时 | 10秒、1分钟、5分钟 |
| 3小时 | 10秒、1分钟、5分钟、1小时 |
| 12小时、今天、昨天 | 1分钟、5分钟、1小时 |
| 24小时、2天 | 1分钟、5分钟、1小时、1天 |
| 7天、30天 | 1小时、1天 |

## 设置刷新时间
您可设置系统监控页的刷新时间（默认关闭），以便实时观测实例监控变化。
在 [系统监控](#ckjkxx) 页，单击![](https://qcloudimg.tencent-cloud.cn/raw/21e447500165860dd294edff8c529116.png)后的下拉键，设置数据刷新时间频次，支持设置为30s，5min，30min，1h。
![](https://qcloudimg.tencent-cloud.cn/raw/2e5264740adae3d7b5a9b8d2db8473e9.png)
