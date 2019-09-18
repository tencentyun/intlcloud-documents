# iOS推送证书说明


## 消息推送证书介绍
本指南用于介绍如何生成信鸽推送所需要的iOS 消息推送证书。
iOS 推送证书分为开发环境的推送证书和发布环境的推送证书。
按照本教程，分别制作开发环境和发布环境的推送证书。



## APNs 推送证书申请

第一步：制作消息推送证书请求文件

首先，打开 ```Keychain Access``` 工具
![](https://main.qcloudimg.com/raw/a11ed45755c05b45d9c203fac7b11820.png)



 然后，选择 ```Request a Certificate From a Certificate Authority```
 ![](/assets/iOSCert/2.jpg)

最后，填写邮件地址，其它留空，将证书保存到本地

![](/assets/iOSCert/3.jpg)

第二步：配置应用，使其拥有推送能力

首先，登录苹果开发者中心网站点击 ```Certificates,Identifiers & Profiles```

![](/assets/iOSCert/4.jpg)



然后，选中需要制作消息推送证书的应用，勾选消息推送服务

![](/assets/iOSCert/5.jpg)




第三步：创建消息推送证书



首先，点击 ```Create Certificate```，这里我们需要用到开发环境&生产环境合并版本的证书

 ![](/assets/iOSCert/6.jpg)


然后，选择第一步中创建的消息推送证书请求文件，上传完毕之后，点击 ```Generate```

![](/assets/iOSCert/8.jpg)



最后，将生成的消息推送证书下载到本地
![](/assets/iOSCert/9.jpg)



第四步，安装证书

双击上一步中下载的证书，会自动将消息推送证书安装到 Keychain 应用中



第五步，导出证书



打开 Keychain Access选中需要导出的消息推送证书，右键，选择导出证书，导出的格式为P12，设置密码
![](/assets/iOSCert/10.jpg)



## 上传证书

第一步：[登录控制台](https://console.cloud.tencent.com/tpns/applist)

第二步：在【应用列表】中选择需要上传推送证书的应用

第三步：在【应用配置】页面上传推送证书即可完成

