## Creating a SAML IdP

You can create an IdP through the CAM console or APIs.

### Creating in the console

1. To create a SAML IdP, you need to first retrieve a federation metadata document from the IdP. This metadata document includes the issuer's name and keys that can be used to validate the SAML assertions that are received from the IdP.
>?Metadata documents are in XML format and are encoded in UTF-8 format without a byte order mark (BOM). A document can be up to 40 KB in size. If its size exceeds the limit, you can manually modify the metadata document as long as the elements mentioned above are retained.
>
2. Log in to the CAM console, select **[IdPs > Role SSO](https://console.cloud.tencent.com/cam/idp)** and click **Create IdP**.
3. On the **Create IdP** page, select SAML for **IdP Type**, configure the IdP information, and click **Next**.
	- IdP Name: Enter an IdP name.
	- Remarks: Enter the IdP remarks.
	- Metadata File: Upload the SAML metadata file downloaded in step 1 to **Metadata File**. The file will be successfully uploaded once its validity is verified.
	![](https://qcloudimg.tencent-cloud.cn/raw/ca3156e9ba7725ef99657cb97ea124a4.png)
4. Double check the IdP information and click **Complete**.

### Creating through APIs

To create an IdP and upload the metadata file, call the [CreateSAMLProvider](https://intl.cloud.tencent.com/document/product/598/32237) API.
