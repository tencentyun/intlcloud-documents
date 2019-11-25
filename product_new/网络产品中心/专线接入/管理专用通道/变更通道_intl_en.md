## Descriptions of Parameter Changes
The following parameters can be changed for a dedicated tunnel:
- **IP address**:
Changing the IP address will interrupt the service.
- **BGP ASN**:
Changing the BGP ASN will interrupt the service.
- **Bandwidth**:
Changing the bandwidth will not interrupt the service, and the system will automatically overwrite the configuration.
>In the Shared Connection mode, you cannot apply for a bandwidth change for a dedicated tunnel; instead, such a change can only be applied for by the connection owner.
- **BGP KEY**:
Changing the BGP KEY will not interrupt the service, and the system will automatically overwrite the configuration.
- **User IDC IP range**:
The user IDC IP range can be modified, and the system will automatically distribute the configuration.

After a tunnel change request is submitted, the system will complete the device configuration in a few minutes.
![](https://main.qcloudimg.com/raw/0cbe81284b443ecef024c570f880e84c.png)

## Use Limits on Large IP Range
 In order to improve the fine-grained scheduling capabilities of your network, please avoid distributing the following routes:
`10.0.0.0/8`, `172.16.0.0/12`, `192.168.0.0/16`, `100.64.0.0/10`.
 You can split the above large routes into the following ones for distribution:
 - <strong>`10.0.0.0/8`</strong>
should be split into `10.0.0.0/9` + `10.128.0.0/9`.
 - <strong>`172.16.0.0/12`</strong>
should be split into `172.16.0.0/13` + `172.24.0.0/13`.
 - <strong>`192.168.0.0/16`</strong>
should be split into `192.168.0.0/17` + `192.168.128.0/17`.
 - <strong>`100.64.0.0/10`</strong>
should be split into `100.64.0.0/11` + `100.96.0.0/11`.
