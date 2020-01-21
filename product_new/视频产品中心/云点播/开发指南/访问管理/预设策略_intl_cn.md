访问管理实质上是将子账号与策略进行绑定，或者说将策略授予子账号。开发者可以在控制台上直接使用预设策略来实现一些简单的授权操作，复杂的授权操作请参见 [自定义策略](https://intl.cloud.tencent.com/document/product/266/33972)。

云点播目前提供了以下预设策略：

|        策略名称         |       策略描述       |
| :---------------------: | :------------------: |
|   QcloudVODFullAccess   | 云点播全读写访问权限 |
| QcloudVODReadonlyAccess |  云点播只读访问权限  |

## 预设策略使用示例


### 创建拥有云点播完整权限的子用户

1. 以 [主账号](https://intl.cloud.tencent.com/document/product/598/32633) 的身份访问 CAM 控制台的[【用户列表】](https://console.cloud.tencent.com/cam)，单击【新建用户】。
   ![](https://main.qcloudimg.com/raw/e700947b468ef25d4bf70ad1fecc6348.png)
2. 在“新建用户”页面单击子用户类型下的【自定义创建】，进入“新建子用户”页面。
   ![](https://main.qcloudimg.com/raw/b8351b38a1df79df1836cb62268ecc74.png)
3. 填写用户信息。
   - 填写用户名，勾选【编程访问】和【腾讯云控制台访问】，其余选项按需配置。
   - 单击【下一步】，按照页面的提示完成身份验证。
     ![](https://main.qcloudimg.com/raw/19b98c0b2dde4824d5eeaa52304ea3df.png)
4. 设置用户权限。
   - 搜索并勾选预设策略`QcloudVODFullAccess`。
   - 单击【下一步】。
		<img src="https://main.qcloudimg.com/raw/0bd65772428242306300e315537853cd.png" width="704">
5. 在“审阅信息和权限”分栏下单击【完成】，完成子用户的创建，在成功页面下载并保管好该子用户的登录链接和安全凭证，其中包含的信息如下表：
   ![](https://main.qcloudimg.com/raw/cc223f380730f8dbfe81caa799be2dfc.png)
<table>
     <tr>
         <th nowrap="nowrap">信息</th>  
         <th nowrap="nowrap">来源</th>  
         <th nowrap="nowrap">作用</th>  
         <th nowrap="nowrap">是否必须保存</th>  
     </tr>
	 <tr>      
         <td>登录链接</td>   
	     <td>在页面中复制</td>   
	     <td nowrap="nowrap">方便登录控制台，省略填写主账号的步骤</td>   
	     <td>否</td>
     </tr> 
	 <tr>      
         <td nowrap="nowrap">用户名 </td>   
	     <td>安全凭证 CSV 文件</td>   
	     <td>登录控制台时填写</td>   
	     <td>是</td>
     </tr> 
	 <tr>      
         <td>密码</td>   
	     <td>安全凭证 CSV 文件 </td>   
	     <td >登录控制台时填写</td>   
	     <td >是</td>
     </tr> 
		  <tr>      
         <td>SecretId</td>   
	     <td>安全凭证 CSV 文件</td>   
	     <td >调用服务端 API 时使用，详见 <a href="https://intl.cloud.tencent.com/document/product/598/32675">访问密钥</a></td>   
	     <td >是</td>
     </tr> 
	     <tr>      
         <td>SecretKey</td>   
	     <td>安全凭证 CSV 文件</td>   
	     <td >调用服务端 API 时使用，详见 <a href="https://intl.cloud.tencent.com/document/product/598/32675">访问密钥</td>   
	     <td >是</td>
     </tr> 
</table>

将上述登录链接和安全凭证提供给云点播使用方，后者即可使用该子用户对云点播做所有操作（包括访问云点播控制台、请求云点播服务端 API 等）。
>创建子用户的通用流程请参见 CAM 的 [创建子用户](https://intl.cloud.tencent.com/document/product/598/13674) 文档。

### <span id="p2"></span>将云点播完整权限授予已存在的子用户

1. 以 [主账号](https://intl.cloud.tencent.com/document/product/598/32633) 的身份访问 CAM 控制台的[【用户列表】](https://console.cloud.tencent.com/cam)，单击想要进行授权的子账号。
   ![](https://main.qcloudimg.com/raw/86a75ce62dde0ba4c061975181186974.png)
2. 单击“用户详情”页面权限栏的【添加策略】，如下图所示（实际操作中，根据子账号已有权限的不通过，页面的信息可能有所差异。如果子账号的权限非空，则单击【关联策略】）。
   ![](https://main.qcloudimg.com/raw/e775e39eec0292f31a78d5a2332d6d09.png)
3. 选择【从策略列表中选取策略关联】，搜索并勾选预设策略`QcloudVODFullAccess`。后续按页面提示完成授权流程即可。

### 解除子用户的云点播完整权限

1. 以 [主账号](https://intl.cloud.tencent.com/document/product/598/32633) 的身份访问 CAM 控制台的[【用户列表】](https://console.cloud.tencent.com/cam)，单击想要解除授权的子账号。
   ![](https://main.qcloudimg.com/raw/86a75ce62dde0ba4c061975181186974.png)
2. 在“用户详情”页面权限栏找到预设策略`QcloudVODFullAccess`，单击右侧的【解除】。按页面提示完成解除授权流程即可。
   <img src="https://main.qcloudimg.com/raw/4d221c52efe40913031355c877f28a47.png" width="704">
