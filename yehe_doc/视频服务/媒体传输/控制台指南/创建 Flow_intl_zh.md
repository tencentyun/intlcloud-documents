在控制台[Flow Management](https://console.tencentcloud.com/mdc/flow)页面，点击左上角的**Create Flow**按钮创建Flow。
![](https://qcloudimg.tencent-cloud.cn/raw/b7ea1765ad2384f3b2c5ceeef2a76ce7.png)

在跳转后的页面中，您需要填写流名称（Flow Name）、流的最大码率、Input相关信息。
- **Name**：Flow名称，您可以填写一个简单的名称，方便您管理多个Flow信息。
- **Max Bandwidth**：选择您的流的最大码率，系统会据此为您分配网络资源。
- **Source Name**：源名称，您可以填写一个简单的名称，方便管理。
- **Protocol Type**：推流协议，目前支持协议 RTMP、SRT、RTP、RTSP。

## RTMP
若选择此协议，您需要将流推送到系统生成的推流地址上。可以在Flow列表页查看推流地址。
![](https://qcloudimg.tencent-cloud.cn/raw/74cf0e4bb392f4474261703eec7974ea.png)

- **Failover**：容灾功能，若开启容灾，系统将会生成两个推流地址，您可以同时推送两路流到StreamLink。 先收到的流将会作为主路生效，主路断开后将会自动切换到另外一路。
- **CIDR IP Allowlist**：IP 白名单，用于限制推流使用的IP ，以此增强安全性。示例： 203.3.3.3/28. 如需输入多个，请使用分号隔开，示例：203.3.3.3/28;202.3.3.3/28。


## RTMP_PULL
若选择此协议，StreamLink将从您指定的流地址拉流。
![](https://qcloudimg.tencent-cloud.cn/raw/751d78b56498ba5d9eafaddb8bdccf57.png)

- **Source Address**：RTMP Url, 示例：rtmp://example.com/live。
- **Source Key**：RTMP流密钥， 示例： e18c3c4dd05aef020946e6afbf9e04ef。
- **Failover**：目前此协议不支持容灾切换，故此选项暂不开放，敬请期待。

## SRT Listener
![](https://qcloudimg.tencent-cloud.cn/raw/30760bb8411f2a14bb630b3eb3cd8637.png)
- **Mode**：选择Listener模式，此模式下，您需要在推流侧使用SRT的Caller模式请求Streamlink，并推送流到Input节点。具体地址，您可以在Flow列表页查看。
- **Latency Setting**：设置服务侧Latency参数，若推流侧和StreamLink的区域在同一个国家，建议设置为120ms；若推流侧和 Stream Link 的区域在不同的国家建议设置 200ms；若推流侧和 Stream Link 的区域在不同的洲建议设置 1000ms；具体可以根据分配的 IP 进行实际调整。
- **Decryption Settings**：如果您需要更高的安全性，您可以使用SRT的加密功能。需要您在此处打开开关，并填写Decryption Key以及Key Length两个字段。同时，您需要在推流侧设置加密KEY以及kEY的长度，否则您将推流失败。
  - **Decryption Key**：开启加密后，您需要在此字段填写用于加密和解密的key，同时需要在推流侧设置相同的key。
  - **Key Length**：开启加密后，您需要在此字段选择加密key的长度，推流侧参数需要与此处保持一致。
- **Failover**：目前此协议不支持容灾切换，故此选项暂不开放，敬请期待。
- **CIDR IP Allowlist**：IP 白名单，用于限制推流使用的 IP ，以此增强安全性。示例： 203.3.3.3/28. 如需输入多个，请使用分号隔开，示例：203.3.3.3/28;202.3.3.3/28。

## SRT Caller
![](https://qcloudimg.tencent-cloud.cn/raw/b8a8ae4e50e6375b635795c4d60e2577.png)
- **Mode**：选择Caller模式，此模式下，StreamLink将使用SRT协议Call您提供的源流地址，以此获取源流。
- **Source IP**：您源流的IP地址，此处也可以填写域名。
- **Source Port**：您源流地址的端口。
- **Latency Setting**：设置服务侧Latency参数，源流地址和StreamLink的区域在同一个国家，建议设置为120ms；源流地址和StreamLink的区域在不同的国家建议设置200ms；源流地址和StreamLink的区域在不同的洲建议设置1000ms；具体可以根据分配的 IP 进行实际调整。
- **Decryption Settings**：如果源流开启了加密，则需要打开此开关，并填写Decryption Key以及Key Length两个字段，否则将拉流失败。
  - **Decryption Key**：如果您的源流开启了加密，您需要在此字段填写相关的key，否则将拉流失败。
  - **Key Length**：如果您的源流开启了加密，您需要在此字段选择Key的长度，长度需要和源流设置的长度保持一致。
- **Failover**：目前此协议不支持容灾切换，故此选项暂不开放，敬请期待。

## RTP
若选择此协议，您需要将流推送到系统生成的推流地址上。您可以在Flow列表页查看推流地址。
![](https://qcloudimg.tencent-cloud.cn/raw/1e91a938d681e46e48ec8bb7405df2c4.png)

- **Failover**：目前此协议不支持容灾切换，故此选项暂不开放，敬请期待。
- **CIDR IP Allowlist**：IP 白名单，用于限制推流使用的 IP ，以此增强安全性。示例： 203.3.3.3/28. 如需输入多个，请使用分号隔开，示例：203.3.3.3/28;202.3.3.3/28。