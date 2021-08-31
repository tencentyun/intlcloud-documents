## Scenarios
This document describes how to install an SSL certificate on a GlassFish server.
>?
>- The certificate name `cloud.tencent.com` is used as an example in this document.
>- GlassFish 4.0 is used as an example.
>- The current server OS is CentOS 7. Detailed steps vary slightly with the OS version.
>- Before installing the SSL certificate, open the port 443 on the GlassFish server to ensure that HTTPS can be enabled after certificate installation. For more information, see [How Do I Open the Port 443 on the Server?](https://intl.cloud.tencent.com/document/product/1007/36738).
>- To upload a SSL certificate to CVMs, see [Copying Local Files to CVMs](https://intl.cloud.tencent.com/document/product/213/34821).

## Prerequisites
- A remote file copy tool such as WinSCP has been installed. You are recommended to obtain the latest version from the official website.
- A remote login tool such as PuTTY or Xshell has been installed. You are recommended to obtain the latest version from the official website.
- The GlassFish service has been installed and configured on the current server.
- The data required to install the SSL certificate includes:
<table>
<tr>
<td>Name</td>
<td>Description</td>
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
>- For a CVM instance purchased on the Tencent Cloud official website, log in to the [CVM Console](https://console.cloud.tencent.com/cvm) to obtain the server IP address, username, and password.
>- If you selected the **Paste CSR** method when applying for the SSL certificate, or purchased the Wotrus certificate, the option to download the Tomcat certificate file is not provided. Instead, you manually convert the format to generate a keystore by following the procedure below:
     - Access the [conversion tool](https://myssl.com/cert_convert.html).
     - Upload the certificate and private key files in the Nginx folder to the conversion tool, enter the keystore password, click **Submit**, and convert the certificate to a .jks certificate.
>- The current GlassFish service is installed in the `/usr/share` directory.


## Directions
1. Go to the [SSL Certificate Service Console](https://console.cloud.tencent.com/ssl), download the certificate package for the `cloud.tencent.com` domain name, and decompress it to a local directory.
After decompression, you can obtain the relevant certificate files, including the Apache folder, Tomcat folder, and CSR file:
 - **Folder name**: Apache
    - `2_cloud.tencent.com.crt`: certificate file
    - `3_cloud.tencent.com.key`: private key file
  - **CSR file**: `cloud.tencent.com.csr`
>?The CSR file is uploaded by you or generated online by the system when you apply for the certificate and is provided to the CA. It is irrelevant to the installation.
2. Remotely log in to the GlassFish server. For example, you can use [PuTTY](https://intl.cloud.tencent.com/document/product/213/32502) for remote login.
3. Go to the `/usr/share/glassfish4/glassfish/bin` directory, run the `./asadmin` command, and then run the `change-master-password --savemasterpassword=true domain1` command to change the domain administrator password.
>!
>- The default installation directory of the domain1 service is `/usr/share/glassfish4/glassfish/domains`. Change the domain name after you execute the `change-master-password --savemasterpassword=true domain1` command.
>- The default password is **changeit**. Press **Enter** and enter the new password, which should be the **private key password** you set when applying for the certificate.
>- If you did not set a private key password when applying for the certificate, enter the password in the `keystorePass.txt` file in the `Tomcat` folder.
>
4. In the `/usr/share` directory, run the `mkdir temp` command to create the `temp` folder.
5. Use WinSCP (a tool for copying files between a local computer and a remote computer) to log in to the GlassFish server, and then copy the certificate file `2_cloud.tencent.com.crt` and the private key file `3_cloud.tencent.com.key` from the local directory to the `temp` folder.
6. In the `temp` folder, run the following command to generate the PKCS12 file. When the system prompts you for a password during the process, enter the new password, which is the private key password.
```
openssl pkcs12 -export -in 2_cloud.tencent.com.crt -inkey 3_cloud.tencent.com.key -out mycert.p12 -name s1as
```
7. In the `temp` folder, run the `ls -l` command to check whether the PKCS12 file contains the certificate you applied for.
8. In the `temp` folder, run the following command to generate the `keystore.jks`.
```
keytool -importkeystore -destkeystore keystore.jks -srckeystore mycert.p12 -srcstoretype PKCS12 -alias s1as
```
9. In the `temp` folder, run the following command to generate the `cacert.jks` file. When the system prompts you for a password during this process, enter the new password, which is the private key password.
```
keytool -importcert -trustcacerts -destkeystore cacerts.jks -file 2_cloud.tencent.com.crt -alias s1as
```
If the system asks whether to trust the certificate, enter **yes** as shown in the following figure.
![](https://main.qcloudimg.com/raw/aee68705e1e8b135d47bda9af499e15f.png)
10. Use the `keystore.jks` and `cacert.jks` files generated in steps 8 and 9 to replace the corresponding files in the `domain1/config` directory. 
11. In the `/usr/share/glassfish4/glassfish/domains/domain1/config` directory, change the port configuration in the `domain.xml` file.
```
<network-listeners>
          <network-listener port="80" protocol="http-listener-1" transport="tcp" name="http-listener-1" thread-pool="http-thread-pool"></network-listener>
          <network-listener port="443" protocol="http-listener-2" transport="tcp" name="http-listener-2" thread-pool="http-thread-pool"></network-listener>
          <network-listener port="4848" protocol="admin-listener" transport="tcp" name="admin-listener" thread-pool="admin-thread-pool"></network-listener>
        </network-listeners>
```
12. Start the GlassFish server. After the server is started, access it through `https://cloud.tencent.com`.
![](https://main.qcloudimg.com/raw/fcdf919a22f0c9b07bc837e4d9a5e269.png)

>!If any problems occur during this process, please [contact us](https://intl.cloud.tencent.com/document/product/1007/30951).

