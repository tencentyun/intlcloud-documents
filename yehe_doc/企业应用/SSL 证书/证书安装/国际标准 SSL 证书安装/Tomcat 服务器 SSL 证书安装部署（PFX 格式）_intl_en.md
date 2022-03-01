## Overview
This document describes how to install an SSL certificate (PFX format) on a Tomcat server.

>?
>- The certificate name `cloud.tencent.com` is used as an example.
>- The `tomcat9.0.40` version is used as an example.
>- The current server OS is CentOS 7. Detailed steps vary slightly with the OS.
>- If you need to install an SSL certificate (JKS format) on a Tomcat server, see [Installing an SSL Certificate (JKS Format) on a Tomcat Server](https://intl.cloud.tencent.com/document/product/1007/43804).
>- Before you install an SSL certificate, enable port 443 on the Tomcat server so that HTTPS can be enabled after the certificate is installed. For more information, please see [How Do I Enable Port 443 for a VM?](https://intl.cloud.tencent.com/document/product/1007/36738)
>- For more information about how to upload SSL certificate files to a server, see [Copying Local Files to CVMs](https://intl.cloud.tencent.com/document/product/213/34821).

## Prerequisites
- A remote file copy tool such as WinSCP has been installed. Please download the latest version from the official website.
- A remote login tool such as PuTTY or Xshell has been installed. Please download the latest version from the official website.
- The Tomcat service has been installed and configured on the server.
- The data required to install the SSL certificate includes the following:
<table>
<tr>
<th>Item</th>
<th>Description</th>
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
>- Currently, the Tomcat server is installed in the `/usr` directory. For example, if the Tomcat folder name is `tomcat9.0.40`, `/usr/*/conf` is actually `/usr/tomcat9.0.40/conf`.

# Directions

### Certificate Installation

1. Log in to the [SSL Certificate Service console](https://console.cloud.tencent.com/ssl), and click **Download** for the certificate you need to install.
2. In the pop-up window, select **Tomcat** for the server type, click **Download**, and decompress the `cloud.tencent.com` certificate file package to the local directory.
After decompression, you can get the certificate file of the corresponding type, which includes the `cloud.tencent.com_tomcat` folder.
   - **Folder**: `cloud.tencent.com_tomcat`
   - **Files in the folder**:
     - `cloud.tencent.com.pfx`: certificate file
     - `keystorePass.txt`: password file (if you have set a private key password, this file will not be generated)
3. Log in to the Tomcat server using WinSCP (a tool copying files between a local computer and a remote computer).
4. Copy the obtained `cloud.tencent.com.pfx` certificate file from the local directory to the `/usr/*/conf` directory.
5. Remotely log in to the Tomcat server using a login tool such as [PuTTY](https://intl.cloud.tencent.com/document/product/213/32502).
6. Edit the `server.xml` file in the `/usr/*/conf` directory by using either of the following methods as needed:
>?If you use method 1, Tomcat automatically selects an SSL implementation mode for you. If you are unable to complete the subsequent configuration according to method 1, it may be because your environment does not support the implementation mode. In that case, you can use method 2 to manually select an SSL implementation mode based on your environment properties.
>
<dx-tabs>
::: Method 1: automatically selecting an SSL implementation mode
Modify the value of the `Connector` attribute in the `server.xml` file to the following:
```
<Connector port="443"  
protocol="HTTP/1.1"
    SSLEnabled="true"
    scheme="https"
    secure="true"
    keystoreFile="/usr/*/conf/cloud.tencent.com.pfx" # Path of the certificate file
    keystoreType="PKCS12"
    keystorePass="Certificate password"  # Replace the value with the content in the `keystorePass.txt` password file.
    clientAuth="false"
    SSLProtocol="TLSv1.1+TLSv1.2+TLSv1.3"
    ciphers="TLS_RSA_WITH_AES_128_CBC_SHA,TLS_RSA_WITH_AES_256_CBC_SHA,TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA,TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256,TLS_RSA_WITH_AES_128_CBC_SHA256,TLS_RSA_WITH_AES_256_CBC_SHA256"/>
```
:::
::: Method 2: manually selecting an SSL implementation mode 
Modify the value of the `Connector` attribute in the `server.xml` file to the following:
```
<Connector
    protocol="org.apache.coyote.http11.Http11NioProtocol"
    port="443" maxThreads="200"
    scheme="https" secure="true" SSLEnabled="true"
    keystoreFile="/usr/*/conf/cloud.tencent.com.pfx" keystorePass="Certificate password" # Replace `pfx` with the path of the certificate file, and replace `Certificate password` with the content in the `keystorePass.txt` password file.
    clientAuth="false" sslProtocol="TLS"/>
```
:::
</dx-tabs>

The main parameters of the configuration file are described as below:
 - **keystoreFile**: location of the certificate file. You can specify an absolute path or a path relative to the &lt;CATALINA_HOME&gt; (Tomcat installation directory) environment variable. If this parameter is not set, Tomcat reads the file named ".keystore" from the user directory of the current OS user.
 - **keystorePass**: password in the password file, i.e., keystore password. If you have set a private key password when applying for the certificate, enter the private key password; otherwise, enter the password in the `keystorePass.txt` file in the `cloud.tencent.com_tomcat` folder.
 - **clientAuth**: If it is set to true, Tomcat requires all SSL clients to provide a security certificate for identity verification.

7. Confirm whether the Tomcat server is started.
   - If the Tomcat server is already started, you need to run the following commands in sequence in the `/usr/*/bin` directory to shut down and restart it.
```
./shutdown.sh  (Shut down the Tomcat server)
./startup.sh (Start the Tomcat server)
```
 - If the Tomcat server is not started, you need to run the following command in the `/usr/*/bin` directory to start it.
 ```
./startup.sh
 ```
8. If the server is started successfully, you can access it through `https://cloud.tencent.com`.

### (Optional) security configuration for automatic redirect from HTTP to HTTPS
You can redirect HTTP requests to HTTPS by configuring the following settings:

1. Edit the `web.xml` file in the `/usr/*/conf` directory and find the `<\/welcome-file-list>` tag.
2. Insert a new line after `<\/welcome-file-list>` and add the following:
```
<login-config>  
    <!-- Authorization setting for SSL -->  
    <auth-method>CLIENT-CERT</auth-method>  
    <realm-name>Client Cert Users-only Area</realm-name>  
</login-config>  
<security-constraint>  
    <!-- Authorization setting for SSL -->  
    <web-resource-collection >  
        <web-resource-name >SSL</web-resource-name>  
        <url-pattern>/*</url-pattern>  
    </web-resource-collection>  
    <user-data-constraint>  
        <transport-guarantee>CONFIDENTIAL</transport-guarantee>  
    </user-data-constraint>  
</security-constraint>
```
3. Edit the `server.xml` file in the `/usr/*/conf` directory by changing the `redirectPort` parameter to the port of the SSL connector, i.e., port 443, as shown below:
```
<Connector port="80" protocol="HTTP/1.1"
  connectionTimeout="20000"
  redirectPort="443" />
```
>? This change allows a non-SSL connector to redirect to an SSL connector.
>
4. Shut down the Tomcat server by running the following command in the `/usr/*/bin` directory:
```
./shutdown.sh
```
5. Run the following command to confirm whether there is a problem with the configuration:
```
./configtest.sh
```
 - If yes, reconfigure or fix the problem as prompted.
 - If no, proceed to the next step.
6. Run the following command to start the Tomcat server. In this way, you can access it through `http://cloud.tencent.com`.
```
./startup.sh
```

