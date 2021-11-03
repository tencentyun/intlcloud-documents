## 新增通道

1. 登录 [全球应用加速控制台](https://console.cloud.tencent.com/gaap)，进入“接入管理”页面，单击**新增**。
2. 在弹出的窗口中，填写通道信息。
![](https://main.qcloudimg.com/raw/d30c08d1cf9dedb12ed805bf731e073f.png)
   
   - 项目：该通道所属项目（后续可以更换项目）。
   - 通道名称：最多30个字符，支持中英文、常规符号。
   - IP版本：可根据需要选择 IPv4 或 IPv6，其中 IPv6 暂时只支持国内区域。
   - 接入节点：选择客户端所在区域或距离客户端最近区域的节点。
   <blockquote class="d-mod-notice">
   						<div class="d-mod-title d-notice-title">
   							<i class="d-icon-notice"></i>注意：
   						</div>
               <p>中国香港提供精品 BGP 网络，如有需要，可通过工单联系我们。</p>
               <p>中国大陆提供三网节点网络，如有需要，可通过工单联系我们。</p>
   					</blockquote>
   - 回源节点：选择目标服务器所在区域或距离目标服务器最近区域的节点。
   <blockquote class="d-mod-notice">
   						<div class="d-mod-title d-notice-title">
   							<i class="d-icon-notice"></i>注意：
   						</div>
               <p>中国台湾无法与中国大陆进行直连。</p>
   					</blockquote>
   - 带宽上限：通道的带宽上限，最大值10000Mbps（部分通道最大值为1000Mbps）。
   - 并发上限：通道的最大并发连接数，最大值100万（部分通道最大值为30万）。
   - 标签：非必填项，可通过设置标签实现对通道的分类管理；
   - 费用：根据您选择的带宽与并发数，下方会给出相应的通道费和带宽费。
     a.通道费：按日计算，直到通道被删除为止，请特别注意通道创建后未满一天删除也会按一天计费；
     b.带宽费：按每日实际出入带宽峰值计费。
3. 单击**确定**，完成新增通道。
4. 在“接入管理”页面中，查看通道列表信息。
![](https://main.qcloudimg.com/raw/b326c683b47321704d0269a0eb047f2d.png)
   
   - ID/通道名：通道的 ID 和名字，其中通道名可以修改。
   - VIP：用于客户端访问的接入 IP 地址。
   - 域名：用于客户端访问的接入域名（系统分配，且自动绑定到 VIP）。
   - 状态：仅“运行中”状态下，加速通道才可以正常使用。

## 查看通道信息

1. 登录 [全球应用加速控制台](https://console.cloud.tencent.com/gaap)，进入“接入管理”页面，单击指定通道的 **ID/通道名**，进入下一级页面。
![](https://qcloudimg.tencent-cloud.cn/raw/dba1d1cb841d8575a1b653c9d47f640b.png)
2. 在“通道信息”标签页，可以查看通道的详细信息。其中，“转发 IP”是指加速通道末端的转发节点 IP，该转发节点负责将加速通道的数据通过公网转发给源站。如果您希望多条通道使用同一个域名，可单击**未关联**跳转至 [统一域名](https://console.cloud.tencent.com/gaap/domain) 页面进行配置。<br>
<img src="https://main.qcloudimg.com/raw/0f3097be7c9bb138d4287683a97863d1.png" width="50%">
