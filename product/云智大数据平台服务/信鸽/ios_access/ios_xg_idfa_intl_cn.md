** 本文档针对 iOS 信鸽 <font color="#FF0000"> SDK 3.1.0 及以上 </font>  版本 **

## 功能说明
在 iOS 平台上，对于信鸽可能提供的关于精准消息推送的能力来说，IDFA 是比较有效的识别参数，所以 信鸽 SDK 采用插件化的方式来实现按需集成的需要.

## 集成步骤

信鸽 iOS SDK 集成 idfa 模块的步骤：
1.在下载的 SDK 文件包中打开 idfa 目录，获取 libxgidfa.a 静态库文件
2.将 libxgidfa.a 静态库文件，添加到工程即可完成 idfa 插件的集成，如图：
![](/assets/xgidfa.png)

** 注意 **

如果您期望采集IDFA但是并未使用任何广告，可以采用以下方法通过Appstore审核
![](http://docs.developer.qq.com/mta/assets/用户画像.png)

1.serve advertisements within the app

应用内广告服务，适用于应用内集成了广告的场景，如果您的情况符合，需要勾选此选项。

2.Attribute this app installation to a previously served advertisement.

用于跟踪和统计广告带来的安装量，需要勾选。

3.Attribute an action taken within this app to a previously served advertisement

用于跟踪和统计广告安装后带来的用户行为，需要勾选。

4.Limit Ad Tracking setting in iOS

此项属于确认项，需要勾选。






