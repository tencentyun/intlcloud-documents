本篇文档将为您指导，如何创建 Ckafka 触发器并完成函数的调用。

### 1. 创建函数
在云函数“新建”页面，完成您的函数代码上传与部署。

![](https://main.qcloudimg.com/raw/f8047105b56df5f01d2da6524b70fddc.png)

此处以 Ckafka 示例模版为例，创建函数项目，模版默认创建流程中，直接配置触发器，实际创建中，您也可以创建完成后再进行配置，此处以创建完成后配置为例进行说明：
![](https://main.qcloudimg.com/raw/be4e6fef7619073b9a73a9f04e30bdb0.png)


### 2. 配置触发器
选择【 Ckafka 触发器】后，按照指引，配置队列名称、主题等信息，即可完成触发器创建：
>! 注意：请保证您的函数与 Ckafka 在相同 VPC 下

![](https://main.qcloudimg.com/raw/fdb2f5da3bc22dae4d748f284d86ed0f.png)

### 3. 管理触发器
创建完成后，在“触发器管理”页面可以看到创建的触发器信息，并进行触发器的开启与关闭

