This document describes how to review merge requests.

 

## Open Project

1. Log in to the [CODING Console](https://console.cloud.tencent.com/coding) and click the team domain name to go to CODING.
2. Click <img src ="https://main.qcloudimg.com/raw/d94a8e60dd3a41d0af07d72ae0e9d70e.png" style ="margin:0"> in the upper-right corner to open the project list page and click a project icon to open the corresponding project.
3. In the menu on the left, select **Code Repositories** > **Merge Requests**.

Before creating a merge request or performing a merge, developers can update the title and description, add other project members as reviewers, and associate resources in the project (such as tasks, files, merge requests, and Wiki pages). You can also [automatically add reviewers](https://help.coding.net/docs/ci/plugins/reviewer.html) using the CI plugin.

>? If the target branch of a merge request is a protected branch and admins have been configured for the protected branch with **Automatically Add Branch Admin as Reviewer** enabled, the specified number of branch admins will be automatically added as reviewers.

## Review Content[](id:review-content)

After a reviewer receives a review notification, they should generally focus on the following:
-   The title, description, and associated resources of the merge request can clearly describe the code modification. The reviewer can communicate and check with the initiator using comments.
-   Review (comment) code at the line level for the committed file changes.


## Start Review[](id:start)

Code reviewers can comment on a code file line by line on the **File Changes** tab of **Merge Requests**. When you hover over a line in a code file, a plus sign `+` will appear. Click the plus sign to comment on the code. After entering a comment:

-   Click **Comment** to post the comment.
-   Click **Start Review** to post the comment and change the request status to **Reviewing**.

![](https://qcloudimg.tencent-cloud.cn/raw/d4e4ad17266dd7d709d0544404e7d4b8.png)

After the comment is posted, the comment and review status (if any) will be shown in the action log on the overview page of the merge request.

![](https://qcloudimg.tencent-cloud.cn/raw/d4e4ad17266dd7d709d0544404e7d4b8.png)


## Track File Viewing Progress[](id:file-view)

When you need to review multiple code files, click *Viewed* after you have finished reviewing a file to mark your progress. The file viewing progress bar will be automatically updated.

>?Marking a file as **Viewed** does not affect the review status and only serves to track the file viewing progress. It only applies to the current user.

![](https://qcloudimg.tencent-cloud.cn/raw/0f366ebe6b745fd2d51561fab5dd0416.png)

## Complete Review[](id:start)

After you have reviewed all code files, click **Complete Review** in the upper-right corner to publish the review result and end the review.
>?The number to the right of **Complete Review** indicates the total number of code comments on the current page.

-   **Comment**: Comment is required. 
-   **Allow Merge**: Comment is optional. The review result is published as **Allow Merge**.
-   **Require Changes**: Comment is optional. The review result is published as **Require Changes**.

![](https://qcloudimg.tencent-cloud.cn/raw/4e3f6f72e0fbf10fa5b447b8ab29421d.png)

After a review is completed, the comment or review result will be shown in the action log on the overview page of the merge request.
![](https://qcloudimg.tencent-cloud.cn/raw/682d193e4c7060c2cb59a57dff462268.png)


- If the target branch of a merge request is a protected branch, the review status of the merge request will be shown (if one of the results is **Require Changes**, the review status will be failed).
- If the review result is **Allow Merge**, the result will be shown in the branch status as a tag, regardless of whether the target branch is a protected branch.
![](https://qcloudimg.tencent-cloud.cn/raw/14d45f1281ebfb0f85d735865df5e18e.png)
