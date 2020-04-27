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
      <td rowspan="8">标准存储</td>
      <td rowspan="1">中国大陆</td>
      <td>-</td>
      <td>0.058 USD/GB/Month (0.00008056 USD/GB/时)</td>
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
      </tr>
        <tr>
      <td>多伦多</td>
      <td>-</td>
      <td>0.09 USD/GB/月 （0.00012500 USD/GB/时）</td>
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

该小时 CFS 总费用 = (11*1024 + 105.6) * 0.00008056 = 0.92 USD

  
