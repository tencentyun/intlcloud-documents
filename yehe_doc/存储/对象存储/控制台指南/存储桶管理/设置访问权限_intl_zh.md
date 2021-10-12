## 简介

您可以通过对象存储控制台来设置或修改存储桶的访问权限。对象存储 COS 支持设置两种权限类型：

- **公共权限**：私有读写、公有读私有写和公有读写。关于公共权限的说明，请参见存储桶概述中的 [权限类别](https://intl.cloud.tencent.com/document/product/436/13312)。
- **用户权限**：主账号默认拥有存储桶所有权限（即完全控制）。另外 COS 支持添加子账号有数据读取、数据写入、权限读取、权限写入，甚至**完全控制**的最高权限。

## 单个授权

**操作步骤**

1. 登录 [对象存储控制台](https://console.cloud.tencent.com/cos5)。
2. 在左侧导航栏中，单击【存储桶列表】。
3. 找到您需要设置或修改访问权限的存储桶，单击其存储桶名称。
4. 在存储桶配置页面，单击【权限管理】>【存储桶访问权限】，对存储桶的公共权限和用户权限（例如添加子账号，子账号 ID 可在 [访问管理](https://console.cloud.tencent.com/cam) 控制台查看）进行设置。
![](https://main.qcloudimg.com/raw/34e464b33c4b9bffe72c734d1c1dcb2d.png)
5. 单击页面右侧的【保存】，即可完成存储桶访问权限设置。

## 批量授权

**操作步骤**

1. 登录 [对象存储控制台](https://console.cloud.tencent.com/cos5)。
2. 在左侧导航栏中，单击【存储桶列表】。
3. 单击列表上方的【授权管理】。
![](https://main.qcloudimg.com/raw/9bfbb2948c61a9b3a522d61331d90a51.png)
4. 在弹窗中选择希望授权的存储桶。然后对存储桶的公共权限和用户权限（例如添加子账号，子账号 ID 可在 [访问管理](https://console.cloud.tencent.com/cam) 控制台查看）进行设置。
![](https://main.qcloudimg.com/raw/23eff9055312eaa122e247f9cf0ebf53.png)
5. 配置完成后，单击【确定】，即可完成多个存储桶的访问权限设置。
