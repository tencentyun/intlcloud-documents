Image signing and signature verification can avoid man-in-the-middle attacks and the update and running of invalid images, ensuring image consistency across the entire linkage ranging from distribution to deployment. TCR Enterprise supports namespace-level automatic image signing. When an image is pushed to the repository, it will be automatically signed according to the matched signing policy to ensure image content trustworthiness in your repository.

## Prerequisites

Before using the image signing feature, you need to perform the following operations:
- [Create a TCR Enterprise Instance](https://intl.cloud.tencent.com/document/product/1051/35486).

- If you are using a sub-account, you must have granted the sub-account operation permissions for the corresponding instance. For more information, see [Example of Authorization Solution of TCR Enterprise](https://intl.cloud.tencent.com/document/product/1051/37248).

- [Key Management Service (KMS)](https://intl.cloud.tencent.com/document/product/1030/32774) has been activated.


## Directions

### Creating an asymmetric signature verification key
1. Log in to the [KMS console](https://console.cloud.tencent.com/kms2).

2. Choose **Key Management** > **Customer Managed CMK** and click **Create**.

3. In the **Create Key** window that pops up, set key parameters and click **OK**. The container signature feature requires that the KMS key usage be set to **Asymmetric Signature Verification** and the encryption algorithm be set to **RSA_2048**. For the settings of the other parameters, see [Creating a Key](https://intl.cloud.tencent.com/document/product/1030/31971).
   

   > ?
   > TCR supports obtaining user keys in all regions of the KMS service. To reduce the cross-region communication overhead, it is recommended that the KMS user key and the image repository instance be located in the same region.

### Authorizing TCR to use the KMS key

To enable TCR to read the asymmetric signature verification key under your account, you need to configure a policy as follows under your account:
1. Log in to the [CAM console](https://console.cloud.tencent.com/cam/overview).

2. On the **Role** page, click **TCR_QCSRole**.

3. On the TCR_QCSRole details page, associate the preset policy **QcloudKMSFullAccess**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/4Rrt689_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230106162915.png)


### Creating an image signing policy
1. Log in to the [TCR console](https://console.cloud.tencent.com/tcr).

2. On the instance management page, select a target image repository instance.

3. Select **Image Security** in the left sidebar to go to the image signing details page.

4. Click **Create**. In the signing policy creation window that pops up, set parameters as instructed. 

 - **Policy Name**: Image signing policy name. The value must be 2 to 50 characters in length and can contain only lowercase letters, numbers, and separators, including periods (.), underscores (_), hyphens (-), and slashes (/). It can neither start or end with a separator nor contain consecutive separators.
   
 - **Namespace**: Namespace where the image signing policy takes effect. Only one signing policy is supported per namespace.
   
 - **KMS Key**: KMS customer managed CMK that supports signing. Only a key that is used for RSA2048 asymmetric key verification can be loaded.
   
 - **Domain Name**: Domain name used to access the repository instance service.
   
5. Click **OK**.
   

   > ?
   >- Once created, the signing policy takes effect for new images immediately. That is, when an image is pushed to the repository, it will be automatically signed according to the matched signing policy.
   >- An enabled signing policy does not take effect for images that already exist in the repository. For existing images, you need to manually trigger signing on the **Image Repository** > **Tag Management** page in the console.


### Viewing image signing status
- You can check whether the signing policy is enabled on the **Namespace** page.

- You can check whether the signing policy is enabled for images on the **Image Repository** > **Tag Management** page. For images that have been pushed to the image repository before the signing policy is enabled, you can manually trigger signing in the **Operation** column.


### Deleting an image signing policy

On the **Image Signature** page, select the signing policy to delete and click **Delete**. In the window that pops up, click **OK**.

> ?
> Deleting the signing policy will also delete the image signing information in the existing namespace, which may cause signature verification failure.

