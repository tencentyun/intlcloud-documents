使用基于 OIDC 协议的角色 SSO 时，需要在腾讯云控制台创建身份提供商并为其创建角色，然后再使用身份提供商签发的 OIDC Token 换取腾讯云的 STS Token（角色的临时秘钥）。

## 一、创建 OIDC 身份提供商

1. 在CAM控制台的左侧导航栏，选择身份提供商 > 角色SSO。
2. 在角色 SSO 页面，单击新建提供商。
3. 在新建身份提供商页面，选择提供商类型“OIDC”，并填写身份提供商信息：
	○ **身份提供商名称**：自定义身份提供商的名称，同一个腾讯云账号下必须唯一。
	○ **身份提供商 URL**：OIDC 身份提供商标识，由外部 IdP 提供，必须以 http 开头，符合标准 URL 格式。
	○ **客户端 ID**：在 OIDC 身份提供商注册的客户端 ID，如果有多个应用需要访问腾讯云，可以配置多个客户端ID。
	○ **签名公钥**：验证 OIDC 身份提供商 ID Token 签名的公钥。对应身份提供商提供的 OIDC 元数据文档中 "jwks_uri" 字段中链接的内容（在浏览器中打开链接获取内容）。为了您的帐号安全，建议您定期轮换签名公钥。
	○ **备注信息**：为身份提供商添加的备注信息。
4. 单击 下一步 进入信息审阅页面。
5. 确认信息无误后，单击完成按钮保存。


## 二、为身份提供商创建角色
1. 在CAM控制台的左侧导航栏，单击角色。
2. 在角色管理页面，单击新建角色。
3. 选择角色载体为身份提供商。
4. 在新建自定义角色页面，选择身份提供商类型为 OIDC。
5. 选择已经创建好的身份提供商。
6. 设置角色的使用条件：
	○ **oidc:iss**：OIDC颁发者（Issuer），必填。该限定条件必须使用string_equal，条件值只能是您在OIDC身份提供商中填写的身份提供商URL。用来扮演角色的OIDC令牌中的iss字段值必须满足该限制条件要求，角色才允许被扮演。
	○ **oidc:aud**：OIDC受众（Audience），必填。该限定条件必须使用string_equal，条件值只能使用在OIDC身份提供商中配置的一个或多个客户端ID。用来扮演角色的OIDC令牌中的aud字段值必须满足该限制条件要求，角色才允许被扮演。
	○ **oidc:sub**：OIDC主体（Subject），选填。该限定条件可以使用任何string类的条件操作类型，且条件值最多可以设置10个OIDC主体。用来扮演角色的OIDC令牌中的sub字段值必须满足该限制条件要求时，角色才允许被扮演。
7. 单击下一步。
8. 在配置角色策略页面，为角色关联权限策略，并单击下一步。
9. 在审阅页面，输入角色名称和角色描述（选填），并单击完成按钮保存。

## 三、在身份提供商签发 OIDC Token
腾讯云不支持使用OIDC登录控制台，需要使用程序访问的方式完成OIDC SSO流程（即通过调用 API 获取临时秘钥，再使用临时秘钥访问腾讯云）。由于生成OIDC Token本质上是个OAuth流程，所以需要通过标准的OAuth 2.0流程从 OIDC 身份提供商（例如：Okta）获取OIDC Token，具体方式参见提供商的相关文档。

## 四、使用 OIDC Token 换取 STS Token
从身份提供商处获取到 OIDC Token 后，可以直接调用 AssumeRoleWithWebIdentity API 以换取可以访问腾讯云的 STS Token。
请求示例：
```
POST / HTTP/1.1
Host: sts.tencentcloudapi.com
Content-Type: application/json
X-TC-Action: AssumeRoleWithWebIdentity
<公共请求参数>

{
    "DurationSeconds": "5000",
    "RoleSessionName": "test_OIDC",
    "WebIdentityToken": "eyJraWQiOiJkT**********CNOQ",
    "RoleArn": "qcs::cam::uin/798950673:roleName/OneLogin-Role",
    "ProviderId": "OIDC"
}
```
返回示例：
```
{
  "Response": {
    "ExpiredTime": 1543914376,
    "Expiration": "2018-12-04T09:06:16Z",
    "Credentials": {
      "Token": "1siMD5r0tPAq9xpR******6a1ad76f09a0069002923def8aFw7tUMd2nH",
      "TmpSecretId": "AKID65zyIP0mp****qt2SlWIQVMn1umNH58",
      "TmpSecretKey": "q95K84wrzuE****y39zg52boxvp71yoh"
    },
    "RequestId": "f6e7cbcb-add1-47bd-9097-d08cf8f3a919"
  }
}
```
## 五、使用 STS Token 访问腾讯云资源
使用从上述步骤中换取的临时秘钥（STS Token）访问有权限的腾讯云资源。

