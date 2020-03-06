
## Generating a CSR File

Follow these steps to generate a Certificate Signing Request (CSR).
 <img src="//main.qcloudimg.com/raw/76c59ee727f1147693f6da95bc1db070.png" width=640 />
 
Specify the email address (of the paid account for applying for an AppID) and common name (the name of your computer by default, which does not need to be changed). Then, select "Save to disk".
 <img src="//main.qcloudimg.com/raw/12c80d3cb45d44e6b9fb8f63bc616347.png" width=640 />
 
Click "Continue".
 <img src="//main.qcloudimg.com/raw/b393d5662e94646b24aa14979c17b3c3.png" width=640 />
 
 The CSR file TXIMDemoAPS.certSigningRequest is created locally.

## Creating an App ID

Log in to developer.apple.com and click "Member Center".
<img src="//main.qcloudimg.com/raw/d39160bb0713cd67fd78377328c3928a.png" width=640 />

On the page that appears, select "Certificates, Identifiers & Profiles".
<img src="//main.qcloudimg.com/raw/4f6fb2c58856d47a3fdce33d0b446bc1.png" width=640 />

Select "Identifiers" to go to the identifier management page.
<img src="//main.qcloudimg.com/raw/bfbe4ef16748542215a203268395638f.png" width=640 />

Generate an app ID as follows:
Click "App IDs" under "Identifiers", and a list of app IDs appears on the right. Skip to step 3 if you have already configured your app. Otherwise, click "+" to add an app ID.
<img src="//main.qcloudimg.com/raw/8c18cf7548705e9557f77fb76637a465.png" width=640 />

For "App ID Description", you can enter your project name. For "Bundle ID", which can be found under the "General" tab of your project, it is usually in com.youcompany.youprojname format. Select the checkbox for "Push Notifications" and click "Continue".
<img src="//main.qcloudimg.com/raw/dca8a2cda77581eeeda92882fce90119.png" width=640 />

Click "Submit".
<img src="//main.qcloudimg.com/raw/b24c07c8ad8f70e4aa0eb878a8d8dfeb.png" width=640 />

## Creating an APS Certificate for the App

Return to "App IDs", select the app that needs push notifications, and then click "Edit".
<img src="//main.qcloudimg.com/raw/11b2213530dc164d45f2da2293cce07f.png" width=640 />

Scroll down to "Push Notifications" and click "Create Certificate…" to create a push certificate. **Development certificates and production certificates need to be created separately, which means you need to go through the same process twice.**
<img src="//main.qcloudimg.com/raw/257aa0f4d8ebcb3ff3e2bb5f327a5edd.png" width=640 />

Click "Continue".
<img src="//main.qcloudimg.com/raw/359899fa7fead219335499a42ca01a82.png" width=640 />

Upload the CSR file "xxx.certSigningRequest" created in section 1 (TXIMDemoAPS.certSigningRequest in this example) and click "Generate".
<img src="//main.qcloudimg.com/raw/5ce5ec899e22ee7361efdd3b052d70a6.png" width=640 />

Now, you have finished creating the APS certificates. Click "Download" to save them locally (the development certificate is aps_development.cer, and the production certificate is aps.cer.)
<img src="//main.qcloudimg.com/raw/8949831833544f35b1eb8c749b420edf.png" width=640 />

Click "Done". The push state of this environment becomes "Enabled".
<img src="//main.qcloudimg.com/raw/67910c40b8e8b84ba81bd6f84fe16a58.jpg" width=640 />

Note: the "Apple Push Notification service" column for some app IDs is grayed out and the "Configure" button is unavailable. This is because APNS does not support app IDs that contain wildcards.

## Generating a Push Certificate

Import the certificate
Double-click the downloaded files in the previous section (aps_development.cer and aps.ce) to install them on your computer. In "Keychain Access", you can find the imported certificates.
<img src="//main.qcloudimg.com/raw/51b99080f9f479319ee6d742aedd3a3a.png" width=640 />

Right-click the certificate and export it as a .p12 file. For example, save the certificate as TXIMDemoAPS.p12.
<img src="//main.qcloudimg.com/raw/af2ead9db94586c2e18bf2b59b2151ec.png" width=640 />

Note: development certificates are valid only for development in debug mode. Always use distribution certificates for production release.

## Generating a Provisioning Profile (PP)
This section describes how to create a development provisioning profile. You can create a distribution provisioning profile by following the same process. First, click "Continue".
<img src="//main.qcloudimg.com/raw/6c4eff074f24e0ae1b3bb73dda9dea26.png" width=640 />

Select the App ID for which the push certificate was created in Step 3.3 and click "Continue".
<img src="//main.qcloudimg.com/raw/ec5fd56e7269a9f75299e636dd644d58.png" width=640 />

Select the development certificate generated in Step 3.3 (or the distribution certificate in Step 3.3 when creating a distribution provisioning profile) and click "Continue".
<img src="//main.qcloudimg.com/raw/12e2e9dd0820f4e7e7f5ee4f9580fb02.png" width=640 />

Select the devices to be included into the testing of the app (distribution certificates do not require this step) and click "Continue".
<img src="//main.qcloudimg.com/raw/10742a7703b04984bf94a1386a9642c9.png" width=640 />

Enter the name of the PP, which is IMDevPP in this example.
<img src="//main.qcloudimg.com/raw/405ac56131c2c38d4f98cda13c5327e2.png" width=640 />

The PP is generated successfully.
<img src="//main.qcloudimg.com/raw/e21aca45d642de8050605073e9f3a942.png" width=640 />


Note: in all the preceding steps, no certificates, except the generated p12 certificate, need to be downloaded and installed locally.

Check the generated PP.
Verify that the state of the PP is "Active".
<img src="//main.qcloudimg.com/raw/fe957f8e017d22e4e4812eea046e5e45.png" width=640 />

Click the PP to go to the details page and verify that its state is "Active".
<img src="//main.qcloudimg.com/raw/20ec87d3caac9cb8d0119762e0d53da5.png" width=640 />

## Configuration in Xcode
The latest version of Xcode does not require the manual configuration of certificates and provisioning profiles. Instead, you only need to select the correct team in "General" and click "Fix Issue". This is why you do not need to download and install the generated certificates locally, as mentioned previously.
<img src="//main.qcloudimg.com/raw/22db4c59af9d26d562f916e87e10fbc2.png" width=640 />
