#测试Demo的使用方法

##下载Demo

一. Demo工程的未知在信鸽SDK文档内[下载SDK](http://xg.qq.com/ctr_index/download).

二. 在信鸽的web端注册测试应用，测试应用名称不限，包名必须为com.qq.xgdemo,然后获取注册应用的AccessID和Accesskey.

![](/assets/注册信鸽demo.png)

二. 将SDK内的demo工程导入相应的开发工具。并修改工程内配置信鸽ID和key的节点。

**[AndroidStudioDemo]**

将注册测试应用获取到的 ACCESSID 和 ACCESSKEY 配置到测试工程内app模块下的```build.gradle```文件内的```manifestPlaceholders```节点。如图所示：

![](/assets/AndroidStudioDemo.png)

**[eclipse]**

将注册测试应用获取到的 AccessID 和 Accesskey 配置到测试工程内```AndroidManifest.xml```下的```<mata-data>```节点。如图所示：

![](/assets/eclipseDemo.png)

##运行Demo

通过log控制台，过滤信鸽日志，（日志tag为TPush），出现如下日志说明注册信鸽成功：

```xml
10-09 20:08:46.922 24290-24303/com.qq.xgdemo I/XINGE: [TPush] get RegisterEntity:RegisterEntity [accessId=2100250470, accessKey=null, token=5874b7465d9eead746bd9374559e010b0d1c0bc4, packageName=com.qq.xgdemo, state=0, timestamp=1507550766, xgSDKVersion=3.11, appVersion=1.0]
10-09 20:08:47.232 24290-24360/com.qq.xgdemo D/TPush: 注册成功，设备token为：5874b7465d9eead746bd9374559e010b0d1c0bc4
```
##推送测试

获取日志内的设备token，打开信鸽管理创建推送：

![](/assets/推送测试.png)
