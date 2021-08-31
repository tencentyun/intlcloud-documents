
This document describes how to generate and upload an iOS message push certificate.

>?TPNS recommends you use .p12 certificates to manage the push services of your applications separately. Although a .p8 certificate is valid longer than a .p12 certificate, it has a wider push permission and scope. If leaked, it may cause more severe consequences.

## Step 1. Activate the remote push service for your application
1. Log in to the [Apple Developer](https://developer.apple.com/account/) website and click **Certificates, Identifiers & Profiles** in the right pane or **Certificates, IDS & Profiles** in the left sidebar to access the **Certificates, IDS & Profiles** page.
![](https://main.qcloudimg.com/raw/71c3b2db72e1bdcb55c0a68bae15e546.jpg)
2. Click **+** on the right of Identifiers.
![](https://main.qcloudimg.com/raw/185cbd57e0a1a206d1e97e9f59c9cec5.jpg)
3. Register an AppID by following the steps below. You can also enable `Push Notification Service` using your existing AppID. Note that your `Bundle ID` cannot contain the wildcard `*`; otherwise, you will be unable to use the remote push service.
 1. Check **App IDs** and click **Continue**.
![](https://main.qcloudimg.com/raw/1e047d154a30d4dc95e3d9fa52779a37.jpg)
 2. Select **App** and click **Continue**.
![](https://main.qcloudimg.com/raw/584b1b697c21832d864a75c541da7fde.jpg)
 2. Configure `Bundle ID` and other information. Click **Continue**.
![](https://main.qcloudimg.com/raw/234c0d498689a1231fe0d00eb444702a.jpg)
 4. Check **Push Notifications** to activate the remote push service.
![](https://main.qcloudimg.com/raw/4720490316ac5180de0742ca1ed50c8f.jpg)

## Step 2. Generate and upload a .p12 certificate
1. Select your AppID and click **Configure**.
![](https://main.qcloudimg.com/raw/ef9be51df8bb1c5d56febd10d8deb2a2.jpg)
2. In the **Apple Push Notification service SSL Certificates**, you will see two SSL certificates: **Development SSL Certificate** and **Production SSL Certificate**.
![](https://main.qcloudimg.com/raw/bd55cffb96e80b505e70db33c73e27dd.jpg)
3. <span id="step3"></span>Click **Create Certificate** under **Development SSL Certificate** to create a certificate. You will be prompted that `Certificate Signing Request (CSR)` is required.
![](https://main.qcloudimg.com/raw/637ce37ec54ca5a4bf3006b527572da5.jpg)
4. Open **Keychain Access** on macOS. Select **Keychain Access** > **Certificate Assistant** > **Request a Certificate From a Certificate Authority**.
![](https://main.qcloudimg.com/raw/39ae2c71f2e288d4ca922e079198229b.png)
5. Enter your email for **User Email Address** and your name or company name for **Common Name**. Select **Saved to disk** and click **Continue**. Then the system will generate a `*.certSigningRequest` file.
![](https://main.qcloudimg.com/raw/2fcabb9a7d06f3b3aa16e8f5da156bb7.png)
6. Return to the `Apple Developer` page as shown in [step 3](#step3) and click **Choose File** to upload the `*.certSigningRequest` file.
![](https://main.qcloudimg.com/raw/59dfdb08864d6469199684c50c53b7e6.jpg)
7. Click **Continue** to generate the push certificate.
![](https://main.qcloudimg.com/raw/c337d5282ac10f6bec7c5ef5864b94cb.jpg)
8. Click **Download** to save the `Development SSL Certificate` locally.
![](https://main.qcloudimg.com/raw/9dece7f318c93e97732fe7ea7806f961.jpg)
9. Repeat the steps 1–8 to generate and download the `Production SSL Certificate`.
>? Actually, this certificate is a `Sandbox` and `Production` merged certificate that applies to both the development and production environments.
![](https://main.qcloudimg.com/raw/eaa08da45f36435155a4a37938ddc84e.jpg)
![](https://main.qcloudimg.com/raw/bf80c3a06f74080bf81fd857f15a2b86.jpg)
9. Double-click and open the `Development SSL Certificate` and `Production SSL Certificate` that have been download to import them to Keychain Access.
10. Open Keychain Access, select **Login** > **My Certificates**, and right-click to export the .p12 files for `Apple Development IOS Push Service: com.tpnssdk.pushdemo` and `Apple Push Services: com.tpnssdk.pushdemo` respectively.

>!Do set the password when saving the .p12 file.


## Step 3. Upload certificates to the TPNS Console
1. Log in to the [TPNS Console](https://console.cloud.tencent.com/tpns) and select **Product Management** > **Configuration Management**.

2. Click **Upload Certificate** in the **Push Certificate** pane to upload the Development SSL Certificate and Production SSL Certificate.

3. Enter the certificate password and click **Click to select**.

4. Choose your certificate and click **Upload**.

