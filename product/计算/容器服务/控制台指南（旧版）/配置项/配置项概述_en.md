### What is Configuration Item

Configuration is used to specify the read-in settings of some programs when they start. You can apply different configurations to different objects.

Configuration item is a collection of multiple configurations. The value of configuration item can be a string or a file.
Configuration item supports YAML format and visual editing. Click to view [YAML Syntax](https://wikipedia.org/wiki/YAML).
Configuration item supports only new versions instead of modified versions.

### Benefits of Configuration Item

1. Configuration item feature can help you manage configurations of different businesses under different environments. It supports multiple versions and YAML format.
2. Configuration item enables you to configure different environments for the same application. It supports multiple versions, which allows you to update and roll back application.
3. With this feature, you can quickly import your configurations into the container in the form of files.

## How to Use and Work With Configuration Item
### Creation of Configuration File

1. Go to configuration file list page, and click "New"
2. Enter basic information and the content of configuration file. YAML format and visual editing are supported.
3. Step 2: Set a mount path for the volume in the container configuration.
![Alt text](https://main.qcloudimg.com/raw/a19523d8778330c0f8d7678f0dd4cb09.png)
![Alt text](https://main.qcloudimg.com/raw/f0552efa59f56cc0e95293a4d129fa8c.png)

### Revised Version of Configuration File

1. Click configuration file ID to go to configuration file details page.
2. Select one of the versions and click "Generate New Version". A new version is generated based on the revision of this version.
![Alt text](https://main.qcloudimg.com/raw/680a2704cb81919eec9aaa08246027cd.png)

### Deletion of Configuration File
1. You can delete a specified version in configuration file details page
2. You can delete a configuration file in configuration file list page and delete all versions under this file

## Usage of Configuration File
Method 1:  Mount the configurations in the configuration file to a container in the form of data volume.
Method 2:  Deploy multiple environments using configuration file and application template.
Method 3:  When you create a service, import configurations to environment variable using configuration file.




