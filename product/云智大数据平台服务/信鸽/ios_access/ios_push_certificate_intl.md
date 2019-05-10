# Notes on iOS Push Certificate


## Message Push Certificate Overview
This section describes how to generate iOS message push certificates required by TPNS.
iOS push certificates include push certificates for the development environment and push certificates for the release environment.
You can create push certificate for the development environment and push certificate for the release environment using this tutorial.



## APNs Push Certificate Request

Step 1: Make a message push certificate request file

First, open the ```Keychain Access``` tool.
![](/assets/iOSCert/1.jpg)



 Then, select ```Request a Certificate From a Certificate Authority```.
 ![](/assets/iOSCert/2.jpg)

Finally, enter your email address, leave the rest fields blank, and save the certificate locally.

![](/assets/iOSCert/3.jpg)

Step 2: Configure the app to make it able to push

First, log in to the Apple Developer website and click ```Certificates, Identifiers & Profiles```.

![](/assets/iOSCert/4.jpg)



Then, select the app for which to create a message push certificate, and select the message push service.

![](/assets/iOSCert/5.jpg)



The following is a demonstration of creating a push certificate for the **development environment**. **The steps for creating a certificate for the release environment are basically the same.**

Step 3: Create a message push certificate



First, click ```Create Certificate```.

 ![](/assets/iOSCert/6.jpg)
 ![](/assets/iOSCert/7.jpg)



Then, select the message push certificate request file created in step 1, upload it, and click ```Generate```.

![](/assets/iOSCert/8.jpg)



Finally, download the generated message push certificate to the local system.
![](/assets/iOSCert/9.jpg)



Step 4: Install the certificate.

Double-click the certificate downloaded in the previous step to automatically install the certificate to the Keychain application.



Step 5: Export the certificate



Open Keychain Access, select the message push certificate to be exported, right-click it and select Export Certificate. The format of the export is P12. Then, set the password.
![](/assets/iOSCert/10.jpg)



## Making a Certificate in the TPNS-specific Format

TPNS currently only support push certificates in PEM format. You need to convert the push certificate in P12 format exported in the steps above to PEM format.

Here are two ways to do so:

### Automatic Generation

First, download the [TPNS testing tool](http://xg.qq.com/pigeon_v2/resource/sdk/XGPushTool.zip).

Second, open the app, select the APNs server, upload the P12 push certificate file, enter the password (required), and click ```Push```. The tool will then generate the PEM file for TPNS in the same directory.



### Manual Generation

```javascript
openssl pkcs12 -in CertificateName.p12 -out CertificateName.pem -nodes
```


## Uploading a Certificate

Step 1: Log in to the [TPNS console](http://xg.qq.com).

Step 2: Select the app for which to upload the push certificate in **App list**.

Step 3: Upload the push certificate corresponding to the environment on the **App configuration** page.
