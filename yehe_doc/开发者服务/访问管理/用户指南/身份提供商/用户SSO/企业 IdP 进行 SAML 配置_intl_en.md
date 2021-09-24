To make sure that a user in the enterprise’s identity system (your IdP) can log in to Tencent Cloud (the SP) via user-based SSO, you need to configure SAML for Tencent Cloud in IdP to make your IdP trust Tencent Cloud.



### **Configuration process**

1. Obtain the URL of SAML SP's metadata from Tencent Cloud.
    1. Log in to the CAM console by using a Tencent Cloud account.
    2. On the left sidebar, click **Identity Providers** > **User-Based SSO**.
    3. On the user-based SSO management page, you can view or copy the URL of the metadata provided by the current user’s SAML SP.
2. Create an SAML SP in your IdP and configure Tencent Cloud as the reliable SP by using the methods below according to the actual situation of your IdP:
    1. **If your IdP supports URL-based configuration:** copy the SAML SP metadata URL of Tencent Cloud in step 1 to your IdP.
    2. **If your IdP supports configuration based on the uploaded file:** copy the SAML SP metadata URL of Tencent Cloud in step 1 to the browser and open it, save the metadata as an XML file, and upload the file to your IdP.
    3. **If your IdP does not support the two methods above:** configure the parameters below in your IdP:
        1. `Entity ID`: the value of the `entityID` attribute in the `md:EntityDescriptor` element of the downloaded metadata file.
        2. `ACS URL`: the value of the `Location` attribute in the `md:AssertionConsumerService` element of the downloaded metadata file.
        3. `RelayState` (optional): if your IdP supports the `RelayState` parameter, set the value of the parameter to a URL to which users will be redirected after SSO succeeds. If you do not configure this parameter, users will be redirected to the homepage of Tencent Cloud Console after SSO succeeds.