## 简介
此处介绍如何将自定义域名绑定至存储桶中，您可以通过这个自定义域名访问存储桶内文件。

>? 通过 COS 控制台添加自定义域名上限为20个，如您想提高自定义域名的个数上限，请 [提交工单](https://console.cloud.tencent.com/workorder/category) 与我们联系。

### 操作步骤

1. 登录 [对象存储控制台](https://console.cloud.tencent.com/cos5) 。 在左侧导航栏中，单击【存储桶列表】，进入存储桶列表页面。
2. 单击需要配置域名的存储桶，进入存储配置页面，如下图所示：
![自定义源站域名入口](https://main.qcloudimg.com/raw/8a4ceacd4892f0f9f660a6f6fa9dacd0.png)
3. 单击上方的【域名管理】，找到**自定义源站域名**栏后，单击【添加域名】。如果您的自定义域名已经在工信部 [备案](https://cloud.tencent.com/product/ba) 且在 域名服务添加解析，您可以直接将您的自定义域名填写至【域名】输入框后，然后单击【保存】即可。
![](https://main.qcloudimg.com/raw/9c1b6532351fc4c0d1daf9fba724a55e.png)


### 新旧版本控制台差异	
当前新旧版本控制台的存储桶域名有所差别，以广州地域为例，新版本控制台的存储桶地域简称为 `ap-guangzhou`，旧版本存储桶则是 `cosgz`。有关域名详情请参阅 [地域和访问域名](https://intl.cloud.tencent.com/document/product/436/6224)。	

 由于域名的差异，您在使用自定义源站域名时需要注意 CNAME 的配置。我们**推荐**您使用新版本的存储桶域名作为 CNAME，相较于旧版本的存储桶域名，使用新版本域名作为 CNAME 可以进行更丰富的操作。	

 您可以到您的 DNS 厂商处修改您的 CNAME 信息：	
- 如果您的 DNS 厂商是腾讯云，可以前往 [腾讯云域名解析控制台](https://console.cloud.tencent.com/domain) 配置。	
- 如果您的 DNS 厂商是阿里云，可以前往阿里云域名解析控制台配置。	
- 如果您的 DNS 厂商是亚马逊云，可以前往亚马逊云域名解析控制台配置。	

>!除了域名差异外，新旧版本控制台所调用的 API 也存在差异，我们**推荐**您使用新版本控制台以及使用新版本 API、工具、SDK，因为这能够让您体验更加丰富和稳定的功能。COS 新版本控制台所调用的操作对象或存储桶的 API 是 XML API，旧版本控制台上调用的则是 JSON API，有关新旧两个版本 API 的差异，可参阅 [API 常见问题](https://intl.cloud.tencent.com/document/product/436/10687)。
