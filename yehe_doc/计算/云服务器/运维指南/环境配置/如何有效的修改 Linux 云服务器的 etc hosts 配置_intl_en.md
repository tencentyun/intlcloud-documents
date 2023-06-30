## Overview

From March 1, 2018, the Linux public image provided by Tencent Cloud has the open-source tool Cloud-Init pre-installed, and all initialization operations on an instance are done via Cloud-Init, making operations inside the instance more transparent. For more information, see [Cloud-Init and Cloudbase-Init](https://intl.cloud.tencent.com/document/product/213/19670).
In **each launch**, Cloud-Init generates a new `/etc/hosts` file according to the `/etc/cloud/templates/hosts.${os_type}.tmpl` template and overwrites the original `/etc/hosts` file of the instance involved. Hence, after you manually modify the internal `/etc/hosts` configuration of the instance and restart it, the `/etc/hosts` configuration goes back to the original default configuration.

## Precautions
Tencent Cloud has fixed this problem for instances created by using a public image **after September 2018**, and the `/etc/hosts` configuration will not be overwritten.
For instance created **before September 2018**, follow the steps below for modification.

## Directions

### Solution 1 
1. Log in to the Linux CVM.
2. Execute the following command to change the `- update_etc_hosts` in the `/etc/cloud/cloud.cfg` configuration file to `- ['update-etc-hosts', 'once-per-instance']`:
```shellsession
sed -i "/update_etc_hosts/c \ - ['update_etc_hosts', 'once-per-instance']" /etc/cloud/cloud.cfg
```
3. Execute the following command to create a `config_update_etc_hosts` file under the `/var/lib/cloud/instance/sem/` path:
```shellsession
touch /var/lib/cloud/instance/sem/config_update_etc_hosts
```

### Solution 2


<dx-alert infotype="explain" title="">
This solution takes the CentOS 7.2 operating system as an example.
</dx-alert>


#### Obtaining the `hosts` template file path
1. Log in to the Linux CVM.
2. Execute the following command to view the system `hosts` template file:
```shellsession
cat /etc/hosts
```
The `hosts` template file is as shown in the following figure:
![](https://main.qcloudimg.com/raw/f51f9c53004574f72d32f5ed790c8563.png)


#### Modifying the `hosts` template file


<dx-alert infotype="explain" title="">
Taking adding `127.0.0.1 test test` as an example, you can modify the `hosts` template and `/etc/hosts` file as needed.
</dx-alert>


1. Execute the following command to modify the `hosts` template file:
```shellsession
vim /etc/cloud/templates/hosts.redhat.tmpl
```
2. Press **i** to switch to the editing mode.
3. Add the following content to the end of the file:
```shellsession
127.0.0.1 test test
```
4. Press **Esc** and enter **:wq** to save and close the file.

#### Modifying the `/etc/hosts` file
1. Execute the following command to modify the `/etc/hosts` file:
```shellsession
vim /etc/hosts
```
2. Press **i** to switch to the editing mode.
3. Add the following content to the end of the file:
```shellsession
127.0.0.1 test test
```
4. Press **Esc** and enter **:wq** to save and close the file.

