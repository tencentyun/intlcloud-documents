## Overview

This document describes how to install an SSL certificate (JKS format) on a Tomcat server.

>?
> 
> - The certificate name `cloud.tencent.com` is used as an example.
> - The `tomcat-9.0.56` version is used as an example.
> - The current server OS is CentOS 7. Detailed steps vary slightly by OS.
> - Before you install an SSL certificate, enable port `443` on the Tomcat server so that HTTPS can be enabled after the certificate is installed. For more information, see [How Do I Enable Port 443 for a VM?](https://intl.cloud.tencent.com/document/product/1007/36738).
> - For detailed directions on how to upload SSL certificate files to a server, see [Copying Local Files to CVMs](https://intl.cloud.tencent.com/document/product/213/34821).


## Prerequisites
- Install the remote file copy tool such as WinSCP. The latest official version is recommended.
We recommend that you use CVM's file upload feature for deployment to CVM.

- Install the remote login tool such as PuTTY or Xshell. The latest official version is recommended.

- The Tomcat service has been installed and configured on the server.

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
   >   - Currently, the Tomcat service is installed in the `/usr` directory by default. For example, if the Tomcat folder is `Tomcat-9.0.56`, the configuration file directory will be `/usr/Tomcat-9.0.56/conf`.

- If you have selected the **Paste CSR** method when applying for the SSL certificate, or your certificate brand is Wotrus, the option to download the JKS certificate file is not provided. Instead, you need to manually convert the format to generate a keystore as follows: 

- Access the [conversion tool](https://myssl.com/cert_convert.html).

- Upload the certificate and private key files in the Nginx folder to the conversion tool, enter the keystore password, click **Submit**, and convert the certificate to a .jks certificate.

- Currently, the Tomcat service is installed in the `/usr` directory by default. For example, if the Tomcat folder is `Tomcat-9.0.56`, the configuration file directory will be `/usr/Tomcat-9.0.56/conf`.


## Directions

### Installing the certificate
1. Log in to the [SSL Certificate Service console](https://console.cloud.tencent.com/ssl), and click **Download** for the certificate you need to install.

2. In the pop-up window, select **JKS** for the server type, click **Download**, and decompress the `cloud.tencent.com` certificate file package to the local directory.
After decompression, you can get the certificate file of the corresponding type, which includes the `cloud.tencent.com_jks` folder.

  - **Folder**: `cloud.tencent.com_jks`

  - **Files in the folder**:

    - `cloud.tencent.com.jks`: keystore file

    - `keystorePass.txt`: password file (if you have set a private key password, this file will not be generated)

3. Use WinSCP (a tool for copying files between a local computer and a remote computer) to log in to the Tomcat server. Then, copy the `cloud.tencent.com.jks` keystore file from the local directory to the `/usr/Tomcat-9.0.56/conf` directory of the Tomcat configuration file.
   

   >?
   > 
   >   - For detailed directions, see [Uploading files via WinSCP to a Linux CVM from Windows](https://intl.cloud.tencent.com/document/product/213/2131).
   >   - We recommend that you use CVM's file upload feature for deployment to CVM.

4. Add the following content to the `server.xml` file in the `/usr/Tomcat-9.0.56/conf` directory:

   ``` bash
   <Connector port="443" protocol="HTTP/1.1" SSLEnabled="true"
     maxThreads="150" scheme="https" secure="true"
   # Path of the certificate
     keystoreFile="Tomcat installation directory/conf/cloud.tencent.com.jks" 
   # Keystore password
     keystorePass="******"
     clientAuth="false"/>
   ```

   The main parameters of the configuration file are described as below:

  - **keystoreFile**: The location of the keystore file. You can specify an absolute path or a path relative to the <CATALINA_HOME> (Tomcat installation directory) environment variable. If this parameter is not set, Tomcat will read the file named `.keystore` from the user directory of the current OS user.

  - **keystorePass**: keystore password. If you set a private key password when applying for the certificate, enter the private key password; otherwise, enter the password in the `keystorePass.txt` file in the Tomcat folder.

  - **clientAuth**: If it is set to true, Tomcat requires all SSL clients to provide a security certificate for identity verification.


For details about the `server.xml` file, see below:
>! 
> Do not copy the content of the `server.xml` file; otherwise, the format will be incorrect.




      ``` xml
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
                      keystoreFile="Tomcat installation directory/conf/cloud.tencent.com.jks"
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



5. Check whether the Tomcat server is started.

  - If so, you need to run the following commands to shut down and restart the Tomcat service in the `bin` directory (for example, `/usr/Tomcat-9.0.56/bin`) of the Tomcat installation directory.

      ``` bash
      ./shutdown.sh (Shut down the Tomcat service)
      ./startup.sh (Start the Tomcat service)
      ```
  - If not, you need to run the following command to start the Tomcat service in the `bin` directory (for example, `/usr/Tomcat-9.0.56/bin`) of the Tomcat installation directory.

      ``` bash
      ./startup.sh
      ```
6. If the server is started successfully, you can access it through `https://cloud.tencent.com`.

  - If the security lock icon is displayed in the browser, the certificate has been installed successfully.

  - In case of a website access exception, troubleshoot the issue by referring to the following FAQs:

    - [Website Inaccessible After an SSL Certificate is Deployed](https://intl.cloud.tencent.com/document/product/1007/39821)

    - ["Your Connection is Not Secure" is Displayed After the SSL Certificate is Installed](https://intl.cloud.tencent.com/document/product/1007/40674)

    - [Why Does the Website Prompt "Connection Is Untrusted"?](https://intl.cloud.tencent.com/document/product/1007/30184)


    - [404 Error After the SSL Certificate is Deployed on IIS](https://intl.cloud.tencent.com/document/product/1007/39820)


### (Optional) Security configuration for automatic redirect from HTTP to HTTPS

To redirect HTTP requests to HTTPS, complete the following settings:
1. Edit the `web.xml` file in the `conf` directory (for example, `/usr/Tomcat-9.0.56/conf`) of the Tomcat installation directory and find the `</welcome-file-list>` tag.

2. Insert a new line after `</welcome-file-list>` and add the following:

   ``` xml
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
3. Edit the `server.xml` file in the `conf` directory (for example, `/usr/Tomcat-9.0.56/conf`) of the Tomcat installation directory by changing the `redirectPort` parameter to the port of the SSL connector, i.e., port `443`, as shown below:

   ``` bash
   <Connector port="80" protocol="HTTP/1.1"
     connectionTimeout="20000"
     redirectPort="443" />
   ```

   >?
   >
   >  This change allows a non-SSL connector to redirect to an SSL connector.
   > 

4. Run the following command to shut down the Tomcat service in the `/bin` directory (for example, `/usr/Tomcat-9.0.56/bin`) of the Tomcat installation directory.

   ``` bash
   ./shutdown.sh
   ```
5. Run the following command to confirm whether there is a problem with the configuration:

   ``` bash
   ./configtest.sh
   ```
  - If yes, reconfigure or fix the problem as prompted.

  - If no, proceed to the next step.

6. Run the following command to start the Tomcat service. In this way, you can access it through `http://cloud.tencent.com`.

   ``` bash
   ./startup.sh
   ```
