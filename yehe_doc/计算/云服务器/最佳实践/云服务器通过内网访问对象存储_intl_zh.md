
本文介绍云服务器 CVM 访问对象存储 COS 时使用的访问方式及内网访问的判断方法，并提供了连通性测试示例。您可参考本文进一步了解 CVM 访问 COS 相关信息。

## 访问方式说明
如果您在腾讯云内部署了服务用于访问 COS，不同地域访问方式有以下区别：
- **同地域访问**：同地域范围内的源站域名访问将会自动被指向到内网地址，即自动使用内网连接，产生的内网流量不计费。因此选购腾讯云不同产品时，建议尽量选择相同地域，减少您的费用。
- **跨地域访问**：暂不支持内网访问，默认将会解析到外网地址。

## 内网访问判断方法
您可通过本步骤，测试 CVM 是否通过内网访问 COS：
以云服务器 CVM 访问 COS 为例，判断是否使用内网访问 COS ，可在 CVM 上使用 `nslookup` 命令解析 COS 域名，若返回内网 IP，则表明 CVM 和 COS 之间是内网访问，否则为外网访问。
1. 获取存储桶访问域名，并记录该地址。详情请参见 [存储桶概览](https://intl.cloud.tencent.com/document/product/436/38493)。
2. 登录实例，并执行 nslookup 命令。假设 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com` 为目标存储桶地址，则执行以下命令：
```
nslookup examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com
```
返回如下图所示结果，其中`10.148.214.13`和`10.148.214.14`这两个 IP 就代表了是通过内网访问 COS。
<dx-alert infotype="explain" title="">
内网 IP 地址一般形如`10.*.*.*`、`100.*.*.*` ，VPC 网络一般为`169.254.*.*` 等，这两种形式的 IP 都属于内网。
</dx-alert>
<img src="https://main.qcloudimg.com/raw/49a7d7429ec2a96d271f6a63926286ea.png"/>

## 测试连通性
提供外网访问 COS、同地域 CVM（基础网络）访问 COS 及同地域 CVM（VPC 网络）访问 COS 示例，详情请参见 [测试连通性](https://intl.cloud.tencent.com/document/product/436/30613)。


## 相关操作
- [将 COS 作为本地磁盘挂载到 Windows 服务器](https://intl.cloud.tencent.com/document/product/436/40490)
- [将 WordPress 远程附件存储到 COS](https://intl.cloud.tencent.com/document/product/436/34082)


