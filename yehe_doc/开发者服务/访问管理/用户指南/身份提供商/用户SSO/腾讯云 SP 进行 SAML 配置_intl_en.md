To make sure that a user in your IdP can log in to Tencent Cloud (the SP) via user-based SSO, you need to configure SAML for the IdP in Tencent Cloud to make Tencent Cloud trust your IdP.



### **Configuration process**

1. Log in to the CAM console by using a Tencent Cloud account.
2. On the left sidebar, click **Identity Providers** > **User-Based SSO**.
3. On the user-based SSO management page, you can view the user-based SSO status and the configuration information.
![](https://main.qcloudimg.com/raw/51539b5c18dc5100a8e492f6df96100a.png)
4. You can enable or disable user-based SSO by clicking on the button next to it.
   1. When user-based SSO is enabled: CAM sub-users cannot log in to Tencent Cloud via account ID and password. All CAM sub-users will be redirected to the IdP user login page for identity verification.
   2. When user-based SSO is disabled: CAM users can login to Tencent Cloud via account ID and password, and the user-based SSO settings will not take effect.
5. Click **Select File** to upload the metadata file provided by your IdP. If you want to upload another file to replace the uploaded one, click **Upload Again**.

>? 
>1. The metadata file (usually in XML format) is provided by your IdP. It contains the login URL and X.509 public key certificate that is used to verify the validity of the SAML assertion issued by the IdP.
>2. If your IdP only provides the access address of the metadata, you can copy the address to the browser to open it. Then you can save the metadata as an XML file and upload it.
