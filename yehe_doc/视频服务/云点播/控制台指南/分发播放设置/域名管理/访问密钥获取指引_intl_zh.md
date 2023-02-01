### 阿里云 OSS

1. 登录[阿里云控制台](https://home-intl.console.aliyun.com/?spm=a3c0i.7911826.6791778070.44.44193870NcDmuq)，点击右上角【 AceessKey 管理】

![img](https://qcloudimg.tencent-cloud.cn/raw/fce5a6308421d3dc5ca8527386f6db38.png)

2. 在左侧导航栏选择【AceessKey Pair】，点击【创建 Access Key 】即可生成 AceessKey ID和 AceessKey Secret

![img](https://qcloudimg.tencent-cloud.cn/raw/f08cb6fc9aacb90aac1d0cf464cbb734.png)

![img](https://qcloudimg.tencent-cloud.cn/raw/a327576c1d2ecac57c466a09e4f651b1.png)



| 配置项     | 描述                                                  |
| ---------- | ----------------------------------------------------- |
| Access ID  | 腾讯云点播账号的  Access ID 为阿里云账号的 AccessKey  |
| Access Key | 腾讯云点播账号的  Access Key 为阿里云账号的 SecretKey |

### **AWS S3**

1. 登录[AWS 控制台](https://signin.aws.amazon.com/signin?redirect_uri=https%3A%2F%2Fconsole.aws.amazon.com%2Fconsole%2Fhome%3FhashArgs%3D%23%26isauthcode%3Dtrue%26nc2%3Dh_ct%26src%3Dheader-signin%26state%3DhashArgsFromTB_ap-northeast-1_c1ce58b06ec43f75&client_id=arn%3Aaws%3Asignin%3A%3A%3Aconsole%2Fcanvas&forceMobileApp=0&code_challenge=CaZWRvqV_1cfih72WiKyQLFILOJeAb_rJ6fQljIZ3sM&code_challenge_method=SHA-256)

2. 在“AWS services”搜索框中搜索“access key”

![img](https://qcloudimg.tencent-cloud.cn/raw/b66a0dd3553c02eb0d19201c25d2a6a6.png)

3. 点击搜索跳出的选项：IAM

![img](https://qcloudimg.tencent-cloud.cn/raw/457b6e760b769da5d05e479abced4d3a.png)

4. 点击“Rotate your access keys ”，点击Button：Manage User Access Keys

![img](https://qcloudimg.tencent-cloud.cn/raw/371563847e2a174dfb2fbe47f8ee956a.png)

5. 选择Security credentials标签，点击Button “Create access key ”自动生成Access Key ID 和 Secret Access Key

![img](https://qcloudimg.tencent-cloud.cn/raw/9befceace4a4c367649ba283ea34a509.png)

6. 弹框显示生成的Access Key ID 和 Secret Access Key，点击Button “Download.csv file”下载，这是唯一的机会可以保持Access Key ID 和 Secret Access Key，下发显示了Access Key ID 和 Secret Access Key，点击“Show”可查看Secret Access Key，内容与下载的

accessKeys.csv 内容一致。如果以后无法找到Secret Access Key，可以删除重新创建一对。

![img](https://qcloudimg.tencent-cloud.cn/raw/dc5350c516a96aca53da7f56d7f3abeb.png)

| 配置项     | 描述                                                         |
| ---------- | ------------------------------------------------------------ |
| Access ID  | 腾讯云点播账号的  Access ID 为 AWS 账号的 Access ID          |
| Access Key | 腾讯云点播账号的  AccessKey 为 AWS 账号的 Secret  Access Key |