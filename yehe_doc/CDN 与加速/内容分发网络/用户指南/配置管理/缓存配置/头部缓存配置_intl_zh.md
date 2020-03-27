
## 配置场景
除资源内容外，腾讯云 CDN 默认会缓存以下来自于源站的头部，并返回给用户：
+ Access-Control-Allow-Origin
+ Timing-Allow-Origin
+ Content-Disposition
+ Accept-Ranges

若您的源站存在特殊头部，需要 CDN 进行缓存并返回给用户，可通过开启头部缓存配置实现。

## 配置指南
### 查看配置
登录 [CDN 控制台](https://console.cloud.tencent.com/cdn)，在菜单栏里选择【域名管理】，单击域名右侧【管理】，即可进入域名配置页面，第三栏【缓存配置】中可看到 HTTP 头部缓存配置，默认情况下为关闭状态。
![](https://main.qcloudimg.com/raw/6020723bafae2e222d8c5e01bf1db0b2.png)

### 修改配置
可以直接单击开关按钮关闭或开启 HTTP 头部缓存配置，配置下发全网生效时间大约为5分钟：
![](https://main.qcloudimg.com/raw/1324a75f35cad0f0b80427a50137aad1.png)

>
> + 若您的加速域名服务区域为全球加速，设置的参数缓存配置会全球生效，不支持境内、境外差异化配置。
> + 头部缓存配置正在全网升级中，若您单击关闭时提示错误，可能由于升级导致，可 [联系我们](https://intl.cloud.tencent.com/support) 进行后台配置项关闭。





