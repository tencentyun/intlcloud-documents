### Downloading the files
Click [here](https://main.qcloudimg.com/raw/037dee0e98e30eb15055645ff0a48694.zip) to download the file.

## General Version
### File Description

| File | Description |
| ----------------- | ------------------------------------------------------------ |
| WinPcap_4_1_3.exe | WinPcap driver, see [WinPcap Documentation](https://www.winpcap.org/) for details |
| lib_toa.lib | TOA static library |
| toa_fetcher.h | Header file that the static library relies on |
| pcap.h | Header file that the static library relies on |

### Preparing the environment
1. Double-click WinPcap_4_1_3.exe to install the WinPcap driver (no restart is required).
2. Add lib_toa.lib to the .lib library path of the project.
3. Add toa_fetcher.h and pcap.h to the header file of the project.

## Go Version
### File Description

| File | Description |
| ------------------- | ------------------------------------------------------------ |
| WinPcap_4_1_3.exe | WinPcap driver, see [WinPcap Documentation](https://www.winpcap.org/) for details |
| toa_win.exe | TOA program for Windows server |
| toa_win.conf | Config file of TOA program for Windows server |
| program_auto_up.bat | bat script for Windows server |
| demo.go | A sample program written in Go language, used to access TOA services |

### Deployment Steps
1. Modify the toa_win.conf file as instructed below:
<table>
<tr>
<th>Parameter</th><th>Required</th><th>Description</th>
</tr>
<tr>
<td>ToaWinPort</td><td>Yes</td><td>The service port of toa_win.exe, used to communicate with TOA client, default is 9999.</td>
</tr>
<tr>
<td>NetworkCardIP</td><td>Yes</td><td>This is used to identify the IP address of the network interface, for example, 10.75.132.39. This is the NIC that communicates with the client.</td>
</tr>
<tr>
<td>ServerListenIP</td><td>Yes</td><td>The IP address of the server, for example, 10.75.132.39. It is used to filter TCP flows.</td>
</tr>
<tr>
<td>ServerListenPortList</td><td>No</td><td>The port list of the server. It is used to filter TCP flows. A maximum of 3 ports can be added.<br><b>Either ServerListenPortList or PortRange must be configured.</b></td>
</tr>
<tr>
<td>PortRange</td><td>No</td><td>The port range of the server. It is used to filter TCP flows. A maximum of 3 port ranges can be added.<br><b>Either ServerListenPortList or PortRange must be configured.</b></td>
</tr>
<tr>
<td>CacheSeconds</td><td>No</td><td>The length of the cache time, unit in seconds. The default is 15 seconds. </td>
</tr>
</table>

 >The configuration file must be placed in the same directory as toa_win.exe.
 
 ![](https://main.qcloudimg.com/raw/d53c1cb161f45c9ad75789ac1c832af6.png)
2. Modifying program_auto_up.bat.
Modify the path to the directory where the program is located. Add the script to the scheduled task, and execute on it periodically. The script is used to monitor the toa_win.exe program and automatically activate the program when it exits.
![](https://main.qcloudimg.com/raw/046bbd4282aa51f85baa6879de8586d4.png)
3. Run the toa_win.exe program. The log is saved to toa_win.log in the same directory. Now, you can get the real IP address from TOA services through UDP communication. For details, see [How to Use](https://cloud.tencent.com/document/product/608/17670).
