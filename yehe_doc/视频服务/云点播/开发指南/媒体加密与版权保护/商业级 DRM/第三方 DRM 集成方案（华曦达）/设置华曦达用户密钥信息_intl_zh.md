如果使用第三方 DRM 密钥提供商（华曦达 SDMC）集成 DRM 功能，那么需要从华曦达获取相关的用户密钥信息（UID、SecretID 、SecretKey 以及 FairPlay 证书地址）。因此，本文主要说明如何在华曦达控制台获取用户密钥信息。

## 操作步骤
1. 如果您没有华曦达账号，则需先完成注册，可访问 [华曦达（SDMC）官网](https://www.xmediacloud.com/contact-us/) 。
    ![](https://qcloudimg.tencent-cloud.cn/raw/e92825b46f81fce995a115c0905915cb.png)

2. 填写完右侧表单后，点击 **Send message**，一般几个小时后，您将收到由华曦达发送的系统邮件反馈，后续将会有华曦达商务人员联系您并确认相关信息。
    ![](https://qcloudimg.tencent-cloud.cn/raw/73ca49235b99ef7c42c97514a46f47c8.png)

3. 华曦达审核通过后会给您发送 DRM 服务开通邮件，邮件中包含华曦达 DRM 控制台地址及登录初始密码。

4. 登录 [华曦达 DRM 控制台](https://sso.multidrm.tv/login)，输入账号及密码即可成功登录。
    ![](https://qcloudimg.tencent-cloud.cn/raw/1833a48650c8ba607ad57701839b6d33.png)

5. 进入控制台点击左侧导航栏`DRM SETTING` ，查询用户密钥信息 UID、SecretID 及 SecretKey。
    ![](https://qcloudimg.tencent-cloud.cn/raw/59b1edb28e121521e9806b0d062b7495.png)

6. 查询得到 FairPlay 证书地址。

    ![](https://qcloudimg.tencent-cloud.cn/raw/81407e990466afe606bba4c378f66fe6.png)

7. 登录腾讯云点播控制台。

8. 提交华曦达的用户密钥信息（包括Uid、SecretID、SecretKey 以及 FairPlay 证书地址）。

    点击展开左侧导航栏`视频处理设置`，点击` 商业级 DRM 配置 `，点击右侧`华曦达用户密钥信息配置`中的  `编辑`：
    
     ![](https://qcloudimg.tencent-cloud.cn/raw/cf92bbe8ad649b609ed6b71a54e3ec67.png)
    
    填写用户密钥信息并保存：
    
    ![](https://qcloudimg.tencent-cloud.cn/raw/42a17f61100e06b909c4e5da4747eff5.png)

## 总结

  至此，您已在腾讯云点播控制台完成了华曦达用户密钥信息的配置。
>? 在您对接 DRM 或者华曦达的过程中的任何问题，都可以提工单 [联系我们](https://console.cloud.tencent.com/workorder/category)，我们全程负责帮您解决。
