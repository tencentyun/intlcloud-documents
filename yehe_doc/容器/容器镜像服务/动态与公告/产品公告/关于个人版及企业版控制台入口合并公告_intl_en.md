The entries of TCR Enterprise and TCR Individual in the console are merged. The entry for TCR Individual in the console is discontinued, and you will be redirected to the TCR console if you go to the original entry. The most of the existing features of the TCR Individual are retained. The legacy image building and trigger features are no longer available. You can use the latest image building service based on CODING DevOps, or directly use CODING DevOps service to implement container DevOps.

## Updates

- The change is only limited to entries in the console. Other operations, such as pushing and pulling of existing container images and creation of namespaces and image repositories, are not affected.
- The legacy TCR Individual entry in the console (TKE > Application > Image Repositories > TCR Individual) is discontinued. The new entry can be accessed through **TKE console > Application > Image Repositories**. Then, you will be directed to **TCR console > Resource Center > Image Repository**.
- The features of password management and global image lifecycle management accessed through **TCR Individual > My images** are merged into **TCR > Instance Management**. Please see details below:
  - After the merger, you can check the TCR Individual instances in the specified region. Also, you can click **More** > **Reset the login password** to reset the password.
  - For Global Image Lifecycle Management feature, you can check the TCR Individual instances in the specified region. Also, you can click **More** > **Configure garbage collection** to set the policy.
  - The feature of Source Authorization is no longer available. The service will be provided by CODING DevOps.
- The features of image repositories management accessed through **TCR Individual > My images** are merged into **TCR > Resource Center > Image Repository**. Please see details below:
  - You can create, query, edit and delete image repositories.
  - You can query and delete image tags. Copying of image tags is no longer supported.
  - The legacy Auto Clearing feature is no longer supported. Please directly configure the global image clearing policy.
  - The image building feature is no longer supported, and the image building service will be provided by CODING DevOps. The legacy configuration data of image building is retained, but data creation and edit are no longer supported. Please switch to the latest image building service as soon as possible.
  - The trigger feature is no longer available.
- The features of namespace management features accessed through **TCR Individual > Namespace** are merged into **TCR > Resource Center > Namespace**. Please see details below:
  - You can create, query, edit and delete namespaces.

## Notes

- The changes are only limited to the entry of TCR Individual in the console and some features. The TCR Individual service is still free of charge within the quota.
- The changes do not affect TKE and other products that support TCR Individual service. You can continue to use the images in TCR Individual image repositories through these products.
- If you have any questions, please [contact us](https://intl.cloud.tencent.com/document/product/1051/46260).

## FAQs

### How to upgrade the TCR Individual service to the TCR Enterprise service?

You can refer to [Migration from TCR Individual to TCR Enterprise](https://intl.cloud.tencent.com/document/product/1051/39844), to migrate images in the TCR Individual image repositories to TCR Enterprise instances, and change the container cluster configurations.

### Why can't I see TCR Individual instances in the regions of Shanghai and Beijing after the merger of entries in the console?

In the Chinese mainland, TCR Individual service is only deployed in Guangzhou, Shenzhen Finance, Shanghai Finance and Beijing Finance. Guangzhou region was the default region before the merger, and it supported cross-region usage in Beijing, Shanghai and Chengdu. After the merger, the TCR Individual instances are only displayed in Guangzhou region. You can still access the TCR Individual image repositories managed in Guangzhou in other regions such as Beijing and Shanghai. If you want to improve the access speed and stability, please use TCR Enterprise service in a nearby region.

## Contact Us

Please [contact us](https://intl.cloud.tencent.com/document/product/1051/46260) if you have any questions. Thank you for your support for Tencent Cloud. We will continue to provide you with more cost-effective products.
