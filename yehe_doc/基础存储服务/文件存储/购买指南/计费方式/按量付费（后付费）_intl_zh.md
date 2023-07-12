文件存储（Cloud File Storage，CFS）的计费方式分为按量计费（后付费）和资源包（预付费）两种，本文主要介绍按量计费的计费详情。按量计费方式适用于文件存储提供服务的所有地域。CFS 当前根据用户的存储容量计量项用量进行计费，对用户账户按小时进行扣费结算。

若您对用量具有详细的评估或者有额外的吞吐需求，我们推荐您使用 [资源包（预付费）](https://intl.cloud.tencent.com/document/product/582/40330) 的方式，这样能享受更多的优惠，您可以到 [资源包购买页](https://intl.cloud.tencent.com/login/subAccount?s_url=https%3A%2F%2Fbuy.cloud.tencent.com%2Fcfs_package%3Frid%3D1%26zoneId%3D100003%26StorageType%3DHP%26FileSystemId%3Dcfs-3bd20beed) 购买所需的资源包。

## 计费说明

<table>
   <tr>
      <th>计费项</th>
      <th>计费方式</th>
      <th>计费周期</th>
      <th>计费周期说明</th>
   </tr>
   <tr>
      <td>存储量</td>
      <td>按量计费（后付费）</td>
      <td>小时</td>
      <td>每小时进行扣费、存储量按单位小时内实际使用存储空间的最大值计算（峰值）</td>
   </tr>
</table>


## 后付费价格详情 

>? NFS 文件系统及 CIFS/SMB 文件系统统一价格。
>

<table>
   <tr>
      <th>存储类型</th>
      <th>地区</th>
      <th>存储空间的最大值（峰值）区间</th>
      <th nowrap="nowrap">单价</th>
   </tr>
   <tr>
      <td rowspan="7">通用标准型存储</td>
      <td rowspan="1">中国大陆</td>
      <td>-</td>
      <td>0.058美元/GiB/月 （0.00008056 美元/GiB/时）</td>
   </tr>

   <tr>
      <td rowspan="1">中国香港</td>
      <td>-</td>
      <td>0.09美元/GiB/月 （0.000125 美元/GiB/时）</td>
   </tr>
  <tr>
      <td>新加坡</td>
      <td>-</td>
      <td>0.09美元/GiB/月 （0.000125 美元/GiB/时）</td>
   </tr>
   <tr>
      <td>东京</td>
      <td>-</td>
      <td>0.09美元/GiB/月 （0.000125 美元/GiB/时）</td>
   </tr>
     <tr>
      <td>硅谷</td>
      <td>-</td>
      <td>0.08美元/GiB/月（0.00011111 元/GiB/时）</td>
   </tr>
     <tr>
      <td>孟买</td>
      <td>-</td>
      <td>0.09美元/GiB/月 （0.000125 美元/GiB/时）</td>
   </tr>
        <tr>
      <td>首尔</td>
      <td>-</td>
      <td>0.09美元/GiB/月 （0.000125 美元/GiB/时）</td>
   </tr>
     <tr>
      <td rowspan="1">Turbo标准型存储</td>
      <td rowspan="1">中国大陆</td>
      <td> 40TiB以上 </td>
      <td>0.09美元/GiB/月 （0.000125 美元/GiB/时）</td>
   </tr>
     <tr>
      <td rowspan="1">Turbo性能型存储</td>
      <td rowspan="1">中国大陆</td>
      <td> 20TiB以上 </td>
      <td>0.2美元/GiB/月 （0.00027778 元/GB/时）</td>
   </tr>
</table>

