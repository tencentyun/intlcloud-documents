# Notes on iOS push certificates


## Message push certificate overview
This guide describes how to generate iOS message push certificates required by TPNS.
iOS push certificates include push certificate for the development environment and push certificate for the release environment.
You can create push certificate for the development environment and push certificate for the release environment using this tutorial.



## APNs push certificate request

Step 1: Create a request file for message push certificate

First, open the ```Keychain Access``` tool.
![](https://main.qcloudimg.com/raw/a11ed45755c05b45d9c203fac7b11820.png)



 Then, select ```Request a Certificate From a Certificate Authority```.
 ![](https://main.qcloudimg.com/raw/5f1726f1e78b7b9cc512a4964dcbd1d9.png)

Finally, enter your email address, leave other fields blank, and save the certificate locally.

![](https://main.qcloudimg.com/raw/6f988ae446d4500e2843dc31aa5a4caf.png)

Step 2: Configure the app to enable it to push messages

First, log in to the Apple Developer website and click ```Certificates, Identifiers & Profiles```.

![](https://main.qcloudimg.com/raw/673951a14724416e2850718ee7ae3160.png)



Then, select the app that needs a message push certificate, and select the message push service.

![](https://main.qcloudimg.com/raw/1a08ca5cd0054873dc80cc03c9d3fd04.png)




Step 3: Create a message push certificate



First, click ```Create Certificate```. Here, we need a certificate version that applies to both the development environment and the production environment.

 ![](https://main.qcloudimg.com/raw/93cad1a9d1b22a47c7d4381035ab1390.png)


Then, select the message push certificate request file created in step 1, upload it, and click ```Generate```.

![](https://main.qcloudimg.com/raw/d494bdde10e37c3b3b3c2bf926bf4451.png)



Finally, download the generated message push certificate to the local system.
![](https://main.qcloudimg.com/raw/36c508ec62427edb06d0d171f87f5ac4.png)



Step 4: Install the certificate

Double-click the certificate downloaded in the previous step to automatically install the certificate to the Keychain application.



Step 5: Export the certificate



Open Keychain Access, select the message push certificate to be exported and right-click it. The export format is P12, then set the password.
![](https://main.qcloudimg.com/raw/c7eb856a4793e7e4a0297873ba0bc08e.png)



## Uploading a certificate

Step 1: [Log in to the console](https://console.cloud.tencent.com/tpns).

Step 2: In **App List**, select the app that needs to have the push certificate uploaded

Step 3: On **App Configuration** page, upload the push certificate

