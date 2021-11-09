## Overview
Tencent Cloud is the service provider (SP) and the enterprise is the identity provider (IdP) when they collaborate to implement user-based single sign-on (SSO). The user-based SSO allows an enterprise employee to access Tencent Cloud resources as a CAM sub-user.

## Directions
### Configuration process
Before implementing user-based SSO, you must establish trust between Tencent Cloud and your IdP by configuring Security Assertion Markup Language (SAML) on both sides.

1. Configure your IdP to Tencent Cloud.
	- Purpose: to establish Tencent Cloud's trust in your IdP.
	- Steps: please see [Configuring SAML in Tencent Cloud](https://intl.cloud.tencent.com/document/product/598/42366).
 
2. Configure Tencent Cloud as a trusted SP in your IdP and configure the SAML assertion attributes.
	- Purpose: to establish your IdP's trust in Tencent Cloud.
	- Steps: please see [Configuring SAML in IdP](https://intl.cloud.tencent.com/document/product/598/42367).
 
3. Log in to the [CAM console](https://console.cloud.tencent.com/cam) or call an API to create a CAM sub-user with the same name as that in the IdP.
	- Purpose: to use sub-users for subsequent logins.
	- Steps: please see [Creating Sub-user](https://intl.cloud.tencent.com/document/product/598/13674).
 
 


### Login and verification process
After user-based SSO is configured, the enterprise employee (for example, "user1") in IdP can log in to Tencent Cloud console and access the resources he or she has permission to access with the steps below:
1. "user1" initiates user-based SSO login on the sub-user login page.
2. Tencent Cloud returns an SAML assertion authentication request to the browser.
3. The browser forwards the SAML authentication request to the IdP.
4. The IdP authenticates user1 and returns the generated SAML response to the browser after the authentication is passed.
5. The browser forwards the SAML response to Tencent Cloud.
6. Tencent Cloud verifies the authenticity and integrity of the SAML assertion based on the SAML mutual trust configuration and then maps the value of the `NameID` element in the SAML assertion to the CAM sub-user.
7. After successful verification and mapping, Tencent Cloud returns the URL of Tencent Cloud console to the browser, and user1 can log in to the console successfully.

