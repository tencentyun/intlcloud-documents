DNSPod 控制台现已全面接入腾讯云 CAM 访问管理，用户可通过 CAM 策略设置，将指定域名授权给子用户或协作者，并分配只读、全读写权限。

**什么是 CAM 访问管理？**

访问管理（Cloud Access Management，CAM）是腾讯云平台提供的服务，帮助用户管理腾讯云账号的访问权限，可自由管理资源及使用权限。通过 CAM，您可以创建、管理子用户及协作者，并通过策略管理控制哪些身份可以使用哪些云资源。包括腾讯云 DNSPod，以及域名注册、CVM 等其他云产品。

[查看 CAM 访问管理介绍](https://intl.cloud.tencent.com/document/product/598/10583)

**如何使用 CAM 访问管理？**

请参考 CAM [授权管理](https://intl.cloud.tencent.com/document/product/598/10602) ，将预设策略授权给指定用户：

DNSPod 只读访问权限：QcloudDNSPodReadOnlyAccess

DNSPod 全读写访问权限：QcloudDNSPodFullAccess

> 注意：上述两个预设策略，包含了该账号下 DNSPod 的相关全部资源，如域名解析、付费套餐等。

> DNSPod 只读访问权限：是指授权用户只能查看资源，但无法编辑修改。比如只能查看某个域名下有什么解析记录，但无法修改记录。

> DNSPod 全读写访问权限：是指授权用户可以查看资源，并修改管理资源。比如修改解析记录、删除域名等操作。但不包含账号设置、费用中心等操作。