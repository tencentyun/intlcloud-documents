## CVD Instance Specifications
CVD instances differ in terms of compute resources (including vCPU and memory), management unit (standard or graphic), and storage resources (including system and data disks), which are suited for different business scenarios.

### Compute resources

| Specification | vCPU | Memory | GPU | Recommended Scenarios |
|---------|---------|---------|---------|---------|
| CVD - Standard S1_4-core 8 GB | 4 vCPUs | 8 GB | - | Basic OA |
| CVD - Standard S1_4-core 16 GB | 4 vCPUs | 16 GB | - | OA |
| CVD - Standard S2_8-core 16 GB | 8 vCPUs | 16 GB | - | High-performance OA and coding |
| CVD - Graphic G1_4-core 16 GB | 4 vCPUs | 16 GB | 1/4 NVIDIA T4 | Light 3D requirements, such as drawing viewer |
| CVD - Graphic G1_8-core 32 GB | 8 vCPUs | 32 GB | 1/2 NVIDIA T4 | Moderate 3D requirements, such as online design |
| CVD - Graphic G1_16-core 64 GB | 16 vCPUs | 64 GB | 1 NVIDIA T4 | Heavy 3D requirements, such as video editing |

>? More CVD compute specifications will be available in the future.

### Management unit

A management unit provides support for end users' connection and use of a virtual desktop. Management units come in two types – standard and graphic. When you buy a desktop instance, the system will automatically select a management unit according to the compute resources you purchase.

| Type   | Description                                                     |
| ------ | -------------------------------------------------------- |
| Standard | Provides support for the connection and use of standard desktops. |
| Graphic | Provides support for the connection and use of graphic desktops. |

### Storage resources

Storage resources include system disks and data disks, each of which correspond to one cloud disk. You can select the disk type ([SSD](https://buy.cloud.tencent.com/cvd) or [Premium](https://buy.cloud.tencent.com/cvd)) and size as needed.

| Type   | Description                                                     |
| ------ | :----------------------------------------------------------- |
| System disk | A system disk is similar to the C drive on Windows. It contains a full copy of the image used to launch an instance and its running environment. The system disk of the instance must be larger than that of the image used. |
| Data disk | A data disk is similar to the D drive on Windows. It stores user data.              |

### CVD image
An image is a template of software configurations (operating systems, pre-installed programs, etc.) needed to launch a virtual desktop instance. An image can be used to launch multiple instances and can be reused. It is like the installation disk of a virtual desktop.

Tencent Cloud provides the following types of images:

| Type | Description |
|---------|---------|
| Public image | A public image provides a preconfigured OS and is available to all users. |
| Custom image | A custom image is created based on a manually configured desktop. You can use a custom image to create multiple desktops with the same configuration. |