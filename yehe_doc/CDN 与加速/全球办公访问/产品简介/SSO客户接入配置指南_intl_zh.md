SSO客户接入配置指南

 

 

 

 

 

 

 

 

 

## 配置Azure Active Directory做为IDaaS认证源

## 配置OneLogin做为IDaaS认证源

## 配置Okta做为IDaaS认证源

## 配置LDAP 认证源

## 配置GSuite做为IDaaS认证源

 

 

 

 

 

 

 

## 一、 配置Azure Active Directory做为IDaaS认证源

用户需要提供给GOA的配置信息：

**需要将Base64的公钥证书，Login URL，以及Azure AD Identifier提供给GOA配置人员。**

GOA提供给用户的配置信息：

**GOA配置人员会提供Entity ID和ACS URL。**

 

具体操作流程：

#### 1.  进入Azure控制台 https://portal.azure.com/#home

#### 2.  进入Azure Active Directory管理台

#### 3.  进入Enterprise applications管理台

![img](https://main.qcloudimg.com/raw/6596a7deb7b3225f829d27798a3e6de7.jpg)

#### 4.  添加SAML-based SSO应用

![img](https://main.qcloudimg.com/raw/12ee4e528a32c7fb6ab1f62ed1d9c648.jpg)

![img](https://main.qcloudimg.com/raw/f21293fe4592e598f5acab9c5d6ef3dd.jpg)

![img](https://main.qcloudimg.com/raw/1b0b369a98d1a2ed1354629afd770450.jpg)

#### 5.  提供SAML相关信息到IDaaS

![img](https://main.qcloudimg.com/raw/66fdcfb3a370b4c9a58e4ebbf38350e4.jpg)

![img](https://main.qcloudimg.com/raw/b4bc246f91eeab0cfebb8191bc5def54.jpg)

需要将Base64的公钥证书，Login URL，以及Azure AD Identifier提供给GOA配置人员。

#### 6.  配置SAML参数

GOA配置人员会提供Entity ID和ACS URL。

![img](https://main.qcloudimg.com/raw/d8b23991a6d23fefc491a9a53e76629a.jpg)

#### 7.  授权可以使用SAML登陆的用户或组

![img](https://main.qcloudimg.com/raw/f371146c47338bfd7fcb3d18da9b6c5b.jpg)

 

## 二、 配置OneLogin做为IDaaS认证源

用户需要提供给GOA的配置信息：

**需要将X.509证书，Issuer URL, SAML 2.0 Endpoint提供给GOA配置人员**

GOA提供给用户的配置信息：

**GOA****配置人员会提供Entity ID和ACS URL。**

 

具体操作流程：

（这里假设客户的onelogin域名为 https://magical.onelogin.com）

#### 1.  进入OneLogin控制台 https://magical.onelogin.com/

#### 2.  进入Applications管理页面 https://magical.onelogin.com/apps

#### 3.  添加SAML类型应用

![img](https://main.qcloudimg.com/raw/55aedd18476d43f4ebdd0fc777ac8f1e.jpg)

#### 4.  提供SAML相关信息到IDaaS

![img](https://main.qcloudimg.com/raw/725ffe55a46dd54777b20643e49e3b6d.jpg)

需要将X.509证书，Issuer URL, SAML 2.0 Endpoint提供给GOA配置人员。

#### 5.  配置SAML参数

GOA配置人员会提供EntityID，ACS URL。

![img](https://main.qcloudimg.com/raw/aba43e75ff7f2b5206b3540525eef2ef.jpg)

设置用户字段

![img](https://main.qcloudimg.com/raw/4c5aae9bb60650535bf44f874f63a73d.jpg)

![img](https://main.qcloudimg.com/raw/85111a88c0eb314d4cf758cb77fafc65.jpg)

#### 6.  授权使用SAML登陆的用户

![img](https://main.qcloudimg.com/raw/a9891ff322e6479bfb7f631bf4ddaf01.jpg)

![img](https://main.qcloudimg.com/raw/c6c4e0009503b7b9e0bd238d0ba5d09c.jpg)

 

 

## 三、 配置Okta做为IDaaS认证源

用户需要提供给GOA的配置信息：

**提供应用的Client ID，Client Secret以及客户的Okta域名https://dev-xxxxxx.okta.com给到GOA配置人员**

GOA提供给用户的配置信息：

**GOA****配置人员会提供Login redirect URLs、Logout redirect URLs和Base URL。**

 

具体操作流程：

（这里假设客户的okta域名为 https://dev-xxxxxx.okta.com）

#### 1.  进入Okta管理端添加应用

![img](https://main.qcloudimg.com/raw/1be2d37cd4b960b429e807f18492dfcd.jpg)

选择Web应用

![img](https://main.qcloudimg.com/raw/53a2aeba78611f4c0856e1f898a90b1b.jpg)

GOA配置人员提供登陆跳转相关参数：

![img](https://main.qcloudimg.com/raw/ea505fa803d2fe0d6afbb0197bab5d0a.jpg)

#### 2.  提供OIDC相关信息到IDaaS

应用添加完成后，提供应用的Client ID，Client Secret以及客户的Okta域名https://dev-xxxxxx.okta.com给到GOA配置人员。

![img](https://main.qcloudimg.com/raw/39eca907326e5151c4d2b1fe8a9a8db3.jpg)

#### 3.  授权用户登陆应用

![img](https://main.qcloudimg.com/raw/781dd931cbf70990d3de2878dba2e00f.jpg)

 

 

## 四、 配置LDAP 认证源

#### 1.  操作场景

GOA支持企业成员通过 LDAP/AD 用户名密码登录门户，本文将为您详细介绍如何进行 LDAP 认证源配置。

#### 2.  配置步骤

1.   管理员登录 GOA 控制台，单击【认证源管理】。

2.     选择【启用】LDAP 认证源，即进入 LDAP 认证源设置页面。

3.     填写认证源配置信息。

![img](https://main.qcloudimg.com/raw/28d57287433eabeead48cbdb72769e66.jpg)LDAP URL：请填写 LDAP 服务器 IP 与端口号。若服务器 IP 为196.0.0.0，端口号为389，则填写

ldap://196.0.0.0:389/，目前暂不支持 IPv6。

LDAP Base：LDAP 中的节点，认证时将会从该节点下匹配用户节点进行认证，如：dc=users,dc=com

LDAP 账户：请填写有上述 LDAP Base 管理权限的节点，认证过程需有管理权限才能进行，如：

cn=administrator,dc=users,dc=com

LDAP 账户密码：请填写上述 LDAP 账户对应的密码。

用户过滤条件：请填写 LDAP 匹配腾讯云 IDaaS 用户 ID 的过滤条件，如：sAMAccountName=$userId$，$userId$ 为本系统用户 ID 参数，是目录用户唯一标识符。

\4.     单击【提交】，LDAP 认证源配置成功！

 

## 五、 配置GSuite做为IDaaS认证源

用户需要提供给GOA的配置信息：

**需要将SSO URL、Entity ID、Certificate提供给GOA配置人员**

GOA提供给用户的配置信息：

**ACS URL****和 Entity ID 填写 GOA配置人员会提供提供的信息。**

 

具体操作流程：

#### 1.  From the Admin console dashboard, go to Apps > SAML Apps. To see Apps on the dashboard, you might have to click More controls at the bottom.

![img](https://main.qcloudimg.com/raw/0b29584486be82cc20342fecdad3f634.jpg)

#### 2.  Click the plus (+) icon at the bottom right.

#### 3.  Click Zoom.

#### 4.  The Google IDP Information window opens and the Single Sign-On URL and the Entity ID URL fields automatically populate.

#### 5.  Copy the Entity ID and the Single Sign-On URL field values and download the Certificate, as they will be used later in the setup. 

需要将SSO URL、Entity ID、Certificate提供给GOA配置人员。

 

![img](https://main.qcloudimg.com/raw/9124e9a689a5fffcc876fe331a7d8e45.jpg)

#### 6.  Click Next.

#### 7.  In the Service Provider Details window, add an ACS URL, an Entity ID, and a start URL.

ACS URL和 Entity ID 填写 GOA配置人员会提供提供的信息。如

ACS URL：http://sigma-test.cloudidaas.com/idp/saml/callback/4406

Entity ID：http://sigma-test.cloudidaas.com/idp/saml/4406

Start URL: leave blank

![img](https://main.qcloudimg.com/raw/5ceab5a4c4daa4474665d869fccc49b7.jpg)

#### 8.  Click Finish.

 

 

 

 

 

 

 
