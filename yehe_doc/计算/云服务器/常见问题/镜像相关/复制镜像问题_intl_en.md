### When do I need to copy an image?
The custom image can only be used in the same region. If you want to:
- Deploy applications on the CVM instance in multiple regions.
- Migrate the CVM instance to other regions.
- Use the custom image across regions.

You can solve all of these by [Copying Images](https://intl.cloud.tencent.com/document/product/213/4943).

### Which images can be copied?
You can only copy custom images, but cannot copy public images, service marketplace images or images shared with others.

### Which regions now support the image replication?
All Tencent Cloud regions support the image replication.

### How long does it take to copy an image?
The time depends on the network transmission speed and task waiting queue. To copy an image, you need to transfer the image files from the availability zone of one region to the availability zone of the target region via network. Please wait patiently.

### How much does it cost to copy an image？
Cross-region replication of images is free of charge for now, but the copied image occupies the snapshot capacity and incurs a cost. For more information, see [Pricing List](https://intl.cloud.tencent.com/document/product/362/2413)

### How do I copy my image resources to other regions under another Tencent Cloud account?
You need to first copy your image to the target region, and share the image in the target region with another Tencent Cloud account. After your sharing, the target account can see this image in its shared image list.

### Is there any capacity limit for image replication?
No.

