## Create Release Order
We recommend that you grant the **Developer** user group the permission to access and manage Continuous Deployment (CD). For more information, see [Permission Control](https://intl.cloud.tencent.com/document/product/1137/45449).
![](https://qcloudimg.tencent-cloud.cn/raw/9bf33813ea65c77eb87d288eaeb42d5a.png)
Developers with the permission can submit a release order, but cannot modify deployment configurations in the CODING-CD Console. Ops user group can add a manual confirmation process to the deployment pipeline of an application to ensure that the application is reconfirmed when it is released via a release order. In this way, high-quality application can be achieved through permission control.
![](https://qcloudimg.tencent-cloud.cn/raw/05f3a3b8bf8e950d713dfeaeb5e5cf0d.png)
Click **Create Release Order** to run existing applications and pipelines.
![](https://qcloudimg.tencent-cloud.cn/raw/7e91657b0c592f610cfc422e060d9fbb.png)

### Quick Release

To directly use CODING-CD without complex permission configurations, you can use the **Quick Release** feature. It allows you to release images to a cluster without configuring a pipeline in the console. This feature applies to more flexible and complex pipelines. For example, when such emergencies like temporary image changes occur, you don't have to release artifacts to the cluster immediately.

![](https://qcloudimg.tencent-cloud.cn/raw/b3c7864d71160bb90ad0b796fce3f86c.png)

To do this, your user group must have the permission to manage CD and the permission scope of the released artifacts must be set to public, so that the artifacts can be accessed by the cluster.

![](https://qcloudimg.tencent-cloud.cn/raw/1b4f13ffdc10156801299e457ab5cc75.png)

After release, you can view the release details in Continuous Deployment.

![](https://qcloudimg.tencent-cloud.cn/raw/fe73843393d654af5d5b8a4cad612501.png)
