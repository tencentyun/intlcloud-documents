使用 HTTP/HTTPS 监听器后，源站可直接从 HTTP 请求头中 X-Real-IP 或 X-Forwarded-For 字段中获取客户端真实 IP，此为默认生效功能。

同时支持从 [“回源 HTTP 请求头配置”](https://intl.cloud.tencent.com/document/product/608/17539) 自定义，若从源站到程序还有中间链路 (如 CLB,自建 nginx)，则需要自行配置，以防字段被中间链路覆盖。

