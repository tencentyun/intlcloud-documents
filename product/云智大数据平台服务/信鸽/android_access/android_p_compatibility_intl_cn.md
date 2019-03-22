# Demo配置

## TLS默认启用
在res目录下的xml目录添加文件xg_network_security_config.xml，内容为：
```xml
<?xml version="1.0" encoding="utf-8"?>
<network-security-config>
    <domain-config cleartextTrafficPermitted="true">
        <domain includeSubdomains="true">182.254.116.117</domain>
        <domain includeSubdomains="true">pingma.qq.com</domain>
    </domain-config>
</network-security-config>
```

在AndroidManifest的application节点添加一下配置：
```xml
android:networkSecurityConfig="@xml/xg_network_security_config"
```
## 添加使用Apache HTTP client库

在AndroidManifest的application节点内添加以下配置即可
```xml
<uses-library android:name="org.apache.http.legacy" android:required="false"/>
```
## 修改compileSdk和targetSdk
编译APK时使用compileSdkVersion和targetSdkVersion都使用28
