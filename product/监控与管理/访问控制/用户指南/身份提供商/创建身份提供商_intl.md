## Creating SAML IdP

You can create an (identity provider) IdP via either CAM console or CAM API.

### Create via console

1. To create an SAML IdP, you need to obtain a federation metadata document from the IdP. The metadata document includes the issuer's name and the keys used to verify the SAML assertions received from the IdP.
> The metadata document must be in UTF-8-encoded XML format without a byte order mark (BOM). The document size is limited to 64 KB. If this upper limit is exceeded, you can manually modify the metadata document to retain only the elements mentioned above.
2. Log in to the CAM console, go to the [Identity Provider](https://console.cloud.tencent.com/cam/idp) page, and click **Create Provider**.
3. The provider type supported by default is SAML. Enter a name in the **Provider Name** box, and enter remarks on the provider in the **Notes** box.
4. You need to upload the SAML metadata document downloaded in Step 1 in **Metadata Document**. The metadata document can be uploaded if it is verified successfully.
5. Confirm the IdP information and click **Done**.

### Create via API

Create an IdP and upload the metadata document.
- Call [CreateSAMLProvider](https://cloud.tencent.com/document/product/598/30295).

