## 如何停用 CLS 服务或停止计费？

日志服务（Cloud Log Service，CLS）无一键停用服务的功能。若您不再使用 CLS 服务，您可以选择将您的日志主题等资源完全删除以避免继续计费，无需注销账号（如有使用其他腾讯云服务，注销账号会受到影响）。

CLS 的计费是后付费模式，所以您删除资源后的第二天可以查询相关资源的计费情况。如下图9月16日可以查看9月15日的账单：
![](https://qcloudimg.tencent-cloud.cn/raw/5467f1c6122851224c6d45b09ffd74c0.png)

## 删除所有的日志主题

>! Demo 日志主题不会产生费用，可以放心体验。
>

1. 登录日志服务控制台，在 [概览](https://console.cloud.tencent.com/cls/overview) 页面查看各地域资源统计情况，找到存在日志主题的地域，**单击该日志主题数**，进入日志主题管理页面。
![](https://qcloudimg.tencent-cloud.cn/raw/d0a058b920d887da4ef57f87cc0b0958.png)
2. 在 [日志主题](https://console.cloud.tencent.com/cls/topic) 管理页面，单击日志主题后**删除**，删除所有地域的所有日志主题。
您可选择左上角的地域，切换到其他有资源的地域。
![](https://qcloudimg.tencent-cloud.cn/raw/d5f4e82f35a98690bf163290fd5a3962.png)
3. 返回 [概览](https://console.cloud.tencent.com/cls/overview) 页面，再次查看日志主题数，确认日志主题数为0，即表示日志主题资源清理完成，不再产生相关费用。


## 相关链接

- 关于 CLS 的欠费停服策略：数据的保留和销毁时间、以及相关计费说明，可参见 CLS [欠费说明](https://intl.cloud.tencent.com/document/product/614/50246)。
- 若您对 CLS 计费仍有疑问，可参见计费 [常见问题](https://www.tencentcloud.com/document/product/614/50265) 寻求答案。
