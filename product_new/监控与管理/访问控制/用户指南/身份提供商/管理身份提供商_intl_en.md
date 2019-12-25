## Deleting SAML IdP

You can manage your IdPs via either CAM console or CAM API.

### Deleting via console
1. Log in to the CAM console, and go to [Identity Providers](https://console.cloud.tencent.com/cam/idp).
2. Select the IdP you want to delete from the list and click **Delete** in the **Operation** column.
3.3. Confirm that you are deleting the right IdP, click **OK**.

### Deleting via API

- (Optional) To list all IdP information in pages, call [ListSAMLProviders](https://intl.cloud.tencent.com/document/product/598/32234).
- (Optional) To get the details of a specific IdP, call [GetSAMLProvider](https://intl.cloud.tencent.com/document/product/598/32235).
- To delete a SAML IdP, call [DeleteSAMLProvider](https://intl.cloud.tencent.com/document/product/598/32236).

## Modifying SAML IdP

You can modify an IdP via either CAM console or CAM API.

### Modify via console
1. Log in to the CAM console, and go to [Identity Providers](https://console.cloud.tencent.com/cam/idp).
2. Select the IdP you want to modify from the list, and click the IdP name to enter the details page.
3. You can upload the metadata document to redefine the current IdP, or download the current metadata document.

### Modifying via API

Update the description or the metadata document of an SAML IdP.
- Call [UpdateSAMLProvider](https://intl.cloud.tencent.com/document/product/598/32233)
