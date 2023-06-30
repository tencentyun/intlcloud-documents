## Instance
### Why can’t I use an instance name to create an instance?
An instance name cannot be used to create an instance for the following reasons:
- An instance name must consist of 5 to 50 characters. It supports only the combination of lowercase letters, digits, and "-" and cannot start or end with "-". Only the instance names that meet the requirements can be used to create instances.  
- An instance name directly determines the access domain name of the instance. Therefore, an instance name is globally unique at the Tencent Container Registry (TCR) product level. When an instance is created, the name of the instance cannot be identical with an existing instance name of the current user or other users.
- Some instance names are reserved or shielded and cannot be used to create instances.


### What should I do if I fail to log in to the instance?
To log in to the instance, you should run the command `docker login` in the access client and enter the user name and password.
Follow the instructions below:
1. Check whether the token is correct. You can obtain a temporary token to test the instance login through **[TCR console](https://console.cloud.tencent.com/tcr/instance)** > **Instance** > **Access TCR Instance**.
2. Check whether the access credential is valid. The temporary access credential is valid for 1 hour. For more information, see [Obtaining an Instance Access Credential](https://intl.cloud.tencent.com/document/product/1051/37253).
3. Check whether the instance allows traffic from the network of CVM. For more information, see [Network Access Control Overview](https://intl.cloud.tencent.com/document/product/1051/35490).

If the problem persists, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) to contact us.






## Image


### How does the TKE cluster implement the secret-free pulling of images?
We recommend the TKE user to use the TCR add-on to implement the secret-free pulling of images. For more information, see [TKE Clusters Use the TCR Addon to Enable Secret-free Pulling of Container Images via Private Network](https://intl.cloud.tencent.com/document/product/1051/38386).

You can set the access level of the namespace where the image is located to public, and all image repositories and Helm Charts in this namespace will become public. As "Anonymous Access" is enabled for instance by default, any clients that pass access control can get the images and charts directly without logging in. We recommend that you only set the basic image repository.




### What is the solution for the prompt "unauthorized: authentication required" when an image is pushed or pulled?
When the Docker client is used to push and pull images, the client must have the credential for accessing registry instances. To solve the problem, refer to the following steps:
1. Make sure that the correct access credential is used to run the `docker login` command on the server and the access credential of the instance has been stored in the Docker client. For more information, refer to [Pushing and Pulling an Image](https://intl.cloud.tencent.com/document/product/1051/35484).  
2. If the `docker login command has been run on the server and login is successful, check whether the temporary password used for login last time is still within the validity period.
By default, the instance access credential obtained by the console is only valid within 24 hours to guarantee data security of enterprise-class instances. Beyond the period, a new credential must be generated.

### Can I delete an image version?
Yes. When you delete a specified image version, the image versions with the same content (namely the same SHA256) will also be deleted.



## Access Permission

### How do I restrict user to access the specified namespace/image repository?
In TCR, you can configure the resource access permission for the sub-account through CAM. For more information, see [Example of Authorization Solution of the Enterprise Edition](https://intl.cloud.tencent.com/document/product/1051/37248) or [Example of Authorization Solution of the Personal Edition](https://intl.cloud.tencent.com/document/product/1051/37250).


## Network Control

### How is the network traffic billed?
Using the public network to upload and download the cloud-native applications such as container images and Helm charts will generate public network traffic fees in COS. We recommend you to use the private network access because it will not incur traffic fees, and the access speed is better than public network access.

<dx-alert infotype="notice" title="">
Using the instance synchronization feature for cross-regional synchronization of container images and Helm charts will not generate COS public network traffic fees.
</dx-alert>




### How do I determine if I am accessing via a private network or public network?
By default, the private network is used for VPC and the public network is used for non-VPC. For more information, see [How do I determine if I am accessing COS over a private network?](https://intl.cloud.tencent.com/document/product/436/6281).









## DevSecOps
### Why is the account of CODING DevOps locked?
It may be that the password was entered incorrectly five times, or the admin locks it. Please contact your admin.

### How do I specify the Dockerfile path and building directory when building an image by using source code?
- If you do not enter a path, the system uses the following default values:
  - Default Dockerfile path: Dockerfile under the root directory of the code repository.
  - Default building directory: the root directory of the code repository.
- To specify a path, enter a relative path with the project path as the root path.




## Synchronization and Replication

### How do I implement image acceleration?
Currently, TCR supports the [accelerated pull of images outside the Chinese mainland](https://intl.cloud.tencent.com/document/product/457/39139) and [P2P image acceleration](https://intl.cloud.tencent.com/document/product/457/38708).


### What are the differences between instance synchronization and replication?
#### Object
- The instance synchronization works on two independent instance.
- The instance replication works on an instance that acts as the primary instance and can create sub-instances in other region.

#### Effect
- The instance synchronization allows user to customize synchronization rules to synchronize data as needed.
- In instance replication, data is fully replicated and the application images used by multi-regional services are managed uniformly.

#### Underlying implementation
Based on COS cross-region synchronization capability, the instance replication supports real-time streaming synchronization of image data and is faster than instance synchronization.
The instance replication feature is only available for the premium instance and the cross-border replication is not supported.



## Other
### Why does the size of the image displayed on the cluster node and in the repository differ?
The image is compressed and stored in the image repository. The image size on the cluster node shall prevail.

### What features are not supported in the international version?

Currently, the CODING DevOps related features and some new features are not supported in the international version.
