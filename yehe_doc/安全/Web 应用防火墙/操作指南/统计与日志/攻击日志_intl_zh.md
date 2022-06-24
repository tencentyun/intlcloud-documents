本文为您介绍如何使用攻击日志进行攻击日志索引、快速分析和查询。

## 背景信息
Web 应用防火墙默认提供攻击日志，详细记录攻击产生的时间、攻击源IP、攻击类型及攻击详情等信息，攻击日志仅支持查询或导出最近30天日志。攻击日志支持全文检索、模糊搜索和组合条件搜索等检索方式，同时支持根据检索条件下载日志，支持百万级日志下载。

## 操作指南
1. 登录 [Web 应用防火墙控制台](https://console.cloud.tencent.com/guanjia/tea-overview)，在左侧导航栏中，选择**日志服务** > **攻击日志**。
2. 在日志查询页签，您可以根据需要，选择域名、攻击类型、执行动作及时间维度等信息，筛选查看攻击日志。
![](https://qcloudimg.tencent-cloud.cn/raw/731de6f37b9d5f3fd732d1427263d171.png)

**字段说明：**
  - **域名过滤**：支持多选，默认显示全部域名。
  - **攻击类型过滤**：支持多选，默认为全部攻击类型，攻击类型包括各个安全模块产生的观察和拦截日志。
  - **执行动作过滤**：单选，默认为全部，包括观察和拦截两种类型。
  - **风险等级**：单选，包括：高危、中危和低危三种类型
  - **时间范围**：默认为近一小时，支持选择最近时间及相对时间，您根据需要进行选择。
  - **自动刷新**：自动刷新当前页面，默认为关闭，若开启开关，您可选择按照时间范围刷新当前页面，获取最新攻击日志数据。
![](https://qcloudimg.tencent-cloud.cn/raw/a03a2a72f133b79e4c732668dbbbd307.png)
3. 设置完成检索条件，单击**检索分析**，即可查看检索分析结果。
4. 在攻击日志原始数据页面左侧，单击具体统计字段，可快速查看符合检索条件下，各个字段值在攻击日志中的占比。
![](https://qcloudimg.tencent-cloud.cn/raw/5e1907615f3519e3f39e05d7c300e97c.png)

- **自定义字段列表**：在日志列表右上方，单击<img src="https://main.qcloudimg.com/raw/9ebb9fa1652d9154137fa1d934329043.png" style="margin:0;">，可设置列表展示字段，选择完成后，单击**确定**，即可设置成功，各字段说明，请参见 [日志详情字段说明](#Log)。
![](https://qcloudimg.tencent-cloud.cn/raw/7b1f43321ab8f1bbccf3214fc9524b98.png)

- **攻击日志下载**：
1. 在日志列表右上方，单击<img src="https://main.qcloudimg.com/raw/ac6451a8dab74a5cf57770ff8af30954.png" style="margin:0;">，即可成功创建下载任务。

>?
>- 同一时间段内只允许创建一个下载任务，请耐心等待。单次最多支持下载100万条日志，如果您需要下载的日志超过100万条，建议您分多次任务进行下载，或 [联系我们](https://intl.cloud.tencent.com/contact-us) 为您提供支持服务。
>- 当选择泛域名（如*.abc.com）时，所有关联子域名（如以.abc.com结尾）的日志也将会被下载。


2. 在 [攻击日志](https://console.cloud.tencent.com/guanjia/attack) 页面上方，单击**下载任务**，可以查看创建日志文件的下载状态信息。
![](https://qcloudimg.tencent-cloud.cn/raw/1c3cf3df951a1094051f25d788006f3a.png)
3. 输入任意任务名称，单击**创建**后即可下载。
![](https://qcloudimg.tencent-cloud.cn/raw/ce8caf381810f21a77f1d321b55ea022.png)
4. 在攻击日志原始数据页面右侧，单击日志前方展开按钮，可以查看日志详情信息，默认展示“日志详情”，单击 **JSON**，可查看对应 JSON 格式展示样式。
![](https://qcloudimg.tencent-cloud.cn/raw/cd8746f122bf9086e0f2650261b778b1.png)
5. 在日志详情中，单击具体参数值，将自动填充检索条件，进行快速检索，支持多种字段组合。
![](https://qcloudimg.tencent-cloud.cn/raw/1b3a0085e1e91ead6a2c48f27c227102.png)

## 附录

[](id:Log)
### 日志详情字段说明
**基本信息**

|字段名称	|字段说明|
|----|---|
|host	|客户端访问域名。|
|attack_type|	详细攻击类型，全部攻击类型信息。|
|attack_category 	|攻击一级分类，暂未提供。|
|count	|聚合攻击次数，相同攻击源 IP 和攻击类型，汇总每10秒产生的攻击次数。|
|attack_ip|	攻击源 IP，客户端攻击的源 IP。|
|rule_id|	命中规则 ID，触发防护策略的规则 ID，其中 AI 引擎检出的攻击，规则 ID 为0。|
|method|	请求方法，客户端攻击请求方法。|
|risk_level|	风险等级，客户端攻击触发的风险等级。|
|attack_time	|攻击时间，客户端攻击触发的时间。|
|attack_place|	攻击位置，攻击方式在 HTTP 请求中的位置。|
|action|执行动作客户端攻击触发的动作。|
|uri|请求 URI 的内容。|
|attack_content|	攻击内容，客户端触发攻击的内容。|
|http_log|	请求的其他信息，包括请求协议、协议版本等信息。|
|user_agent	|User-Agent。攻击源 IP 向服务器用来表明自己的浏览器类型和操作系统标识等信息。|
|headers	|协议头部信息，包括自定义头部信息。|
|UUID	|日志唯一标识。|

**攻击 IP 属性**

|字段名称	|字段说明|
|----|---|
|ipinfo_province| 	攻击 IP 省份信息。|
|ipinfo_state 	|攻击 IP 国家信息，国家英文缩写。|
|pinfo_nation|	攻击 IP 国家名称。|
|ipinfo_city |	攻击 IP 城市。|
|ipinfo_isp	|攻击 IP 运营信息。|
|ipinfo_dimensionality |	攻击 IP 纬度信息。|
|ipinfo_longitude 	|攻击源 IP 的经度信息。|


### [日志文件字段说明](id:log2)

|字段名称	|字段说明|
|----|---|
|uuid	|日志唯一标识。|
|attack_time	|客户端攻击事件。|
|rule_id	|客户端攻击触发的策略 ID。|
|count|	攻击聚合次数，相同攻击源 IP 和攻击类型，每10秒产生的攻击次数汇总。|
|status|	执行动作，0表示观察，1表示拦截。|
|domain	|客户端攻击的域名信息。|
|attack_ip	|客户端攻击 IP。|
|attack_type	|客户端攻击类型。|
|args_name	|客户端请求攻击发生的位置，如请求参数、URI、IP 等。|
|attack_content|	客户端攻击的攻击内容。|
|uri	|客户端攻击 URI 信息。|
|method	|客户端攻击请求使用的方法。|
|user_agent|	客户端的 User_Agent 信息。|
