OpenSSL is a well-known open source cryptography toolkit for secure communications, and contains cryptographic algorithms, common passwords, and certificate packaging feature.

#### 1. Official Website of OpenSSL

Official download address: https://www.openssl.org/source/

#### 2. Installation Method on Windows

Windows version of the installation package is not provided on OpenSSL official website. You can choose tools provided by other open source platforms, for example: http://slproweb.com/products/Win32OpenSSL.html 
Taking this tool as an example, the installation steps and usage are as follows:

1. Download a 32-bit or 64-bit version, for example, Win64OpenSSL_Light-1_0_2h.exe, as shown below:
  ![](https://main.qcloudimg.com/raw/8427f565530e3c73551707f3b0bebea4.png)

2. Set environment variables. If the tool is installed in C:\OpenSSL-Win64, copy `C:\OpenSSL-Win64\bin；` to Path

   

   ![](https://main.qcloudimg.com/raw/4aefd5ab97c19e04d68105584f313ee9.png)

3. Open the command line program cmd (run as an administrator), enter the directory where 2_www.domain.com.key and 1_www.domain.com_cert.crt are stored, and run the command below
```
openssl pkcs12 -export -out www.domain.com.pfx -inkey 2_www.domain.com.key -in 1_www.domain.com_cert.crt
```
For example, the key and crt files are stored in D:\ and the operation is as follows:
![](https://main.qcloudimg.com/raw/159d8d55ab8f2762eb7135da54371f08.png)
Note: If Export Password is not required, press Enter directly without input.

4. After www.domain.com.pfx is generated in D:\, you can continue to complete the certificate installation in IIS Manager.

