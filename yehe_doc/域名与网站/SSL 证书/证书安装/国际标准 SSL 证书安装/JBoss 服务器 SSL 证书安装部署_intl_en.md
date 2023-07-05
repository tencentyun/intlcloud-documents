## Overview

This document describes how to install an SSL certificate on a JBoss server.

>?
> 
> - The certificate name `cloud.tencent.com` is used as an example.
> - The `jboss-7.1.1` version is used as an example.
> - The current server OS is CentOS 7. Detailed steps vary slightly by OS.
> - Before you install an SSL certificate, enable port `443` on the JBoss server so that HTTPS can be enabled after the certificate is installed. For more information, see [How Do I Enable Port 443 for a VM?](https://intl.cloud.tencent.com/document/product/1007/36738).
> - For detailed directions on how to upload SSL certificate files to a server, see [Copying Local Files to CVMs](https://intl.cloud.tencent.com/document/product/213/34821).


## Prerequisites
- Install the remote file copy tool such as WinSCP. The latest official version is recommended.
We recommend that you use CVM's file upload feature for deployment to CVM.

- Install the remote login tool such as PuTTY or Xshell. The latest official version is recommended.

- The JBoss service has been installed and configured on the current server.

- The data required to install the SSL certificate includes the following:

<table>
<tr>
<td rowspan="1" colSpan="1" >Name</td>
<td rowspan="1" colSpan="1" >Description</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >Server IP address</td>
<td rowspan="1" colSpan="1" >IP address of the server, which is used to connect the PC to the server.</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >Username</td>
<td rowspan="1" colSpan="1" >The username used to log in to the server.</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >Password</td>
<td rowspan="1" colSpan="1" >The password used to log in to the server.</td>
</tr>
</table>


>!
> 
>   - For a CVM instance purchased on the Tencent Cloud official website, log in to the [CVM console](https://console.cloud.tencent.com/cvm) to get the server IP address, username, and password.
>   - If you have selected the **By pasting** method when applying for the SSL certificate, or your certificate brand is WoTrus, the option to download the JKS certificate file is not provided. Instead, you need to manually convert the format to generate a keystore as follows: 
>   - Access the [conversion tool](https://myssl.com/cert_convert.html).
>   - Upload the certificate and private key files in the Nginx folder to the conversion tool, enter the keystore password, click **Submit**, and convert the certificate to a `.jks` certificate.
>   - The JBoss service is installed in the `/usr/local` directory.

- If you have selected the **Paste CSR** method when applying for the SSL certificate, or your certificate brand is Wotrus, the option to download the JKS certificate file is not provided. Instead, you need to manually convert the format to generate a keystore as follows: 

- Access the [conversion tool](https://myssl.com/cert_convert.html).

- Upload the certificate and private key files in the Nginx folder to the conversion tool, enter the keystore password, click **Submit**, and convert the certificate to a .jks certificate.

- The JBoss service is installed in the `/usr/local` directory.


## Directions
1. Log in to the [SSL Certificate Service console](https://console.cloud.tencent.com/ssl), and click **Download** for the certificate you need to install.

2. In the pop-up window, select **JKS** for the server type, click **Download**, and decompress the `cloud.tencent.com` certificate file package to the local directory.
After decompression, you can get the certificate file of the corresponding type, which includes the `cloud.tencent.com_jks` folder.

  - **Folder**: `cloud.tencent.com_jks`

  - **Files in the folder**:

    - `cloud.tencent.com.jks`: keystore file

    - `keystorePass.txt`: password file (if you have set a private key password, this file will not be generated)

3. Remotely log in to the JBoss server. For example, you can use [PuTTY](https://intl.cloud.tencent.com/document/product/213/32502) for remote login.

4. In the `/usr/local/jboss-7.1.1/standalone/configuration` directory, run the `mkdir cert` command to create the `cert` folder.

5. Use WinSCP (a tool for copying files between a local computer and a remote computer) to log in to the JBoss server and copy the keystore file `cloud.tencent.com.jks` from the local directory to the `cert` folder.
   

   >?
   > 
   >   - For detailed directions, see [Uploading files via WinSCP to a Linux CVM from Windows](https://intl.cloud.tencent.com/document/product/213/2131).
   >   - We recommend that you use CVM's file upload feature for deployment to CVM.

6. In the `/usr/local/jboss-7.1.1/standalone/configuration` directory, change the port configuration and add certificate configuration in the `standalone.xml` file.

  - Part 1:

      ``` xml
      <interfaces>
           <interface name="management">
               <inet-address value="${jboss.bind.address.management:127.0.0.1}"/>
           </interface>
                   <!--Enable remote access-->
           <interface name="public">
               <inet-address value="${jboss.bind.address:0.0.0.0}"/>
           </interface>
           <interface name="unsecure">
               <inet-address value="${jboss.bind.address.unsecure:127.0.0.1}"/>
           </interface>
       </interfaces>
       <socket-binding-group name="standard-sockets" default-interface="public" port-offset="${jboss.socket.binding.port-offset:0}">
           <socket-binding name="management-native" interface="management" port="${jboss.management.native.port:9999}"/>
           <socket-binding name="management-http" interface="management" port="${jboss.management.http.port:9990}"/>
           <socket-binding name="management-https" interface="management" port="${jboss.management.https.port:9443}"/>
           <socket-binding name="ajp" port="8009"/>
                   <!--Change the HTTP port-->
           <socket-binding name="http" port="80"/>
                   <!--Change the HTTPS port-->
           <socket-binding name="https" port="443"/>
           <socket-binding name="osgi-http" interface="management" port="8090"/>
           <socket-binding name="remoting" port="4447"/>
           <socket-binding name="txn-recovery-environment" port="4712"/>
           <socket-binding name="txn-status-manager" port="4713"/>
           <outbound-socket-binding name="mail-smtp">
               <remote-destination host="localhost" port="25"/>
           </outbound-socket-binding>
       </socket-binding-group>
      ```




Changes required are as follows:

- **Enabling remote access**: change `${jboss.bind.address:127.0.0.1}` to `${jboss.bind.address:0.0.0.0}`.
- **Changing the HTTP port**: change port 8080 to 80.

- **Changing the HTTPS port**: change port 8443 to 443.




  - Part 2: adding certificate configuration

      ``` xml
      <subsystem xmlns="urn:jboss:domain:web:1.1" default-virtual-server="default-host" native="false">
               <connector name="http" protocol="HTTP/1.1" scheme="http" socket-binding="http"/>
               <connector name="https" protocol="HTTP/1.1" scheme="https" socket-binding="https" secure="true">
                   <ssl name="https" password="******" certificate-key-file="../standalone/configuration/cert/cloud.tencent.com.jks" cipher-suite="TLS_RSA_WITH_AES_256_CBC_SHA,TLS_DHE_RSA_WITH_AES_256_CBC_SHA,TLS_DHE_DSS_WITH_AES_128_CBC_SHA,SSL_RSA_WITH_3DES_EDE_CBC_SHA,SSL_DHE_RSA_WITH_3DES_EDE_CBC_SHA,SSL_DHE_DSS_WITH_3DES_EDE_CBC_SHA" protocol="TLSv1,TLSv1.1,TLSv1.2"/>
               </connector>
               <virtual-server name="default-host" enable-welcome-root="true">
                   <alias name="localhost"/>
                   <alias name="example.com"/>
               </virtual-server>
           </subsystem>
      ```
      
      
      
7. Go to the `/usr/local/jboss-7.1.1/bin` directory and run the `./standalone.sh` command to start the JBoss server.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/UuQv190_00000000.png)

8. The certificate is deployed and you can access the website through `https://cloud.tencent.com`.

- If the security lock icon is displayed in the browser, the certificate has been installed successfully.


- In case of a website access exception, troubleshoot the issue by referring to the following FAQs:

    - [Website Inaccessible After an SSL Certificate is Deployed](https://intl.cloud.tencent.com/document/product/1007/39821)

    - ["Your Connection is Not Secure" is Displayed After the SSL Certificate is Installed](https://intl.cloud.tencent.com/document/product/1007/40674)

    - [Why Does the Website Prompt "Connection Is Untrusted"?](https://intl.cloud.tencent.com/document/product/1007/30184)


    - [404 Error After the SSL Certificate is Deployed on IIS](https://intl.cloud.tencent.com/document/product/1007/39820)




>!
> If anything goes wrong during this process, [contact us](https://intl.cloud.tencent.com/document/product/1007/30951).

