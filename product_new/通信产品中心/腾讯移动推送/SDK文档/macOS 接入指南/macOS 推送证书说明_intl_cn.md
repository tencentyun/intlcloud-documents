# macOS推送证书说明


## 操作场景

macOS 推送证书分为开发环境的推送证书和发布环境的推送证书。
按照本教程，分别制作开发环境和发布环境的推送证书。



## 操作步骤
#### 生成证书


1.在您的电脑中，打开 Keychain Access 工具，选择【Request a Certificate From a Certificate Authority】。

![](https://main.qcloudimg.com/raw/17152ed67a1673af899b14d751f7084c.png)


2.填写邮件地址，其它留空，单击【continue】，将证书保存到本地。

![](https://main.qcloudimg.com/raw/3f7cd266e952c0cac893424b78e5e668.png)

3.登录苹果开发者中心网站，单击【Certificates,Identifiers & Profiles】。```Certificates,Identifiers & Profiles```

![](https://main.qcloudimg.com/raw/a96a6c0eba20dde46fbda6f50fc88e4e.png)



4.选中需要制作消息推送证书的应用，勾选消息推送服务

![](https://main.qcloudimg.com/raw/bf9a68373369833ecd7ccbc3a5936b75.png)




创建消息推送证书

下面以制作开发环境的消息推送证书为例演示，发布环境的消息推送证书操作步骤一致

进入到【Certificate】栏目，点击添加按钮
![](https://main.qcloudimg.com/raw/edc4fa4eb3cb962095015bf8b2ff0784.png)

这里我们选择开发环境的推送证书。
 ![](https://main.qcloudimg.com/raw/712e3aa08ed2e807bd1522ca8bda92e0.png)


然后，选择第2步中创建的消息推送证书请求文件，上传完毕之后，点击 ```continue```

![](https://main.qcloudimg.com/raw/0f7d66730a4b2a1e10f066522b3f2a74.png)



最后，将生成的消息推送证书下载到本地
![](https://main.qcloudimg.com/raw/c1101776b6044d6ba53b3e5b37fe3c69.png)



第四步，安装证书

双击上一步中下载的证书，会自动将消息推送证书安装到 Keychain 应用中



第五步，导出证书



打开 Keychain Access选中需要导出的消息推送证书，右键，选择导出证书，导出的格式为P12，设置密码
![](https://main.qcloudimg.com/raw/30a6544222eec5408e554c743348b47a.png)



## 上传证书

第一步：[登录控制台](https://console.cloud.tencent.com/tpns/applist)

第二步：在【应用列表】中选择需要上传推送证书的应用

第三步：在【应用配置】页面上传推送证书即可完成

