# macOS Push Certificate Instructions


## Scenario

There are two types of macOS push certificates: push certificates for development environment and push certificates for production environment.
This tutorial will teach you how to create both types of push certificates. 



## Directions
#### Generating a Certificate


1. On your computer, open the Keychain Access tool and select **Request a Certificate From a Certificate Authority**.

![](https://main.qcloudimg.com/raw/17152ed67a1673af899b14d751f7084c.png)


2. Enter your email address, and leave the rest blank. Click **Continue** to save the certificate locally.

![](https://main.qcloudimg.com/raw/3f7cd266e952c0cac893424b78e5e668.png)

3. Log in to the Apple Developer Center website, and click **Certificates, Identifiers & Profiles**. ```Certificates, Identifiers & Profiles```

![](https://main.qcloudimg.com/raw/a96a6c0eba20dde46fbda6f50fc88e4e.png)



4. Select the application you want to create a push certificate for, and choose **Push Notifications**.

![](https://main.qcloudimg.com/raw/bf9a68373369833ecd7ccbc3a5936b75.png)




5. Create a Push Certificate

The following is a demonstration of how to create a push certificate for the development environment. You can use the same process to create push certificates for the product environment.

6. Enter the **Certificate** column, and click **Add**.
![](https://main.qcloudimg.com/raw/edc4fa4eb3cb962095015bf8b2ff0784.png)

7. Here we select the push certificate for the development environment.
 ![](https://main.qcloudimg.com/raw/712e3aa08ed2e807bd1522ca8bda92e0.png)


8. Then, we select the push certificate request file created in step 2. After it uploads, click ```Continue```.

![](https://main.qcloudimg.com/raw/0f7d66730a4b2a1e10f066522b3f2a74.png)



9. Finally, download the generated push certificate locally.
![](https://main.qcloudimg.com/raw/c1101776b6044d6ba53b3e5b37fe3c69.png)



10: Install the certificate

Double-click on the push certificate you downloaded in the previous step, and the push certificate will automatically be installed in the Keychain application.



11: Export the certificate



Open Keychain Access, and select the push certificate you want to export. Right-click the certificate and select **Export Certificate**. The certificate will be exported in P12 format. Set a password.
![](https://main.qcloudimg.com/raw/30a6544222eec5408e554c743348b47a.png)



## Uploading Certificates

Step 1: Log in to the [Console] (https://console.cloud.tencent.com/tpns/applist)

Step 2: In the **App List**, select the application to which you want to upload the push certificate.

Step 3: Upload the certificate in the **Application configuration** page to complete the process.

