## Operation Scenarios
This document describes how to generate and upload an iOS message push certificate.


## Directions
### Generating certificate
1. On your computer, open the Keychain Access tool and select **Request a Certificate From a Certificate Authority**.
![](https://main.qcloudimg.com/raw/39ae2c71f2e288d4ca922e079198229b.png)
2. Enter your email address, leave other fields empty, and click **Continue** to save the certificate locally.
![](https://main.qcloudimg.com/raw/2fcabb9a7d06f3b3aa16e8f5da156bb7.png)
3. Log in to the Apple Developer website and click **Certificates, Identifiers & Profiles**.
![](https://main.qcloudimg.com/raw/386427c16373937665aa2f73039b6530.png)
4. Select the application that needs a message push certificate and check the message push service.
![](https://main.qcloudimg.com/raw/3c9ca2d79481e46ed91ef6fff7c94ae2.png)
5. Click **Create Certificate**. Here, you need a certificate version that applies to both the development environment and the production environment.
![](https://main.qcloudimg.com/raw/d9095d18eed198fadfd91ffbc0b8767f.png)
6. Select the message push certificate request file created in step 2, upload it, and click **Continue**.
![](https://main.qcloudimg.com/raw/4432124268de16e50b4c9b37af48d5fd.png)
7. Download the generated message push certificate to the local system.
![](https://main.qcloudimg.com/raw/32e563cd779fc896ecd83ae896da6c9b.png)
8. Double-click the certificate downloaded in the previous step to automatically install the certificate to the Keychain application.
9 .Open Keychain Access, select the message push certificate to be exported, and right-click it. The export format is P12. Then, set the password.
![](https://main.qcloudimg.com/raw/1ef81b819d8c98d8f9d82dca45407416.png)



### Uploading certificate
1. Log in to the [TPNS Console](https://console.cloud.tencent.com/tpns) and select **Configuration Management** on the left sidebar.
2. Enter the configuration management page and select the application that needs to have the push certificate uploaded.
3. Enter the certificate password, click **Upload Certificate**, and select the certificate to complete the upload.






