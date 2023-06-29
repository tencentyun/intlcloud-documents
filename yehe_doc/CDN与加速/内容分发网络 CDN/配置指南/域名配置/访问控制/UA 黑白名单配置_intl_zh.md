## 配置场景

腾讯云 CDN 支持通过配置 User-Agent 黑白名单规则实现访问控制。
通过对用户 HTTP 请求头中的 User-Agent 进行规则判断，按需放行或拒绝用户访问。

## 配置指南

### 配置约束

- 仅支持全部设置为黑名单或全部设置为白名单，不支持同时设置黑、白名单规则。
- 最多可配置 10 条黑或白名单规则。
- 规则内容支持通配符`*`，多个值情况下使用 `|`分隔。
- 生效类型支持全部文件、文件类型、文件目录、指定文件路径四种模式，暂不支持正则匹配。

### 配置说明

登录 [CDN 控制台](https://console.cloud.tencent.com/cdn)，在菜单栏里选择【域名管理】，单击域名右侧【管理】，即可进入域名配置页面，第二栏【访问控制】中可看到 UA 黑白名单配置，默认情况下为关闭状态：
![](https://main.qcloudimg.com/raw/07914bd30b3d422fb4bddf3a323d92f2.png)
关闭状态下，单击【新增规则】，可按需逐条添加黑(白)名单：
![](https://main.qcloudimg.com/raw/66d3fc72f575efaa4ae42382d8fde179.png)

>!
>1. 仅支持通配符`*`，暂时不支持其他正则表达式。
>2. 无`*`情况下，其他字符均为完全匹配。
 
规则添加完成后，此时整体配置为关闭状态，因此不会影响现网服务：
![](https://main.qcloudimg.com/raw/679129885ec36329178e87af671d6743.png)
可通过单击【开启】按钮，将所配置的黑(白)名单发布至现网：
![](https://main.qcloudimg.com/raw/fd85de8e702b24e7d2eaaf8b34667c95.png)

## 配置示例

若加速域名`cloud.tencent.com`的 UA 黑白名单配置如下：
![](https://main.qcloudimg.com/raw/c7e06060bc627aab2e4939b53460951d.png)
当 HTTP Request Header 中 User-Agent 如下时：

```
user-agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.61 Safari/537.36
```

命中黑名单，将直接返回403。

