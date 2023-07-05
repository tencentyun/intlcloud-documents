>!
>- You need to configure cipher suites compliant with PFS specifications. The recommended configuration is:
`ECDHE-RSA-AES128-GCM-SHA256:ECDHE:ECDH:AES:HIGH:!NULL:!aNULL:!MD5:!ADH:!RC4`
>- You need to enable the TLS1.2 protocol on the server. The recommended configuration is:
`TLSv1 TLSv1.1 TLSv1.2`

### Nginx certificate configuration
Update the `conf/nginx.conf` file in the Nginx root directory as follows:
```
server {
	ssl_ciphers ECDHE-RSA-AES128-GCM-SHA256:ECDHE:ECDH:AES:HIGH:!NULL:!aNULL:!MD5:!ADH:!RC4;
	ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
}
```

### Apache certificate configuration
Update the `conf/httpd.conf` file in the Apache root directory as follows:
```
<IfModule mod_ssl.c>
        <VirtualHost *:443>
		SSLProtocol TLSv1 TLSv1.1 TLSv1.2
		SSLCipherSuite ECDHE-RSA-AES128-GCM-SHA256:ECDHE:ECDH:AES:HIGH:!NULL:!aNULL:!MD5:!ADH:!RC4
		</VirtualHost>
</IfModule>
```

### Tomcat certificate configuration
Update the `%TOMCAT_HOME%\conf\server.xml` file as follows:
```
<Connector port="443" protocol="HTTP/1.1" SSLEnabled="true"
    scheme="https" secure="true"
    SSLProtocol="TLSv1+TLSv1.1+TLSv1.2"
    SSLCipherSuite="ECDHE-RSA-AES128-GCM-SHA256:ECDHE:ECDH:AES:HIGH:!NULL:!aNULL:!MD5:!ADH:!RC4" />
```

### IIS certificate configuration
#### Method 1
Windows Server 2008 and earlier versions do not support the TLS1.2 protocol. Therefore, SSL tools are disabled on those versions. To address this issue, enable the TLS1.2 protocol to meet the ATS requirements.

Taking Windows Server 2008 R2 as an example, there is no adjustment to protocols and cipher suites after the certificate is imported.
 The cipher suites will support ATS requirements after the certificate is imported but the TLS1.2 protocol required for ATS is not enabled. You can use ssltools ([click to download](http://www.trustasia.com/down/ssltools.zip)) to enable the TLS1.2 protocol, as shown below:
![](https://main.qcloudimg.com/raw/21fde4a6d02969a22c02d279f71750f5.png) 

- Select the 3 TLS protocols, and restart the system.
- If PFS is not supported, select ECDHE and DHE in **Cipher Suites**.

#### Method 2
1. Choose **Start** -> **Run**. Enter `regedit`.
2. Find `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols`, right-click it, and then choose **New** -> **Item** -> **Create TLS 1.1, TLS 1.2**.
3. Right-click TLS 1.1 and TLS 1.2, and choose **New** -> **Item** -> **Create Server, Client**.
4. Create the following items (4 in total, DWORD 32-bit value) in the new servers and clients.
 - DisabledByDefault [Value = 0]
 - Enabled [Value = 1]
![2](https://main.qcloudimg.com/raw/c371b0309b3233d5b37da1bb74b43e4c.png)
![3](https://main.qcloudimg.com/raw/656639fcb89350c9dbd5f11b63d6cd19.png)
![4](https://main.qcloudimg.com/raw/a65d675b742144e817eef3fd882b48a8.png)
![5](https://main.qcloudimg.com/raw/a58d8d4fd525777eb1d7bf523c4fcda6.png)
5. Restart the system.
6. Adjust the cipher suites: choose **Start** -> **Run**, and enter `gpedit.msc` for the cipher suite adjustments after enabling the TLS1.2 protocol.
>!Adjustments can be made through the Group Policy Editor if PFS is not supported by the cipher suites.

![3](https://main.qcloudimg.com/raw/11f246fad52917de46de6eff14183137.png)
7. Double-click **SSL Cipher Suite Order** and enter information, as shown in the following figure:
![4](https://main.qcloudimg.com/raw/2f2a9c96b351282957827358cf96cc2d.png)
  - Select `Enabled`.
  - Add the supported ECDHE cipher suites to the SSL cipher suites, separated by commas (,).
  - Enter the cipher suite information as follows:
      a. Open a blank WordPad document.
      b. Copy the list of available suites on the right in the figure below and paste it into the document.
      c. Sort the suites in the correct order and delete any suites you do not want to use.
      d. Type a comma at the end of each suite name (except for the last one). Make sure no space is entered.
      e. Remove all the line breaks so that the cipher suite names are in a single, long line.
      f. Copy the cipher suite line to the clipboard and paste it into the edit box. You can enter up to 1,023 characters.
8. After the cipher suite information is entered, the content in the window is updated, as shown in the following figure:
![5](https://main.qcloudimg.com/raw/2214ae20462cd0aeaa8a4593bea7f40e.png)
The following suites can be added to the cipher suite:
TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA
TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA
TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256
TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384
TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256
TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384
The following suite combination is recommended:
TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA_P256
TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA_P384
TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA_P521
TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA_P256
TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA_P384
TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA_P521
TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256_P256
TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256_P384
TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256_P521
TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384_P256
TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384_P384
TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384_P521
TLS_DHE_RSA_WITH_AES_256_GCM_SHA384
TLS_RSA_WITH_AES_128_CBC_SHA
TLS_RSA_WITH_AES_256_CBC_SHA
TLS_RSA_WITH_3DES_EDE_CBC_SHA
TLS_RSA_WITH_AES_128_CBC_SHA256
TLS_RSA_WITH_AES_256_CBC_SHA256
TLS_RSA_WITH_AES_128_GCM_SHA256
TLS_RSA_WITH_AES_256_GCM_SHA384



