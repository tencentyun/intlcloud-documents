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


>SQL Server Enterprise edition is available in East China (Shanghai), South China (Guangzhou), and North China (Beijing). SQL Server Standard edition is available in Korea (Seoul).




## Network
### Network Restrictions
- Tencent Cloud services in the same region can communicate with each other via private network.
- If a CVM instance on a private network need to access TencentDB for SQL Server on a basic network in a different AZ in the same region, you need to manually configure the subnet and assign a private network IP to enable communication.
- Tencent Cloud services in different regions cannot communicate with one another through a private basic network. Their communication through a private network requires Peering Connection.
- Currently, public IP is not supported by TencentDB for SQL Server. If you need to use a public IP, you can use the port mapping function of SSH2 to connect, configure, and manage an instance from the internet. 
- When purchasing TencentDB for SQL Server, we recommend selecting the same region as your CVM instance to reduce the access delay.

### Network Connectivity Test
The network connectivity test tool provided on the [TencentDB for SQL Server purchase page](https://buy.cloud.tencent.com/sqlserver#/) can be used to check if there are CVM instances that can communicate with TencentDB for SQL Server over a private network for the selected regions/AZ and network types. 
![](https://main.qcloudimg.com/raw/a302d5de7907b7820a0a6d60c4cc5d19.png)
Click **View Details** to view information about the eligible CVM instances, including ID/instance name, AZ, configuration (CPU, memory, disk, and network), and master IP address. You can also use the search function to easily find eligible CVM instances.
![](https://main.qcloudimg.com/raw/5d39b94b29e77d342e1d6379e470d70f.png)
