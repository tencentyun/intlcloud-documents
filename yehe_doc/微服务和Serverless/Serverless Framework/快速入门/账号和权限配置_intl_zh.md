当前，Serverless Framework 在部署项目时，需要通过账号中 `SLS_QcsRole` 的 [角色](https://intl.cloud.tencent.com/document/product/598/19420) 授权才可正常部署。该角色中包含 Serverless Framework 在部署中所需要用到的关联产品的对应策略，可以分为主账号和子账号两种情况进行配置。

## 主账号权限配置
目前支持通过账号密钥配置的方式进行授权，由于主账号拥有创建角色和绑定策略的权限，因此可以通过下列方式关联 `SLS_QcsRole` 并进行访问：

### 账号密钥配置授权

如您希望配置持久的环境变量/密钥信息，不需要每次都进行扫码部署，也可以在项目目录下创建`.env`文件，将 SecretId 和 SecretKey 信息并保存。
```ini
# .env
TENCENT_SECRET_ID=123  //您的SecretId 
TENCENT_SECRET_KEY=123 //您的SecretKey
```
由于 Serverless Framework 在部署时会默认检测是否为中国用户，如果开发环境在中国境外地域，但希望使用中国版体验的 Serverless Framework，则可以在 .env 文件中增加下列配置，即可指定默认提供中国版体验，包括交互式的一键部署流程等。
```ini
# .env
TENCENT_SECRET_ID=123
TENCENT_SECRET_KEY=123
SERVERLESS_PLATFORM_VENDOR=tencent
```

>
>- 如果没有腾讯云账号，请先 [注册新账号](https://intl.cloud.tencent.com/register)。
>- 如果已有腾讯云账号，可以在 [API 密钥管理](https://console.cloud.tencent.com/cam/capi) 中获取 SecretId 和 SecretKey。

## 子账号权限配置

针对子账号的权限配置，如果希望支持扫码授权部署，则要确保子账号具备创建角色和绑定角色策略的权限。可以为子账号增加预设策略 `QcloudCamRoleFullAccess` 或 `QcloudCamSubaccountsAuthorizeRoleFullAccess`。

如果不开通上述两个权限，也可以在 [访问管理控制台](https://console.cloud.tencent.com/cam/role) 通过主账号配置增加 `SLS_QcsRole` 从而开通对 Serverless Framework 的资源访问能力，该角色的角色载体为 `sls.cloud.tencent.com`，主要包含如下策略授权：
- QcloudSLSFullAccess
- QcloudSSLFullAccess
- QcloudMongoDBFullAccess
- QcloudAPIGWFullAccess
- QcloudElasticsearchServiceFullAccess
- QcloudCKafkaFullAccess
- QcloudSCFFullAccess
- QcloudMonitorFullAccess
- QcloudCOSFullAccess
- QcloudCDBFullAccess

此外，需要为子账号的用户绑定一条自定义策略，确保该账号具有使用 Serverless Framework 产品的接口权限，提供两种授权方式示例，参考如下：

### 授予子账号 Serverless Framework 所有资源的操作权限
1. 在 [CAM 用户列表](https://console.cloud.tencent.com/cam/user) 页，选取对应子账号，单击用户名称，进入用户详情页。
2. 单击【关联策略】，在添加策略页面单击【从策略列表中选取策略关联】。
3. 搜索并关联 `QcloudSLSFullAccess`，单击【下一步】。
4. 单击【确定】，即可授予子账号 Serverless Framework 所有资源的操作权限。
策略语法如下：
```json
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "sls:*"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```

### 授予子账号 Serverless Framework 特定资源的操作权限

如果希望子账号仅对 Serverless Framework 某些特定资源有操作权限，可通过如下步骤操作：
1. 在 [CAM 用户列表](https://console.cloud.tencent.com/cam/user) 页，选取对应子账号，单击用户名称，进入用户详情页。
2. 单击【关联策略】，在添加策略页面单击【从策略列表中选取策略关联】。
3. 并单击【新建自定义策略】，按策略语法创建一条自定义策略并关联到用户，参考策略语法如下：
```json
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "sls:*"
            ],
            "resource": "qcs::sls:ap-guangzhou::appname/${appname}/stagename/${stagename}",
            "effect": "allow"
        }
    ]
}
```

配置完毕后，则子账号仅对 `${appname}` 和 `${stagename}` 下的 Serverless 应用具有操作权限。
