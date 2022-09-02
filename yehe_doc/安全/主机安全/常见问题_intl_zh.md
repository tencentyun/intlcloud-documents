本文将为您介绍主机安全的常见问题。

## 购买相关
[](id:RHGMYZJAQZYB)
### 如何购买主机安全专业版与旗舰版？
请参见 [购买防护授权](https://intl.cloud.tencent.com/document/product/296/48331)。

### 主机安全产品是否与其他安全产品冲突？
主机安全与其他安全产品并不冲突，属于不同的防护维度，通过在不同的层面上提供安全能力，保障用户安全。

### 如何关闭主机安全专业版或旗舰版防护？
登录 [主机安全控制台](https://console.tencentcloud.com/cwp) ，在左侧导航栏中，选择 **授权管理**，搜索需要关闭专业版或旗舰版的主机，操作列中点击**解绑**操作，即可以关闭专业版或旗舰版服务。请参见 [授权管理](https://console.tencentcloud.com/cwp/setting/authorize)。

### 如何卸载腾讯云服务器主机安全客户端?
登录 [主机安全控制台](https://console.tencentcloud.com/cwp)，在左侧导航栏选择 **主机列表**，找到您要卸载的主机，单击操作列**卸载**操作，即可卸载（约10分钟后会同步最新状态）。

## 功能相关
### 病毒库及漏洞库更新周期是多久？
病毒库：每日零点更新。
漏洞库：不定时更新。

### 为什么Jar包类的漏洞多次扫描时，每次检测结果可能不一致？
Jar 包类漏洞，例如 struts2 漏洞的检测依赖 Jar 包运行态是否加载，未运行服务时是不能检测到漏洞的，运行服务时 Webserver 对于Jar 包的加载分为动态加载和静态加载。在动态加载模式下，struts2 漏洞只有在 Jar 包运行时才能被检测出来，所以每个时段检测结果存在差异。建议您针对高危 Jar 包漏洞进行多次检测，提升检测结果的准确度。

### 在文件查杀功能中，文件的扫描频率是多少？
文件的扫描频率可由用户自行配置，请参见 [文件查杀](https://intl.cloud.tencent.com/document/product/296/13008)。

### 安全评分机制是怎样的？
请参见 [安全评分说明](https://intl.cloud.tencent.com/document/product/296/49373) 。

### 安全基线在产品设置过后，多久可以生效？
安全基线在产品设置后，即时生效。

### 主机安全基线检测“未通过”怎么处理？
1. 进入 [基线管理](https://intl.cloud.tencent.com/document/product/296/45862) ，筛选未通过的检测项，单击**查看详情**，打开检测项详情弹窗。
![](https://qcloudimg.tencent-cloud.cn/raw/3c43d5f355b502f4f8a544587b920672.png)
2. 在检测项详情弹窗中，可见当前受影响的服务器，单击某服务器操作列的**详情**，打开检测结果弹窗。
![](https://qcloudimg.tencent-cloud.cn/raw/6fe28add56b1f6c2757370e11ef017da.png)
3. 在检测结果弹窗中，可查看基线修复建议。
![](https://qcloudimg.tencent-cloud.cn/raw/849fd2ec448f52acad8f5c78aab238f2.png)


### 主机安全发现漏洞木马等攻击是否会进行通知？
会。若主机安全发现木马、应急漏洞或者其他攻击的行为，会通过站内信、短信、邮件或企业微信方式的方式进行告警通知，您可在 [告警设置](https://console.tencentcloud.com/cwp/setting)中设置。

