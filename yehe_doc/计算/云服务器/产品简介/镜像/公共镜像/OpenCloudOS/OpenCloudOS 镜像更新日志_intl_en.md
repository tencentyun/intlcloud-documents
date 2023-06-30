
<dx-alert infotype="explain" title="">
- The image update history is organized by release time.
- Images are released region by region. If an image is not of the latest version in the update history when you create a CVM instance, the image may have not yet been released to the region.
- If an image in the image update history cannot be found in the console, the image may have not been fully open. In this case, you can [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) to obtain more information about the image.
</dx-alert>

## Image Update History

<table>
<thead>
<tr>
<th width="60%"><strong>Updated Feature</strong></th>
<th><strong>Update Date</strong></th>
</tr>
</thead>
<tbody>
<tr>
<td>
<ul class="params">
<li>Disabled the firewalld\sssd\rngd service</li>
<li>Uninstalled the microcode_ctl/nss-softokn/avahi package</li>
<li>Set keymap</li>
<li>Set timezone</li>
<li>Set the cloudinit.target dependency for the boot of kdump</li>
<li>Configured mirrors.tencentyun.com as the first URL in repo</li>
<li>Modified the /etc/rc.d/rc.local file permission to 755</li>
<li>Fixed permission errors of some directories in /var/lib/</li>
</ul>
</td>
<td>2022-09-16</td>
</tr>
<tr>
<td>
<ul class="params">
<li>Updated the kernel version to 5.4.119-19.0010</li>
<li>Updated other user mode software</li>
<li>Updated the image timestamp</li>
</ul>
</td>
<td>2022-07-27</td>
</tr>
<tr>
<td>
<ul class="params">
<li>Launched OpenCloudOS 8.5 to the public cloud</li>
</ul>
</td>
<td>2022-03-04</td>
</tr>
</tbody></table>                                                 
