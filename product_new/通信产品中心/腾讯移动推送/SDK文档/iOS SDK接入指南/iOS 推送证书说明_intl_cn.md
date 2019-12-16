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
 ![](https://main.qcloudimg.com/raw/5f1726f1e78b7b9cc512a4964dcbd1d9.png)

最后，填写邮件地址，其它留空，将证书保存到本地

![](https://main.qcloudimg.com/raw/6f988ae446d4500e2843dc31aa5a4caf.png)

第二步：配置应用，使其拥有推送能力

首先，登录苹果开发者中心网站点击 ```Certificates,Identifiers & Profiles```

![](https://main.qcloudimg.com/raw/673951a14724416e2850718ee7ae3160.png)



然后，选中需要制作消息推送证书的应用，勾选消息推送服务

![](https://main.qcloudimg.com/raw/1a08ca5cd0054873dc80cc03c9d3fd04.png)




第三步：创建消息推送证书



首先，点击 ```Create Certificate```，这里我们需要用到开发环境&生产环境合并版本的证书

 ![](https://main.qcloudimg.com/raw/93cad1a9d1b22a47c7d4381035ab1390.png)


然后，选择第一步中创建的消息推送证书请求文件，上传完毕之后，点击 ```Generate```

![](https://main.qcloudimg.com/raw/d494bdde10e37c3b3b3c2bf926bf4451.png)



最后，将生成的消息推送证书下载到本地
![](https://main.qcloudimg.com/raw/36c508ec62427edb06d0d171f87f5ac4.png)



第四步，安装证书

双击上一步中下载的证书，会自动将消息推送证书安装到 Keychain 应用中



第五步，导出证书



打开 Keychain Access选中需要导出的消息推送证书，右键，选择导出证书，导出的格式为P12，设置密码
![](https://main.qcloudimg.com/raw/c7eb856a4793e7e4a0297873ba0bc08e.png)



## 上传证书

第一步：[登录控制台](https://console.cloud.tencent.com/tpns)

第二步：在【应用列表】中选择需要上传推送证书的应用

第三步：在【应用配置】页面上传推送证书即可完成

