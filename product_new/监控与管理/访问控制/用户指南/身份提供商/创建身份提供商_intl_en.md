## Creating a SAML IdP

You can create an identity provider (IdP) through the CAM Console or the CAM APIs.

### Creating via the console

1. To create a SAML IdP, you need to first retrieve a federation metadata document from the IdP. This metadata document includes the issuer’s name and keys that can be used to validate the SAML assertions that are received from the IdP.
> Metadata documents are in XML format and are encoded in UTF-8 format without a byte order mark (BOM). The upper limit on the domument size is 40 KB. If its size exceeds the limit, you can manually modify the metadata document as long as the elements mentioned above are retained.
2. Log in to the CAM console, go to the [Identity Providers](https://console.cloud.tencent.com/cam/idp) page, and click **Create Provider**.
3. Currently the default provider type is SAML. Enter a name in the **Provider Name** box. You may leave some description about the provider in the **Notes** box.
4. Upload the SAML metadata document retrieved in Step 1 to **Metadata Document**. The document will be successfully uploaded once its validity is verified.
5. Double check the IdP information and click **Done**.

### Creating using the API

Create an IdP and upload the metadata document.
- Call: [CreateSAMLProvider](https://intl.cloud.tencent.com/document/product/598/32237).
