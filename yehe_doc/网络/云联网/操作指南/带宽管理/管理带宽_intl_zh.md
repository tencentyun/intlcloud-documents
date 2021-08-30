若您创建月95后付费云联网，您可以在控制台查看带宽上限、变更限速方式等操作。此功能正在内测中，如需使用，请[联系商务](https://intl.cloud.tencent.com/contact-sales)。

## 前提条件
- 创建并关联云联网，具体操作请参见[ 新建云联网实例](https://intl.cloud.tencent.com/document/product/1003/30062)、[关联网络实例](https://intl.cloud.tencent.com/document/product/1003/30064)。
- 检查路由表，确保没有路由冲突，具体操作请参见 [查看路由信息](https://intl.cloud.tencent.com/document/product/1003/30066)。

## 查看月95后付费带宽
1. 登录 [私有网络控制台](https://console.cloud.tencent.com/vpc/vpc?rid=1) ，并在左侧导航栏中单击【云联网】。
2. 在云联网列表页面，选择【地域】，单击目标月95后付费云联网实例的 ID，然后在实例详情页面单击【带宽管理】页签。
  在“带宽管理”页签中，您可以查看当前限速模式下的带宽上限。
  - 地域间带宽限速模式
  - 地域出口限速模式
3. （可选）变更限速方式。
  1. 在“限速方式”右侧，单击【变更】。
  2. 在“变更限速方式”弹窗中的下拉框内调整限速方式。
  > !限速方式变更后，原有限速配置将删除，带宽将设置为1Gbps（默认），如需更大默认带宽，请提[ 工单申请](https://console.cloud.tencent.com/workorder/category)。
  > 
    <table>
			 <tr>
			 <th>限速方式</th>
			 <th>说明</th>
			 </tr>
			 <tr>
			 <td>地域出带宽</td>
			 <td>某地域去往其他地域的总体出带宽限速。</td>
			 </tr>
			 <tr>
			 <td>地域间带宽</td>
			 <td>两地域之间的出入带宽限速。</td>
			 </tr>
			 </table>
  3. 单击【确定】，即可修改限速方式。
