## 购买 CVM 实例的账号限制

- 用户需注册腾讯云账号，注册指引可参考 [注册腾讯云](https://intl.cloud.tencent.com/document/product/378/17985)。
- 创建按量计费的云服务器时系统会冻结一个小时的主机费用，请确保账号有足够余额以支付订单。

## CVM 实例的使用限制

- 暂不支持虚拟化软件安装和再进行虚拟化（如安装使用 VMware 或者 Hyper-V）。
- 暂不支持声卡应用、直接加载外接硬件设备（如 U 盘、外接硬盘、银行 U 盾等）。
- 公网网关目前仅支持 Linux 系统。

## CVM 实例的购买限制

- 每个用户在每个可用区可购买的按量计费云服务器实例的**总数量**为30台或60台不等，具体视云服务器购买页实际情况而定。
- 更多详情请参考 [CVM 实例购买限制](https://intl.cloud.tencent.com/document/product/213/2664)。


## 镜像相关限制

- 公共镜像暂无使用限制。
- 自定义镜像：每个地域下最多支持10个自定义镜像。
- 共享镜像：每个自定义镜像最多可共享给50个腾讯云用户，且仅支持共享到对方账户相同地域下。
- 更多详情请参考 [镜像类型限制](https://intl.cloud.tencent.com/document/product/213/4941)。


## 网卡相关限制

根据 CPU 和内存配置不同，云服务器可以绑定的弹性网卡数和单网卡绑定内网 IP 数有较大不同，网卡和单网卡 IP 配额数如下表所示：
>! 单个网卡绑定 IP 数量仅代表网卡可以绑定的 IP 数量上限，不承诺按照上限提供 EIP 配额，账号的 EIP 配额按照 [EIP 使用限制](https://intl.cloud.tencent.com/document/product/213/5733) 提供。

<dx-tabs>
::: 云服务器支持绑定的弹性网卡配额
<table >
   <tr >
    <th width="6%"  rowspan="2" style = "text-align:center;">机型</th>
    <th  width="8%"  rowspan="2" style = "text-align:center;">实例类型</th>
    <th width="86%" colspan="10" style = "text-align:center;">弹性网卡配额</th>
   </tr>
   <tr >
    <th style = "text-align:center;">CPU：1核</th>
    <th style = "text-align:center;">CPU：2核</th>
    <th style = "text-align:center;">CPU：4核</th>
    <th style = "text-align:center;">CPU：6核</th>
    <th style = "text-align:center;">CPU：8核</th>
    <th style = "text-align:center;">CPU：10核</th>
    <th style = "text-align:center;">CPU：12核</th>
    <th style = "text-align:center;">CPU：14核</th>
    <th style = "text-align:center;">CPU：16核</th>
    <th style = "text-align:center;">CPU：&gt;16核</th>
   </tr>
   <tr >
    <th rowspan="9" style = "text-align:center;">标准型</th>
    <th style = "text-align:center;">标准型 S5</th>
    <td >2</td>
    <td >4</td>
    <td >4</td>
    <td >-</td>
    <td >6</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >8</td>
    <td >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;">标准存储增强型 S5se</th>
    <td >-</td>
    <td >-</td>
    <td >4</td>
    <td >-</td>
    <td >6</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >8</td>
    <td >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;">标准型 SA2</th>
    <td >2</td>
    <td >4</td>
    <td >4</td>
    <td >-</td>
    <td >6</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >8</td>
    <td >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;">标准型 S4</th>
    <td >2</td>
    <td >4</td>
    <td >4</td>
    <td >-</td>
    <td >6</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >8</td>
    <td >8</td>
   </tr>
   <tr>
    <th style = "text-align:center;">标准网络优化型 SN3ne</th>
    <td >2</td>
    <td >4</td>
    <td >4</td>
    <td >-</td>
    <td >6</td>
    <td >-</td>
    <td >8</td>
    <td >-</td>
    <td >8</td>
    <td >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;">标准型 S3</th>
    <td >2</td>
    <td >4</td>
    <td >4</td>
    <td >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >8</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;">标准型 SA1</th>
    <td >2</td>
    <td >2</td>
    <td >4</td>
    <td >-</td>
    <td >6</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >8</td>
    <td >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;">标准型 S2</th>
    <td >2</td>
    <td >4</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >8</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;">标准型 S1</th>
    <td  >2</td>
    <td  >4</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >8</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr >
    <th rowspan="2" style = "text-align:center;">高 IO 型</th>
    <th style = "text-align:center;">高 IO 型 IT5</th>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr  >
    <th  style = "text-align:center;">高 IO 型IT3</th>
    <td  >-</td>
    <td  >-</td>
    <td >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr >
    <th rowspan="5" style = "text-align:center;">内存型</th>
    <th  style = "text-align:center;">内存型 M5</th>
    <td  >2</td>
    <td  >4</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >8</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;">内存型 M4</th>
    <td >2</td>
    <td  >4</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >8</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr  >
    <th  style = "text-align:center;">内存型 M3</th>
    <td  >2</td>
    <td  >4</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >8</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr  >
    <th  style = "text-align:center;">内存型 M2</th>
    <td  >2</td>
    <td  >4</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >8</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr  >
    <th  style = "text-align:center;">内存型 M1</th>
    <td  >2</td>
    <td  >4</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >8</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr >
    <th rowspan="4" style = "text-align:center;">计算型</th>
    <th  style = "text-align:center;">计算型 C4</th>
    <td  >-</td>
    <td  >-</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;">计算网络增强型 CN3</th>
    <td  >-</td>
    <td  >-</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr  >
    <th  style = "text-align:center;">计算型 C3</th>
    <td  >-</td>
    <td >-</td>
    <td >4</td>
    <td  >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td >8</td>
    <td  >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;" >计算型 C2</th>
    <td  >-</td>
    <td  >-</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td >8</td>
    <td  >8</td>
   </tr>
   <tr >
    <th  rowspan="6" style = "text-align:center;">GPU 机型</th>
     <th class="xl71" x:str style = "text-align:center;">GPU 计算型 GN6</th>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;">GPU 计算型 GN6S</th>
    <td  >-</td>
    <td  >-</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
   </tr>
   <tr >
    <th style = "text-align:center;">GPU 计算型 GN7</th>
    <td >-</td>
    <td >-</td>
   <td  >4</td>
    <td >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >8</td>
   </tr>
   <tr  >
    <th style = "text-align:center;">GPU 计算型 GN8</th>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >4</td>
    <td >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >8</td>
    <td  >-</td>
    <td  >8</td>
   </tr>
   <tr >
    <th  style = "text-align:center;">GPU 计算型 GN10X</th>
   <td >-</td>
    <td  >-</td>
    <td  >-</td>
     <td  >-</td>
    <td  >6</td>
      <td  >-</td>
    <td  >-</td>
    <td  >-</td>
     <td  >-</td>
    <td  >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;">GPU 计算型 GN10Xp</th>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >6</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td >8</td>
   </tr>
   <tr  >
    <th style = "text-align:center;">FPGA 机型</th>
    <th style = "text-align:center;">FPGA 加速型 FX4</th>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >6</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >8</td>
   </tr>
   <tr >
    <th rowspan="3" style = "text-align:center;">大数据型</th>
    <th  style = "text-align:center;">大数据型 D3</th>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >6</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;">大数据型 D2</th>
    <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >6</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;">大数据型 D1</th>
    <td >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >6</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >-</td>
    <td  >8</td>
   </tr>
   <tr >
    <th colspan="2" style = "text-align:center;">裸金属云服务器</th>
    <td colspan="10" style = "text-align:center;">不支持绑定弹性网卡</td>
   </tr>
  </table>
:::
::: 云服务器单网卡支持绑定的内网IP配额
<table >
   <tr >
    <th width="6%"  rowspan="2" style = "text-align:center;">机型</th>
    <th  width="8%"  rowspan="2" style = "text-align:center;">实例类型</th>
    <th width="86%" colspan="10" style = "text-align:center;">单网卡绑定内网 IP 配额</th>
   </tr>
   <tr >
    <th style = "text-align:center;">CPU：1核</th>
    <th style = "text-align:center;">CPU：2核</th>
    <th style = "text-align:center;">CPU：4核</th>
    <th style = "text-align:center;">CPU：6核</th>
    <th style = "text-align:center;">CPU：8核</th>
    <th style = "text-align:center;">CPU：10核</th>
    <th style = "text-align:center;">CPU：12核</th>
    <th style = "text-align:center;">CPU：14核</th>
    <th style = "text-align:center;">CPU：16核</th>
    <th style = "text-align:center;">CPU：&gt;16核</th>
   </tr>
   <tr >
    <th rowspan="9" style = "text-align:center;">标准型</th>
    <th style = "text-align:center;">标准型 S5</th>
    <td >6</td>
    <td >10</td>
    <td >10</td>
    <td >-</td>
    <td >20</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >30</td>
    <td >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">标准存储增强型 S5se</th>
    <td >-</td>
    <td >-</td>
    <td >20</td>
    <td >-</td>
    <td >20</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >30</td>
    <td >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">标准型 SA2</th>
    <td >6</td>
    <td >10</td>
    <td >10</td>
    <td >-</td>
    <td >20</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >30</td>
    <td >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">标准型 S4</th>
    <td >6</td>
    <td >10</td>
    <td >10</td>
    <td >-</td>
    <td >20</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >30</td>
    <td >30</td>
   </tr>
   <tr>
    <th style = "text-align:center;">标准网络优化型 SN3ne</th>
    <td >6</td>
    <td >10</td>
    <td >10</td>
    <td >-</td>
    <td >20</td>
    <td >-</td>
    <td >30</td>
    <td >-</td>
    <td >30</td>
    <td >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">标准型 S3</th>
    <td >6</td>
    <td >10</td>
    <td >10</td>
    <td >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >30</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">标准型 SA1</th>
    <td >内存=1G：2<br/>内存&gt;1G：6</td>
    <td >10</td>
    <td >内存=8G：10<br/>内存=16G：20</td>
    <td >-</td>
    <td >20</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >30</td>
    <td >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">标准型 S2</th>
    <td >6</td>
    <td >10</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >30</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">标准型 S1</th>
    <td  >6</td>
    <td  >10</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >30</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr >
    <th rowspan="2" style = "text-align:center;">高 IO 型</th>
    <th style = "text-align:center;">高 IO 型 IT5</th>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr  >
    <th  style = "text-align:center;">高 IO 型IT3</th>
    <td  >-</td>
    <td  >-</td>
    <td >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr >
    <th rowspan="5" style = "text-align:center;">内存型</th>
    <th  style = "text-align:center;">内存型 M5</th>
    <td  >6</td>
    <td  >10</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >30</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">内存型 M4</th>
    <td >6</td>
    <td  >10</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >30</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr  >
    <th  style = "text-align:center;">内存型 M3</th>
    <td  >6</td>
    <td  >10</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >30</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr  >
    <th  style = "text-align:center;">内存型 M2</th>
    <td  >6</td>
    <td  >10</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >30</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr  >
    <th  style = "text-align:center;">内存型 M1</th>
    <td  >6</td>
    <td  >10</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >30</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr >
    <th rowspan="4" style = "text-align:center;">计算型</th>
    <th  style = "text-align:center;">计算型 C4</th>
    <td  >-</td>
    <td  >-</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">计算网络增强型 CN3</th>
    <td  >-</td>
    <td  >-</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr  >
    <th  style = "text-align:center;">计算型 C3</th>
    <td  >-</td>
    <td >-</td>
    <td >10</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td >30</td>
    <td  >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;" >计算型 C2</th>
    <td  >-</td>
    <td  >-</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td >30</td>
    <td  >30</td>
   </tr>
   <tr >
    <th  rowspan="7" style = "text-align:center;">GPU 机型</th>
    <th  style = "text-align:center;">GPU 计算型 GN2</th>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >30</td>
   </tr>
   <tr >
    <th class="xl71" x:str style = "text-align:center;">GPU 计算型 GN6</th>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">GPU 计算型 GN6S</th>
    <td  >-</td>
    <td  >-</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
   </tr>
   <tr >
    <th style = "text-align:center;">GPU 计算型 GN7</th>
    <td >-</td>
    <td >-</td>
   <td  >10</td>
    <td >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >30</td>
   </tr>
   <tr  >
    <th style = "text-align:center;">GPU 计算型 GN8</th>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >10</td>
    <td >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >30</td>
    <td  >-</td>
    <td  >30</td>
   </tr>
   <tr >
    <th  style = "text-align:center;">GPU 计算型 GN10X</th>
   <td >-</td>
    <td  >-</td>
    <td  >-</td>
     <td  >-</td>
    <td  >20</td>
      <td  >-</td>
    <td  >-</td>
    <td  >-</td>
     <td  >-</td>
    <td  >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">GPU 计算型 GN10Xp</th>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >20</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td >30</td>
   </tr>
   <tr  >
    <th style = "text-align:center;">FPGA 机型</th>
    <th style = "text-align:center;">FPGA 加速型 FX4</th>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >20</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >30</td>
   </tr>
   <tr >
    <th rowspan="3" style = "text-align:center;">大数据型</th>
    <th  style = "text-align:center;">大数据型 D3</th>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >20</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">大数据型 D2</th>
    <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >20</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">大数据型 D1</th>
    <td >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >20</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >-</td>
    <td  >30</td>
   </tr>
   <tr >
    <th colspan="2" style = "text-align:center;">裸金属云服务器</th>
    <td colspan="10" style = "text-align:center;">不支持绑定弹性网卡</td>
   </tr>
  </table>
:::
</dx-tabs>


## 带宽相关限制

- 出网带宽上限（下行带宽）：
 - 2020年2月24日00:00以后创建的机器按以下规则执行：
<table>
<tr><th rowspan="2">网络计费模式</th><th colspan="2">实例</th><th rowspan="2">带宽上限的可设置范围（Mbps）</th></tr>
<tr><th style="width: 18.5607%;">实例计费模式</th><th style="width: 24.5814%;">实例配置</th></tr>
<tr><td>按流量计费</td><td>按量计费实例</td><td>ALL</td><td>0 - 100</td></tr>
<tr><td>按带宽计费</td><td>按量计费实例</td><td>ALL</td><td>0 - 100</td></tr>
<tr><td>共享带宽</td><td colspan="2">ALL</td><td>0 - 2000</td></tr>
</table>

 - 2020年2月24日00:00以前创建的机器按以下规则执行： 
<table>
<tr><th rowspan="2">网络计费模式</th><th colspan="2">实例</th><th rowspan="2">带宽上限的可设置范围（Mbps）</th></tr>
<tr><th>实例计费模式</th><th>实例配置</th></tr>
<tr><td>按流量计费</td><td>按量计费实例</td><td>ALL</td><td>0 - 100</td></tr>
<tr><td>按带宽计费</td><td>按量计费实例</td><td>ALL</td><td>0 - 100</td></tr>
<tr><td>共享带宽</td><td colspan="2">ALL</td><td>0 - 2000</td></tr>
</table>


- 入网带宽上限（上行带宽）：
	- 用户购买的固定带宽大于10Mbps时，腾讯云会分配与购买的带宽相等的外网入方向带宽。
	- 用户购买的固定带宽小于10Mbps时，腾讯云会分配10Mbps外网入方向带宽。

## 磁盘相关限制

<table>
	<tr><th>限制类型</th><th>限制说明</th></tr>
	<tr><td>弹性云盘能力</td><td>自2018年5月起，随云服务器一起购买的数据盘均为弹性云硬盘，支持从云服务器上卸载并重新挂载。 本功能在所有 <a href="https://intl.cloud.tencent.com/document/product/213/35071">可用区</a> 均支持。</td></tr>
	<tr><td>云硬盘性能限制</td><td>I/O 性能同时生效。</br>例如，1TB的 SSD 云硬盘，最大随机 IOPS 能达到26,000，意味着读 IOPS 和写 IOPS 均可达到该值。同时，由于多个性能限制，该例中使用 block size 为4KB/8KB的 I/O 可达到 IOPS 最大值，但使用 block size 为16KB的 I/O 则无法达到 IOPS 最大值（吞吐已经达到了260MB/s的限制）。</td></tr>
	<tr><td>单台云服务器可挂载弹性云硬盘数量</td><td>最多20块。</td></tr>
	<tr><td>单地域下快照配额</td><td>64 + 地域内云硬盘数量 * 64（个）。</td></tr>
	<tr><td>云硬盘可挂载云服务器限制</td><td>云服务器和云硬盘必须在同一可用区下。</td></tr>
	<tr><td>快照回滚限制</td><td>快照数据只能回滚到创建快照的源云硬盘上。</td></tr>
	<tr><td>快照创建云硬盘类型限制</td><td>只有数据盘快照才能用来创建新的弹性云硬盘。</td></tr>
	<tr><td>快照创建云硬盘大小限制</td><td>使用快照创建的新云硬盘容量必须大于或等于快照源云硬盘的容量。</td></tr>
</tr>
</table>



## 安全组相关限制

- 安全组区分地域，一台云服务器只能与相同地域中的安全组进行绑定。
- 安全组适用于任何处在 [网络环境](https://intl.cloud.tencent.com/document/product/213/5227) 的云服务器实例。
- 每个用户在每个地域每个项目下最多可设置50个安全组。
- 一个安全组入站方向或出站方向的访问策略，各最多可设定100条。
- 一个云服务器可以加入多个安全组，一个安全组可同时关联多个云服务器。
- **基础网络**内云服务器绑定的安全组**无法过滤**来自（或去往）腾讯云上的关系型数据库（MySQL、MariaDB、SQL Server、PostgreSQL）、NoSQL 数据库（Redis、Memcached）的数据包。如果您需要过滤这类实例的流量，您可以使用 iptables 或者购买云防火墙产品实现。
- 相关配额限制如下表所示：
<table>
<tr><th>功能描述</th><th>限制</th></tr>
<tr><td>安全组个数</td><td>50个/地域</td></tr>
<tr><td>安全组规则数</td><td>100条/入站方向，100条/出站方向</td></tr>
<tr><td>单个安全组关联的云服务器实例数</td><td>2000个</td></tr>
<tr><td>每个云服务器实例可以关联的安全组个数</td><td>5个</td></tr>
<tr><td>每个安全组可以引用的安全组 ID 的个数</td><td>10个</td></tr>
</table>

## VPC 相关限制

| 资源| 限制（个） | 
|---------|---------|
| 每个账号每个地域内的私有网络个数 | 20 | 
| 每个私有网络内的子网数 | 100 |
| 每个私有网络支持关联的基础网络主机个数 | 100 |
| 每个私有网络内的路由表个数 | 10 |
| 每个子网关联路由表个数 | 1 |
| 每个路由表的路由策略数 | 50 |
| 每个私有网络的 HAVIP 默认配额数 | 10 |

