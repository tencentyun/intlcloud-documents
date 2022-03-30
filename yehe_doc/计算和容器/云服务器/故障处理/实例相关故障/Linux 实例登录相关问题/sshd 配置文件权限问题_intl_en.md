## Issue Description
During login to a Linux instance via SSH key, "ssh_exchange_identification: Connection closed by remote host" or "no hostkey alg" is displayed.


## Common Causes
sshd configuration file permissions, such as the permissions of the `/var/empty/sshd` or `/etc/ssh/ssh_host_rsa_key` configuration file, are modified, which may cause a failure in login via SSH key.


## Solution
Perform the steps based on the actual error message to modify the configuration file permissions:
 - If the error message is "ssh_exchange_identification: Connection closed by remote host", see [Modifying permissions of `/var/empty/sshd` file](#sshd).
 - If the error message is "no hostkey alg", see [Modifying permissions of `/etc/ssh/ssh_host_rsa_key` file](#rsa_key).



## Troubleshooting Procedure

### Modifying permissions of `/var/empty/sshd` file[](id:sshd)
1. [Log in to the Linux instance via VNC](https://intl.cloud.tencent.com/document/product/213/32494).
2. Run the following command to view the error cause:
```
sshd -t
```
Information similar to the following is returned:
```plaintext
"/var/empty/sshd must be owned by root and not group or world-writable."
```
3. Run the following command to modify the permissions of the `/var/empty/sshd/` file:
```
chmod 711 /var/empty/sshd/
```



### Modifying permissions of `/etc/ssh/ssh_host_rsa_key` file[](id:rsa_key)
1. [Log in to the Linux instance via VNC](https://intl.cloud.tencent.com/document/product/213/32494).
2. Run the following command to view the error cause:
```
sshd -t
```
The returned information contains the following field:
```plaintext
"/etc/ssh/ssh_host_rsa_key are too open"
```
3. Run the following command to modify the permissions of the `/etc/ssh/ssh_host_rsa_key` file:
```
chmod 600 /etc/ssh/ssh_host_rsa_key
```
