### How do I install OpenSSL?
OpenSSL is a well-known open source cryptography toolkit for secure communications, featuring cryptographic algorithms, common passwords, and certificate packaging.

#### OpenSSL official website

For the official download address: click [here](https://www.openssl.org/source/).

#### Installing OpenSSL on Windows

No installation package for Windows is provided on the OpenSSL official website. Instead, you can use tools provided by other open source platforms, such as, [Win32/Win64 OpenSSL](http://slproweb.com/products/Win32OpenSSL.html). 
The following describes how installation and usage information Windows users.

1. Download a 32-bit or 64-bit version, for example, `Win64OpenSSL_Light-1_0_2h.exe`, as shown in the following figure.
![](https://main.qcloudimg.com/raw/d37d791cf12c0b42dddcc53a691a86d9.png)
2. Set the environment variables. If the tool is installed in `C:\OpenSSL-Win64`, copy `C:\OpenSSL-Win64\bin;` to **Path**, as shown in the following figure.
![](https://main.qcloudimg.com/raw/4aefd5ab97c19e04d68105584f313ee9.png)
3. Open the Command Prompt (you must be logged in as the admin), go to the directory in which the files `2_www.tencent.com.key` and `1_www.tencent.com_cert.crt` are saved, and run the following command:
```
openssl pkcs12 -export -out www.tencent.com.pfx -inkey 2_www.tencent.com.key -in 1_www.tencent.com_cert.crt
```
If the .key and .crt files are stored in `D:\`, the running status will be as follows:
![](https://main.qcloudimg.com/raw/159d8d55ab8f2762eb7135da54371f08.png)

>!If Export Password is not required, press **Enter** directly.
4. After the file `www.tencent.com.pfx` is generated in `D:\`, continue to complete the certificate installation in IIS Manager.

