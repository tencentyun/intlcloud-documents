## 计费说明

<table>
   <tr>
      <th>计费项</th>
      <th>计费方式</th>
      <th>计费周期</th>
      <th>计费周期说明</th>
   </tr>
   <tr>
      <td>文件存储量</td>
      <td>按量计费（后付费）</td>
      <td>小时</td>
      <td>每小时进行扣费、存储量按单位小时内实际使用存储空间的最大值计算（峰值）</td>
   </tr>
</table>



## 存储空间

文件系统创建时，会默认占用 32MB 的存储空间，该存储量将不会被计入实际计费的存储空间。

## 支持地域

以下是 CFS 文件存储已开放使用的地区：

> 已售罄地区主机或服务若需要使用文件存储，建议在该地域下选择一个 VPC 、在其他有的资源可用区下创建子网，然后在该子网下创建 CFS 文件系统，详情请参阅 [挂载帮助](https://intl.cloud.tencent.com/document/product/582/9551)。

<table>
<tr>
    <th>地域</th>
    <th>可用区</th>
  </tr>
  <tr>
    <td rowspan="4">北京</td>
    <td>北京一区</td>
  </tr>
	<tr>
    <td>北京二区</td>
  </tr>
	<tr>
    <td>北京三区</td>
  </tr>
		<tr>
    <td>北京四区</td>
  </tr>
	<tr>
    <td rowspan="2">上海</td>
    <td>上海二区</td>
  </tr>
	<tr>
    <td>上海三区</td>
  </tr>
	<tr>
    <td rowspan="3">广州</td>
    <td>广州二区</td>
  </tr>
	<tr>
    <td>广州三区</td>
  </tr>
	<tr>
    <td>广州四区</td>
  </tr>
	<tr>
    <td>成都</td>
    <td>成都一区</td>
  </tr>
	<tr>
    <td>中国香港</td>
    <td>中国香港一区</td>
  </tr>
	<tr>
    <td>新加坡</td>
    <td>新加坡一区</td>
  </tr>
  <tr>
    <td>东京</td>
    <td>东京一区</td>
  </tr>
    <tr>
    <td>硅谷</td>
    <td>硅谷一区</td>
  </tr>
  <tr>
    <td>孟买</td>
    <td>孟买一区</td>
  </tr>
    <tr>
    <td>首尔</td>
    <td>首尔一区</td>
  </tr>
</table>



## CIFS/SMB 公测说明

CIFS/SMB 协议本阶段公测已结束，后续开放时间请静待通知。已经获得公测名额的客户可以继续使用， CIFS/SMB 文件系统暂不收费。	


## 价格详情

自2017年11月10日凌晨起，中国大陆标准型文件存储所有地区执行以下最新价格。

>NFS 文件系统及 CIFS/SMB 文件系统统一价格。

<table>
   <tr>
      <th>存储类型</th>
      <th>地区</th>
      <th>存储空间的最大值（峰值）区间</th>
      <th nowrap="nowrap">单价</th>
   </tr>
   <tr>
      <td rowspan="7">标准存储</td>
      <td rowspan="1">中国大陆</td>
      <td>-</td>
      <td>0.058 USD/GB/Month (0.00008056 USD/GB/hr)</td>
   </tr>
   <tr>
      <td >中国香港</td>
      <td>-</td>
      <td>0.09 USD/GB/月 （0.000125 USD/GB/时）</td>
   </tr>
      <td>新加坡</td>
      <td>-</td>
      <td>0.09 USD/GB/月 （0.000125 USD/GB/时）</td>
   </tr>
   <tr>
      <td>东京</td>
      <td>-</td>
      <td>0.09 USD/GB/月 （0.000125 USD/GB/时）</td>
   </tr>
     <tr>
      <td>硅谷</td>
      <td>-</td>
      <td>0.08 USD/GB/月 （0.000111111 USD/GB/时）</td>
   </tr>
     <tr>
      <td>孟买</td>
      <td>-</td>
      <td>0.09 USD/GB/月 （0.000125 USD/GB/时）</td>
   </tr>
        <tr>
      <td>首尔</td>
      <td>-</td>
      <td>0.09 USD/GB/月 （0.000125 USD/GB/时）</td>
   </tr>
      <tr>
      <td rowspan="1">性能存储</td>
      <td rowspan="2">中国大陆</td>
      <td> - </td>
      <td>0.26 USD/GB/月 （0.000361111 USD/GB/时）</td>
   </tr>
</table>



## 计费案例

某企业拥有20台云服务器（CVM），分别访问2个中国大陆地区的文件系统。 文件系统 A 用于做冷数据存储，标准型存储量为11TB，且无增长。文件系统 B 用于企业云盘， 当前该小时中标准型峰值存储量为105.6GB。  

该小时 CFS 总费用 = （11*1024+105.6 ）* 0.00048611= 5.53 USD

  
