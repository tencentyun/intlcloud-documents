企业原有的身份系统作为身份提供商（IdP），需进行腾讯云SP的SAML 配置，以建立企业 IdP对腾讯云的信任，实现企业IdP用户通过用户SSO的方式登录腾讯云。



### **配置步骤**

1. 从腾讯云获取 SAML 服务提供商元数据 URL。
    1. 腾讯云账号登录 CAM 控制台
    2. 在左侧导航栏中，单击身份提供商-用户 SSO
    3. 在用户 SSO 管理页面可查看或复制当前用户的 SAML 服务提供商元数据 URL
2. 在企业IdP中创建一个SAML SP并将腾讯云配置为可信赖的服务提供商，具体配置方式可根据企业 IdP 的实际情况选择以下几种：
    1. **企业 IdP 支持 URL 配置：**将步骤1中的腾讯云服务提供商元数据 URL 直接复制到企业 IdP 中进行配置
    2. **企业 IdP 支持上传文件配置：**将步骤1中的腾讯云服务提供商元数据 URL 复制到浏览器打开并保存为 XML 格式的文件，然后再将文件上传到企业 IdP 中进行配置。
    3. **上述两种方式企业 IdP 均不支持：**这种情况，需要在企业 IdP 上手动配置以下参数：
        1. Entity ID：下载的元数据XML中，EntityDescriptor 元素的 entityID 属性值。
        2. ACS URL：下载的元数据XML中，AssertionConsumerService 元素 Location属性值。
