This document describes how to use the code owner mechanism.

 

## Open Project

1. Log in to the [CODING Console](https://console.cloud.tencent.com/coding) and click the team domain name to go to CODING.
2. Click <img src ="https://main.qcloudimg.com/raw/d94a8e60dd3a41d0af07d72ae0e9d70e.png" style ="margin:0"> in the upper-right corner to open the project list page and click a project icon to open the corresponding project.
3. Select **Code Repositories** in the menu on the left and click **Branches** to go to the branch management page.

The code owner mechanism must be used together with [Branch Protection](https://intl.cloud.tencent.com/document/product/1132/44715). Place the declaration file `CODEOWNERS` in a code repository to declare the owner of the code files in this repository. Generally, the code owner is the project owner.

When the target branch of a merge request is a protected branch and the files changed in the request involve the paths or files set in the declaration file, the merge request details will list the corresponding owners and their review statuses.
![](https://qcloudimg.tencent-cloud.cn/raw/d9daaae130b06415339f75d4cc8176e0.png)

In the figure above, the `CODEOWNER` file declares that the owner of the files in the `charts/repos/**` path is Sally. When a merge request is submitted for a protected branch and it involves changes to files in the `chars/repos/` path, Sally is automatically added as a reviewer for this request.

>? You can use the continuous integration plugin to automatically add reviewers. For details, see [Automatically Add Merge Request Reviewers](https://help.coding.net/docs/ci/plugins/reviewer.html).

In the **protected branch** settings, toggle on Enable Review by Code Owner. Then, code owners must Allow Merge for every merge request that changes code under their jurisdictions.
![](https://qcloudimg.tencent-cloud.cn/raw/0b502a2daf494b1499969b7343018120.png)

### Declaration file URL[](id:address)

By default, `CODEOWNERS` files are searched for layer by layer from the following locations. The file name must be in uppercase, and the search will stop when one file is found.

-   Root directory
-   `docs/` directory

### Declaration file format reference[](id:reference)

The declaration file is a normal text file. Blank lines and lines starting with `#` are ignored. Each line uses the following format:
<dx-codeblock>
:::  bash
pattern email email email ...
:::
</dx-codeblock>
`pattern` indicates a file path mode. email is the owner's email. You can enter multiple owners separated by spaces. Sample file:
<dx-codeblock>
:::  bash
# Declares all files with the extension .js
*.js yourname@coding.net

# Declares the files in the build/logs/ directory (including subdirectories) under the repository root directory
/build/logs/ yourname@coding.net

# Declares all files in docs/ folders (not including subdirectories)
docs/* yourname@coding.net

# Declares all files in the docs/ folder (including subdirectories) under the root directory
/docs/ yourname@coding.net
:::
</dx-codeblock>

