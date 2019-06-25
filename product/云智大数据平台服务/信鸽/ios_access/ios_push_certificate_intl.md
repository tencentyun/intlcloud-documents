## Message Push Certificate Overview
This section describes how to generate iOS message push certificates required by TPNS.
iOS push certificates include push certificates for the development environment and push certificates for the release environment.
You can create push certificate for the development environment and push certificate for the release environment using this tutorial.



## APNs Push Certificate Request

Step 1: Make a message push certificate request file

First, open the ```Keychain Access``` tool.
![](https://main.qcloudimg.com/raw/0084fcd3bcefac6d913f9b2f8242c8d1.jpg)



 Then, select ```Request a Certificate From a Certificate Authority```.
 ![](https://main.qcloudimg.com/raw/b7359b42f2919282e72f2287ac3ee668.jpg)

Finally, enter your email address, leave the rest fields blank, and save the certificate locally.

![](https://main.qcloudimg.com/raw/ab4e0f93ea49a8cc8ee46c4748626fe2.jpg)

Step 2: Configure the app to make it able to push

First, log in to the Apple Developer website and click ```Certificates, Identifiers & Profiles```.

![](https://main.qcloudimg.com/raw/b8b71902bb88a0170f84710ca1814ec9.jpg)



Then, select the app for which to create a message push certificate, and select the message push service.

![](https://main.qcloudimg.com/raw/1924b78496bfb9b85b46a9e6b18aad7b.jpg)



The following is a demonstration of creating a push certificate for the **development environment**. **The steps for creating a certificate for the release environment are basically the same.**

Step 3: Create a message push certificate



First, click ```Create Certificate```.

 ![](https://main.qcloudimg.com/raw/f927871edffba2a7234307f2fe03afef.png)
 ![](https://main.qcloudimg.com/raw/1d4f7a396d7af40d3ffe799ad2466678.jpg)



Then, select the message push certificate request file created in step 1, upload it, and click ```Generate```.

![](https://main.qcloudimg.com/raw/36b6aa8950e02345dc319038ed59eb29.jpg)



Finally, download the generated message push certificate to the local system.
![](https://main.qcloudimg.com/raw/4365f83487523f535406ea1346e55586.jpg)



Step 4: Install the certificate.

Double-click the certificate downloaded in the previous step to automatically install the certificate to the Keychain application.



Step 5: Export the certificate



Open Keychain Access, select the message push certificate to be exported, right-click it and select Export Certificate. The format of the export is P12. Then, set the password.
![](https://main.qcloudimg.com/raw/d123733dae13b05709844b3161307e24.jpg)



## Making a Certificate in the TPNS-specific Format

TPNS currently only support push certificates in PEM format. You need to convert the push certificate in P12 format exported in the steps above to PEM format.

Here are two ways to do so:

### Automatic Generation

First, download the [TPNS testing tool](http://ixg.qq.com/pigeon_v2/resource/sdk/XGPushTool.zip).

Second, open the app, select the APNs server, upload the P12 push certificate file, enter the password (required), and click ```Push```. The tool will then generate the PEM file for TPNS in the same directory.



### Manual Generation

```javascript
openssl pkcs12 -in CertificateName.p12 -out CertificateName.pem -nodes
```


## Uploading a Certificate

Step 1: Log in to the [TPNS console](http://ixg.qq.com).

Step 2: Select the app for which to upload the push certificate in **App list**.

Step 3: Upload the push certificate corresponding to the environment on the **App configuration** page.
