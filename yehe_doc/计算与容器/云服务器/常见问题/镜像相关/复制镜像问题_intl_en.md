### Under what circumstances do I need to copy an image?
Custom images can only be used in the same region. You can perform the following operations by [copying images](https://intl.cloud.tencent.com/document/product/213/4943): 
- Deploy applications on the CVM instance in multiple regions.
- Migrate the CVM instance to other regions.
- Use custom images across regions.

### Which images can I copy?
You can only copy custom images and cannot copy public images, service marketplace images, and images that others have shared with you.

### Which regions currently support copying images?
All Tencent Cloud regions support copying images.

### How long does it take to copy an image?
It depends on the network transmission speed and the task waiting queue length. To copy an image, you need to transfer the image files from a region’s availability zone to the target region’s availability zone via the network. Please wait patiently.

### How much does it cost to copy an image？
Copying images across regions is free for now, but the copied image will occupy the snapshot capacity and incur a cost. For more information, see [Pricing List](https://intl.cloud.tencent.com/document/product/362/2413)

### How do I copy the image resources under my account to other regions under another Tencent Cloud account?
You need to first copy your image to the target region, and then share the image under the target region with another Tencent Cloud account. After the image is shared, it will appear in the target account’s shared image list.

### Is there a capacity limit for copying images?
No.

