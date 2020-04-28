# macOS Push Certificate Description


## Operation Scenarios

macOS push certificates include push certificate for the development environment and push certificate for the release environment.
According to this tutorial, create a push certificate for the development environment and a push certificate for the release environment.



## Directions
#### Generating certificate


1. On your computer, open the Keychain Access tool and select **Request a Certificate From a Certificate Authority**.

![](https://main.qcloudimg.com/raw/17152ed67a1673af899b14d751f7084c.png)


2. Enter your email address, leave other fields empty, and click **Continue** to save the certificate locally.

![](https://main.qcloudimg.com/raw/3f7cd266e952c0cac893424b78e5e668.png)

3. Log in to the Apple Developer website and click **Certificates, Identifiers & Profiles**.

![](https://main.qcloudimg.com/raw/a96a6c0eba20dde46fbda6f50fc88e4e.png)



4. Select the application that needs a message push certificate and check the message push service.

![](https://main.qcloudimg.com/raw/bf9a68373369833ecd7ccbc3a5936b75.png)




Create a message push certificate

The following is a demonstration of creating a push certificate for the development environment. The steps for creating a certificate for the release environment are basically the same.

Go to the **Certificate** column and click "Add".
![](https://main.qcloudimg.com/raw/edc4fa4eb3cb962095015bf8b2ff0784.png)

Here, create a push certificate for the development environment as an example.
 ![](https://main.qcloudimg.com/raw/712e3aa08ed2e807bd1522ca8bda92e0.png)


Then, select the message push certificate request file created in step 2, upload it, and click ```Continue```.

![](https://main.qcloudimg.com/raw/0f7d66730a4b2a1e10f066522b3f2a74.png)



Finally, download the generated message push certificate to the local system.
![](https://main.qcloudimg.com/raw/c1101776b6044d6ba53b3e5b37fe3c69.png)



Step 4. Install the certificate

Double-click the certificate downloaded in the previous step to automatically install the certificate to the Keychain application.



Step 5. Export the certificate



Open Keychain Access, select the message push certificate to be exported and right-click it. The export format is P12, then set the password.
![](https://main.qcloudimg.com/raw/30a6544222eec5408e554c743348b47a.png)



## Uploading Certificate

Step 1. [Log in to the console](https://console.cloud.tencent.com/tpns/applist)

Step 2. In the **Application List**, select the application that needs to have the push certificate uploaded

Step 3. On the **Application Configuration** page, upload the push certificate

