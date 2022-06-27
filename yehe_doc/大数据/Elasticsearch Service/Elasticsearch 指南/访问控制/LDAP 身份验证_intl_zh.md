本文介绍如何基于腾讯云Elasticsearch Service配置轻量目录访问协议LDAP（Lightweight Directory Access Protocol）认证，以实现相应角色的LDAP用户访问腾讯云Elasticsearch Service。

## 使用限制
LDAP身份验证是Elasticsearch官方商业特性[X-pack](https://intl.cloud.tencent.com/document/product/845/30943)提供的高级功能，当前仅在白金版集群支持。其他版本集群如需使用，请先升级至白金版。

## 设置LDAP身份验证
1. 登录腾讯云[ Elasticsearch 控制台](https://console.cloud.tencent.com/es)，单击**集群名称**访问目标集群，跳转至**基础配置**页面。
2. 在**访问控制**模块，单击**身份验证**的编辑按钮，进入身份验证设置界面。
![avatar](https://qcloudimg.tencent-cloud.cn/raw/dae57fcab0bcdcca80a9c189c937b026.png)
3. 填写相关内容
   - url：LDAP服务器地址。ldap服务器地址，以“ldap://”开头，后面填写域名或者IP地址。请确保填写的URL可在您的VPC下内网访问，否则该配置将无法生效。
   - bind_dn：用于LDAP服务器认证的成员DN。需满足DN层次型语法结构，如：cn=admin,dc=husor,dc=com，长度不超过200个字符。
   - bind_password：LDAP服务器连接密码。支持大小写字母、数字及符号-!@#$%&^*+=_:;,.?的组合，长度为6～63个字符。
   - user_search.base_dn：用于检索已绑定LDAP成员的基准DN。需满足DN层次型语法结构，如：ou=HusorSSO,ou=People,dc=husor,dc=com，长度不超过200个字符。
   - user_search.filter：查询过滤条件，系统将过滤满足条件的绑定关系。如：(uid={0})。
   - group_search.base_dn：用于检索已绑定LDAP用户组的基准DN。需满足DN层次型语法结构，如：ou=HusorSSO,ou=People,dc=husor,dc=com，长度不超过200个字符。
![avatar](https://qcloudimg.tencent-cloud.cn/raw/3a03b3f63662fa218475b2b90b8eecf0.png)
4. 确认填写内容无误后，单击**确定**，在弹出的对话框中，阅读注意事项，确认后，集群将会重启，可以在集群变更记录中查看变更进度。
![avatar](https://qcloudimg.tencent-cloud.cn/raw/6bd38cf0325f4b4e1fa960aa17fdb1d7.png)
5. 设置成功后，您将会在**身份验证**看到**LDAP已开启**，如需修改LDAP身份验证设置，点击**LDAP已开启** 即可进行编辑。
![avatar](https://qcloudimg.tencent-cloud.cn/raw/7c98e387085b5054c16c1e9b2c61a8b0.png)

## 配置LDAP用户角色权限

1. 设置了LDAP身份验证后，LDAP用户还没有被分配任何权限，无法使用LDAP方式访问ES集群/Kibana，需要在Kibana中对LDAP用户进行角色映射。
2. 登陆腾讯云[ Elasticsearch 控制台](https://console.cloud.tencent.com/es)，跳转进入集群的Kibana主页，进入Kibana的**Dev Tools**页面。
3. 参考官方文档 [role mapping API](https://www.elastic.co/guide/en/elasticsearch/reference/master/security-api-put-role-mapping.html)，创建LDAP用户与角色的映射关系。例如下面的示例，为LDAP用户**zhangsan**赋予了**superuser**角色的权限。
```
   POST _xpack/security/role_mapping/ldap_role_mapping_zhangsan?pretty
   {
     "roles": [ "superuser" ],
     "enabled": true,
     "rules": {
       "any": [
         {
           "field": {
             "username": "zhangsan"
           }
         }
       ]
     }
   }
```

## 关闭LDAP身份验证
1. 登录腾讯云[ Elasticsearch 控制台](https://console.cloud.tencent.com/es)，单击**集群名称**访问目标集群，跳转至**基础配置**页面。
2. 在**访问控制**模块，单击**身份验证**中的**关闭**按钮，在弹出的对话框中，阅读注意事项，确认后，LDAP关闭操作开始，集群将会重启，可以在集群变更记录中查看变更进度。

## 注意事项
- 如果集群健康状态为 YELLOW 或 RED，进行修改配置操作有较大风险，需要先修复集群状态，再进行操作。
- 如果集群存在无副本索引，修改集群配置时会有强制重启的提示和选项框，此时进行修改重启操作有较大风险，可能会出现部分数据短暂无法访问的情况，建议为所有索引添加副本之后，再进行修改配置操作。


