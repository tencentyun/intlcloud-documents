### 如何查看地域列表？

您可以通过以下方式进行查看：
- 查看 [地域和可用区](https://intl.cloud.tencent.com/document/product/213/6091) 文档
- 通过 API 接口查询：
 - [查询地域列表](https://intl.cloud.tencent.com/document/product/213/15708)
 - [查询可用区列表](https://intl.cloud.tencent.com/document/product/213/35071)

### 已购买的云服务器可以更换地域吗？

已购买的云服务器不支持更换地域。一个已经启动的实例是无法更改其可用区的，若您有更换地域和可用区的需求，可参考以下两种解决方式：

- 先将原始实例创建自定义镜像，再使用自定义镜像在新可用区中创建实例、启动实例以及更新新实例的配置。
  1. 创建当前实例的自定义镜像，详情请参考  [创建自定义镜像](https://intl.cloud.tencent.com/document/product/213/4942)。
  2. 如果当前实例的网络环境为 [私有网络](https://intl.cloud.tencent.com/document/product/213/5227) 且需要在迁移后保留当前内网 IP 地址，需先删除当前可用区中的子网，再在新可用区中用与原始子网相同的 IP 地址范围创建子网。
  > 如果删除的子网含有可用实例，须先将当前子网中的所有实例移至新子网，再删除。
  >
  3. 使用刚创建的自定义镜像在新的可用区中创建一个新实例。
  用户可以选择与原始实例相同的实例类型及配置，也可以选择新的实例类型及配置。详情请参考 [创建实例](https://intl.cloud.tencent.com/document/product/213/4855)。
  4. 如果原始实例有关联的弹性公网 IP 地址，则将其与旧实例解关联并与新实例相关联。详情请参考 [弹性公网 IP](https://intl.cloud.tencent.com/document/product/213/5733)。
  5. （可选）若原有实例为 [按量计费](https://intl.cloud.tencent.com/document/product/213/2180) 类型，可选择销毁原始实例。详情请参考 [销毁实例](https://intl.cloud.tencent.com/document/product/213/4930)。
