在没有子网的情况下，当您购买 CVM 等实例时，系统会为您在相应地域创建默认子网，默认子网可以帮助您更快速地部署业务，节省时间。

系统默认的子网，与您自行创建的子网功能完全一致，且默认子网不会占用您在某个地域下的配额。如果您不再需要默认子网，可以自行删除。

## 创建子网
用户可以同时创建一个或多个子网。
1. 登录 [私有网络控制台](https://console.cloud.tencent.com/vpc)。
2. 单击左侧目录中的【子网】，进入管理页面。
3. 选择需要创建子网的地域和私有网络，单击【+新建】。
4. 填写子网名称、CIDR、可用区和关联路由表。
![2](https://main.qcloudimg.com/raw/1a6801a275b142ba7689284ffab536d1.png)
5. （可选）单击【+新增一行】，可以同时创建多个子网。
6. 单击【创建】即可。

## 向子网中添加云服务器
1. 登录 [私有网络控制台](https://console.cloud.tencent.com/vpc)。
2. 单击左侧目录中的【子网】，进入管理页面。
3. 在需要添加云服务器的子网所在行，单击添加云服务器的图标。
![](https://main.qcloudimg.com/raw/68c28c0cf70f2a6e053a2130f4e6433a.png)
4. 根据页面提示，完成云服务器的购买即可，详情请参见云服务器文档 [购买方式](https://intl.cloud.tencent.com/document/product/213/506)。

## 修改云服务器主内网 IP
云服务器主网卡的主内网 IP 支持修改，辅助网卡的主内网 IP 不支持修改，修改步骤如下：
1. 登录 [云服务器控制台](https://console.cloud.tencent.com/cvm) 。
2. 单击左侧目录中的【实例】，进入管理页面。
3. 在列表中，找到需要修改的云服务器，单击实例 ID，进入详情页。
4. 选择【弹性网卡】标签页，找到需要修改的主网 IP，单击操作栏下的【修改主IP】。
![](https://main.qcloudimg.com/raw/c2ecf69fb390033c3eaa8f3cf7ea4445.png)
5. 在弹出框中，填写新的 IP 地址，单击【确定】即可。
![2](https://main.qcloudimg.com/raw/88aa617e26ca4b1600034da6e846640e.png)

## 更换子网关联的路由表
每个子网都必须关联一个 [路由表](https://intl.cloud.tencent.com/document/product/215/4954)，用来指定子网的出站路由。您可以实时更改子网关联的路由表，如需新建路由表，请参见 [创建自定义路由表](https://intl.cloud.tencent.com/document/product/215/35236)。
1. 登录 [私有网络控制台](https://console.cloud.tencent.com/vpc)。
2. 单击左侧目录中的【子网】，进入管理页面。
3. 在列表中，找到需要更换路由表的子网，单击操作栏中的【更换路由表】。
![](https://main.qcloudimg.com/raw/6126ca32358c0ecb4af20c7dfcb0c506.png)
4. 在下拉框中，选择需要更换的路由表，单击【确定】即可。
![](https://main.qcloudimg.com/raw/37ff6a790162d500bbbe583ea1f5de4d.png)

## 删除子网
>删除子网的前提条件：子网内的 IP 没有被占用，且子网内没有资源（如云服务器，云数据库等）。

1. 登录 [私有网络控制台](https://console.cloud.tencent.com/vpc)。
2. 单击左侧目录中的【子网】，进入管理页面。
3. 在列表上方，选择需要删除的子网所在地域和私有网络。
4. 在列表中，找到选择需要删除的子网所在行，单击操作栏下的【删除】，并确认操作即可。
![](https://main.qcloudimg.com/raw/2c24ebe33c4ae4ee769d30c66c104b81.png)

## 子网分配与释放 IPv6 CIDR
1. 登录 [私有网络控制台](https://console.cloud.tencent.com/vpc)。
2. 在左侧目录单击【子网】，在“子网”列表上方，选择【地域】和【私有网络】，将会展示所属地域和私有网络下的所有子网信息。
3. 选择一个子网，单击【获取 IPv6 CIDR】，系统将为该子网分配1个`/64`的 IPv6 CIDR。 
![](https://main.qcloudimg.com/raw/8c257df75fe747dbd17e5b2cd173576a.png)
4. 选择一个已获取到 IPv6 CIDR 的子网，单击【释放 IPv6】并确定操作，系统将回收该子网的 IPv6 CIDR。
![](https://main.qcloudimg.com/raw/63d7dcb4dfb1ef9f2e6a94046a763ada.png)
