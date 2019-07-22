## Scenario
This document guides you through how to install an SSL certificate on a Tomcat server.
>
>- This document takes the domain name `www.domain.com` as an example.
>- The current server OS is CentOS 7. The detailed steps vary slightly by OS version.
## Prerequisites
- The certificate package for the domain name `www.domain.com` in the SSL Certificate Service Console has been downloaded and decompressed to a local directory.
After decompression, you can get the Tomcat folder and CSR file:
 - **Folder name**: Tomcat
 - **Folder content**:
    - `www.domain.com.jks`   Keystore
    - `keystorePass.txt`   Password file
  - **CSR file content**: 	`www.domain.com.csr` file
- The remote copy tool WinSCP has been installed (you are recommended to get the latest version from its official website).
- The remote login tool PuTTY or Xshell has been installed (you are recommended to get the latest version from their official websites).
- The Tomcat server (version number: tomcat7.0.94) has been installed and configured on the current server.

>
- If you selected the "Paste CSR" method when applying for the SSL certificate, the option for downloading the Tomcat certificate file is not provided, and you need to generate the keystore by manually converting the format as detailed below: 
 - Access the [conversion tool](https://myssl.com/cert_convert.html).
 - Upload the certificate and private key files in the Nginx folder to the conversion tool, enter the keystore password, click **Submit**, and convert the certificate to a .jks certificate.
- If you have already set a private key password when applying for the SSL certificate, there is no keystorePass.txt file in this folder.
- The CSR file is uploaded by you or generated online by the system when you apply for the certificate and is provided to the CA, which can be ignored during installation.
- Currently, the Tomcat server is installed in the `/usr` directory. For example, if the Tomcat folder name is `tomcat7.0.94`, then `/usr/*/conf` is actually `/usr/tomcat7.0.94/conf`.


## Data
The data to be prepared before installing the SSL certificate includes:

| Name | Description | Sample Value |
|---------|---------|---------|
| Server IP address | IP address of the server, which is used to connect the PC to the server. | 192.168.22.10 |
| Username | The username used to log in to the server. | root |
| Password | The password used to log in to the server. | abc |

## Directions

### Certificate Installation
1. Log in to the Tomcat server using WinSCP (a tool copying files between a local computer and a remote computer).
2. Copy the obtained `www.domain.com.jks` keystore file from the local directory to the `/usr/*/conf` directory.
3. Close WinSCP.
4. Log in to the Tomcat server using a remote login tool such as PuTTY.
5. Edit the `server.xml` file in the `/usr/*/conf` directory by adding the following:
```
<Connector port="443" protocol="HTTP/1.1" SSLEnabled="true"
  maxThreads="150" scheme="https" secure="true"
  keystoreFile="/usr/*/conf/www.domain.com.jks" # Storage path of the certificate
  keystorePass="******"# Keystore password
  clientAuth="false"/>
```
For details of the `server.xml` file, see below:
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
                keystoreFile="/usr/*/conf/www.domain.com.jks"
                keystorePass="******" />
    <Connector port="8009" protocol="AJP/1.3" redirectPort="8443" />
   <Engine name="Catalina" defaultHost=“www.domain.com">
      <Realm className="org.apache.catalina.realm.LockOutRealm">
        <Realm className="org.apache.catalina.realm.UserDatabaseRealm"
               resourceName="UserDatabase"/>
      </Realm>
    <Host name=“www.domain.com"  appBase="webapps" 
        unpackWARs="true" autoDeploy="true" >
        <Context path="" docBase ="Knews" />
    <Valve className="org.apache.catalina.valves.AccessLogValve" directory="logs"
           prefix="localhost_access_log" suffix=".txt"  
           pattern="%h %l %u %t "%r" %s %b" />
      </Host>
    </Engine>
  </Service>
</Server>
```
The main parameters of the configuration file are described as below:
 - **keystoreFile**: Where the keystore file is saved. You can specify an absolute path or the relative path to the &lt;CATALINA_HOME&gt; (Tomcat installation directory) environment variable. If this parameter is not set, by default, Tomcat reads the file named ".keystore" from the user directory of the current operating system user.
 - **keystorePass**: Keystore password. If you set a private key password when applying for the certificate, enter the private key password; otherwise, enter the password in the keystorePass.txt file in the Tomcat folder.
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
7. After it is started successfully, it can be accessed using `https://www.domain.com`.

### Security Configuration for Automatic Redirect from HTTP to HTTPS (Optional)

If you don't know how to access a website over HTTPS, you can configure the server to make it automatically redirect HTTP requests to HTTPS in the following steps:
1. Edit the `web.xml` file in the `/usr/*/conf` directory and find the `</welcome-file-list>` tag.
2. Insert a new line below `</welcome-file-list>` and add the following:
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
3. Edit the `server.xml` file in the `/usr/*/conf` directory by modifying the redirectPort parameter to the port of the SSL connector, i.e., changing port 8443 to port 443, as shown below:
```
<Connector port="80" protocol="HTTP/1.1"
  connectionTimeout="20000"
  redirectPort="443" />
```
> This modification allows a non-SSL connector to redirect to an SSL connector.
>
4. Shut down the Tomcat server by running the following command in the ` /usr/*/bin` directory.
```
./shutdown.sh
```
5. Run the following command to confirm whether there is a problem with the configuration.
```
./configtest.sh
```
 - If yes, reconfigure or fix the problem as prompted.
 - If no, proceed to the next step.
5. Run the following command to start the Tomcat server and then it can be accessed using `http://www.domain.com`.
```
./startup.sh
```

> If anything goes wrong during this procedure, [contact us](https://intl.cloud.tencent.com/document/product/1007/30951).

