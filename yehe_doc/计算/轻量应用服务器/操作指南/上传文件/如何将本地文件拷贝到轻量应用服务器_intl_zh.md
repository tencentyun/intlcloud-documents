本文介绍如何将您本地的文件拷贝至轻量应用服务器，或将轻量应用服务器上的文件下载至本地。


## 选择传输方式

### 使用自动化助手传输文件
您可通过自动化助手，使用浏览器直接将本地文件上传到轻量应用服务器，或将服务器文件下载到本地。

<table>
<tr>
<th>操作方式</th>
<th>使用限制</th>
</tr>
<tr>
<td>上传文件至轻量应用服务器</td>
<td>
<ul style="margin-bottom:0px">
<li>上传文件大小限制为36KB，且为文本文件</li>
<li>仅支持下载已上传的文件</li>
</ul>
</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/1103/41523">使用 WebShell 登录轻量应用服务器时上传/下载文件</a></td>
<td>
<ul style="margin-bottom:0px">
<li>仅支持 Linux 操作系统的轻量应用服务器</li>
<li>仅支持上传文件至 home > lighthouse 目录</li>
</ul>
</td>
</tr>
</table>



### 其他方式
您也可针对本地操作系统的类型以及购买的轻量应用服务器类型，参考以下方式进行操作。

 <table>
      <tr bgcolor=#5291F8>
        <th>本地操作系统类型</th>
        <th>轻量应用服务器操作系统（Linux）</th>
        <th>轻量应用服务器操作系统（Windows）</th>		 
      </tr>
      <tr>
        <td> Windows </td>
				<td>
					<ul style="margin: 0;"><li><a href="https://intl.cloud.tencent.com/document/product/1103/41531">通过 WinSCP 方式上传文件到轻量应用服务器</a></li>
					<li><a href="https://intl.cloud.tencent.com/document/product/1103/41532">通过 FTP 方式上传文件到轻量应用服务器</a></li></ul>
				</td>
				<td><a href="https://intl.cloud.tencent.com/document/product/1103/41533">通过远程桌面上传文件到轻量应用服务器</a></td>
      </tr>
      <tr>
        <td> Linux </td>
				<td rowspan=2>
					<ul style="margin: 0;"><li><a href="https://intl.cloud.tencent.com/document/product/1103/41534">通过 SCP 方式上传文件到轻量应用服务器</a></li>
					<li><a href="https://intl.cloud.tencent.com/document/product/1103/41535">通过 FTP 方式上传文件到轻量应用服务器</a></li></ul></td>
				<td><a href="https://intl.cloud.tencent.com/document/product/1103/41536">通过远程桌面上传文件到轻量应用服务器</a></td>
      </tr>
      <tr>
        <td>Mac OS</td>
        <td><a href="https://intl.cloud.tencent.com/document/product/1103/41537">通过远程桌面上传文件到轻量应用服务器</a></td>
      </tr>
    </table>
例如，您的本地电脑的操作系统为 Windows，而您购买的轻量应用服务器操作系统为 Linux，则您可以通过 WinSCP 方式上传文件到轻量应用服务器。




## 下一步操作
当您有比较重要的业务数据或者个人文件需要备份时，完成文件上传到轻量应用服务器之后，您还可以对轻量应用服务器实例的系统盘做快照。可以参考 [管理快照](https://intl.cloud.tencent.com/document/product/1103/41394) 了解关于快照适用的场景以及使用方式。

## 出现问题？
非常抱歉您在使用时出现问题，您可以第一时间通过 [提交工单](https://console.intl.cloud.tencent.com/workorder/category) 联系我们，也可以先参考相关文档进行问题定位和解决。

