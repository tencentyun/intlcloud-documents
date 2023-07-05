## Overview
This document describes how to install an SSL certificate on a GlassFish server.
>?
>- The certificate name `cloud.tencent.com` is used as an example.
>- GlassFish 4.0 is used as an example.
>- The current server OS is CentOS 7. Detailed steps vary slightly with the OS.
>- Before you install an SSL certificate, enable port 443 on the GlassFish server so that HTTPS can be enabled after the certificate is installed. For more information, see [How Do I Enable Port 443 for a VM?](https://intl.cloud.tencent.com/document/product/1007/36738)
>- For more information about how to upload SSL certificate files to a server, see [Copying Local Files to CVMs](https://intl.cloud.tencent.com/document/product/213/34821).

## Prerequisites
- A remote file copy tool such as WinSCP has been installed. Please download the latest version from the official website.
- A remote login tool such as PuTTY or Xshell has been installed. Please download the latest version from the official website.
- The GlassFish service has been installed and configured on the current server.
- The data required to install the SSL certificate includes the following:
<table>
<tr>
<td>Name</td>
<td>Remarks</td>
</tr>
<tr>
<td>Server IP address</td>
<td>IP address of the server, which is used to connect the PC to the server.</td>
</tr>
<tr>
<td>Username</td>
<td>The username used to log in to the server.</td>
</tr>
<tr>
<td>Password</td>
<td>The password used to log in to the server.</td>
</tr>
</table>

>!
>- For a CVM instance purchased on the Tencent Cloud official website, log in to the [CVM console](https://console.cloud.tencent.com/cvm) to obtain the server IP address, username, and password.
>- If you have selected the **Paste CSR** method when applying for the SSL certificate, or your certificate brand is Wotrus, the option to download the Tomcat certificate file is not provided. Instead, you need to manually convert the format to generate a keystore as follows: 
    - Access the [conversion tool](https://myssl.com/cert_convert.html).
    - Upload the certificate and private key files in the Nginx folder to the conversion tool, enter the keystore password, click **Submit**, and convert the certificate to a .jks certificate.
>- The GlassFish service is installed in the `/usr/share` directory.


## Directions
1. Log in to the [SSL Certificate Service console](https://console.cloud.tencent.com/ssl), and click **Download** for the certificate you need to install.
2. In the pop-up window, select **Apache** and **JKS** for the server type, click **Download**, and decompress the `cloud.tencent.com` certificate file package to the local directory.
After decompression, you can get the certificate files of the corresponding types, which include the `cloud.tencent.com_apache` and `cloud.tencent.com_jks` folders.
   - **Folder**: `cloud.tencent.com_apache`
     - `cloud.tencent.com.crt`: certificate file
     - `cloud.tencent.com.key`: private key file
   - **CSR file**: `cloud.tencent.com.csr`
>?The CSR file is uploaded by you or generated online by the system and is provided to the certificate authority (CA) when you apply for the certificate. It is not relevant to installation.
3. Remotely log in to the GlassFish server. For example, you can use [PuTTY](https://intl.cloud.tencent.com/document/product/213/32502) for remote login.
4. Go to the `/usr/share/glassfish4/glassfish/bin` directory, run the `./asadmin` command, and then run the `change-master-password --savemasterpassword=true domain1` command to change the domain administrator password.
>!
>- The default installation directory of the domain1 service is `/usr/share/glassfish4/glassfish/domains`. Change the domain name after you execute the `change-master-password --savemasterpassword=true domain1` command.
>- The default password is **changeit**. Press **Enter** and enter the new password, which should be the **private key password** you set when applying for the certificate.
>- If you haven’t set a private key password when applying for the certificate, enter the password of the `keystorePass.txt` file in the `cloud.tencent.com_jks` folder.
>
5. In the `/usr/share` directory, run the `mkdir temp` command to create the `temp` folder.
6. Use WinSCP (a tool for copying files between a local computer and a remote computer) to log in to the GlassFish server, and then copy the certificate file `cloud.tencent.com.crt` and the private key file `cloud.tencent.com.key` from the local directory to the `temp` folder.
7. In the `temp` folder, run the following command to generate the PKCS12 file. When the system prompts you for a password during the process, enter the new password, which is the private key password.
```
openssl pkcs12 -export -in cloud.tencent.com.crt -inkey cloud.tencent.com.key -out mycert.p12 -name s1as
```
8. In the `temp` folder, run the `ls -l` command to check whether the PKCS12 file contains the certificate you applied for.
9. In the `temp` folder, run the following command to generate the `keystore.jks`.
```
keytool -importkeystore -destkeystore keystore.jks -srckeystore mycert.p12 -srcstoretype PKCS12 -alias s1as
```
10. In the `temp` folder, run the following command to generate the `cacert.jks` file. When the system prompts you for a password during this process, enter the new password, which is the private key password.
```
keytool -importcert -trustcacerts -destkeystore cacerts.jks -file cloud.tencent.com.crt -alias s1as
```
If the system asks whether to trust the certificate, enter **yes** as shown in the following figure.
![](https://main.qcloudimg.com/raw/aee68705e1e8b135d47bda9af499e15f.png)
11. Replace the `keystore.jks` and `cacert.jks` files in the `domain1/config` directory with the files generated in steps 9 and 10. 
12. In the `/usr/share/glassfish4/glassfish/domains/domain1/config` directory, change the port numbers in the `domain.xml` file.
```
<network-listeners>
          <network-listener port="80" protocol="http-listener-1" transport="tcp" name="http-listener-1" thread-pool="http-thread-pool"></network-listener>
          <network-listener port="443" protocol="http-listener-2" transport="tcp" name="http-listener-2" thread-pool="http-thread-pool"></network-listener>
          <network-listener port="4848" protocol="admin-listener" transport="tcp" name="admin-listener" thread-pool="admin-thread-pool"></network-listener>
        </network-listeners>
```
13. Start the GlassFish server and then you can access the `cloud.tencent.com` website over the HTTPS protocol.
![](https://main.qcloudimg.com/raw/fcdf919a22f0c9b07bc837e4d9a5e269.png)

>!If you experience any issues with the above steps, please [contact us](https://intl.cloud.tencent.com/document/product/1007/30951).


