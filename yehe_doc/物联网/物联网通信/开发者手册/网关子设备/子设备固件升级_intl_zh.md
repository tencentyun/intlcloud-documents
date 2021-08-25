## 操作场景

当网关子设备有新功能或者需要修复漏洞时，子设备可以通过设备固件升级服务快速的进行固件升级。


## 实现原理

固件升级的过程中，需要网关代子设备使用下面两个 Topic 来实现与云端的通信，如下图所示：
![OTA topic](https://main.qcloudimg.com/raw/88d82dafcafc9e2ccf162e8828e9474e.png)

示例代码如下：
```php
$ota/report/${productID}/${deviceName}
用于发布（上行）消息，设备上报版本号及下载、升级进度到云端
$ota/update/${productID}/${deviceName}
用于订阅（下行）消息，设备接收云端的升级消息
```


## 操作流程

以 MQTT 为例，子设备的升级流程图如下所示：
>?固件升级的具体操作步骤，详情请参见 [设备固件升级](https://intl.cloud.tencent.com/document/product/1105/41507)。
>
![](https://main.qcloudimg.com/raw/08f08cfb2fe06fba6d9ced1a2bc76e16.png)




