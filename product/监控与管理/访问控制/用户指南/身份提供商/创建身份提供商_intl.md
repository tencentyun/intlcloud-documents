## Creating SAML IdP

You can create an (identity provider) IdP via either CAM console or CAM API.

### Create via console

1. To create an SAML IdP, you need to obtain a federation metadata document from the IdP. The metadata document includes the issuer's name and the keys used to verify the SAML assertions sent by the IdP.
> Metadata documents are XML formatted and UTF-8 encoded without byte order mark (BOM). The document size limit is 64K. If the document size exceeds the limit, you can manually modify the metadata document, keeping only the elements mentioned above.
2. Log in to the CAM console, go to [Identity Provider](https://intl.cloud.tencent.com/login.tencent.com/cam/idp), and click **Create Provider**.
3. The supported provider type by default is SAML. Enter a name in the **Provider Name** box, and enter remarks on the provider in the **Notes** box.
4. You need to upload the SAML metadata document downloaded in Step 1 in **Metadata Document**. You can upload the metadata document once it is successfully verified.
5. Confirm the IdP information and click **Done**.

### Create via API

Create an IdP and upload the metadata document.
- Call [CreateSAMLProvider](https://intl.cloud.tencent.com/document/product/598/30295).

