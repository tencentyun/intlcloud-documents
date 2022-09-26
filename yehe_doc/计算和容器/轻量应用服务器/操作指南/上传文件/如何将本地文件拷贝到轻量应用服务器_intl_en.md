This document describes how to upload local files to a Lighthouse instance or download the files on it to your local file system.


## Transfer Method

### Using TencentCloud Automation Tools to transfer files
You can use TencentCloud Automation Tools to upload a local file to a Lighthouse instance or download a file on it to your local file system through the browser.

<table>
<tr>
<th>Operation</th>
<th>Use Limits</th>
</tr>
<tr>
<td>Uploading a file to a Lighthouse instance</td>
<td>
<ul style="margin-bottom:0px">
<li>Only a text file of up to 36 KB in size can be uploaded.</li>
<li>Only the uploaded files can be downloaded.</li>
</ul>
</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/1103/41523">Log in to a Lighthouse instance with WebShell for file upload/download</a></td>
<td>
<ul style="margin-bottom:0px">
<li>Only Lighthouse instances on Linux are supported.</li>
<li>Files can be uploaded only to the `home > lighthouse` directory.</li>
</ul>
</td>
</tr>
</table>



### Other methods
Follow the instructions below based on your local operating system and the operating system of the purchased Lighthouse instance.

 <table>
      <tr bgcolor=#5291F8>
        <th>Local OS</th>
        <th>Lighthouse Instance OS (Linux)</th>
        <th>Lighthouse Instance OS (Windows)</th>		 
      </tr>
      <tr>
        <td> Windows </td>
				<td>
					<ul style="margin: 0;"><li><a href="https://intl.cloud.tencent.com/document/product/1103/41531">Upload files to a Lighthouse instance via WinSCP</a></li>
					<li><a href="https://intl.cloud.tencent.com/document/product/1103/41532">Upload files to a Lighthouse instance via FTP</a></li></ul>
				</td>
				<td><a href="https://intl.cloud.tencent.com/document/product/1103/41533">Upload files to a Lighthouse instance via remote desktop</a></td>
      </tr>
      <tr>
        <td> Linux </td>
				<td rowspan=2>
					<ul style="margin: 0;"><li><a href="https://intl.cloud.tencent.com/document/product/1103/41534">Upload files to a Lighthouse instance via SCP</a></li>
					<li><a href="https://intl.cloud.tencent.com/document/product/1103/41535">Upload files to a Lighthouse instance via FTP</a></li></ul></td>
				<td><a href="https://intl.cloud.tencent.com/document/product/1103/41536">Upload files to a Lighthouse instance via remote desktop</a></td>
      </tr>
      <tr>
        <td>macOS</td>
        <td><a href="https://intl.cloud.tencent.com/document/product/1103/41537">Upload files to a Lighthouse instance via remote desktop</a></td>
      </tr>
    </table>
For example, if you use Windows on your local computer and have a Linux Lighthouse instance, you can use WinSCP to upload files to the instance.




## Subsequent Operations
If you need to back up important business data or personal files, you can create a snapshot of the Lighthouse instance's system disk after uploading the files to the instance. For more information on the use cases and usage methods of snapshots, see [Managing Snapshot](https://intl.cloud.tencent.com/document/product/1103/41394).

## Problem?
[Submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) or use related documentation to troubleshoot.

