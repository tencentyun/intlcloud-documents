This document lists common ports of a CVM instance.
## Common Services on Linux
<table>
<tr>
<th><b>Service</b></th>
<th><b>Feature</b></th>
<th><b>Service Type</b></th>
<th><b>Service Name</b></th>
<th><b>Domain Name for Accessing Backend Service</b></th>
<th><b>Port for Accessing Backend Service</b></th>
</tr>
<tr>
<td rowspan="5">Instance initialization service</td> 
<td rowspan="5">Provides the instance initialization feature.</td> 
<td rowspan="5">Non-resident service, <br>which is exited after execution</td> 
<td rowspan="2">cloud-init</td> 
<td>mirrors.tencentyun.com</td> 
<td>80</td> 
</tr>
<tr>
<td>tlinux-mirrors.tencentyun.com</td>
<td>443</td>
</tr>
<tr>
<td rowspan="3">Public service</td>    
<td>ntpupdate.tencentyun.com</td>
<td>123</td>
</tr>
<tr>
<td>DHCP Server</td> 
<td>67 and 68</td> 
</tr>
<tr>
<td>DNS</td> 
<td>53</td> 
</tr>
<tr>
<td rowspan="3">Cloud Monitor</td> 
<td rowspan="2">Provides cloud monitoring capabilities.</td> 
<td rowspan="2">Resident service</td> 
<td rowspan="2">barad_agent</td> 
<td>receiver.barad.tencentyun.com</td> 
<td>80</td> 
</tr>
<tr>
<td>eventproxy.tencentyun.com</td>
<td>80</td>
</tr>
<tr>
<td>Installs and upgrades the cloud monitoring service.<br></td>    
<td>Resident service</td>
<td>startgate</td>
<td>update2.agent.tencentyun.com</td> 
<td>80</td> 
</tr>
<tr>
<td rowspan="4">Cloud Workload Protection</td> 
<td rowspan="4">Provides cloud security capabilities.</td> 
<td rowspan="4">Resident service</td> 
<td rowspan="4">YDService</td> 
<td>metadata.tencentyun.com</td> 
<td>80</td> 
</tr>
<tr>
<td>l.yd.tencentyun.com</td>
<td>8080</td>
</tr>
<tr>
<td>s.yd.tencentyun.com</td>    
<td>5574</td>
</tr>
<tr>
<td>u.yd.tencentyun.com</td> 
<td>9080 and 80</td> 
</tr>
</table>

## Common Services on Windows
<table>
<tr>
<th><b>Service</b></th>
<th><b>Feature</b></th>
<th><b>Service Type</b></th>
<th><b>Service Name</b></th>
<th><b>Domain Name for Accessing Backend Service</b></th>
<th><b>Port for Accessing Backend Service</b></th>
</tr>
<tr>
<td rowspan="5">Instance initialization service</td> 
<td rowspan="5">Provides the instance initialization feature.</td> 
<td rowspan="5">Non-resident service, <br>which is exited after execution</td> 
<td rowspan="2">cloudbase-init</td> 
<td>kms.tencentyun.com</td> 
<td>1688</td> 
</tr>
<tr>
<td>kms1.tencentyun.com</td>
<td>1688</td>
</tr>
<tr>
<td rowspan="3">Public service</td>    
<td>ntpupdate.tencentyun.com</td>
<td>123</td>
</tr>
<tr>
<td>DHCP Server</td> 
<td>67 and 68</td> 
</tr>
<tr>
<td>DNS</td> 
<td>53</td> 
</tr>
<tr>
<td rowspan="3">Cloud Monitor</td> 
<td rowspan="2">Provides cloud monitoring capabilities.</td> 
<td rowspan="2">Resident service</td> 
<td rowspan="2">BaradAgentSvc</td> 
<td>update2.agent.tencentyun.com</td> 
<td>80</td> 
</tr>
<tr>
<td>custom.message.tencentyun.com</td>
<td>8080</td>
</tr>
<tr>
<td>Installs and upgrades the cloud monitoring service.<br></td>    
<td>Resident service</td>
<td>startgate</td>
<td>update2.agent.tencentyun.com</td> 
<td>80</td> 
</tr>
<tr>
<td rowspan="4">Cloud Workload Protection<br></td> 
<td rowspan="4">Provides cloud security capabilities.</td> 
<td rowspan="4">Resident service</td> 
<td rowspan="4">YDService</td> 
<td>metadata.tencentyun.com</td> 
<td>80</td> 
</tr>
<tr>
<td>l.yd.tencentyun.com</td>
<td>8080</td>
</tr>
<tr>
<td>s.yd.tencentyun.com</td>    
<td>5574</td>
</tr>
<tr>
<td>u.yd.tencentyun.com</td> 
<td>9080 and 80</td> 
</tr>
</table>



