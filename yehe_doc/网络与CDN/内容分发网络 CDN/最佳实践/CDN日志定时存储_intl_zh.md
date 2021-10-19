# CDN日志定时存储

本文介绍如何使用腾讯云的云函数功能，创建两个函数，实现定时将CDN的日志存储到COS中。

# 主要步骤

本教程将介绍如何创建“存储”函数和“任务分发”函数，二者组合在一起并配置定制器触发，即可实现定时将CDN的日志存储到COS中。

主要分为四个大步骤：

A、准备云API的访问密钥和对象存储COS的相关信息

B、创建存储函数（cdn-save-log-into-cos）

C、创建任务函数（cdn-dispatch-log-jobs）

D、配置定时器

# 教程正文

## A、在创建云函数之前，你需要准备好以下资源

1、云API的访问密钥。

请前往[访问密钥管理页面](https://console.cloud.tencent.com/cam/capi) ，查询或新建一个密钥，并记录下 ：

l访问凭证的名称SecretId，例如 AKIDRVI54XXn10r58oZpmzbBOnwt47xO1LRv

l访问凭证的密钥SecretKey，例如 3t0SYPHRIpjmAAUPfKM8b4yXnff4Aq56

2、对象存储COS的存储桶Bucket。

请前往[对象存储管理页面](https://console.cloud.tencent.com/cos) ，进入【存储通列表】，查询或新建一个存储桶，进入存储桶查看【基本信息】，并记录下：

l存储桶空间名称 BucketName，例如 examples-1251002854

l存储桶所属地域 Region，例如 ap-chengdu

## B、创建存储函数（cdn-save-log-into-cos）

1、进入云服务函数的管理页面 https://console.cloud.tencent.com/scf，点击【函数服务】；

2、选择【新建】，函数名称填写【**cdn-save-log-into-cos**】；

3、选择【模板函数】，并搜索关键字“CDN”，选择“下载URL文件并存储到COS”模板，并点击下一步进入函数配置；
![](https://main.qcloudimg.com/raw/402a01a22ca748386617afd2fc7255a2.png)

4、点击【完成】创建函数。
![](https://main.qcloudimg.com/raw/69f87dc5f7314f0cdb21f45684b403ed.png)

## C、创建任务函数（cdn-dispatch-log-jobs）

1、进入 [云服务函数的管理页面](https://console.cloud.tencent.com/scf)，点击【新建】；

2、选择基于【模板函数】，并搜索关键字“CDN”，选择“CDN日志存储任务分发函数”模板；

3、函数名称填写【**cdn-dispatch-log-jobs**】，并点击下一步；

4、接着点击【完成】创建好函数。

![](https://main.qcloudimg.com/raw/b82b157292163ca06b9f43e74bd1a8de.png)

5、点击【函数代码】标签，进入代码编辑框中修改python代码，填写配置信息：

在第134行的config变量中，填写对应的配置信息。

- secret_id、secret_key、cos_region、cos_bucket、scf_region等字段需填写；
- scf_function如果按教程中B步骤进行，没有修改函数名字的话，则保存原值即可。
- cdn_host的默认值为空数组（即保存账号下所有域名的日志），如有需要可以修改填入指定域名列表。

![](https://main.qcloudimg.com/raw/8ed596f7843acacc0e3974057922cd0d.png)

6、点击【保存】。

7、点击【测试】，可以立即执行一次代码，确认是否正常工作。 测试程序运行完毕后，可以进入对象存储COS的管理页面，查看对应的日志是否存储到COS汇总。

## D、配置定时器

上述两个函数创建完毕后，函数服务管理页面的列表如下。

1、点击【**cdn-dispatch-log-jobs**】进入详情页面；

![](https://main.qcloudimg.com/raw/55382244ab24832e280b040f284cd09a.png)

2、点击【触发管理】标签页，并点击【创建触发器】；

![](https://main.qcloudimg.com/raw/36949d35a75f77515caacee834427064.png)

3、选择触发方式为【定时触发】，填写任务名称（随意），触发周期为【每5分钟】，并保存。

![](https://main.qcloudimg.com/raw/fe157cb0c234693920c3efc36ed9c7e3.png)

以上步骤，全部配置完毕后，即完成了本教程的任务目标。