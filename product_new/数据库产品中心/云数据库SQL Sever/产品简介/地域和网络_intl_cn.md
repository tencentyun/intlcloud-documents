## 地域和可用区
### 中国大陆区域
<table class="table-striped">
<tbody>
    <tr>
        <th>地域</th>
        <th>可用区</th>
    </tr> 
    <tr>
	      <td rowspan="3">华南地区（广州）<br> ap-guangzhou</td>
        <td>广州二区<br> ap-guangzhou-2</td>
    </tr>
    <tr>
        <td>广州三区<br> ap-guangzhou-3</td>
    </tr>
    <tr>
        <td>广州四区<br> ap-guangzhou-4</td>
    </tr>

    <tr>
        <td rowspan="3">华东地区（上海）<br>ap-shanghai</td>
        <td>上海一区<br>ap-shanghai-1</td>
    </tr>
    <tr>
        <td>上海二区<br>ap-shanghai-2</td>
    </tr>
    <tr>
        <td>上海三区<br>ap-shanghai-3</td>
    </tr>
    
    <tr>
            <td rowspan="3">华北地区（北京）<br>ap-beijing</td>
            <td>北京一区<br>ap-beijing-1</td>
    </tr>
    <tr>
            <td>北京二区<br>ap-beijing-2</td>
    </tr>
    <tr>
            <td>北京三区<br>ap-beijing-3</td>
    </tr>
</tbody>
</table>


### 国际区域
<table class="table-striped">
    <tbody>
    <tr>
            <th>地域</th>
            <th>可用区</th>
        </tr>

        <tr>
            <td>亚太地区（首尔）<br>ap-seoul</td>
            <td>首尔一区（首尔节点可用于覆盖东北亚地区）<br>ap-seoul-1</td>
        </tr>
    </tbody>
</table>

>?
>
>- 华东地区（上海）、华南地区（广州）、华北地区（北京）售卖版本为SQL Server Enterprise，韩国地区（首尔）售卖版本为 SQL Server Standard。




## 网络
### 网络限制
- 处于同一地域的云服务产品之间通过内网互通。
- 处于同一地域不同可用区的私有网络云服务器访问不同可用区基础网络云数据库 SQL Server，需手动配置子网及分配私有网络 IP 后才能互通。
- 处于不同地域的云服务产品之间基础网络内网不能互通，私有网络之间需要对等连接支持。
- 云数据库 SQL Server 尚未开放实例的外网 IP，有需求的用户可以利用 SSH2 的端口映射在外网连接实例，并对其进行配置和管理，请参见 [连接实例](https://intl.cloud.tencent.com/document/product/238/11627)。
- 选购云数据库 SQL Server 时，建议选择与云服务器相同的地域，可降低访问延迟。

### 网络连通性检测
可用过 [云数据库 SQL Server 购买页](https://buy.cloud.tencent.com/sqlserver#/) 中提供的网络连通性检测工具，检查已选择的地域/可用区和网络类型中，是否存在可与云数据库 SQL Server 内网连通的云服务器。
![](https://main.qcloudimg.com/raw/deaf54baf86f53f842fbde47362fff24.png)
单击【查看详情】可查看内网可连通的云服务器相关信息，包括 ID/实例名、可用区、配置（CPU、内存、磁盘、网络）、主IP地址，并且提供搜索功能，帮助用户快速判断可与云数据库 SQL Server 内网连通的云服务器。
![](https://main.qcloudimg.com/raw/dea8466faaaab332bf0b6f7a4932a49e.png)
