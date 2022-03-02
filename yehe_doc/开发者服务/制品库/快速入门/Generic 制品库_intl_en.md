This document describes how to store generic artifacts in CODING-AR, including how to create a repository and push, pull, and delete artifacts.

## Open CODING-AR

1. Log in to the [CODING Console](https://console.cloud.tencent.com/coding) and click **Use Now** to go to CODING page.
2. Click <img src ="https://main.qcloudimg.com/raw/d94a8e60dd3a41d0af07d72ae0e9d70e.png" style ="margin:0"> in the upper-right corner to open the project list page and click a project icon to open the project.
3. In the menu on the left, click **Artifact Management**.

## Create an Artifact Repository

Click **Create Repository**.

-   Select Generic as the repository type.
-   Enter a repository name.
-   Enter a repository description (optional).
-   Configure the permissions of different roles on the current repository. By default, all project members have the **Pull** and **Push** permissions. 
-   Click **Create**.

![](https://qcloudimg.tencent-cloud.cn/raw/24e8a6b622523ee751b8dc25e975d9c2.png)

## Push a Generic Artifact

You can push a generic artifact in either of the following ways:
-   Command line
-   Direct upload

### Upload via command line

Push an artifact using the command in the **Guide**.
![](https://qcloudimg.tencent-cloud.cn/raw/8f70e94aeacacf1c193d5519ac66101d.png)
For example, to push a file named demo.properties:

```bash
curl -T demo.properties -u username "https://********-generic.pkg.coding.net/my-projects/my-generic/demo.properties?version=0.1"
```
![](https://main.qcloudimg.com/raw/c9917d9dc36fa929b8cb1df1fa3f5490.png)

## Direct upload

On the repository page, click **Direct Upload** or drag a file onto the current page.
![](https://qcloudimg.tencent-cloud.cn/raw/c4cd765c2248ff2217bcd3eb615201b9.png)
Select a file, specify the upload mode and version, confirm the package name, and click **Upload**.
![](https://qcloudimg.tencent-cloud.cn/raw/6f5b960483bcd8af8e74e41f93024d4c.png)

## View a Generic Artifact

After an artifact is uploaded successfully, a success message will be displayed in the lower right corner. Click **Package List** to view the package uploaded.
![](https://qcloudimg.tencent-cloud.cn/raw/2353edc7072a5aab8921294e11911b3e.png)

## Pull a Generic Artifact

You can pull a generic artifact in either of the following ways:
-   Command line
-   Direct download

### Pull via command line

Pull an artifact using the command in the **Guide**.
![](https://qcloudimg.tencent-cloud.cn/raw/693c5120552978f94b6f925ae6513061.png)

```bash
curl -L -u username "https://********-generic.pkg.coding.net/my-projects/my-generic/demo.properties?version=0.1" -o demo.properties
```

### Direct download

On the repository page, select a package in **Package List** and download a version in **Version List** as needed.
![](https://qcloudimg.tencent-cloud.cn/raw/9b1c775927650b07cabd3f4678f5fcfa.png)

## Delete a Generic Artifact

Delete a generic artifact via the command line.
![](https://qcloudimg.tencent-cloud.cn/raw/92a23568c63c00dacd4e66a5506e29a6.png)

Run the command in the guide.

```bash
curl -X DELETE -u username "https://********-generic.pkg.coding.net/my-projects/my-generic/demo.properties?version=0.1"
```
![](https://main.qcloudimg.com/raw/af6adb31cfd9957e457251383c5e7df6.png)