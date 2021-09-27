### How do I get my secret ID and secret key from the SDK?

You can enter **API Key Management** in the [CAM console](https://console.cloud.tencent.com/cam/capi) to obtain your secret ID and secret key. **Please keep them private and avoid disclosure.**

### How do I create a Customer Master Key (CMK)?

You can create a CMK in the [**KMS Console**](https://intl.cloud.tencent.com/document/product/1030/31971), with [**TCCLI**](https://intl.cloud.tencent.com/document/product/1030/32783), or the [**CreateKey API**](https://intl.cloud.tencent.com/document/product/1030/32199).

### Is there a limit to the number of CMKs I can create?

Yes. Up to 200 CMKs can be created under each account in each region, excluding the ones scheduled for deletion and Tencent Cloud managed CMKs. If you need to create more CMKs, please [**submit a ticket**](https://console.cloud.tencent.com/workorder/category) or contact your Tencent Cloud sales rep.
	

### You can create a CMK with an external key material. What does "external" mean and what is BYOK?

- **External** refers to your own key material.
- **BYOK** gives you a full control of key material. You can create a CMK without key material and then import your own key material into the key to be an external CMK, which can be managed and distributed with KMS.
	

### How long does it take to effect after I modify the CMK alias or description information via API calls?

The changes will become effective immediately if the API call is successful.

### Is rotating a CMK supported? How to start rotation?

Yes. You can start rotation in the [**KMS Console**](https://intl.cloud.tencent.com/document/product/1030/31971), with [**TCCLI**](https://intl.cloud.tencent.com/document/product/1030/32783), or the [**EnableKeyRotation API**](https://intl.cloud.tencent.com/document/product/1030/32191).
>!CMKs not supported for rotation include:
> - Asymmetric CMKs 
> - CMKs made from external key materials 
> 

### Do I need to change my application after enabling rotation?

- Key rotation only changes the CMK’s key material. Its attributes (key ID, alias, description, permission) remain.
- After you enable key rotation, KMS will automatically rotate keys based on the specified rotation period (365 days by default). Each rotation will generate a new version of CMK. The rotated keys can be encrypted and decrypted as follows:
	- In encryption, KMS will automatically use the latest version of CMK.
	- In decryption, KMS will automatically use the CMK that is applied in encryption.

### How do I choose an encryption algorithm？

-  **Symmetric encryption**: Tencent Cloud KMS supports SM4 and AES algorithms, which will be automatically determined based on the region where a CMK is uploaded. For example, SM4 will be automatically used if you select **China**.
-  **Asymmetric encryption**: Tencent Cloud KMS supports RSA (size 2048-bit) and SM2, which will be automatically determined based on the region where a CMK is uploaded and the KeyUsage parameter.
>!To create a CMK using APIs, please check the [**encryption methods**](https://intl.cloud.tencent.com/document/product/1030/35177) available in the region of your choice.
