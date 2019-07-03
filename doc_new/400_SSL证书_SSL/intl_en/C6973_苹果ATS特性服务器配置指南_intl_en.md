Configuration Guide:
1. You need to configure the encryption package in line with the PFS specification. The recommended configuration is:
`ECDHE-RSA-AES128-GCM-SHA256:ECDHE:ECDH:AES:HIGH:!NULL:!aNULL:!MD5:!ADH:!RC4`
2. You need to enable TLS1.2 in the TLS protocol of server. The recommended configuration is:
`TLSv1 TLSv1.1 TLSv1.2`

### 1. Nginx certificate configuration

Update the file conf/nginx.conf in the root directory Nginx as follows:
```
server {
	ssl_ciphers ECDHE-RSA-AES128-GCM-SHA256:ECDHE:ECDH:AES:HIGH:!NULL:!aNULL:!MD5:!ADH:!RC4;
	ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
}
```

### 2. Apache certificate configuration

Update the conf/httpd.conf file in the Apache root directory as follows:
```
<IfModule mod_ssl.c>
        <VirtualHost *:443>
		SSLProtocol TLSv1 TLSv1.1 TLSv1.2
		SSLCipherSuite ECDHE-RSA-AES128-GCM-SHA256:ECDHE:ECDH:AES:HIGH:!NULL:!aNULL:!MD5:!ADH:!RC4
		</VirtualHost>
</IfModule>
```

### 3. Tomcat certificate configuration
Update the %TOMCAT_HOME%\conf\server.xml file as follows:
```
<Connector port="443" protocol="HTTP/1.1" SSLEnabled="true"
    scheme="https" secure="true"
    SSLProtocol="TLSv1+TLSv1.1+TLSv1.2"
    SSLCipherSuite="ECDHE-RSA-AES128-GCM-SHA256:ECDHE:ECDH:AES:HIGH:!NULL:!aNULL:!MD5:!ADH:!RC4" />
```

### 4. IIS certificate configuration
Click **Start** -> **Run**. Enter regedit
Find HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols, right-click it, and then click **New** -> **Item** -> **Create TLS 1.1, TLS 1.2**
Right-click TLS 1.1 and TLS 1.2, and click **New** -> **Item** -> **Create Server, Client**
Create the following items (4 in total, DWORD 32-bit value) in the new Server and Client
DisabledByDefault [Value = 0]
Enabled [Value = 1]

![2](https://main.qcloudimg.com/raw/ae6bc5b29dd13f19ef639a6a479ecfcf.png)

![](https://main.qcloudimg.com/raw/c5f17d22c1f9bdbbf47105b925e784d9.png)

![](https://main.qcloudimg.com/raw/5e36aa88e7354c93e0f7bcc18b94db93.png)

![](https://main.qcloudimg.com/raw/6f7df0665ff13291154160052781ecd6.png)

Restart the system after completion

Encryption suite adjustment
Adjustments can be made through the Group Policy Editor if the forward privacy encryption suite is not supported.
Click **Start** -> **Run**, and enter gpedit.msc for encryption suite adjustment after enabling TLS1_2 protocol.

![3](https://main.qcloudimg.com/raw/86b2195e436d0276ea3069c8916a6003.png)
Double-click the **SSL cipher suite order**.

![4](https://main.qcloudimg.com/raw/bdfd7424be1b0644118e9172738320c5.png)

Add the supported ECDHE cipher suites to the SSL cipher suites, separated by comma (,).
Open a blank WordPad document.
Copy the list of available suites on the right in the figure below and paste it into the document.
Sort suites in the correct order and delete any suites you do not want to use.
Type a comma at the end of each suite name (except for the last one). Make sure no space is embedded.
Remove all the line breaks so that the cipher suite names are in a single, long line.
Copy the cipher suite line to the clipboard and paste it into the edit box with the maximum length of 1,023 characters.

![5](https://main.qcloudimg.com/raw/2214ae20462cd0aeaa8a4593bea7f40e.png)

The following suites can be added to the cipher suite
TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA
TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA
TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256
TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384
TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256
TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384

Attachment:
Recommended suite combination:
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
