## 简介

对于直接通过控制台页面、云 API 创建的云资源，可以使用 TIC “资源导入” 功能，无需执行删除和重建操作，即可将存量资源导入到 TIC 资源栈中进行统一编排。

>?仅支持导入到新建资源栈中，不支持导入存量资源栈。

目前支持导入到 TIC 的云产品列表如下：

| 云产品 | 资源类型                                                     | 备注                  |
| ------ | ------------------------------------------------------------ | --------------------- |
| CDN    | [tencentcloud_cdn_domain](https://console.cloud.tencent.com/tic/resource-types/detail/1045) | 不支持 HTTPS 证书导入 |


## 操作步骤

### 资源导入

1. 登录 [TIC 控制台](https://console.cloud.tencent.com/tic)，左侧菜单栏中选择【资源编排】，进入资源栈页面。
2. 在 [资源栈](https://console.cloud.tencent.com/tic/stacks) 页面中，单击【新建资源栈】。
3. 在【模式选择】步骤中，选中地域后，指定【导入资源】模板，勾选需要导入的资源。
![image-20200710154557033](https://main.qcloudimg.com/raw/ec82cc68cfb8f353d36a29f1c7e1bc9f.png)
4. 单击【导入】，执行资源导入操作。
5. 导入的资源个数越多，导入时间越长。单击【导入完成】，执行后续的参数配置操作。
![](https://main.qcloudimg.com/raw/89cf5c05edef27aaeb93ba42ed4968e5.png)

### 资源栈配置

1. 资源导入完成后，将自动生成资源栈配置。
	 ![](https://main.qcloudimg.com/raw/dba3ee9b9394fdd3e6196b0eda65b996.png)
2. 确认配置无误后，单击【下一步】，执行 Plan 操作。
   >!考虑到各产品资源配置复杂性，难免会存在疏漏之处，为保证导入操作不影响现网资源的配置，在确认资源栈中的参数配置时，请遵循如下的原则：
   > 1. 请勿修改参数类型为 ForceNew 的字段。例如，CDN 产品 tencentcloud_cdn_domain 资源类型中的 domain、service_type 参数类型为 ForceNew，修改这两项参数配置内容，将导致现网资源被销毁重建，可能会影响到现网业务；
   > 2. 不支持导入的参数，需要手动配置。例如，CDN 产品中的域名证书无法自动导入到 TIC 中，因此需要手动配置证书，并添加到资源栈配置文件中，便于后续的资源编排和管理；
   > 3. 若对生成的配置参数有疑问，请 [提交工单](https://console.cloud.tencent.com/workorder/category)，联系 TIC 团队确认后，再执行后续的操作。
3. 确认 Plan 操作的执行结果是否符合预期，重点关注是否存在资源 destory、add 的情况，确认无误后，单击【下一步】。
   ![image-20200710154824278](https://main.qcloudimg.com/raw/33533236d7d1e1d06ccf9aa447d56bfc.png)
   >?因为是导入存量资源，正常情况下不会出现资源创建、修改、删除的操作。若 Plan 结果中显示 add、change、destroy 的资源数不为0，请终止后续的操作，检查是否编辑了上一步提到的 ForceNew 参数。若您仍有疑问，请 [提交工单](https://console.cloud.tencent.com/workorder/category)，联系 TIC 团队确认后，再执行后续的操作。
4. 设置资源栈名称以及资源栈描述信息，单击【确认】，完成资源栈创建操作。
![](https://main.qcloudimg.com/raw/7824466b2c40aa13d996a60d95bf6f7d.png)

### 查看资源栈状态


1. 进入 [资源栈](https://console.cloud.tencent.com/tic/stacks) 页面，单击上述步骤资源栈名称，进入资源栈详情页。
2. 单击【事件】，进入资源栈事件页面。查看资源栈状态，APPLY_IN_PROGRESS 表示资源信息同步中的状态。
![image-20200710155056811](https://main.qcloudimg.com/raw/7676c44b8f3055e3ec59773adc313ff7.png)
3. 十几秒后，资源信息同步完成，状态更新为 APPLY_COMPLETED。
![image-20200710155906888](https://main.qcloudimg.com/raw/49a7e5b553f49ed0d7c0d40c69c0739a.png)
4. 资源成功导入到新建的资源栈中，在资源栈【资源】页面中，可以查到本次导入的云资源列表。后续只需要编辑资源栈的配置，即可操作对应的云资源。
![image-20200710155952490](https://main.qcloudimg.com/raw/60414c7cf720def527bd2112d4dafff7.png)
