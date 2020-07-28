### Why can’t I use an instance name to create an instance?
An instance name cannot be used to create an instance for the following reasons:
- An instance name must consist of 5 to 50 characters. It supports only the combination of lowercase letters, digits, and "-" and cannot start or end with "-". Only the instance names that meet the requirements can be used to create instances.  
- An instance name directly determines the access domain name of the instance. Therefore, an instance name is globally unique at the Tencent Container Registry (TCR) product level. When an instance is created, the name of the instance cannot be the same as the name of an existing instance under the current user or the name of an existing instance under other users.
- Some instance names are reserved or shielded and cannot be used to create instances.

### Why do I need to define a network access policy after an instance is created?
Only the TCR Enterprise Edition supports the creation of a dedicated instance. By default, created instances disable the entry for accessing the public network and private network to guarantee the stability and data security of enterprise edition instances. The access of clients that meet the rules is allowed only after the user configures and enables the access policy to avoid malicious attacks caused by leakage of access domain names.

### What is the solution for the prompt "unauthorized: authentication required" when an image is pushed or pulled?
When the Docker client is used to push and pull images, the client must have the credential for accessing registry instances. To solve the problem, refer to the following steps:
1. Make sure that the correct access credential is used to run the `docker login` command on the Docker client and the Docker client has stored the access credential of the instance. For more information, refer to [Pushing and Pulling an Image](https://intl.cloud.tencent.com/document/product/1051/35484).  
2. If the `docker login` command is run on the client and login is successful, check whether the temporary password used for login last time is still within the validity period.
By default, the instance access credential obtained by the console is valid within only 24 hours to guarantee data security of enterprise-class instances. Beyond the period, a new credential must be generated.

### Is synchronizing the data of Personal Edition and Enterprise Edition instances supported?
It is not currently supported. The Personal Edition instances of TCR are shared instances and do not belong to any single user, but Enterprise Edition instances are dedicated instances belonging to a specific user. Therefore, synchronizing image data between the two types of instances is currently not supported. If you use personal edition instances and enterprise edition instances at the same time, you can use the Docker client to or a custom script to manually complete data synchronization.

### How do I select the access level of a namespace?
The current namespace supports setting the access level to public or private to manage public attributes of the image repository and chart repository under the namespace. When a namespace is created, the access level is private by default. If you hope all repositories under a namespace to be obtained by other users without authentication, you can set the access level of the namespace to public. In addition, instances support configuration of anonymous pull by default. If the access level of your namespace is set to public, other users can pull images in all repositories under the namespace and Helm Chart without accessing instances. Set the access level with caution.
