## Scenarios
This document describes how to install an SSL certificate on a JBoss server.
>?
>- The certificate name `cloud.tencent.com` is used as an example in this document.
>- JBoss 7.1.1 is used as an example.
>- The current server OS is CentOS 7. Detailed steps vary slightly with the OS version.
>- Before installing the SSL certificate, open the port 443 on the JBoss server to ensure that HTTPS can be enabled after certificate installation. For more information, see [How Do I Open the Port 443 on the Server?](https://intl.cloud.tencent.com/document/product/1007/36738).
>- To upload a SSL certificate to CVMs, see [Copying Local Files to CVMs](https://intl.cloud.tencent.com/document/product/213/34821).

## Prerequisites
- A remote file copy tool such as WinSCP has been installed. You are recommended to obtain the latest version from the official website.
- A remote login tool such as PuTTY or Xshell has been installed. You are recommended to obtain the latest version from the official website.
- The JBoss service has been installed and configured on the current server.
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
>- The JBoss service is installed in the `/usr/local` directory.


## Directions
1. Go to the [SSL Certificate Service Console](https://console.cloud.tencent.com/ssl), download the certificate package for the `cloud.tencent.com` domain name, and decompress it to a local directory.
After decompression, you can obtain the relevant certificate files, including the Tomcat folder and CSR file:
 - **Folder name**: Tomcat
 - **Folder content**:
    - `cloud.tencent.com.jks`: keystore file
    - `keystorePass.txt`: password file (if you have set a private key password, this file will not be generated)
  - **CSR file**: `cloud.tencent.com.csr`
>?The CSR file is uploaded by you or generated online by the system when you apply for the certificate and is provided to the CA. It is irrelevant to the installation.
2. Remotely log in to the JBoss server. For example, you can use [PuTTY](https://intl.cloud.tencent.com/document/product/213/32502) for remote login.
3. In the `/usr/local/jboss-7.1.1/standalone/configuration` directory, run the `mkdir cert` command to create the `cert` folder.
4. Use WinSCP (a tool for copying files between a local computer and a remote computer) to log in to the JBoss server and copy the keystore file `cloud.tencent.com.jks` from the local directory to the `cert` folder.
5. In the `/usr/local/jboss-7.1.1/standalone/configuration` directory, change the port configuration and add certificate configuration in the `standalone.xml` file.
 - Part 1:
```
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
```
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
6. Go to the `/usr/local/jboss-7.1.1/bin` directory and run the `./standalone.sh` command to start the JBoss server.
![](https://main.qcloudimg.com/raw/0dc9c0ee84b92f7978a7a133d35bcf27.png)
7. After the JBoss server is started, access it through `https://cloud.tencent.com`.

>!If any problems occur during this process, please [contact us](https://intl.cloud.tencent.com/document/product/1007/30951).

