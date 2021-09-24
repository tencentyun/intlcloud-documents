If Tencent Cloud and an enterprise work together to implement user-based single sign-on (SSO), Tencent Cloud is the service provider (SP) and the enterprise is the identity provider (IdP). User-Based SSO allows an employee of the enterprise to access Tencent Cloud resources as a Cloud Access Management (CAM) sub-user.



### **Configuration process**

Before implementing user-based SSO, you must establish trust between Tencent Cloud and your IdP by configuring Security Assertion Markup Language (SAML) for both sides.

1. To make sure that your IdP is trusted by Tencent Cloud, you need to configure the IdP in Tencent Cloud Console. For more information, see **[Configuring SAML in Tencent Cloud](https://intl.cloud.tencent.com/document/product/598/42366)**.
2. To make sure that Tencent Cloud is trusted by your IdP, you need to configure Tencent Cloud as a trusted SP and configure SAML assertions in your IdP. For more information, see **[Configuring SAML in IdP](https://intl.cloud.tencent.com/document/product/598/42367)**.
3. After the SAML configurations for Tencent Cloud (i.e. the SP) and the IdP are completed, you need to create a CAM sub-user that completely matches the user in your IdP by logging in to the CAM console or calling APIs. For details, see [Creating Sub-user](https://intl.cloud.tencent.com/document/product/598/13674).



### **Login and verification process**

After user-based SSO is configured, the enterprise employee (for example, “user1”) in IdP can log in to Tencent Cloud Console and access the resources he or she has permission to access with the steps below:

1. user1 initiates user-based SSO on the Tencent Cloud [CAM user sign in](https://intl.cloud.tencent.com/login/subAccount?s_url=https%3A%2F%2Fintl.cloud.tencent.com) page.
2. Tencent Cloud returns an SAML assertion authentication request to the browser.
3. The browser forwards the SAML authentication request to the IdP.
4. The IdP authenticates user1 and returns the generated SAML response to the browser after the authentication is passed.
5. The browser forwards the SAML response to Tencent Cloud.
6. Tencent Cloud verifies the authenticity and integrity of the SAML assertion based on the SAML mutual trust configuration and then maps the value of the **NameID** element in the SAML assertion to the CAM sub-user.
7. After successful verification and mapping, Tencent Cloud returns the URL of Tencent Cloud Console to the browser, and user1 can log in to the console successfully.
