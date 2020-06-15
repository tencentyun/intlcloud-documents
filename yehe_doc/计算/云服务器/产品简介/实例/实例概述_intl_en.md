## What is a CVM instance?
An **instance** is a Cloud Virtual Machine (CVM). It contains basic computing components such as CPU, memory, operating system, network, and disk.

CVM instances provide elastic computing capacity in the Tencent Cloud securely and reliably, which enable you to scale computing resources up or down to handle changes in requirements, thus greatly reducing your purchasing costs and simplifying IT OPS work.

Each instance type offers different compute and storage capabilities, making them suitable for different use cases. Select an instance type based on the computing capacity, storage and network access method that you need for the instance. For more information about instance types and use cases, see [Instance Types](https://intl.cloud.tencent.com/document/product/213/11518). After you launch an instance, you can interact with it as you would any traditional computer. You also have complete control of your instances.

## Instance Image
**Image** is a template that contains a software configuration (operating systems, pre-installed programs, etc.) required for CVM instances. You can use an image to launch an instance or multiple instances repeatedly. In other words, image is an “installed disk” of the CVM.

Tencent Cloud provides the following types of images:
 - Public image: available to all users and suitable for major operating systems.
 - Custom image: only available to the creator and the users who share these images. Custom images are created from running instances or imported from external sources.
 - Shared image: shared by other users. They can only be used to create instances.

For more information about images, see [Overview](https://intl.cloud.tencent.com/document/product/213/4940) or [Image Types Overview](https://intl.cloud.tencent.com/document/product/213/4941).

## Instance Storage
Similar to normal CVM, instances can be stored in **system disk** and **data disk**:
System disk: similar to C drive in the Windows system. System disk contains a full copy of the image used to launch an instance, and the running environment for the instance. A larger system disk than the used image is required when an instance is launched.
Data disk: similar to D and E drives in the Windows system. Data disk is used to save user data, and supports flexible expansion, mounting and unmounting.

Both system disk and data disk support different types of storage provided by Tencent Cloud. For more information, please see [Storage Overview](https://intl.cloud.tencent.com/document/product/213/4952).

## Instance Security

Tencent Cloud provides the following method to guarantee the instance security:
- **Policy:**(https://intl.cloud.tencent.com/document/product/598/10601): when different accounts need to control the same set of cloud resources, you can use a policy to control their access to cloud resources.
- [Security Groups](https://intl.cloud.tencent.com/document/product/213/12452): you can use a security group to limit the instance accessibility to trusted addresses.
- Login control: log in to your Linux instances using [SSH Keys](https://intl.cloud.tencent.com/document/product/213/6092) method whenever possible. If you log in to your Linux instances using [Login Password](https://intl.cloud.tencent.com/document/product/213/6093), change your password from time to time.

