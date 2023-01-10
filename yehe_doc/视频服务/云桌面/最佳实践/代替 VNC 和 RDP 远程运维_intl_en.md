## Using CVD Instead of VNC and RDP for Remote Desktop Ops
CVD offers quick, on-demand virtual desktop solutions with security guaranteed by encrypted adaptive transfer protocols and policies. You can use CVD for convenient Ops and secure development in place of VNC and RDP and boost the security and continuity of your business access.

### Convenient Ops and secure R&D architecture of CVD
![](https://staticintl.cloudcachetci.com/yehe/backend-news/e7Kd435_PRELIM__%E4%BA%91%E6%A1%8C%E9%9D%A2%E4%BA%A7%E5%93%81%E7%9B%AE%E5%BD%95_%E4%B8%AD%E8%AF%91%E8%8B%B1_EN-US-6.png)

### Feature Comparison of CVD, VNC, RDP, and WebRDP
CVD can implement various features such as batch creation, security control, and convenient access, as compared with VNC, RDP, and WebRDP:

| Item | VNC | RDP | WebRDP | CVD |
| ------------------------------------------- | ------ | ------ | ------ | :--------- |
| Access terminal | HTML5 | Client | HTML5 | HTML5 or client |
| Access latency | High | Medium | Medium | Low |
| EIP required | No | Yes | Yes | No |
| Shortcut operations such as copy and paste | Not supported | Supported | Supported | Supported |
| File transfer | Not supported | Supported | Not supported | Supported |
| Adaptive resolution | Not supported | Supported | Supported | Supported |
| Access to internal resources over the private network | Supported | Supported | Supported | Supported |
| Access to GPU desktops | Not supported | Supported | Supported | Supported |
| Access to Linux desktops | Supported | Supported | Supported | Supported |
| Security policies such as watermark | Not supported | Not supported | Not supported | Supported |
| Restricting access to special users | Not supported | Not supported | Not supported | Supported |
| Restricting access to users with specified IDs or in specified regions | Not supported | Not supported | Not supported | Supported |
| Two-factor authentication | Not supported | Not supported | Not supported | Supported |
| SDK (for inheriting services to internal Ops platform) | Not supported | Not supported | Not supported | Supported |


### Examples of connecting CVM from CVD
#### Prerequisites
- The CVD and CVM instances are in the same VPC or have been interconnected over the private network through [CCN](https://www.tencentcloud.com/products/ccn).
- The CVD instance has been purchased and assigned, and end users can log in to the instance normally. For more information, see [Access Guide](https://www.tencentcloud.com/document/product/1167/51902).
- The CVD IP address and required port have been opened in the security group of the CVM instance. For more information, see [Common Server Ports](https://intl.cloud.tencent.com/document/product/213/12451).


#### Example 1: Connecting Windows CVM from CVD
![](https://qcloudimg.tencent-cloud.cn/raw/e3776805217e88ec9a0f1aea30508280.png)

#### Example 2: Connecting Linux CVM from CVD
![](https://qcloudimg.tencent-cloud.cn/raw/bd43ba32fa29dda29c4fc26def6077f3.png)



