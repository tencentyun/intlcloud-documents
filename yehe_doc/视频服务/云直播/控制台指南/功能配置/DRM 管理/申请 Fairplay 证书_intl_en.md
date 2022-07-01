To encrypt your content with FairPlay, you need to obtain an FPS deployment package from Apple and upload the following files to SDMC’s server.
- FPS certificate file (.der or .cer)
- Private key file (.pem)
- Private key password file (.txt)
- Application secret key (ASK) (.txt)

## Directions
 [](id:step1)
### Step 1. Create an Apple developer account and request an FPS package
1. Create an [Apple developer account](https://developer.apple.com/support/enrollment/).
2. At the bottom of the [FairPlay Streaming](https://developer.apple.com/streaming/fps/) page, click **Request FPS Deployment Package**, and log in with your Apple developer account.
3. Fill out the form and submit it. After your request is approved, Apple will send you a package containing the FPS certificate generation guide.

>! When asked if you have implemented and tested Key Security Module (KSM), you can paste the answer below:
```
I am using a 3rd party DRM company and the company has already built and tested KSM
```

 [](id:step2)
### Step 2. Create a private key and a certificate signing request (CSR)
Create a private key file (`privatekey.pem`) and a CSR file (`certreq.csr`) as instructed in the FPS certificate generation guide. The following describes the OpenSSL method in the guide.
>? Make sure OpenSSL is installed on the computer or server environment where this process is performed.

1. **Create a private key file (`privatekey.pem`)**:
	1. Run the command below to create a private key file:[](id:step1_1)
```
openssl genrsa -aes256 -out privatekey.pem 1024
```
	2. Set a password (not longer than 32 characters) for the private key. Note it for later use.
2. **Create a CSR file**:
	1. Run the command below (you can modify `-subj`):
```
openssl req -new -sha1 -key privatekey.pem -out certreq.csr -subj "/CN=SubjectName/OU=OrganizationalUnit/O=Organization/C=US"
```
	2. Enter the private key password configured in the [previous step](#step1_1).

[](id:step3)
### Step 3. Generate the FPS certificate
1. Log in to [Apple Developer](https://developer.apple.com/) and click [Certificates, IDs & Profiles](https://developer.apple.com/account/ios/certificate/).
![](https://qcloudimg.tencent-cloud.cn/raw/3c2963e1317986b25f05014042f120de.png)
2. Click **+** to enter the **Create a New Certificate** page.
![](https://qcloudimg.tencent-cloud.cn/raw/79a02a3d039ae6bfe40144e2d90b0d44.png)
3. Select **FairPlay Streaming Certificate** and click **Continue**.
![](https://qcloudimg.tencent-cloud.cn/raw/fef15cd65ddf3c21752c3b71c37b9b04.png)
4. Click **Choose File**, select the `certreq.csr` file created, and click **Continue**.
![](https://qcloudimg.tencent-cloud.cn/raw/d179f0554b61453a51e2a6efa83338e9.png)
5. Copy and save the ASK, paste it in the input field below, and click **Continue**.
![](https://qcloudimg.tencent-cloud.cn/raw/3a69ea9e79824df5d39213373830c8a2.png)
6. A window will pop up to confirm that you have saved the ASK. Click **Generate**.
![](https://qcloudimg.tencent-cloud.cn/raw/1a9471e089b5224e393b8efecd5a77c7.png)
7. After the above steps are completed, the FPS certificate generated will appear in the certificate list.
![](https://qcloudimg.tencent-cloud.cn/raw/0a0a4fa58cb43e811b21f34bfa91823e.png)
8. Click **Download** to download the FPS certificate (`fairplay.cer`).
![](https://qcloudimg.tencent-cloud.cn/raw/dcc1be70e6c01658348920c8856ec6c2.png)

[](id:step4)
### Step 4. Upload the certificate to SDMC’s platform
1. Log in to [SDMC’s DRM console](https://www.xmediacloud.com/contact-us/) and find DRM settings in the menu.
![](https://qcloudimg.tencent-cloud.cn/raw/3147f0f1b675351dfdde217fc5449ceb.png)
2. On the DRM settings page, find **FPS Cert Registration**, and click **Update**.
![](https://qcloudimg.tencent-cloud.cn/raw/b6e7c92bab1dc0c7efa7b8bbfc179303.png)
3. Upload the FPS certificate, private key file, private key password file, and ASK file, and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/c318449d607d21ed74d2aaaa89119f9e.png)
