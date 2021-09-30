创建云联网并关联网络实例后，还需要配置带宽才能正常通信。对于月95后付费用户，则需配置云联网关联的两端地域带宽限制。

## 前提条件

- 创建并关联云联网，具体操作请参见[ 新建云联网实例](https://intl.cloud.tencent.com/document/product/1003/30062)、[关联网络实例](https://intl.cloud.tencent.com/document/product/1003/30064)。
- 检查路由表，确保没有路由冲突，具体操作请参见[ 查看路由信息](https://intl.cloud.tencent.com/document/product/1003/30066)。


## 设置跨地域带宽限制（仅适用于月95后付费实例）

若您创建的月95后付费云联网实例，可以按需配置跨地域带宽上限，控制带宽费用。

> ?默认带宽上限为 1Gbps，如需更大默认带宽，请提 [工单申请](https://console.cloud.tencent.com/workorder/category)。

1. 登录 [云联网控制台](https://console.cloud.tencent.com/vpc/ccn) ，进入云联网管理页面。

2. 在云联网列表页面单击目标月95后付费云联网实例的 ID，然后在实例详情页面单击【带宽管理】页签。

3. （可选）若当前限速方式不满足您的需求，可按以下步骤变更限速方式。

   1. 在“限速方式”右侧，单击【变更】。
      ![](https://main.qcloudimg.com/raw/fa211668316de376d3321fe87137e3a4.png)

   2. 在“变更限速方式”弹窗中的下拉框内调整限速方式。

      > !限速方式变更后，原有限速配置将删除，带宽将设置为1Gbps（默认），如需更大默认带宽，请提[ 工单申请](https://console.cloud.tencent.com/workorder/category)。
      >
      ![](https://main.qcloudimg.com/raw/d512626f5a9068673fbf2d1e1cc62abc.png)

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

4. 根据您创建的云联网限速方式，按需配置限速：

  - 设置地域间带宽限速
    单击【调整带宽】，在“调整带宽”对话框中选择需限速的两个地域，并设置带宽上限。若需设置多条带宽限速，则单击【添加】进行配置。完成后单击【确定】。
    ![](https://main.qcloudimg.com/raw/5c85f5e688d795af90d7e09bb38d905f.png)
  - 设置地域出口带宽限速
    单击【调整带宽限速】，在弹框中勾选需要限速的地域，填写地域出口的带宽上限，单击【确定】即可。
    ![img](https://main.qcloudimg.com/raw/2c71d31b0cc2a9bd74f1224083b66cfe.png)

