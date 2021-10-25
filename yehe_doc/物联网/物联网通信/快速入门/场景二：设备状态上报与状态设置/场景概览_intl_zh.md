## 操作场景

假设一个智能家居的场景（非实际产品，仅用于阐述物联网通信功能），如果需实现设置设备及上报设备情况，本文档指导您如何设置设备目标温度和设备上报状态信息。
![](https://main.qcloudimg.com/raw/74ee56cdeb3836ce4c7dc5a21d9540fd.png)

## 设置设备目标温度
![](https://main.qcloudimg.com/raw/93d2e910859d326de663f3793d4be9b1.png)
管理后台通过物联网通信提供的云 API 接口，更新设备影子的配置属性，设备注册相关属性和关联对应的回调函数执行本地配置更新处理。
通过云 API 操作设备影子的相关接口案例实现，请下载 [iotcloud_RestAPI_python.zip](https://mc.qcloudimg.com/static/archive/c6b492abe009de1c47b91b8bfd93c7d2/iotcloud_RestAPI_python.zip)，用户需根据《 RestAPI 操作说明》配置个人信息。通过修改 RestAPI 文件夹下 airConditionerCtrl.py 参数实现自定义功能。

## 设备上报状态信息

![](https://qcloudimg.tencent-cloud.cn/raw/6dd0a5a0162ee02ad2d5801f0a409587.png)
设备通过上报自身状态数据到设备影子，家电管理后台通过 restAPI 接口直接从设备影子获取数据。
