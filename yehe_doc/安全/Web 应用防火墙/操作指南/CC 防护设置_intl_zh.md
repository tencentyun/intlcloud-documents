## 功能简介
CC 防护对网站特定的 URL 进行访问保护，CC 防护2.0全新改版，支持紧急模式 CC 防护和自定义 CC 防护策略。紧急模式 CC 防护，综合源站异常响应情况（超时、响应延迟）和网站历史访问大数据分析，紧急模式决策生成防御策略，实时拦截高频访问请求。自定义 CC 防护可以根据用户访问源 IP 或者 SESSION 频率制定防护规则，对访问进行处置，处置措施包括告警、人机识别和阻断。
>!
>- 紧急模式 CC 防护策略和自定义 CC 规则防护策略，不能同时开启。
>- 使用基于 SESSION 的 CC 防护策略，需要先进行 SESSION 设置，才能设置基于 SESSION 的 CC 防护策略。

## 操作步骤
#### **示例一：紧急模式 CC 防护配置**
紧急模式 CC 防护默认关闭，开启前请确认自定义 CC 防护规则处于未启用状态。
1. 进入 [ Web 应用防火墙控制台](https://console.cloud.tencent.com/guanjia/waf/overview)，在左侧导航栏，选择【实例管理】>【域名接入】选择域名，单击【防护配置】进入配置页面。
![](https://main.qcloudimg.com/raw/707a3e129709d512417e875b2ecb4809.png)
2. 单击【CC 防护设置】，进行紧急模式 CC 防护配置。
![](https://main.qcloudimg.com/raw/12b9dcea8ae59f2954ceafd9e7849b43.png)
**配置项说明：**
**状态开关：** 当开启紧急模式 CC 防护时，若网站遭大流量 CC 攻击会自动触发防护（网站 QPS 不低于1000QPS），无需人工参与。若无明确的防护路径，建议启用紧急模式 CC 防护，可能会存在一定误报。可以在控制台进入 [IP管理-IP封堵状态](https://console.cloud.tencent.com/guanjia/ip/record)，查看拦截 IP 信息，并及时处理。
>?
>- 如果知晓明确的防护路径，建议使用自定义 CC 规则进行防护。
>- CLBWAF 暂不支持紧急模式，请直接使用自定义 CC 进行防护。

#### **示例二： 基于访问源 IP 的 CC 防护设置**
基于 IP 的 CC 防护策略，不需要对 SESSION 维度进行设置，直接配置即可。
1. 进入 [Web 应用防火墙控制台](https://console.cloud.tencent.com/guanjia/waf/overview)，在左侧导航栏，选择【实例管理】>【域名接入】选择域名，找到需要防护的域名，单击【防护配置】进入配置页面。
![](https://main.qcloudimg.com/raw/b44218060a78db08eceeb22570c3582a.png)
2. 单击【CC 防护设置】进行 CC 规则配置，单击【添加规则】填写相应信息。
![](https://main.qcloudimg.com/raw/cb59c16306c765f638454d96377cb307.png)
3. 进入添加 CC 防护规则页面，填写相应信息。
![](https://main.qcloudimg.com/raw/029f2dd3203ffd8338385fe398af2db3.png)

**配置项说明：**
- **规则名称**：CC 防护规则名称，50个字符以内。
- **识别模式**：支持 IP 和 SESSION 识别模式，默认为 IP，SESSION 模式需要提前设置 SESSION 位置信息。
- **匹配条件**：CC 防护规则频率控制匹配条件，默认为 URL。支持设置多个匹配条件，同一规则的多个条件是“与”关系，同时满足才会执行动作，且最多配置10个，需要至少配置URL，详细字段说明如下：

| 匹配字段     | 匹配参数                                                     | 逻辑符号                         | 匹配内容说明                                                 |
| ------------ | ------------------------------------------------------------ | -------------------------------- | ------------------------------------------------------------ |
| URL          | 无                                                           | <li>等于<li>包含<li>前缀匹配               | 必填字段，以/开头，支持目录和具体路径，128字符以内 。          |
| Method       | 无                                                           | <li>等于<li>包含<li>不等于                 | 支持HEAD、GET、POST、PUT、OPTIONS、TRACE、DELETE、PATCH、CONNECT，每次支持输入一个值 。|
| Query        | Query 参数中 key 值                                             | <li>等于                             | Query  需要填写 key-value 组合，填写具体 value 值，512字符以内，可配置多次。 |
| Referer      | 无                                                           | <li>等于<li>包含<li>前缀匹配               | 填写 value 值，512字符以内。                                     |
| Cookie       | Cookie 参数中 key 值                                            | <li>等于<li>包含<li>不等于                 | Cookie 需要填写 key-value 组合，填写具体 value 值，512字符以内。    |
| User-Agent   | 无                                                           | <li>等于<li>包含<li>不等于                 | 填写 value 值，512字符以内。                                     |
| 自定义请求头 | 填写请求头 key 值，如： Accept、Accept-Language ，Accept-Encoding，Connectiton等 | <li>等于<li>包含<li>不等 <li>内容为空 <li>不存在 | 填写具体value值，512字符以内，可配置多次；内容为空或者不存在时，无匹配内容输入框，填写匹配参数即可。 |

- **访问频次**：根据业务情况设置访问频次。建议输入正常访问次数的3倍 - 10倍，例如，网站人平均访问20次/分钟，可配置为60次/分钟 - 200次/分钟，可依据被攻击严重程度调整。
- **执行动作**：默认为拦截，可根据需要进行设置，各个动作详细说明如下：

| 动作类型 | 说明                                                         |
| :------- | :----------------------------------------------------------- |
| 观察     | 符合匹配条件的会话请求将会被监控记录日志，观察结果可在 [攻击日志](https://console.cloud.tencent.com/guanjia/attack) 中查看。 |
| 验证码   | 仅用于浏览器访问场景，符合匹配条件的会话请求将进行验证码挑战，若挑战失败，执行拦截动作。若挑战成功，惩罚时长内正常访问。验证码记录日志为观察。 |
| 精准拦截 | 符合频率控制条件的请求将执行精准拦截，将会拦截该IP对防护 URL 的访问，区别于对整个域名的拦截，可设置惩罚时长，取值为：5分钟 - 10080分钟（7天），拦截结果可在【[攻击日志](https://console.cloud.tencent.com/guanjia/log/attack)】中查看。 |
| 拦截     | 符合频率控制条件的请求将执行拦截，将会拦截该IP对网站所有URL的访问，可设置惩罚时长，取值为：5分钟 - 10080分钟（7天），拦截结果可在【[攻击日志](https://console.cloud.tencent.com/guanjia/log/attack)】中查看，拦截 IP 的实时信息可在【[IP 封堵状态](https://console.cloud.tencent.com/guanjia/ip/record)】中查看。 |

- **惩罚时长**：默认为10分钟，最短为1分钟，最长为一周。
- **优先级**：默认为50，可输入1 - 100的整数，数字越小，代表这条规则的执行优先级越高，相同优先级下，创建时间越晚，优先级越高。


4. 规则操作，选择已经创建的规则，可以对规则进行关闭、修改和删除。
![](https://main.qcloudimg.com/raw/c4b3a5e23cc583009d2a319c394b1def.png)
5. 根据规则设置，触发 CC 攻击行为。
![](https://main.qcloudimg.com/raw/381abed502dc483b2c1ebd1de14ccf26.png)
6. 查看 IP 实时阻断信息。在左侧导航栏，选择【IP 管理】>【IP 封堵状态】 ，可以查看实时阻断的 IP 信息 ,并对 IP 进行加白或者加黑处理。

#### **示例三： 基于 SESSION 的 CC 防护设置**
基于 SESSION 访问速率的 CC 防护，能够有效解决在办公网、商超和公共 WIFI 场合，用户因使用相同 IP 出口而导致的误拦截问题。
1. 进入 [ Web 应用防火墙控制台](https://console.cloud.tencent.com/guanjia/waf/overview)，在左侧导航栏，选择【Web 安全防护】>【防护设置】，进入防护设置页面，在域名列表中，找到需要防护的域名，单击【防护配置】进入配置页面。
![](https://main.qcloudimg.com/raw/a8ee54aa19968970ba6f97d39602301a.png)
2. 选择【CC 防护设置2.0】>【设置】，设置 SESSION 维度信息。
![](https://main.qcloudimg.com/raw/5839e3313206a5449aeeb067f1b26d03.png)
3. 进入 SESSION 设置页面，此示例选择 COOKIE 作为测试内容，标识为 security，开始位置为0，结束位置为9，配置完成后单击【设置】。
![](https://main.qcloudimg.com/raw/602857cecf82505416e26d6566dbb61f.png)
 - **配置项说明：**
 - **SESSION 位置 ：**可选择 COOKIE、GET 或 POST，其中 GET 或 POST 是指 HTTP 请求内容参数，非 HTTP 头部信息。
 - **匹配说明 ：**位置匹配或者字符串匹配。
 - **SESSION 标识 ：**取值标识。
 - **开始位置：**字符串或者位置匹配的开始位置。
 - **结束位置：**字符串或位置匹配的结束位置。
 - **GET/POST 示例 ：**
如果一条请求的完整参数内容为：key_a = 124&key_b = 456&key_c = 789。
	 - 字符串匹配模式下，SESSION 标识为 key_b = ，结束字符为&，则匹配内容为456。
 	- 位置匹配模式下，SESSION 标识为 key_b，开始位置为0，结束位置2，则匹配内容为456。
 - **COOKIE 示例 ：**
如果一条请求的完整 COOKIE 内容为：cookie_1 = 123;cookie_2 = 456;cookie_3 = 789。
 	- 字符串匹配模式下，SESSION 标识为 cookie_2 =，结束字符为“;”，则匹配内容为456。
 	- 位置匹配模式下，SESSION 标识为 cookie_2，开始位置为0，结束位置2，则匹配内容为456。

4. SESSION 维度信息测试。添加完成后，单击【测试】将填写内容进行测试。。
![](https://main.qcloudimg.com/raw/7c5b449d0a04a4caddd2b8a1715f5639.png)
5. 进入 SESSION 设置页面，设置内容为 security = 0123456789……，后继 Web 应用防火墙将把 security 后面10位字符串作为 SESSION 标识，SESSION 信息也可以删除重新配置。
![](https://main.qcloudimg.com/raw/b01ae5205b8b01dbdddee36670e1cff9.png)
6. 设置基于 SESSION 的 CC 防护策略，配置过程和示例一保持一致，识别模式选择 SESSION 即可。
![](https://main.qcloudimg.com/raw/8dbe3f54ff0efca16d83a4731dec36b9.png)7. 配置完成，基于 SESSION 的 CC 防护策略生效。
>!使用基于 SESSION 的 CC 防护机制，无法在 IP 封堵状态中查看封堵信息。

[上一步：DNS 劫持检测](https://intl.cloud.tencent.com/document/product/627)
[下一步：网页防篡改](https://intl.cloud.tencent.com/document/product/627/11710)
