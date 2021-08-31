## Overview
This document describes how to install an SSL certificate on a Tomcat server.
>?
>- The certificate name `cloud.tencent.com` is used as an example.
>- The `tomcat9.0.40` version is used as an example.
>- The current server OS is CentOS 7. Detailed steps vary slightly with the OS.
>- Before you install an SSL certificate, enable port 443 on the Tomcat server so that HTTPS can be enabled after the certificate is installed. For more information, please see [How Do I Enable Port 443 for a VM?](https://intl.cloud.tencent.com/document/product/1007/36738).
>- For more information about how to upload SSL certificate files to a server, please see [Copying Local Files to CVMs](https://intl.cloud.tencent.com/document/product/213/34821).

## Prerequisites
- A remote file copy tool such as WinSCP has been installed. Please download the latest version from the official website.
- A remote login tool such as PuTTY or Xshell has been installed. Please download the latest version from the official website.
- The Tomcat service has been installed and configured on the server.
- The data required to install the SSL certificate includes the following:
<table>
<tr>
<td>Name</td>
<td>Description</td>
</tr>
<tr>
<td>Server IP address</td>
<td>The server IP address, which is used to connect the PC to the server.</td>
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
- If you have selected the **Paste CSR** method when applying for the SSL certificate, or your certificate brand is Wotrus, the option to download the Tomcat certificate file is not provided. Instead, you need to manually convert the format to generate a keystore as follows: 
 - Access the [conversion tool](https://myssl.com/cert_convert.html).
 - Upload the certificate and private key files in the Nginx folder to the conversion tool, enter the keystore password, click **Submit**, and convert the certificate to a .jks certificate.
- Currently, the Tomcat server is installed in the `/usr` directory. For example, if the Tomcat folder name is `tomcat9.0.40`, `/usr/*/conf` is actually `/usr/tomcat9.0.40/conf`.


## Directions

### Certificate installation
1. Download the `cloud.tencent.com` certificate package from the [SSL Certificate Service console](https://console.cloud.tencent.com/ssl) and decompress it to a local directory.
After decompression, you can obtain the relevant certificate files, including the Tomcat folder and CSR file:
 - **Folder name**: Tomcat
 - **Files in the folder**:
    - `cloud.tencent.com.jks`: keystore file
    - `keystorePass.txt`: password file (if you have set a private key password, this file will not be generated)
  - **CSR file**: `cloud.tencent.com.csr`
  >?The CSR file is uploaded by you or generated online by the system and is provided to the certificate authority (CA) when you apply for the certificate. It is not relevant to installation.
2. Log in to the Tomcat server using WinSCP (a tool copying files between a local computer and a remote computer).
3. Copy `cloud.tencent.com.jks` from the local directory to the `/usr/*/conf` directory.
4. Remotely log in to the Tomcat server using a login tool such as [PuTTY](https://intl.cloud.tencent.com/document/product/213/32502).
5. Edit the `server.xml` file in the `/usr/*/conf` directory by adding the following:
```
<Connector port="443" protocol="HTTP/1.1" SSLEnabled="true"
  maxThreads="150" scheme="https" secure="true"
# Path of the certificate
  keystoreFile="/usr/*/conf/cloud.tencent.com.jks" 
# Keystore password
  keystorePass="******"
  clientAuth="false"/>
```
For details of the `server.xml` file, see below:
>!To avoid format issues, you are not advised to copy the content of `server.xml` directly.
>
```
 <?xml version="1.0" encoding="UTF-8"?>
  <Server port="8005" shutdown="SHUTDOWN">
    <Listener className="org.apache.catalina.startup.VersionLoggerListener" />
    <Listener className="org.apache.catalina.core.AprLifecycleListener" SSLEngine="on" />
    <Listener className="org.apache.catalina.core.JreMemoryLeakPreventionListener" />
    <Listener className="org.apache.catalina.mbeans.GlobalResourcesLifecycleListener" />
    <Listener className="org.apache.catalina.core.ThreadLocalLeakPreventionListener" />
 <GlobalNamingResources>
    <Resource name="UserDatabase" auth="Container"
              type="org.apache.catalina.UserDatabase"
              description="User database that can be updated and saved"
              factory="org.apache.catalina.users.MemoryUserDatabaseFactory"
              pathname="conf/tomcat-users.xml" />
  </GlobalNamingResources>
  <Service name="Catalina">
        <Connector port="80" protocol="HTTP/1.1" connectionTimeout="20000"  redirectPort="8443" />
        <Connector port="443" protocol="HTTP/1.1"
               maxThreads="150" SSLEnabled="true" scheme="https" secure="true"
               clientAuth="false"
                keystoreFile="/usr/*/conf/cloud.tencent.com.jks"
                keystorePass="******" />
    <Connector port="8009" protocol="AJP/1.3" redirectPort="8443" />
   <Engine name="Catalina" defaultHost="cloud.tencent.com">
      <Realm className="org.apache.catalina.realm.LockOutRealm">
        <Realm className="org.apache.catalina.realm.UserDatabaseRealm"
               resourceName="UserDatabase"/>
      </Realm>
    <Host name="cloud.tencent.com"  appBase="webapps" 
        unpackWARs="true" autoDeploy="true" >
        <Context path="" docBase ="Knews" />
    <Valve className="org.apache.catalina.valves.AccessLogValve" directory="logs"
           prefix="localhost_access_log" suffix=".txt"  
           pattern="%h %l %u %t &quot;%r&quot; %s %b" />
      </Host>
    </Engine>
  </Service>
</Server>
```
The main parameters of the configuration file are described as below:
 - **keystoreFile**: location of the keystore file. You can specify an absolute path or a path relative to the &lt;CATALINA_HOME&gt; (Tomcat installation directory) environment variable. If this parameter is not set, Tomcat reads the file named ".keystore" from the user directory of the current OS user by default.
 - **keystorePass**: keystore password. If you set a private key password when applying for the certificate, enter the private key password; otherwise, enter the password in the `keystorePass.txt` file in the Tomcat folder.
 - **clientAuth**: If it is set to true, Tomcat requires all SSL clients to provide a security certificate for identity verification.
6. Confirm whether the Tomcat server is started.
   - If the Tomcat server is already started, you need to run the following commands in sequence in the `/usr/*/bin` directory to shut down and restart it.
```
./shutdown.sh  (Shut down the Tomcat server)
./startup.sh (Start the Tomcat server)
```
 - If the Tomcat server is not started, you need to run the following command in the `/usr/*/bin` directory to start it.
 ```
./startup.sh
```
7. If the server is started successfully, you can access it through the `https://cloud.tencent.com` website.

### (Optional) Security configuration for automatic redirect from HTTP to HTTPS

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
    <web-resource-collection>
    <web-resource-name>SSL</web-resource-name>
    <url-pattern>/*</url-pattern>
    </web-resource-collection>
    <user-data-constraint>
    <transport-guarantee>CONFIDENTIAL</transport-guarantee>
    </user-data-constraint>
    </security-constraint>
```
3. Edit the `server.xml` file in the `/usr/*/conf` directory by modifying the `redirectPort` parameter to the port of the SSL connector, i.e., port 443, as shown below:
```
<Connector port="80" protocol="HTTP/1.1"
  connectionTimeout="20000"
  redirectPort="443" />
```
>? This modification allows a non-SSL connector to redirect to an SSL connector.
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

>!If any problems occur during this process, please [contact us](https://intl.cloud.tencent.com/document/product/1007/30951).

