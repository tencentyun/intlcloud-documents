### Why can’t I use an instance name to create an instance?
An instance name cannot be used to create an instance for the following reasons:
- An instance name must consist of 5 to 50 characters. It supports only the combination of lowercase letters, digits, and "-" and cannot start or end with "-". Only the instance names that meet the requirements can be used to create instances.  
- An instance name directly determines the access domain name of the instance. Therefore, an instance name is globally unique at the Tencent Container Registry (TCR) product level. When an instance is created, the name of the instance cannot be identical with an existing instance name of the current user or other users.
- Some instance names are reserved or shielded and cannot be used to create instances.

### Why do I need to define a network access policy after an instance is created?
Only the TCR Enterprise Edition supports the creation of a dedicated instance. By default, the created instances disable the entry for accessing the public network and private network to guarantee the stability and data security of enterprise edition instances. The access of clients that meet the rules is allowed only after the user configures and enables the access policy to avoid malicious attacks caused by leakage of access domain names.

### What is the solution for the prompt "unauthorized: authentication required" when an image is pushed or pulled?
When the Docker client is used to push and pull images, the client must have the credential for accessing registry instances. To solve the problem, refer to the following steps:
1. Make sure that the correct access credential is used to run the `docker login` command on the server and the access credential of the instance has been stored in the Docker client. For more information, refer to [Pushing and Pulling an Image](https://intl.cloud.tencent.com/document/product/1051/35484).  
2. If the `docker login command has been run on the server and login is successful, check whether the temporary password used for login last time is still within the validity period.
By default, the instance access credential obtained by the console is valid within only 24 hours to guarantee data security of enterprise-class instances. Beyond the period, a new credential must be generated.

### Is synchronizing the data of Personal Edition and Enterprise Edition instances supported?
Yes. You can use the open-source tool to synchronize. For more information, see [Migration from TCR Personal Edition to TCR Enterprise Edition](https://intl.cloud.tencent.com/document/product/1051/39844).

### How do I select the access level of a namespace?
The current namespace supports setting the access level to public or private to manage public attributes of the image repository and chart repository under the namespace. When a namespace is created, the access level is private by default. If you hope all repositories under a namespace to be obtained by other users without authentication, you can set the access level of the namespace to public. In addition, instances support configuration of anonymous pull by default. If the access level of your namespace is set to public, other users can pull images in all repositories under the namespace and Helm Chart without accessing instances. Set the access level with caution.
