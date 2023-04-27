子账号默认没有云拨测任何权限。需要主账号授予子账号相关权限，子账号才能正常访问云拨测资源。

## 操作前提

使用主账号或拥有 QcloudCamFullAccess 权限的子账号登录腾讯云控制台，并参见 [新建子用户](https://intl.cloud.tencent.com/document/product/598/13674) 创建子账户。

##  自定义策略

1. 使用主账号或拥有 QcloudCamFullAccess 权限的子账号进入**访问控制** > [**策略**](https://console.cloud.tencent.com/cam/policy)。
2. 单击**新建自定义策略 > 按策略语法创建**，选择空白模板。根据 [策略语法](https://www.tencentcloud.com/document/product/1169/52015) 完成策略编辑。
   ![](https://staticintl.cloudcachetci.com/yehe/backend-news/7tUI660_38intl_%E5%A5%BD%E5%8E%8B%E7%9C%8B%E5%9B%BE.png)

## 策略授权

>?云拨测为您创建默认策略 QcloudCATFullAccess（云拨测（CAT）全读写访问权限）和 QcloudCATReadOnlyAccess（云拨测（CAT）只读访问权限），您可以通过搜索策略名称快速进行默认策略授权。也可以对自定义策略进行授权。授权成功后，子账号才能正常访问相关资源。

1. 使用主账号或拥有 QcloudCamFullAccess 权限的子账号进入**访问控制** > [**策略**](https://console.cloud.tencent.com/cam/policy)。
2. 进入策略管理页，在策略名称搜索框中输入对应的策略名称。
3. 选择只读访问或全读写访问权限，在操作列中单击**关联用户/组**。
   ![](https://staticintl.cloudcachetci.com/yehe/backend-news/9s8U893_39intl_%E5%A5%BD%E5%8E%8B%E7%9C%8B%E5%9B%BE.png)
4. 在弹框中勾选对应的用户，单击**确定**即可。

