This document describes how to reference resources and upload attachments in CODING Project Collaboration.

## Open Project

1. Log in to the [CODING Console](https://console.cloud.tencent.com/coding) and click **Use Now** to go to CODING page.
2. Click <img src ="https://main.qcloudimg.com/raw/d94a8e60dd3a41d0af07d72ae0e9d70e.png" style ="margin:0"> in the upper-right corner to open the project list page and click a project icon to open the project.
3. Click **Project Collaboration** in the menu on the left.

## Feature Overview[](#intro)

CODING Reference Resources provides contextual support, so that team members can learn about the context of issues and quickly locate resources for problem-solving. In the Description or Comments on the details page of epics, user stories, requirements, tasks, bugs, and sub-tasks, you can reference resources and check issues referenced by other resources.

## References and Referenced[](#references)

### Reference resources[](#resource)

In the Description or Comments on the details pages of epics, requirements, tasks, bugs, and sub-tasks, you can use `# + reference ID/title` to select a resource. The resource referenced will be shown in the References list. If the current issue has been referenced by another resource, the resource will be shown in the Referenced By list of the issue. The following shows how to reference resources in "Requirements".

1.  Select resources by using `# + reference ID/title` in **Description** of the issue details page.
![](https://qcloudimg.tencent-cloud.cn/raw/3513e10314ae6f9326e38926b577ad39.png)
2.  Select resources by using `# + reference ID/title` in **Comments** of the issue details page.
![](https://qcloudimg.tencent-cloud.cn/raw/268a50543d222d27dcafaea2281e5fd2.png)

### Referenced resources[](#referenced)

If resource B is referenced by issue A, you can view it in the References list of the resource B's issue list page.

### Code commit reference[](#code)

1. Reference Resources supports associating code commits with issues. When committing code, add the `# + reference ID/title` of the issue to the commit information (for example, this is a commit #3). If the issue to be associated with the code commit is not in the same project as the repository, add `repository name + # + reference ID` to the commit information (for example, this is a cross-project commit code-repo #3).
![](https://qcloudimg.tencent-cloud.cn/raw/d5a4cf73014ee0215d7cae975c26bc49.png)
2. You can view the associated code commit list in the Referenced By list of the issue details page. In the code commit history, you can be redirected to the issue details page through ` # + reference ID` in the commit information.
![](https://qcloudimg.tencent-cloud.cn/raw/b0fd5d31a4557a02d562c654c6a0a5ed.png)

### References and Referenced lists[](#list)

The References and Referenced lists display all resources referenced by and from the current issue, including epics, iterations, requirements, tasks, bugs, sub-tasks, pull requests, code versions, code commits, Wiki pages, files, and external links.
![](https://qcloudimg.tencent-cloud.cn/raw/c973ae3531136a032d5cee60b614ed14.png)

### Resource positioning[](#positioning)

In the References and Referenced lists, you can click the magnifying glass icon on the right of the resource to go to the position where a certain resource is referenced and learn about the context. If the resource is referenced more than once by the current issue, you can select a specific reference position to go to.
![](https://qcloudimg.tencent-cloud.cn/raw/02d55162e492e8b2c119756510633d50.png)

## Upload Attachments[](#annex)

You can click **Upload Attachments** on the issue details page to upload files related to the issue, or drag them to the issue details page. A maximum of 10 files can be uploaded, and the file size cannot exceed 300 MB.
![](https://qcloudimg.tencent-cloud.cn/raw/0f39ec8f3d0926a9d9ee3b8d9c3b7daa.png)

## CoDesign Draft[](#codesign)

CODING supports upload of external drafts from CoDesign in **Upload Attachments**, so that your team can accurately associate product drafts with issues, and communicate in real time based on the online preview. CODING makes it easier for your team to go through the entire process from design, development to release, and deliver products.
>? CoDesign is a one-stop product design collaboration platform developed by Tencent, which allows drafts to be imported and previewed online. It helps Internet product design teams to increase collaboration efficiency, and streamlines the product design process.
> 
1. Go to the issue details page, click **Upload Attachments**, and then select **CoDesign Draft**.
![](https://qcloudimg.tencent-cloud.cn/raw/f1b41b93a12fe81bf43bc30b02046ceb.png)
2. When you upload a CoDesign draft for the first time, you need to select a login method in the pop-up box to log in to your CoDesign account.
![](https://qcloudimg.tencent-cloud.cn/raw/906aac07cd9babb519cdb66f39cfe8a2.png)
3. After login, select the drafts to be associated. More than one draft can be associated with an issue.
![](https://qcloudimg.tencent-cloud.cn/raw/029d642fdeb3e3b22587c14c0ec7cfd0.png)
4. The associated drafts will be shown in the **Attachment** list. Click it for preview. You can upload more drafts, or disassociate a draft by clicking the icon below it.
![](https://qcloudimg.tencent-cloud.cn/raw/94688a3ac27eab00d38f4bc85e8fac13.png)

## MockingBot

CODING supports upload of external prototypes from MockingBot in **Upload Attachments**. This allows your team to view the design prototypes on the current issue page, and easily then discuss, modify, and update them in a simple and efficient way.

First, log in to [MockingBot](https://org.modao.cc/dashboard/okcwtseuldpj2pth9), and then select the MockingBot prototype to be imported to a CODING issue. Then, click **Share**, select "Embed to a Third Party", and then copy the embed code.
![](https://qcloudimg.tencent-cloud.cn/raw/dc1ba342b3e95e33cec6e4c8e6334698.png)

Then, go to the CODING Issue Management page, click any epic, requirement, task, or bug, and then select **From Third Party** > **MockingBot** from the **Upload Attachments** menu.
![](https://qcloudimg.tencent-cloud.cn/raw/11d201886b84696665887756a054fe21.png)

Paste the embed code to associate the prototype with the issue. After upload, you can preview the MockingBot prototype in CODING.
![](https://qcloudimg.tencent-cloud.cn/raw/d38e5246be26d825649193d323dfa75b.png)

## TXC

TXC is a user feedback platform developed by Tencent. It allows users to publish their comments and feedback as posts to help development teams improve service quality and user experience.

CODING allows you to create and view issues in the feedback posts on TXC, and associate or disassociate issues. Besides, you can view the associated TXC post list on the issue details page in CODING.

### Authorize to bind[](#authorize)

Go to the homepage of any project, and then click **Project Settings** > **Project Collaboration** > **Integration Configuration**. Then, click **Bind** to bind TXC.
![](https://qcloudimg.tencent-cloud.cn/raw/e3c25c30067ccccf692e8de3320dc51d.png)

Every product in TXC can bind more than one CODING project. After you log in to TXC via the QR code, select a product to bind.
![](https://qcloudimg.tencent-cloud.cn/raw/2fa458c47a1e90f9e24623fcb540340a.png)

### Create or associate issues[](#create)

After binding, select any feedback on the TXC feedback page, and then associate it with a CODING issue by clicking the CODING icon on the right.
![](https://qcloudimg.tencent-cloud.cn/raw/1a9c84791db9e547bde22c4c7d7875c8.png)

You can select an existing issue or create a new issue for association.
![](https://qcloudimg.tencent-cloud.cn/raw/08f09d3cd10ece7141314ee627f417ae.png)

If you select **Create New Issue**, you will be redirected to CODING to select the desired issue type (requirement, task, or bug), and fill in the issue content.
![](https://qcloudimg.tencent-cloud.cn/raw/6e7a258b6ee340a2cf0c4683549d067a.png)

### View associated issues[](#create)

You can view associated issues in TXC.
![](https://qcloudimg.tencent-cloud.cn/raw/5c0b65bbabbd921b9f562405094628b5.png)

>! If you remove an associated issue from the TXC issue page, the corresponding issue in the CODING project will not be deleted, but is ****disassociated**** with TXC instead.

You can also check the association between an issue and TXC in the CODING project.
![](https://qcloudimg.tencent-cloud.cn/raw/b530ad760de2b08c61a3f583aa172eaf.png)

## Delete References[](#delete)

To remove a resource from the References list, delete the description or comment with `# + reference ID` on the issue details page. If the resource is referenced by more than one issue, delete all descriptions or comments with `# + reference ID` on issue details pages.
