## What is a CVM Instance?
A **CVM instance** contains basic computing components such as the CPU, the memory, the operating system, the network, and the disk.

CVM instances provide elastic computing services in the cloud in a secure and reliable way to meet computing requirements. As business demands change, computing resources can be scaled in real time to lower your software and hardware costs and simplify IT OPS work.

Each instance type offers different computing and storage capabilities, making them suitable for different use cases. You can choose the computing capacity, storage, and network access method of the instance based on the scope of the service you need to provide. For more information about instance types and use cases, see [Instance Types](https://intl.cloud.tencent.com/document/product/213/11518). After you launch an instance, you can use it as you would any traditional computer. You will also have complete control over your instances.

## Instance Image
An **image** is a template that contains software configurations (operating systems, pre-installed programs, etc.) required for launching CVM instances. You can use an image to launch an instance or multiple instances repeatedly. In other words, an image is the “installed disk” of the CVM.

Tencent Cloud provides the following types of images:
 - Public image: available to all users and suitable for major operating systems.
 - Custom image: only available to the creator and the users with whom the image is shared. A custom image is created from running instances or imported from external sources.
 - Shared image: shared by other users. They can only be used to create instances.

For more information about images, see [Image Overview](https://intl.cloud.tencent.com/document/product/213/4940) or [Image Types Overview](https://intl.cloud.tencent.com/document/product/213/4941).

## Instance Storage
A CVM instance can have a **system disk** and **data disks**:
System disk: Similar to the C drive in the Windows system. The system disk contains a full copy of the image used to launch an instance and the running environment for the instance. When you launch an instance by using an image, the size of system disk must be larger than the image.
Data disk: Similar to the D and E drives in the Windows system. The data disk stores user data. You can resize the data disk as required, and attach and detach them to an instance.

Tencent Cloud provide various disk types for system disks and data disks. For more information, see [Storage Overview](https://intl.cloud.tencent.com/document/product/213/4952).

## Instance Security

You can protect your instances by using the following configurations: 
- [Access management policy](https://intl.cloud.tencent.com/document/product/598/10601): When different accounts need to control the same set of cloud resources, you can use a policy to control their access to cloud resources.
- [Security groups](https://intl.cloud.tencent.com/document/product/213/12452): You can use a security group to allow only access from trusted sources.
- Login control: Log in to your Linux instances using [SSH keys](https://intl.cloud.tencent.com/document/product/213/6092) as much as possible. If you want to log in to your Linux instances using [passwords](https://intl.cloud.tencent.com/document/product/213/6093), change your passwords periodically.

