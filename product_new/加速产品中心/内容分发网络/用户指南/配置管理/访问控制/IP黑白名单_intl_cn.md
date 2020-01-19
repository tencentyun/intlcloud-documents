CDN 为您提供了 IP 黑白名单配置功能，您可以根据业务需要对用户请求的源 IP 配置过滤策略，帮助您解决恶意 IP 盗刷、攻击等问题。

## 配置指引
1. 登录 [CDN 控制台](https://console.cloud.tencent.com/cdn)，单击左侧目录的【域名管理】，进入管理页面，在列表中找到您需要编辑的域名所在行，单击操作栏的【管理】。
![img](https://main.qcloudimg.com/raw/9c13a263df1ccc5cc15f2d19a5476e37.png)
2. 单击【访问控制】选项卡，可以在 IP 黑白名单配置模块进行配置。默认情况下，IP 黑白名单未启用，无黑 / 白名单。
![img](https://main.qcloudimg.com/raw/daf36d387ba9b2e74ebf83214321f870.png)
	- IP 黑名单、白名单二者不兼容，同一时间只能生效一种类型。黑名单最多可输100条，白名单最多可输入50条，以换行符相隔，一行输入一个。
	- 目前仅支持如下格式的网段：/8、/16、/24，其他网段格式暂不支持。当 IP 黑名单、白名单输入内容均为空时，表示当前未开启 IP 黑白名单功能。

### 白名单配置
1. 单击【编辑】，默认选中【IP 白名单】，可进行 IP 白名单配置。
   在输入框中输入名单并提交，即可开启 IP 白名单功能，仅当客户源 IP 匹配列表中的 IP 或 IP 段时，访问能够正常返回所请求的内容，其他请求均直接返回403。
![img](https://main.qcloudimg.com/raw/be099978810fec15c883c8745d8a331b.png)
2. 配置完成后，开关为开启状态，下方显示正在生效的 IP 白名单配置信息。单击【编辑】可更改配置信息。
![img](https://main.qcloudimg.com/raw/12e3102f0ab79650a41ada6e3a008648.png)
3. 关闭 **IP 黑白名单**开关后，下方的配置信息失效，即 IP 黑白名单未启用。可再次手动开启。
![img](https://main.qcloudimg.com/raw/9ee22e5632a51a8e5ad5a7030aec80b5.png)

### 黑名单配置

1. 单击【编辑】，选中【IP 黑名单】，可进行黑名单配置。
   在下方输入框中输入名单并提交后，即开启了 IP 黑名单功能，当客户源 IP 匹配列表中的 IP 或 IP 段时，访问直接返回403，其他访问能够正常返回所请求内容。
![img](https://main.qcloudimg.com/raw/361066912bd61b86fcda7ba31596fda6.png)
2. 配置完成后，开关为开启状态，下方显示正在生效的 IP 黑名单配置信息。单击【编辑】可更改配置信息。
![img](https://main.qcloudimg.com/raw/b6a6763732006e229730865b4403c3f2.png)
3. 关闭 **IP 黑白名单**开关后，下方的配置信息失效，即 IP 黑白名单未启用。可再次手动开启。
![img](https://main.qcloudimg.com/raw/cb843154d275ee9c899bb125f33f5d0d.png)

## 配置案例
若域名`www.test.com`的 IP 黑白名单配置如下：
![img](https://main.qcloudimg.com/raw/4116aa2143c33c9bbbb7eba1a0897a7e.png)
则：
- IP 为 `1.1.1.1`的用户访问资源 `http://www.test.com/1.jpg`，匹配白名单，正常返回内容。
- IP 为`2.2.2.2` 的用户访问资源 `http://www.test.com/1.jpg`，未匹配白名单，返回403。
