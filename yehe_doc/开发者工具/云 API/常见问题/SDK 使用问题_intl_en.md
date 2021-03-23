### Python certificate error

While installing Python 3.6 or a later version in macOS, you may encounter a certificate error:
```
Error: [SSL: CERTIFICATE_VERIFY_FAILED] certificate verify failed: self signed certificate in certificate chain (_ssl.c:1056).
```
You can solve this problem by running the following command to install a certificate.
>?In macOS, Python does not use the system default certificate nor provide a certificate. HTTPS requests require a certificate provided in `certifi`.
>
```
sudo "/Applications/Python 3.6/Install Certificates.command"
```



### PHP certificate error

You may encounter an error if your PHP certificate is incorrect:
```
cURL error 60: See http://curl.haxx.se/libcurl/c/libcurl-errors.html
```
Perform the following steps to solve this problem.
1. Download the `cacert.pem` certificate file at `https://curl.haxx.se/ca/cacert.pem` and save it to the PHP installation path.
2. Edit the `php.ini` file, delete the comment symbol `;` before the `curl.cainfo` configuration item and set its value to the absolute path of the `cacert.pem` certificate file.
3. Restart PHP-dependent services.



### php_curl extension

The SDK’s underlying GuzzleHttp requires php_curl extension. Check that php_curl extension is enabled in `php.ini`. For example, to check whether an Apache hosted service using PHP 7.1 in Linux enables php_curl extension, access `/etc/php/7.1/apache2/php.ini` and check for the `extension=php_curl.dll` configuration item. Delete the comment symbol (if any) before the configuration item and restart Apache.



### Java dependency conflict

The SDK currently depends on okhttp 2.5.0. If you also use other okhttp3 packages, an error may occur:
```
Exception in thread "main" java.lang.NoSuchMethodError: okio.BufferedSource.rangeEquals(JLokio/ByteString;)Z
```
Since okhttp3 depends on okio 1.12.0 and okhttp depends on okio 1.6.0, Maven resolves dependencies according to the shortest path and declaration sequence. If the SDK is first declared in the `pom.xml` dependency, then okio 1.6.0 will be used, resulting in an error. Perform the following steps to solve this problem until SDK is upgraded to okhttp3:
1. Specify okio 1.12.0 or a later version required by other packages in `pom.xml`.
2. Place reference SDK at the end of the `pom.xml` file. If the SDK has been compiled early, delete the Maven cached okhttp package. In this example, the okhttp3-dependent CMQ SDK is also used:
```xml
    <dependency>
      <groupId>com.qcloud</groupId>
      <artifactId>cmq-http-client</artifactId>
      <version>1.0.7</version>
    </dependency>
    <dependency>
      <groupId>com.tencentcloudapi</groupId>
      <artifactId>tencentcloud-sdk-java</artifactId>
      <version>3.1.59</version>
    </dependency>
```



### .NET dependency conflict

 The SDK depends on FluentClient 3.2, while FluentClient 4.0 is now launched without backwards compatibility. Upgrading to version 4.0 in NuGet will cause calling failures. 



### Legacy SDK
Legacy SDKs remain available in the QcloudApi directory, but will not be updated. For more information, please see [Overview](https://github.com/QcloudApi). We recommend using the latest SDK.
