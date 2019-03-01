[//]: # (chinagitpath:XXXXX)

## Overview
When forwarding a message field extracted through a rule to a third-party service, you can customize how to process the data. This is the most flexible way for you to process the message. Please note that the third-party service must be HTTP-based. To configure the forwarding to third-party services, you need to provide an HTTP-enabled URL and port number.

The figure below shows the entire process of forwarding data to a third-party service:
![image](https://mc.qcloudimg.com/static/img/b24d804514c29ee7f8810130e9cf6771/service_http2.png)
## Configuration
1. Log in to the [Rule Engine](https://console.cloud.tencent.com/iotcloud/rules/rule) console page and click the rule you want to configure.
![](https://main.qcloudimg.com/raw/0a0a0e5bc48aa0d4492ac0b8d3c7413c.png)
2. On the rule details page, click the **Add Action** button. In the pop-up "Add Action" window, select the action "forward", enter your own HTTP service address and click **Create**. The IoT Hub platform will forward the data reported by the device to the HTTP service address.
![image](https://main.qcloudimg.com/raw/8bd5aa126ed065559667f9880850ba26.png)

