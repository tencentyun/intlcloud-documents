## 什么是腾讯云验证码
腾讯云天御验证码，基于轨迹分析、特征发现、反模拟器等多重安全防御策略，为网页、APP开发者提供全面、立体的人机验证服务，保护企业在注册登录、活动秒杀、点赞发帖、数据保护等各大场景下的业务安全。

验证码服务可以帮助您解决以下业务安全问题：

- 登录注册：有效防止撞库攻击、阻止注册机批量注册小号。
- 活动秒杀：有效拦截刷单操作，防止自动机刷取福利券。
- 点赞发帖：有效解决广告屠版、恶意灌水、刷票问题。
- 数据保护：有效防止自动机、爬虫盗取网页内容和数据。

## 产品功能
### 滑块验证码

用户轻轻一滑，完成图片拼图操作，即可快速通过验证。滑动拼图操作简单，风控能力强，适用于大部分人机识别验证场景。
![](https://qcloudimg.tencent-cloud.cn/raw/54a2f521f5dd2df8093be42e80791b58.png) 

### 智能免验证

智能识别用户特征，可疑用户需要回答验证问题，可信用户直接跳过验证操作，大幅提升真实用户的使用体验。验证流程如下：

![](https://qcloudimg.tencent-cloud.cn/raw/a9ab053404da39b55aa221c58554dbf6.png)

### 立体防御

验证码验证过程中，通过动态加密、虚拟机加固、反模拟器等十道安全防御策略，层层对抗和阻拦黑产破解。

#### 风控等级可控

验证码支持三种风控等级：体验优先、平衡、安全优先，满足不同场景下的风控需求。

![](https://qcloudimg.tencent-cloud.cn/raw/5bfbe8fe70ada4e6feb5014ad304f95b.png)

#### 防御效果

验证码基于多重防御策略，自动拦截恶意用户请求。

| 待验证                                                       | 可信用户：验证成功                                           | 恶意用户：验证拦截                                           |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| <img src="https://qcloudimg.tencent-cloud.cn/raw/bc1fdebc5f9affaf7146c45a54ca02de.png" style="zoom:80%;" /> | <img src="https://qcloudimg.tencent-cloud.cn/raw/60827077028e0df8fe82cf5fd1668717.png" style="zoom:80%;" /> | ![](https://qcloudimg.tencent-cloud.cn/raw/b5d305d285d10ea6b1a4d0b0b3056c65.png) |

### 数据统计

分钟级数据指标统计，实时掌控业务安全动态。

<table class="tg">
<thead>
  <tr>
    <th class="tg-0pky">指标名称</th>
    <th class="tg-0pky">指标说明</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-0pky">请求量</td>
    <td class="tg-0pky">客户端加载验证的次数</td>
  </tr>
  <tr>
    <td class="tg-0pky">验证量</td>
    <td class="tg-0pky">用户回答验证问题后，发起验证的次数</td>
  </tr>
  <tr>
    <td class="tg-0pky">验证通过量</td>
    <td class="tg-0pky">验证通过的次数</td>
  </tr>
  <tr>
    <td class="tg-0pky">验证拦截量</td>
    <td class="tg-0pky">验证未通过，被拦截的次数</td>
  </tr>
  <tr>
    <td class="tg-0pky">答案错误拦截量</td>
    <td class="tg-0pky">因答案错误导致验证被拦截的次数</td>
  </tr>
  <tr>
    <td class="tg-0pky">安全策略打击拦截量</td>
    <td class="tg-0pky">因安全策略打击导致验证被拦截的次数</td>
  </tr>
  <tr>
    <td class="tg-0pky">票据校验量</td>
    <td class="tg-0pky">服务端发起票据校验的次数</td>
  </tr>
  <tr>
    <td class="tg-0pky">票据校验通过量</td>
    <td class="tg-0pky">票据校验通过的次数</td>
  </tr>
  <tr>
    <td class="tg-0pky">票据校验拦截量</td>
    <td class="tg-0pky">票据校验未通过的次数</td>
  </tr>
</tbody>
</table>

## 产品限制

### 并发请求限制

1. 验证码票据校验**每秒并发请求量**（QPS）限制为：1000。
2. 业务调用票据校验API每秒并发量超出1000时：**调用票据校验接口将报错**（RequestLimitExceeded）。
3. 若需要调整并发量限制，请提交工单，或通过商务，联系我们。

## 常见问题

更多产品功能问题，详情参见 [功能相关问题](https://intl.cloud.tencent.com/document/product/1159/49691)。
