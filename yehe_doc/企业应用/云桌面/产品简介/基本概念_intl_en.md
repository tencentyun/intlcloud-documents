## CVD Instance Specification Overview
The specifications of a CVD instance include compute resources (vCPU and memory) and storage resources (system disk and data disk). Different instances have different combinations of CPU, memory, GPU, system disk, and data disk for that are suited for different business scenarios.

### Compute resources

| Specification | vCPU | Memory | GPU | Recommended Scenarios |
|---------|---------|---------|---------|---------|
| CVD - Standard S1_4-core 8 GB | 4 vCPUs | 8 GB | - | Basic OA |
| CVD - Standard S1_4-core 16 GB | 4 vCPUs | 16 GB | - | OA |
| CVD - Standard S2_8-core 16 GB | 8 vCPUs | 16 GB | - | High-performance OA and coding |
| CVD - Graphic G1_4-core 16 GB | 4 vCPUs | 16 GB | 1/4 NVIDIA T4 | Light 3D requirements, such as drawing viewer |
| CVD - Graphic G1_8-core 32 GB | 8 vCPUs | 32 GB | 1/2 NVIDIA T4 | Moderate 3D requirements, such as online design |
| CVD - Graphic G1_16-core 64 GB | 16 vCPUs | 64 GB | 1 NVIDIA T4 | Heavy 3D requirements, such as video editing |
>?More CVD compute specifications will be available in the future.

### Storage resources
The storage of an instance is divided into system disk and data disk, each of which are sustained by a cloud disk. You can choose [SSD cloud disk](https://buy.cloud.tencent.com/cvd) or [premium cloud disk](https://buy.cloud.tencent.com/cvd) and customize the disk size as needed.
<table>
   <tr>
      <th width="100px" style="text-align:center">Category</td>
      <th width="0px" style="text-align:center">Description</td>
   </tr>
   <tr>
      <td style="text-align:center">System disk</td>
      <td>It is similar to the C drive on Windows and contains a full copy of the image used to launch an instance and its running environment. The system disk must be larger than the size of the image used when an instance is launched.</td>
   </tr>
	    <tr>
      <td style="text-align:center">Data disk</td>
      <td>It is similar to the D drive on Windows and stores user data.</td>
   </tr>

</table>

### CVD image
An image is a template that contains software configurations (operating systems, preinstalled programs, etc.) required for launching CVD instances. You can use an image to launch one or multiple instances repeatedly. In other words, an image is the "installation disc" of CVD.

Tencent Cloud provides the following types of images:

| Category | Description |
|---------|---------|
| Public image | It is available to all users and provides a preconfigured OS. |
| Tencent Cloud office image | It is available to all users and comes with preinstalled Tencent Cloud office applications such as WeCom, Tencent Meeting, and Tencent Docs in addition to the OS. |
| Custom image | It is created on a user-specific basis and makes it easier for the admin to batch purchase instances as needed. |

## Portal
The CVD portal is a browser-based secure access portal. End users can access it in emails or SMS messages and obtain the CVD resources assigned by the admin after successful login.

## CVD Policy
A CVD policy defines a set of CVD security rules for configurations such as file redirection, device redirection, clipboard read/write permissions, and watermark, which are used to uniformly control the permissions of end users when they access CVD.
