## Overview
This document guides you through the process of installing the TencentCloud Automation Tools (TAT) agent on a Lighthouse or CVM instance.

<dx-alert infotype="notice" title="">
- The TAT agent supports TencentOS Server, Linux releases and Windows operating systems. 
- TAT agent is only available for VPC-based instances.
</dx-alert>




## Directions
Choose the directions according to your operating system.


<dx-tabs>
::: Linux instances
1. Log in to the Linux instance.
   - For Lighthouse instances, see [Logging in to Linux Instances via WebShell]
   - For CVM instances, see [Logging in to Linux Instance Using Standard Login Method](https://intl.cloud.tencent.com/document/product/213/5436).
2. Run the following command with the root account to install the TAT agent.
```
wget -O - https://tat-gz-1258344699.cos.ap-guangzhou.myqcloud.com/install_agent.sh | sh
```

:::
::: Windows instances

1. Log in to the Windows instance.
 - For Lighthouse instances, see [Logging in to Windows Instance via VNC].
 - For CVM instances, see [Logging in Using Standard Method (Recommended)](https://intl.cloud.tencent.com/document/product/213/41018).


 2. Select the directions for your OS version: 


#### Windows Server 2016 and later versions
1. On the desktop, right click <img src="https://qcloudimg.tencent-cloud.cn/raw/0cfefcbe7474bf6b532a589c53314d5b.png" style="margin:-3px 0px"> and select <b>Windows PowerShell (Admin)</b> in the pop-up window.
2. Run the following command in the powershell window to install the TAT agent.
```
. { Invoke-WebRequest -useb https://tat-gz-1258344699.cos.ap-guangzhou.myqcloud.com/install_agent.ps1 } | Invoke-Expression;
```


#### Windows Server 2012 R2 and earlier versions
1. Download the TAT agent package at: 
```
https://tat-gz-1258344699.cos.ap-guangzhou.myqcloud.com/tat_agent_windows_x86_64.zip
```
2. Decompress the file and open the folder.
3. Right click `install.bat`, and select **Run as administrator** to install the TAT agent.
<dx-alert infotype="explain" title="">
TAT automatically creates a user named TAT-AGENT, and starts the tat-agent process as this user. You can check the creation process in the installation script. For more details, see [winutil.ps1](https://github.com/Tencent/tat-agent/blob/main/install/winutil.ps1).
</dx-alert>




:::
</dx-tabs>


## Notes
For Linux instances and Window instances using Windows Server 2016 and later versions, it’s unnecessary to change the URL. However, for instances using Windows Server 2012 R2 and earlier versions, if the instance does not have the access to internet and is not located in Guangzhou region, you need to modify the URL to a URL in the same region as of the instance in the following format: 
```
https://tat-${short-region}-1258344699.cos.${region}.myqcloud.com/tat_agent_windows_x86_64.zip
```
 - `short-region`: the short region name
 - `region`: the complete region name
 Check below for the list of short and complete region names:
 <table>
 <tr>
  <th>Region</th>
	<th>Short region name</th>
	<th>Complete region name</th>
 </tr>
 <tr>
  <td>Bangkok</td>
	<td>th</td>
	<td>ap-bangkok</td>
 </tr>
 <tr>
  <td>Beijing</td>
	<td>bj</td>
	<td>ap-beijing</td>
 </tr>
 <tr>
  <td>Beijing Finance</td>
	<td>bjjr</td>
	<td>ap-beijing-fsi</td>
 </tr>
 <tr>
  <td>Chengdu</td>
	<td>cd</td>
	<td>ap-chengdu</td>
 </tr>
 <tr>
  <td>Chongqing</td>
	<td>cq</td>
	<td> ap-chongqing</td>
 </tr>
 <tr>
  <td>Guangzhou</td>
	<td>gz</td>
	<td>ap-guangzhou</td>
 </tr>
 <tr>
  <td>Hong Kong (China)</td>
	<td>hk</td>
	<td>ap-hongkong</td>
 </tr>
 <tr>
  <td>Jakarta</td>
	<td>jkt</td>
	<td>ap-jakarta</td>
 </tr>
 <tr>
  <td>Mumbai</td>
	<td>in</td>
	<td> ap-mumbai</td>
 </tr>
 <tr>
  <td>Nanjing</td>
	<td>nj</td>
	<td> ap-nanjing</td>
 </tr>
 <tr>
  <td>Seoul</td>
	<td>kr</td>
	<td>ap-seoul</td>
 </tr>
 <tr>
  <td>Shanghai</td>
	<td>sh</td>
	<td>ap-shanghai</td>
 </tr>
 <tr>
  <td>Shanghai Finance</td>
	<td>shjr</td>
	<td>ap-shanghai-fsi</td>
 </tr>
 <tr>
  <td>Shenzhen Finance</td>
	<td>szjr</td>
	<td>ap-shenzhen-fsi</td>
 </tr>
 <tr>
  <td>Singapore</td>
	<td>sg</td>
	<td>ap-singapore</td>
 </tr>
 <tr>
  <td>Taipei (China)</td>
	<td>tpe</td>
	<td>ap-taipei</td>
 </tr>
 <tr>
  <td>Tokyo</td>
	<td>jp</td>
	<td>ap-tokyo</td>
 </tr>
 <tr>
  <td>Frankfurt</td>
	<td>de</td>
	<td>eu-frankfurt</td>
 </tr>
 <tr>
    <td>Virginia</td>
	<td>use</td>
	<td>na-ashburn</td>
 </tr>
 <tr>
  <td>Silicon Valley</td>
	<td>usw</td>
	<td>na-siliconvalley</td>
 </tr>
 <tr>
  <td>Toronto</td>
	<td>ca</td>
	<td>na-toronto</td>
 </tr>
 <tr>
  <td>São Paulo</td>
	<td>sao</td>
	<td>sa-saopaulo</td>
 </tr>
 </table>


