## TLS is enabled by default
Add the xg_network_security_config.xml file in the xml directory under the res directory with the following content:
```xml
<?xml version="1.0" encoding="utf-8"?>
<network-security-config>
    <domain-config cleartextTrafficPermitted="true">
        <domain includeSubdomains="true">182.254.116.117</domain>
        <domain includeSubdomains="true">pingma.qq.com</domain>
    </domain-config>
</network-security-config>
```

Add the following configuration to the application node of AndroidManifest:
```xml
android:networkSecurityConfig="@xml/xg_network_security_config"
```
## Add and use the Apache HttpClient library

Add the following configuration to the application node of AndroidManifest:
```xml
<uses-library android:name="org.apache.http.legacy" android:required="false"/>
```
## Modify compileSdk and targetSdk
Use compileSdkVersion 28 and targetSdkVersion 28 when compiling.
