This document describes how to merge branches.

 

## Open Project

1. Log in to the [CODING Console](https://console.cloud.tencent.com/coding) and click the team domain name to go to CODING.
2. Click <img src ="https://main.qcloudimg.com/raw/d94a8e60dd3a41d0af07d72ae0e9d70e.png" style ="margin:0"> in the upper-right corner to open the project list page and click a project icon to open the corresponding project.
3. Select **Code Repositories** in the menu on the left and click **Branches** to go to the branch management page.

If a multi-branch development workflow is used, we recommend you set the master branch as a [protected branch](https://intl.cloud.tencent.com/document/product/1132/44715). Developers can create temporary develop branches and initiate merge requests for them. After continuous integration (CI) and code reviews, developers can merge the develop branch into the master branch.

## Create Merge Request[](id:create-merge-request)

You can manually create merge requests on the command line or CODING DevOps platform.

**Create via the command line:**
<dx-codeblock>
:::  shell
git push origin local-branch:mr/target-branch/local-branch
:::
</dx-codeblock>

**Create manually:**

1.  On the details page of a code repository, go to the **Merge Requests** tab and click **Create** in the upper-right corner.
![](https://qcloudimg.tencent-cloud.cn/raw/48111a2e3c5c75b5a968ab495bd92558.png)
2.  Specify a source branch and target branch for the merge request. If no conflicts are found after the source branch is compared with the target branch, the system will indicate that they can be merged. You can view the differences between the files on the **File Changes** tab.
>?You can specify the default target branch for merge requests in [merge request settings](https://intl.cloud.tencent.com/document/product/1132/44718).
>
![](https://qcloudimg.tencent-cloud.cn/raw/3d23c975c8d0277c9303f5435fefde39.png)
3.  Enter a title, a description, and associated resources for the merge request.
>?If the source branch is not ahead of the target branch, merge requests cannot be created.

## Resolving Requests That Cannot Be Automatically Merged[](id:merge-status)

If a conflict is found after the source branch is compared with the target branch, the system will indicate that they cannot be automatically merged. You can view the file changes on the **Compare** tab. Resolve the conflicts to continue merging the branches.
![](https://qcloudimg.tencent-cloud.cn/raw/ff09bbc556284692d01afdc88531767e.png)

For example, if a conflict is found when merging `branch-01` into `master`, you can switch to the `master` branch locally and run the command:
<dx-codeblock>
:::  bash
git merge branch-01
:::
</dx-codeblock>
Find the file with conflicts. The conflicts will be highlighted in the file. You will be prompted to select which content to keep. Select the content you want to keep and save the file before committing it again, and then switch to the `branch-01` branch and enter the command:
<dx-codeblock>
:::  bash
git merge master
:::
</dx-codeblock>

Then, push the modified code to the remote repository.

## Initiate Review[](id:code-review)

When initiating a branch merge request, we recommend that you allow the relevant personnel to review the code to ensure code quality.

>?If the target branch of a merge request is a [protected branch](https://intl.cloud.tencent.com/document/product/1132/44715), the branch admins will be added as reviewers by default. To change the settings, see [Branch Protection Rules](https://intl.cloud.tencent.com/document/product/1132/44715).
>
![](https://qcloudimg.tencent-cloud.cn/raw/38ba72a6c3d11fc3a12345c79bd6f948.png)
After the reviewers have completed the [merge request review](https://intl.cloud.tencent.com/document/product/1132/44720), the review result will be shown on the details page of the merge request.


## Check Merge Status[](id:status-check)

In addition to the common manual code reviews mentioned above, we provide an integrated code review solution with automated tool and CODING Continuous Integration. The code is scanned based on pre-defined rules. When there is an issue with the code quality, the code will not be merged. Only code that has passed checks by the automated tool can be merged, significantly improving the efficiency of code reviews.

### Enable status check[](id:enable-status-check)

Status checks can only be enabled for a [protected branch](https://intl.cloud.tencent.com/document/product/1132/44715). After the option is selected, merging is allowed only after all status checks (CI tasks) have been run and passed.
![](https://qcloudimg.tencent-cloud.cn/raw/eb3a9b938e61fab568383e5184b2c9f7.png)
Select the CI trigger rule **Trigger Build on Merge Request** to trigger a build task after a merge request is created.
![](https://qcloudimg.tencent-cloud.cn/raw/d7b7f8226ee2d70d9283b891efb280bc.png)

### View status check result[](id:view-status-check-result)

After you have completed the above configuration, you can see the status of the merge check if the build task was correctly triggered. If your page is not similar to the following image, you may need to select **Trigger Build on Merge Request** in the CI build task.
![](https://qcloudimg.tencent-cloud.cn/raw/0b2e03298d36214e1606b23e88b1e0b3.png)
You can click the Refresh button in the upper-right corner to get the latest status. If the check result is successful, a prompt at the bottom will indicate that the branches have been merged. If the result is failed, the merge will be rejected. Status checks can be:

-   In progress: Wait for the build to finish.
-   Successful: The merge request can be merged.
-   Failed: Error occurred during the build process and the merge check failed. You can modify and push the code and trigger new build tasks until the build is completed successfully.
-   Exception: Exception occurred during the build process. You can try manually triggering it.

If multiple status checks are used, the branches can only be merged after all status checks are passed. You can also view status check processes in Browse Code, Commit History, and the branch list.
![](https://qcloudimg.tencent-cloud.cn/raw/30a63010b50a303691fa68aa2d63582b.png)

## Confirm Merge[](id:confirm)

-   **The target branch of the merge is a protected branch**
If the initiator of the merge request is a branch admin, they can perform the merge on their own. If the initiator is an ordinary member, the merge can be completed only after it has passed a review by a branch admin.
-   **The target branch of the merge is not a protected branch**
The initiator can initiate and complete a branch merge without review or authorization.

>?To learn how to modify the default branch and set protected branches, see [Set the Default Branch](https://intl.cloud.tencent.com/document/product/1132/44714) or [Set Protected Branches](https://intl.cloud.tencent.com/document/product/1132/44715).

### Delete source branch[](id:delete-source-branch)

When merging branches, select Delete Source Branch to delete the source branch after the merge.
![](https://qcloudimg.tencent-cloud.cn/raw/b7a5fc6f769c12941bf930e8a10f6a46.png)

### Fast-Forward merge[](id:fast-forward)

A merge commit record will be created by default during a non-fast-forward merge. If **Fast-Forward Merge** is selected, the remote repository will determine if the fast-forward rules are met. If the rules are met, this merge will not create a new merge commit record. If this mode is not selected, previous development records will be kept and a new merge record will be created during the merge. This option is equivalent to adding the `-ff` parameter when using `git merge`.


>?You can enable deletion of the source branch and fast-forward merge by default for merge requests in [merge request settings](https://intl.cloud.tencent.com/document/product/1132/44718).
