StreamLive支持通过导出、导入频道配置文件，以及频道克隆功能来快速完成频道创建工作。

## 导出频道
StreamLive的**Channel Management**界面会显示您所有创建的频道及状态，点击右侧的**Export**按钮可快速导出频道配置json文件。
![](https://qcloudimg.tencent-cloud.cn/raw/df66d2e71c1dc9f54e3753eecbf1e12b.png)
![](https://qcloudimg.tencent-cloud.cn/raw/6c6402290ae2b5b9bfc987917f035941.png)

## 导入频道
在**Channel Management**界面点击**Create Channel**按钮，选择**Import Configuration**，选中频道配置json文件，提交json文件后即进入频道编辑状态，接着按照常规配置过程保存并提交频道即可。
![](https://qcloudimg.tencent-cloud.cn/raw/7bf6af58535a57e11a9f92339b8e5e34.png)
频道导入功能实际上是一次快速填写的过程，我们会基于您导入的json文件快速帮您自动填写**Basic Information**、**Output Group Setting**两部分内容，**Input Setting**部分会被忽略，需要您重新选择Input。

>! 编辑频道时如果导入新的配置文件，则原来频道配置信息会被覆盖。

## 克隆频道
频道克隆本质是一次快速且特殊的频道导出/导入操作，打开**Channel Management**界面点击**Operation**中的**Clone**后即可进入克隆频道的配置状态。
![](https://qcloudimg.tencent-cloud.cn/raw/27f233ac35cc1bd1316901ac7457ffa9.png)
此时频道会自动填写被克隆频道的基本信息（**Input Setting**部分除外），接着按照常规配置步骤保存并提交频道即可。