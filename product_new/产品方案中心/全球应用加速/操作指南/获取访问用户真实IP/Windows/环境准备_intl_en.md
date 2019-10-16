### Downloading the Files
Click [here](https://main.qcloudimg.com/raw/037dee0e98e30eb15055645ff0a48694.zip) to download the file.

## General Version
### File Description

| File               | Description |                                                         |
| ----------------- | ------------------------------------------------------------ |
| WinPcap_4_1_3.exe | The WinPcap driver, for details see [WinPcap Documentation](https://www.winpcap.org/). |
| lib_toa.lib       | TOA static library.                                                    |
| toa_fetcher.h     | The header file that the static library is dependent on.                                           |
| pcap.h            | The header file that the static library is dependent on.                                           |

### Environment
1. Double-click WinPcap_4_1_3.exe to install the WinPcap driver (no restart is required).
2. Add lib_toa.lib to the .lib library path of the project.
3. Add toa_fetcher.h and pcap.h to the header file of the project.

## Go Version
### File Description

| File                 | Description |                                                         |
| ------------------- | ------------------------------------------------------------ |
| WinPcap_4_1_3.exe   | The WinPcap driver, for details see [WinPcap Documentation](https://www.winpcap.org/). |
| toa_win.exe         | TOA server client for Windows                            |
| toa_win.conf        | Config file for TOA server client for Windows    
| program_auto_up.bat | bat script for TOA server client for Windows                              |
| demo.go             | A sample program written in the Go programming language, used to access the TOA service program.                    |

### Deployment Steps
1. Modify the toa_win.conf file as instructed below: 
<table>
<tr>
<th>Parameter</th><th>Required</th><th>Description</th>
</tr>
<tr>
<td>ToaWinPort</td><td> Yes </td><td> This is the service port of toa_win.exe. It is used to communicate with TOA obtaining program. The default is 9999.</td>
</tr>
<tr>
<td>NetworkCardIP</td><td> Yes </td><td> This is used to identify the IP address of the network interface, for example, 10.75.132.39. This is the NIC that communicates with the client’s NIC.</td>
</tr>
<tr>
<td>ServerListenIP</td><td> Yes </td><td> This is the IP address of the server, for example, 10.75.132.39. It is used to filter TCP flows.</td>
</tr>
<tr>
<td>ServerListenPortList</td><td> No </td><td> This is the port list of the server. It is used to filter TCP flows. At most 3 ports can be added.<br><b> Either ServerListenPortList or PortRange must be configured.</b></td>
</tr>
<tr>
<td>PortRange</td><td> No </td><td> This is the port range of the server. It is used to filter TCP flows. 3 port ranges can be added at most.<br><b> Either ServerListenPortList or PortRange must be configured.</b></td>
</tr>
<tr>
<td>CacheSeconds</td><td> No </td><td> The length of the cache time, Unit: seconds. The default is 15 seconds. </td>
</tr>
</table>

 >! The configuration file must be placed in the same directory as toa_win.exe.
 
 ![](https://main.qcloudimg.com/raw/d53c1cb161f45c9ad75789ac1c832af6.png)
2. Modify program_auto_up.bat.
Modify the path to the directory where the program is located. Add the script to the scheduled task, and execute it periodically. The script is used to monitor the toa_win.exe program and automatically activate the program when it exits.
![](https://main.qcloudimg.com/raw/046bbd4282aa51f85baa6879de8586d4.png)
3. Run the toa_win.exe program. The log is saved to toa_win.log in the same directory. Now, you can get the real IP address from TOA service through UDP communication. For details, see [Operation Guide](https://cloud.tencent.com/document/product/608/17670).
