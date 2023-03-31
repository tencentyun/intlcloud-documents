You can select an image based on the following attributes:
- Location (see [Regions and Availability Zones](https://intl.cloud.tencent.com/document/product/213/6091))
- Operating system
- Architecture (32-bit or 64-bit)

Tencent Cloud provides three types of images, namely public images, custom images, and shared images.

## Public Images
**Public images** are images provided by Tencent Cloud. Each image contains an operating system and initialization components provided by Tencent Cloud, and is available to all users.

Features:
 - **Operating system:** you can select a preferred operating system, such as Linux or Windows. Operating systems are updated regularly.
 - **Software:** public images are integrated with software packages provided by Tencent Cloud, and support multiple versions of software with full permissions, such as Java, MySQL, SQL Server, Python, Ruby, and Tomcat.
 - **Security:** all provided operating systems are licensed. All images are created by Tencent Cloud’s security and OPS team, and are strictly tested. The Tencent Cloud security components are also available.
 - **Limit:** none.
 - **Fees:** all public images are free of charge, except for Windows images in certain regions outside the Chinese mainland where a license fee may be charged.
 - **Technical support:**
  - Tencent Linux is provided and maintained by Tencent Cloud.
  - For issues involving third-party images, contact the open-source community or the operating system vendor. Tencent Cloud will provide technical assistance during the troubleshooting process if needed.



## Custom Images
**Custom images** are made by users using the image creation feature, or imported using the image import feature. Custom images are only available to creators and the people they share them with.

Features:
 - **Use case:** an image created from a CVM instance with applications deployed can be used to quickly create more instances that contain the same configuration.
 - **Features:** you can create, copy, share and terminate images.
 - **Limitation:** each region only supports a maximum of 10 custom images.
 - **Fees:** image creation may incur fees. For the actual cost, refer to the price shown when you create the image. Cross-region replication of custom image is free of charge.

For more information on custom images, see [Creating Custom Images](https://intl.cloud.tencent.com/document/product/213/4942), [Copying Images](https://intl.cloud.tencent.com/document/product/213/4943), [Sharing Custom Images](https://intl.cloud.tencent.com/document/product/213/4944), [Cancelling Image Sharing](https://intl.cloud.tencent.com/document/product/213/7148), and [Importing Images](https://intl.cloud.tencent.com/document/product/213/4945).

## Shared Images
**Shared images** are custom images shared with you by another Tencent Cloud user using the image sharing feature.
These images are displayed in the same region as the original images.

Features:
 - **Use case:** help other users quickly create a CVM instance.
 - **Features:** the shared image can only be used to create CVM instances. Renaming, copying, or re-sharing the image with others are not supported.
 - **Security**: shared images are not checked by Tencent Cloud, which may pose security risks. We strongly recommend against using images from unknown sources.
 - **Limitations**: each custom image can be shared with a maximum of 50 Tencent Cloud users. Custom images can only be shared with accounts in the same region as the source account.

For more information on shared images, see [Sharing Custom Images](https://intl.cloud.tencent.com/document/product/213/4944) and [Cancelling Image Sharing](https://intl.cloud.tencent.com/document/product/213/7148).


