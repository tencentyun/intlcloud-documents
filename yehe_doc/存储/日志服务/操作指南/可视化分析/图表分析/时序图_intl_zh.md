时序图需要统计数据具备时序字段，依据时间顺序组织与聚合指标。可直观反映指标随时间的变化趋势。统计近一周，每天404错误出现的次数等趋势分析场景适用。

## 图表配置

### 通用配置



| 配置项   | 说明                                                         |
| -------- | ------------------------------------------------------------ |
| 图表名称 | 设置图表的显示名称，可为空。                                 |
| 图例     | 设置图表的图例内容，可以控制图例的样式与位置。同时也支持在图例中添加对比数据。 |
| Tooltip  | 控制鼠标悬浮时触发的气泡提示的内容样式。                     |
| 单位配置 | 设置图表内所有指标类型的字段单位。详情请参考 [单位配置](https://intl.cloud.tencent.com/document/product/614/47788)。     |


### 趋势对比



| 配置项   | 说明                                                         |
| -------- | ------------------------------------------------------------ |
| 趋势对比 | 开启趋势对比后，可以选择和 X 小时、天、月、年以前的同周期数据进行对比。对比数据以虚线的方式显示在图表中。 |



### 时序图配置



| 配置项 | 说明                                                         |
| ------ | ------------------------------------------------------------ |
| 时序图 | 绘制样式：数据在坐标轴上的显示样式，选择线则为折线图，选择柱则为直方图，选择点则为散点图。 <br />线性：点与点之间的连线是否平滑处理。<br />线宽：控制线条的粗细。<br />填充：控制填充区域的透明度，为0时不填充。<br />显示点：显示数据点，无数据则不显示。<br />空值：控制时序序列点位上无数据存在时，该点位的处理，默认填充为0。<br />堆叠：控制是否将数据堆叠显示。 |
| 坐标轴 | 显示：显示/隐藏坐标轴。<br />最大值/最小值：控制坐标轴显示的最大值与最小值，大于最大值，小于最小值的坐标区域不显示。 |

绘制样式示例：
![](https://qcloudimg.tencent-cloud.cn/raw/f6ea7fdde1dd41fe5738488faabbd06d.png)

填充示例：
![](https://qcloudimg.tencent-cloud.cn/raw/f6ea7fdde1dd41fe5738488faabbd06d.png)

空值示例：
![](https://qcloudimg.tencent-cloud.cn/raw/272e502e60446d620031b54abeacebc0.png)

### 阈值配置



| 配置项   | 说明                                                         |
| -------- | ------------------------------------------------------------ |
| 阈值配置 | 阈值点：设置阈值点，可以添加多个阈值区间，点击阈值对应色彩可打开色盘自定义颜色。<br />阈值展示：控制阈值展示的样式，包含阈值线、区域填充、阈值线和区域填充三种模式。选择关闭时，不使用阈值。 |


## 图表操作

### 框选时间范围

![](https://qcloudimg.tencent-cloud.cn/raw/0764c42fde7d9a739b493f0e879bda51.png)

鼠标悬浮在图表上，长按后拖拽触发框选，时间范围将会使用框选区域的时间。适用于异常点的时间范围下钻等场景。

## 使用案例

时序图制图需要具备时间类型的字段，使用中依赖各种函数来对时间字段进行处理。更多的时序图时间函数请参考 [时间与日期函数](https://cloud.tencent.com/document/product/614/58981)。

计算每分钟的 PV 与 UV：
```
* | select histogram( cast(__TIMESTAMP__ as timestamp),interval 1 minute) as time, count(*) as pv,count( distinct remote_addr) as uv group by time order by time desc limit 10000
```
![](https://qcloudimg.tencent-cloud.cn/raw/1c77605c14921b3768b04176b1817684.png)

计算每分钟各协议类型的 PV：
```
* | select histogram( cast(__TIMESTAMP__ as timestamp),interval 1 minute) as time, protocol_type, count(*) as pv group by  time, protocol_type order by time desc limit 10000
```
![](https://qcloudimg.tencent-cloud.cn/raw/09400ef819ba330b6394b357badafe74.png)

计算每分钟的请求失败率(%)：
```
* | select date_trunc('minute', __TIMESTAMP__) as time, round(sum(case when status = 404 then 1.00 else 0.00 end)/ cast(count(*) as double)*100,3) as "404比例", round(sum(case when status >= 500 then 1.00 else 0.00 end)/cast(count(*) as double)*100,3) as "5XX比例", round(sum(case when status >= 400 and status < 500 then 1.00 else 0.00 end)/cast(count(*) as double)*100,3) as "4XX比例", round(sum(case when status >= 400  then 1.00 else 0.00 end)/cast(count(*) as double)*100,3) as "总失败率" group by time order by time limit 10000
```
![](https://qcloudimg.tencent-cloud.cn/raw/b74434e4c08111d570d04cf7ec8f9313.png)
