## Output管理
在控制台[Flow Management](https://console.tencentcloud.com/mdc/flow)页面，在列表中点击某一条Flow，即可查看该Flow的详细信息。
![](https://qcloudimg.tencent-cloud.cn/raw/6e157c3ffc610bcf01c247a441a538cd.png)
进入Flow信息页后，您可以在页面上方点击**Output**，进入Output管理页面，在此页面可以对 Output进行添加、删除、编辑的操作。
![](https://qcloudimg.tencent-cloud.cn/raw/ddfed18e28122e9198549541d3ebfd70.png)


## 创建Output
您可以点击**Create Output**按钮添加Output。点击后，页面会弹出一个窗口，填写相关信息之后便可点击**Confirm**完成Output的添加。
![](https://qcloudimg.tencent-cloud.cn/raw/e9b1da7a805b27d5dcfa452775e7461d.png)

- **Output Name**：Output名称，您可以填写一个简单的名称，方便您管理多个Output信息。
- **Output Region**：Output所在区域，在这里选择您将流传输到的区域。
- **Output Protocol**：需要选择Output的传输协议，不同的协议需要的设置不同。

  | Input 协议 | Output 可选协议 |
  | -----------| ---------------|
  | RTMP、RTMP_PULL       | RTMP 、RTMP_PUSH、RTMP_PULL|
  | SRT         | SRT、RTMP_PUSH|
  | RTP         | RTP        |
  | RTSP        | RTSP       |
  

### RTMP_PUSH
若选择此协议， Output会将流转推到您指定的地址。
![](https://qcloudimg.tencent-cloud.cn/raw/1a379f8a32e9ca1bd5341ade3a24912b.png)

- **Destination URL**：RTMP Url, 示例：rtmp://example.com/live。
- **Flow Key**：RTMP流密钥，示例： e18c3c4dd05aef020946e6afbf9e04ef。


### RTMP_PULL
若您需要从Output拉流，则可以在Output中选择此协议。创建Output后，您可以在Output列表中获取拉流地址。
![](https://qcloudimg.tencent-cloud.cn/raw/678b8da18059dec35579f1515c91e1ff.png)

- **CIDR IP AllowList**：IP白名单，用于限制推流使用的IP，以此增强安全性。示例： 203.3.3.3/28. 如需输入多个，请使用分号隔开，示例：203.3.3.3/28;202.3.3.3/28。

### SRT Listener
![](https://qcloudimg.tencent-cloud.cn/raw/13071f72fe033f1a82b1bba87c7b7a56.png)
- **Mode**：选择Listener模式，您需要在接收侧使用SRT Call模式，请求Output。拉流地址展示在Output列表页。
- **Latency Setting**：设置服务侧Latency参数，若推流侧和StreamLink的区域在同一个国家，建议设置为120ms；若推流侧和 StreamLink的区域在不同的国家，建议设置为200ms；若推流侧和StreamLink的区域在不同的洲建议设置1000ms；具体可以根据分配的 IP 进行实际调整。
- **Enable Encryption**：如果开启了加密，您在接收侧也需要开启加密，并填写 Encryption Key 以及 Key Length 两个字段，否则将拉流失败。
  - **Encryption Key**：您需要在此字段填写相关的key，用于加密。
  - **Key Length**：您需要在此字段选择Key的长度。
- **Failover**：目前此协议不支持容灾切换，故此选项暂不开放，敬请期待。
- **CIDR IP Allowlist**：IP白名单，用于限制推流使用的 IP ，以此增强安全性。示例： 203.3.3.3/28. 如需输入多个，请使用分号隔开，示例：203.3.3.3/28;202.3.3.3/28。

### SRT Caller
![](https://qcloudimg.tencent-cloud.cn/raw/254cb4af2ca2e3d27be2f0ff724b02f4.png)
- **Mode**：选择Caller模式，此模式下，StreamLink将使用SRT协议Call您提供的接收地址，以此将流传送到您指定的地址。
- **Destination**：接收SRT推流的IP地址，此处也可以填写域名。
- **Port**：接收SRT推流的端口。
- **Latency Setting**：设置服务侧Latency参数，源流地址和StreamLink的区域在同一个国家，建议设置为120ms；源流地址和StreamLink 的区域在不同的国家建议设置 200ms；源流地址和StreamLink的区域在不同的洲建议设置1000ms；具体可以根据分配的IP 进行实际调整。
- **Enable Encryption**：如果接收侧开启了加密，则需要打开此开关，并填写Encryption Key以及Key Length两个字段，否则Output将推送失败。
  - **Encryption Key**：您需要在此字段填写相关的key，用于加密。
  - **Key Length**：您需要在此字段选择Key的长度，长度需要和接收侧设置的长度保持一致。
- **Failover**：目前此协议不支持容灾切换，故此选项暂不开放，敬请期待。


### RTP
若选择此协议，Output会将流推送到您指定的地址。
![](https://qcloudimg.tencent-cloud.cn/raw/4cca576a3a1da76f0e2a2a4ab7d80b48.png)

- **Destination**：Output会将流推送到您指定的地址。
- **Output Protocol**：目前Output传输协议的选择，强依赖于Input的协议。