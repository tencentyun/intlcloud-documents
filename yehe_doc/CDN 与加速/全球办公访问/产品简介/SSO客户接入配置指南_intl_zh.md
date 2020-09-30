SSO客户接入配置指南

 

 

 

 

 

 

 

 

 

## 配置Azure Active Directory做为IDaaS认证源

## 配置OneLogin做为IDaaS认证源

## 配置Okta做为IDaaS认证源

## 配置LDAP 认证源

## 配置GSuite做为IDaaS认证源

 

 

 

 

 

 

 

# 一、 配置Azure Active Directory做为IDaaS认证源

用户需要提供给GOA的配置信息：

**需要将Base64的公钥证书，Login URL，以及Azure AD Identifier提供给GOA配置人员。**

GOA提供给用户的配置信息：

**GOA****配置人员会提供Entity ID和ACS URL。**

 

具体操作流程：

#### 1.  进入Azure控制台 https://portal.azure.com/#home

#### 2.  进入Azure Active Directory管理台

#### 3.  进入Enterprise applications管理台

![img](file:///C:/Users/V_VWYZ~1/AppData/Local/Temp/msohtmlclip1/01/clip_image002.jpg)

#### 4.  添加SAML-based SSO应用

![img](file:///C:/Users/V_VWYZ~1/AppData/Local/Temp/msohtmlclip1/01/clip_image004.jpg)

![img](file:///C:/Users/V_VWYZ~1/AppData/Local/Temp/msohtmlclip1/01/clip_image006.jpg)

![img](file:///C:/Users/V_VWYZ~1/AppData/Local/Temp/msohtmlclip1/01/clip_image008.jpg)

#### 5.  提供SAML相关信息到IDaaS

![img](file:///C:/Users/V_VWYZ~1/AppData/Local/Temp/msohtmlclip1/01/clip_image010.jpg)

![img](file:///C:/Users/V_VWYZ~1/AppData/Local/Temp/msohtmlclip1/01/clip_image012.jpg)

需要将Base64的公钥证书，Login URL，以及Azure AD Identifier提供给GOA配置人员。

#### 6.  配置SAML参数

GOA配置人员会提供Entity ID和ACS URL。

![img](file:///C:/Users/V_VWYZ~1/AppData/Local/Temp/msohtmlclip1/01/clip_image014.jpg)

#### 7.  授权可以使用SAML登陆的用户或组

![img](file:///C:/Users/V_VWYZ~1/AppData/Local/Temp/msohtmlclip1/01/clip_image016.jpg)

 

# 二、 配置OneLogin做为IDaaS认证源

用户需要提供给GOA的配置信息：

**需要将X.509证书，Issuer URL, SAML 2.0 Endpoint提供给GOA配置人员**

GOA提供给用户的配置信息：

**GOA****配置人员会提供Entity ID和ACS URL。**

 

具体操作流程：

（这里假设客户的onelogin域名为 https://magical.onelogin.com）

#### 1.  进入OneLogin控制台 https://magical.onelogin.com/

#### 2.  进入Applications管理页面 https://magical.onelogin.com/apps

#### 3.  添加SAML类型应用

![img](file:///C:/Users/V_VWYZ~1/AppData/Local/Temp/msohtmlclip1/01/clip_image018.jpg)

#### 4.  提供SAML相关信息到IDaaS

![img](file:///C:/Users/V_VWYZ~1/AppData/Local/Temp/msohtmlclip1/01/clip_image020.jpg)

需要将X.509证书，Issuer URL, SAML 2.0 Endpoint提供给GOA配置人员。

#### 5.  配置SAML参数

GOA配置人员会提供EntityID，ACS URL。

![img](file:///C:/Users/V_VWYZ~1/AppData/Local/Temp/msohtmlclip1/01/clip_image022.jpg)

设置用户字段

![img](file:///C:/Users/V_VWYZ~1/AppData/Local/Temp/msohtmlclip1/01/clip_image024.jpg)

![img](file:///C:/Users/V_VWYZ~1/AppData/Local/Temp/msohtmlclip1/01/clip_image026.jpg)

#### 6.  授权使用SAML登陆的用户

![img](file:///C:/Users/V_VWYZ~1/AppData/Local/Temp/msohtmlclip1/01/clip_image028.jpg)

![img](file:///C:/Users/V_VWYZ~1/AppData/Local/Temp/msohtmlclip1/01/clip_image030.jpg)

 

 

# 三、 配置Okta做为IDaaS认证源

用户需要提供给GOA的配置信息：

**提供应用的Client ID，Client Secret以及客户的Okta域名https://dev-xxxxxx.okta.com给到GOA配置人员**

GOA提供给用户的配置信息：

**GOA****配置人员会提供Login redirect URLs、Logout redirect URLs和Base URL。**

 

具体操作流程：

（这里假设客户的okta域名为 https://dev-xxxxxx.okta.com）

#### 1.  进入Okta管理端添加应用

![img](file:///C:/Users/V_VWYZ~1/AppData/Local/Temp/msohtmlclip1/01/clip_image032.jpg)

选择Web应用

![img](file:///C:/Users/V_VWYZ~1/AppData/Local/Temp/msohtmlclip1/01/clip_image034.jpg)

GOA配置人员提供登陆跳转相关参数：

![img](file:///C:/Users/V_VWYZ~1/AppData/Local/Temp/msohtmlclip1/01/clip_image036.jpg)

#### 2.  提供OIDC相关信息到IDaaS

应用添加完成后，提供应用的Client ID，Client Secret以及客户的Okta域名https://dev-xxxxxx.okta.com给到GOA配置人员。

![img](file:///C:/Users/V_VWYZ~1/AppData/Local/Temp/msohtmlclip1/01/clip_image038.jpg)

#### 3.  授权用户登陆应用

![img](file:///C:/Users/V_VWYZ~1/AppData/Local/Temp/msohtmlclip1/01/clip_image040.jpg)

 

 

# 四、 配置LDAP 认证源

#### 1.  操作场景

GOA支持企业成员通过 LDAP/AD 用户名密码登录门户，本文将为您详细介绍如何进行 LDAP 认证源配置。

#### 2.  配置步骤

\1.   管理员登录 GOA 控制台，单击【认证源管理】。

\2.     选择【启用】LDAP 认证源，即进入 LDAP 认证源设置页面。

\3.     填写认证源配置信息。

![img](file:///C:/Users/V_VWYZ~1/AppData/Local/Temp/msohtmlclip1/01/clip_image042.jpg)LDAP URL：请填写 LDAP 服务器 IP 与端口号。若服务器 IP 为196.0.0.0，端口号为389，则填写

ldap://196.0.0.0:389/，目前暂不支持 IPv6。

LDAP Base：LDAP 中的节点，认证时将会从该节点下匹配用户节点进行认证，如：dc=users,dc=com

LDAP 账户：请填写有上述 LDAP Base 管理权限的节点，认证过程需有管理权限才能进行，如：

cn=administrator,dc=users,dc=com

LDAP 账户密码：请填写上述 LDAP 账户对应的密码。

用户过滤条件：请填写 LDAP 匹配腾讯云 IDaaS 用户 ID 的过滤条件，如：sAMAccountName=$userId$，$userId$ 为本系统用户 ID 参数，是目录用户唯一标识符。

\4.     单击【提交】，LDAP 认证源配置成功！

 

# 五、 配置GSuite做为IDaaS认证源

用户需要提供给GOA的配置信息：

**需要将SSO URL、Entity ID、Certificate提供给GOA配置人员**

GOA提供给用户的配置信息：

**ACS URL****和 Entity ID 填写 GOA配置人员会提供提供的信息。**

 

具体操作流程：

#### 1.  From the Admin console dashboard, go to Apps > SAML Apps. To see Apps on the dashboard, you might have to click More controls at the bottom.

![img](file:///C:/Users/V_VWYZ~1/AppData/Local/Temp/msohtmlclip1/01/clip_image044.jpg)

#### 2.  Click the plus (+) icon at the bottom right.

#### 3.  Click Zoom.

#### 4.  The Google IDP Information window opens and the Single Sign-On URL and the Entity ID URL fields automatically populate.

#### 5.  Copy the Entity ID and the Single Sign-On URL field values and download the Certificate, as they will be used later in the setup. 

需要将SSO URL、Entity ID、Certificate提供给GOA配置人员。

 

![img](file:///C:/Users/V_VWYZ~1/AppData/Local/Temp/msohtmlclip1/01/clip_image046.jpg)

#### 6.  Click Next.

#### 7.  In the Service Provider Details window, add an ACS URL, an Entity ID, and a start URL.

ACS URL和 Entity ID 填写 GOA配置人员会提供提供的信息。如

ACS URL：http://sigma-test.cloudidaas.com/idp/saml/callback/4406

Entity ID：http://sigma-test.cloudidaas.com/idp/saml/4406

Start URL: leave blank

![img](file:///C:/Users/V_VWYZ~1/AppData/Local/Temp/msohtmlclip1/01/clip_image048.jpg)

#### 8.  Click Finish.

 

 

 

 

 

 

 