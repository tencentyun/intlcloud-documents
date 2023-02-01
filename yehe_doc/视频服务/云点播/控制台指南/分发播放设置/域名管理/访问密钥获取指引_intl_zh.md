### 阿里云 OSS

1. 登录[阿里云控制台](https://home-intl.console.aliyun.com/?spm=a3c0i.7911826.6791778070.44.44193870NcDmuq)，点击右上角【 AceessKey 管理】

![img](https://wdoc-76491.picgzc.qpic.cn/MTY4ODg1MDUzOTk2NzAxNw_235189_QpR3p5p8VK1cC02m_1675165190?w=601&h=405)

2. 在左侧导航栏选择【AceessKey Pair】，点击【创建 Access Key 】即可生成 AceessKey ID和 AceessKey Secret

![img](https://wdoc-76491.picgzc.qpic.cn/MTY4ODg1MDUzOTk2NzAxNw_638463_ynPkI9zDhEclio1t_1675165362?w=702&h=359)

![img](https://wdoc-76491.picgzc.qpic.cn/MTY4ODg1MDUzOTk2NzAxNw_280350_VezfgXsHdXo6r9pv_1675165448?w=547&h=276)



| 配置项     | 描述                                                  |
| ---------- | ----------------------------------------------------- |
| Access ID  | 腾讯云点播账号的  Access ID 为阿里云账号的 AccessKey  |
| Access Key | 腾讯云点播账号的  Access Key 为阿里云账号的 SecretKey |

### **AWS S3**

1. 登录[AWS 控制台](https://signin.aws.amazon.com/signin?redirect_uri=https%3A%2F%2Fconsole.aws.amazon.com%2Fconsole%2Fhome%3FhashArgs%3D%23%26isauthcode%3Dtrue%26nc2%3Dh_ct%26src%3Dheader-signin%26state%3DhashArgsFromTB_ap-northeast-1_c1ce58b06ec43f75&client_id=arn%3Aaws%3Asignin%3A%3A%3Aconsole%2Fcanvas&forceMobileApp=0&code_challenge=CaZWRvqV_1cfih72WiKyQLFILOJeAb_rJ6fQljIZ3sM&code_challenge_method=SHA-256)

2. 在“AWS services”搜索框中搜索“access key”

![img](https://wdoc-76491.picgzc.qpic.cn/MTY4ODg1MDUzOTk2NzAxNw_772039_9_sV5oc4ylmUBmF2_1664527422?w=700&h=560)

3. 点击搜索跳出的选项：IAM

![img](https://wdoc-76491.picgzc.qpic.cn/MTY4ODg1MDUzOTk2NzAxNw_532381_Ub85YbWYvbYqp4ZR_1664527435?w=700&h=579)

4. 点击“Rotate your access keys ”，点击Button：Manage User Access Keys

![img](https://wdoc-76491.picgzc.qpic.cn/MTY4ODg1MDUzOTk2NzAxNw_77171_1Ry56PZKBAeb76yu_1664527446?w=700&h=422)

5. 选择Security credentials标签，点击Button “Create access key ”自动生成Access Key ID 和 Secret Access Key

![img](https://wdoc-76491.picgzc.qpic.cn/MTY4ODg1MDUzOTk2NzAxNw_93273_o2eD7Fi3_0W1z9kF_1664527463?w=700&h=446)

6. 弹框显示生成的Access Key ID 和 Secret Access Key，点击Button “Download.csv file”下载，这是唯一的机会可以保持Access Key ID 和 Secret Access Key，下发显示了Access Key ID 和 Secret Access Key，点击“Show”可查看Secret Access Key，内容与下载的

accessKeys.csv 内容一致。如果以后无法找到Secret Access Key，可以删除重新创建一对。

![img](https://wdoc-76491.picgzc.qpic.cn/MTY4ODg1MDUzOTk2NzAxNw_997603_3DzOJTGpMqk_SuNO_1664527472?w=700&h=374)

| 配置项     | 描述                                                         |
| ---------- | ------------------------------------------------------------ |
| Access ID  | 腾讯云点播账号的  Access ID 为 AWS 账号的 Access ID          |
| Access Key | 腾讯云点播账号的  AccessKey 为 AWS 账号的 Secret  Access Key |