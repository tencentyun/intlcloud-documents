## Overview
This document describes how to install an SSL certificate on a Jetty server.
>?
>- The certificate name `cloud.tencent.com` is used as an example.
>- Jetty 9.4.28.v20200408 is used as an example.
>- The current server OS is CentOS 7. Detailed steps vary slightly with the OS.
>- Before you install an SSL certificate, enable port 443 on the Jetty server so that HTTPS can be enabled after the certificate is installed. For more information, see [How Do I Enable Port 443 for a VM?](https://intl.cloud.tencent.com/document/product/1007/36738)
>- For more information about how to upload SSL certificate files to a server, please see [Copying Local Files to CVMs](https://intl.cloud.tencent.com/document/product/213/34821).

## Prerequisites
- A remote file copy tool such as WinSCP has been installed. Please download the latest version from the official website.
- A remote login tool such as PuTTY or Xshell has been installed. Please download the latest version from the official website.
- The Jetty service has been installed and configured on the current server.
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
- If you have selected the **Paste CSR** method when applying for the SSL certificate, or your certificate brand is Wotrus, the option to download the JKS certificate file is not provided. Instead, you need to manually convert the format to generate a keystore as follows: 
 - Access the [conversion tool](https://myssl.com/cert_convert.html).
 - Upload the certificate and private key files in the Nginx folder to the conversion tool, enter the keystore password, click **Submit**, and convert the certificate to a .jks certificate.
- The Jetty service is installed in the `/usr/local/jetty` directory.


## Directions
1. Log in to the [SSL Certificate Service console](https://console.cloud.tencent.com/ssl), and click **Download** for the certificate you need to install.
2. In the pop-up window, select **JKS** for the server type, click **Download**, and decompress the `cloud.tencent.com` certificate file package to the local directory.
After decompression, you can get the certificate file of the corresponding type, which includes the `cloud.tencent.com_jks` folder.
 - **Folder**: `cloud.tencent.com_jks`
 - **Files in the folder**:
    - `cloud.tencent.com.jks`: keystore file
    - `cloud.tencent.com.key`: private key file
    - `keystorePass.txt`: password file (if you have set a private key password, this file will not be generated)
3. Remotely log in to the Jetty server. For example, you can use [PuTTY](https://intl.cloud.tencent.com/document/product/213/32502) for remote login.
4. In the `/usr/local/jetty/jetty-distribution-9.4.28.v20200408/etc` directory, run the `mkdir cert` command to create the `cert` folder.
5. Use WinSCP (a tool for copying files between a local computer and a remote computer) to log in to the Jetty server and copy the keystore file `cloud.tencent.com.jks` from the local directory to the `cert` folder.
6. In the `/usr/local/jetty/jetty-distribution-9.4.28.v20200408/etc` directory, modify the configuration in the `jetty-ssl-context.xml` file.
>?
>- **KeyStorePath**: set the default value to the path of the certificate file.
>- **KeyStorePassword**: set the default value to the keystore password. If you have set a private key password when applying for the certificate, enter the private key password; otherwise, enter the password in the `keystorePass.txt` file in the `cloud.tencent.com_jks` folder.
>- **KeyManagerPassword**: set the value to the password in the `keystorePass.txt` file in the `cloud.tencent.com_jks` folder.
>- **TrustStorePath**: set the default value to the certificate file path.
>
```
<?xml version="1.0"?><!DOCTYPE Configure PUBLIC "-//Jetty//Configure//EN" "http://www.eclipse.org/jetty/configure_9_3.dtd">
<!-- ============================================================= --><!-- SSL ContextFactory configuration                              --><!-- ============================================================= -->
<!-- 
  To configure Includes / Excludes for Cipher Suites or Protocols see tweak-ssl.xml example at 
     https://www.eclipse.org/jetty/documentation/current/configuring-ssl.html#configuring-sslcontextfactory-cipherSuites
-->
<Configure id="sslContextFactory" class="org.eclipse.jetty.util.ssl.SslContextFactory$Server">
  <Set name="Provider"><Property name="jetty.sslContext.provider"/></Set>
  <Set name="KeyStorePath"><Property name="jetty.base" default="." />/<Property name="jetty.sslContext.keyStorePath" deprecated="jetty.keystore" default="etc/cert/cloud.tencent.com.jks"/></Set>
  <Set name="KeyStorePassword"><Property name="jetty.sslContext.keyStorePassword" deprecated="jetty.keystore.password" default="4d5jtdq238j1l"/></Set>
  <Set name="KeyStoreType"><Property name="jetty.sslContext.keyStoreType" default="JKS"/></Set>
  <Set name="KeyStoreProvider"><Property name="jetty.sslContext.keyStoreProvider"/></Set>
  <Set name="KeyManagerPassword"><Property name="jetty.sslContext.keyManagerPassword" deprecated="jetty.keymanager.password" default="4d5jtdq238j1l"/></Set>
  <Set name="TrustStorePath"><Property name="jetty.base" default="." />/<Property name="jetty.sslContext.trustStorePath" deprecated="jetty.truststore" default="etc/cert/cloud.tencent.com.jks"/></Set>
  <Set name="TrustStorePassword"><Property name="jetty.sslContext.trustStorePassword" deprecated="jetty.truststore.password"/></Set>
  <Set name="TrustStoreType"><Property name="jetty.sslContext.trustStoreType"/></Set>
  <Set name="TrustStoreProvider"><Property name="jetty.sslContext.trustStoreProvider"/></Set>
  <Set name="EndpointIdentificationAlgorithm"><Property name="jetty.sslContext.endpointIdentificationAlgorithm"/></Set>
  <Set name="NeedClientAuth"><Property name="jetty.sslContext.needClientAuth" deprecated="jetty.ssl.needClientAuth" default="false"/></Set>
  <Set name="WantClientAuth"><Property name="jetty.sslContext.wantClientAuth" deprecated="jetty.ssl.wantClientAuth" default="false"/></Set>
  <Set name="useCipherSuitesOrder"><Property name="jetty.sslContext.useCipherSuitesOrder" default="true"/></Set>
  <Set name="sslSessionCacheSize"><Property name="jetty.sslContext.sslSessionCacheSize" default="-1"/></Set>
  <Set name="sslSessionTimeout"><Property name="jetty.sslContext.sslSessionTimeout" default="-1"/></Set>
  <Set name="RenegotiationAllowed"><Property name="jetty.sslContext.renegotiationAllowed" default="true"/></Set>
  <Set name="RenegotiationLimit"><Property name="jetty.sslContext.renegotiationLimit" default="5"/></Set>
  <Set name="SniRequired"><Property name="jetty.sslContext.sniRequired" default="false"/></Set>
  <!-- Example of how to configure a PKIX Certificate Path revocation Checker
  <Call id="pkixPreferCrls" class="java.security.cert.PKIXRevocationChecker$Option" name="valueOf"><Arg>PREFER_CRLS</Arg></Call>
  <Call id="pkixSoftFail" class="java.security.cert.PKIXRevocationChecker$Option" name="valueOf"><Arg>SOFT_FAIL</Arg></Call>
  <Call id="pkixNoFallback" class="java.security.cert.PKIXRevocationChecker$Option" name="valueOf"><Arg>NO_FALLBACK</Arg></Call>
  <Call class="java.security.cert.CertPathBuilder" name="getInstance">
    <Arg>PKIX</Arg>
    <Call id="pkixRevocationChecker" name="getRevocationChecker">
      <Call name="setOptions">
        <Arg>
          <Call class="java.util.EnumSet" name="of">
            <Arg><Ref refid="pkixPreferCrls"/></Arg>
            <Arg><Ref refid="pkixSoftFail"/></Arg>
            <Arg><Ref refid="pkixNoFallback"/></Arg>
          </Call>
        </Arg>
      </Call>
    </Call>
  </Call>
  <Set name="PkixCertPathChecker"><Ref refid="pkixRevocationChecker"/></Set>
  -->
</Configure>
```
7. In the `/usr/local/jetty/jetty-distribution-9.4.28.v20200408/etc` directory, change the port number to 443 in the `jetty-ssl.xml` file.
```
 <Call  name="addConnector">
    <Arg>
      <New id="sslConnector" class="org.eclipse.jetty.server.ServerConnector">
        <Arg name="server"><Ref refid="Server" /></Arg>
        <Arg name="acceptors" type="int"><Property name="jetty.ssl.acceptors" deprecated="ssl.acceptors" default="-1"/></Arg>
        <Arg name="selectors" type="int"><Property name="jetty.ssl.selectors" deprecated="ssl.selectors" default="-1"/></Arg>
        <Arg name="factories">
          <Array type="org.eclipse.jetty.server.ConnectionFactory">
            <!-- uncomment to support proxy protocol
            <Item>
              <New class="org.eclipse.jetty.server.ProxyConnectionFactory"/>
            </Item>-->
          </Array>
        </Arg>
        <Set name="host"><Property name="jetty.ssl.host" deprecated="jetty.host" /></Set>
        <Set name="port"><Property name="jetty.ssl.port" deprecated="ssl.port" default="443" /></Set>
        <Set name="idleTimeout"><Property name="jetty.ssl.idleTimeout" deprecated="ssl.timeout" default="30000"/></Set>
        <Set name="acceptorPriorityDelta"><Property name="jetty.ssl.acceptorPriorityDelta" deprecated="ssl.acceptorPriorityDelta" default="0"/></Set>
        <Set name="acceptQueueSize"><Property name="jetty.ssl.acceptQueueSize" deprecated="ssl.acceptQueueSize" default="0"/></Set>
        <Get name="SelectorManager">
          <Set name="connectTimeout"><Property name="jetty.ssl.connectTimeout" default="15000"/></Set>
        </Get>
      </New>
    </Arg>
  </Call>
```
8. In the `/usr/local/jetty/jetty-distribution-9.4.28.v20200408` directory, add the following content to the `start.ini` file:
```
etc/jetty-ssl.xml
etc/jetty-ssl-context.xml
etc/jetty-https.xml
```
9. In the Jetty root directory, run the `java -jar start.jar` command to start the Jetty server and then you can access it through `https://cloud.tencent.com`.

## Notes
After the certificate is deployed, the following error message may be displayed when you access `https://cloud.tencent.com`:
![](https://main.qcloudimg.com/raw/2ad181d6ed021958c214b04df9fa67a6.png)
If the error message is displayed, copy the `ROOT` file from the `/usr/local/jetty/jetty-distribution-9.4.28.v20200408/demo-base/webapps` directory to the `/usr/local/jetty/jetty-distribution-9.4.28.v20200408/webapps` directory, and then restart the Jetty server.

>!If you experience any issues with the above steps, please [contact us](https://intl.cloud.tencent.com/document/product/1007/30951).


