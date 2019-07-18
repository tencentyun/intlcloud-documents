## Region and Availability Zone
### Mainland China
<table class="table-striped">
<tbody>
    <tr>
        <th>Region</th>
        <th>AZ</th>
    </tr> 
    <tr>
	      <td rowspan="3">South China (Guangzhou) <br>ap-guangzhou</td>
        <td>Guangzhou Zone 2 <br>ap-guangzhou-2</td>
    </tr>
    <tr>
        <td>Guangzhou Zone 3 <br>ap-guangzhou-3</td>
    </tr>
    <tr>
        <td>Guangzhou Zone 4 <br>ap-guangzhou-4</td>
    </tr>
   
    <tr>
        <td rowspan="3">East China (Shanghai) <br>ap-shanghai</td>
        <td>Shanghai Zone 1 <br>ap-shanghai-1</td>
    </tr>
    <tr>
        <td>Shanghai Zone 2 <br>ap-shanghai-2</td>
    </tr>
    <tr>
        <td>Shanghai Zone 3 <br>ap-shanghai-3</td>
    </tr>
    
    <tr>
            <td rowspan="3">North China (Beijing) <br>ap-beijing</td>
            <td>Beijing Zone 1 <br>ap-beijing-1</td>
    </tr>
    <tr>
            <td>Beijing Zone 2 <br>ap-beijing-2</td>
    </tr>
    <tr>
            <td>Beijing Zone 3 <br>ap-beijing-3</td>
    </tr>
</tbody>
</table>


### Global
<table class="table-striped">
    <tbody>
    <tr>
            <th>Region</th>
            <th>AZ</th>
        </tr>

        <tr>
            <td>Asia Pacific (Seoul) <br>ap-seoul</td>
            <td>Seoul Zone 1 (nodes in Seoul can cover Northeast Asia) <br>ap-seoul-1</td>
        </tr>
    </tbody>
</table>

>?
>?SQL Server Enterprise edition is available in East China (Shanghai), South China (Guangzhou), and North China (Beijing). SQL Server Standard edition is available in Korea (Seoul).




## Network
### Network Restrictions
- Tencent Cloud services in the same region can communicate with each other via private network.
- If a CVM instance on a private network need to access TencentDB for SQL Server on a basic network in a different AZ in the same region, you need to manually configure the subnet and assign a private network IP to enable communication.
- Tencent Cloud services in different regions cannot communicate with one another through a private basic network. Their communication through a private network requires [Peering Connection](https://cloud.tencent.com/document/product/553/18827).
- Currently, public IP is not supported by TencentDB for SQL Server. If you need to use a public IP, you can use the port mapping function of SSH2 to connect, configure, and manage an instance from the internet. For more information, see [Connecting to an Instance](https://cloud.tencent.com/document/product/238/11627#.E4.BA.8C.E3.80.81.E8.BF.9E.E6.8E.A5-sql-server-.E4.BA.91.E6.95.B0.E6.8D.AE.E5.BA.93.E5.AE.9E.E4.BE.8B.EF.BC.88.E6.9C.AC.E5.9C.B0.E7.AB.AF.EF.BC.89).
- When purchasing TencentDB for SQL Server, we recommend selecting the same region as your CVM instance to reduce the access delay.

### Network Connectivity Test
The network connectivity test tool provided on the [TencentDB for SQL Server purchase page](https://buy.cloud.tencent.com/sqlserver#/) can be used to check if there are CVM instances that can communicate with TencentDB for SQL Server over a private network for the selected regions/AZ and network types. 
![](https://main.qcloudimg.com/raw/deaf54baf86f53f842fbde47362fff24.png)
Click **View Details** to view information about the eligible CVM instances, including ID/instance name, AZ, configuration (CPU, memory, disk, and network), and master IP address. You can also use the search function to easily find eligible CVM instances.
![](https://main.qcloudimg.com/raw/dea8466faaaab332bf0b6f7a4932a49e.png)
