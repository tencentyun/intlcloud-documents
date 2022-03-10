## 新建发布单
我们推荐赋予**开发**用户组访问与持续部署管理权限。详情请参见 [权限控制](https://intl.cloud.tencent.com/document/product/1137/45449) 。
![](https://qcloudimg.tencent-cloud.cn/raw/9bf33813ea65c77eb87d288eaeb42d5a.png)
设置后，开发具备提交发布单的权限，不具备前往部署控制台修改部署配置的权限。运维组用户还可以在应用的部署流程中添加人工确认步骤，确保通过发布单发布时是经二次确认的，通过权限控制把控发布质量。
![](https://qcloudimg.tencent-cloud.cn/raw/05f3a3b8bf8e950d713dfeaeb5e5cf0d.png)
单击**新建发布单**，可以运行已有应用及部署流程。
![](https://qcloudimg.tencent-cloud.cn/raw/7e91657b0c592f610cfc422e060d9fbb.png)

## 快速发布

若不希望在团队设置复杂的权限限制，而直接希望体验持续部署功能，可以使用**快速发布**功能。无需在控制台中配置部署流程即可将镜像发布至集群中，适用于更加灵活复杂的部署流程的场景，例如临时镜像变更等突发场景，无需快速将制品发布至集群中。

![](https://qcloudimg.tencent-cloud.cn/raw/b3c7864d71160bb90ad0b796fce3f86c.png)

成员所在用户组需具备部署管理权限，所发布的制品的权限范围需设置为公开状态，从而能够被集群访问。

![](https://qcloudimg.tencent-cloud.cn/raw/1b4f13ffdc10156801299e457ab5cc75.png)

发布完成后可以在持续部署中查看发布详情。

![](https://qcloudimg.tencent-cloud.cn/raw/fe73843393d654af5d5b8a4cad612501.png)
