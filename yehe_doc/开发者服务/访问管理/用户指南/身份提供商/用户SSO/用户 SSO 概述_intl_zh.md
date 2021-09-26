腾讯云与企业进行用户SSO时，腾讯云是服务提供商（SP），而企业自有的身份管理系统则是身份提供商（IdP）。通过用户SSO，企业员工在登录后，将以CAM子用户访问腾讯云。



### **配置流程**

为了建立腾讯云与企业IdP之间的互信关系，需要对腾讯云SP进行SAML配置，同时也要对企业IdP进行SAML配置，两边配置完成后才能进行用户SSO。

1. 为了建立腾讯云对企业IdP的信任，需要将企业IdP配置到腾讯云。具体配置操作请参见[腾讯云SP进行SAML配置](https://intl.cloud.tencent.com/document/product/598/42366)。
2. 为了建立企业IdP对腾讯云的信任，需要在企业IdP中配置腾讯云为可信SP并进行SAML断言属性的配置。具体配置操作请参见[企业IdP进行SAML配置](https://intl.cloud.tencent.com/document/product/598/42367)。
3. 腾讯云SP和企业IdP都配置完成后，企业需要登录到 CAM 控制台或通过 API 调用创建与企业IdP中名称完全匹配的 CAM 子用户。具体配置操作请参见[新建子用户](https://intl.cloud.tencent.com/document/product/598/13674)



### **登录验证流程**

完成上述用户SSO的相关配置后，企业IdP中的用户便可通过 SSO 的方式登录腾讯云并访问有权限的资源。以用户 user1 为例，其具体的登录验证流程如下：

1. user1 在腾讯云[子用户登录](https://intl.cloud.tencent.com/login/subAccount?s_url=https%3A%2F%2Fintl.cloud.tencent.com)界面发起用户 SSO 登录
2. 腾讯云将SAML认证请求返回给浏览器
3. 浏览器将接收到的SAML认证请求转发给企业 IdP
4. 企业IdP认证用户 user1，并在认证通过后生成SAML响应返回给浏览器
5. 浏览器将接收到的SAML响应转发给腾讯云
6. 腾讯云通过SAML互信配置，验证SAML断言的真伪和完整性，并通过SAML断言中的**NameID**元素值，匹配到腾讯云账号中的CAM子用户
7. 验证且匹配成功后，腾讯云向浏览器返回控制台的URL并成功登录
