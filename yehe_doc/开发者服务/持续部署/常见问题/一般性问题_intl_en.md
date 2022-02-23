### What types of artifacts does continuous deployment support?
Continuous deployment supports Docker images, Generic files, and WAR packages.

### What types of clusters does continuous deployment support?
Continuous deployment supports CVM (Linux OS), TKE, and SCF clusters.

### How can I protect sensitive information when configuring continuous deployment processes?
To protect tokens, SSH keys, Kubernetes certificates, and other confidential information, select **Project Settings** > **Developer Options** > **Credentials Management** in a project in CODING DevOps for Web to open the credentials management page. You can also set the continuous deployment release processes that can use the information.

### How do I release source code?
Many common dynamic programming languages involve no compilation and build processes. You can configure Git repository in the application's artifact settings to specify the file path and release the source code.

### How can I configure an approval process?
You can configure an approval process in two steps:
1. Open CODING DevOps for Web and select a project. In the project, select **Settings** > **Fields and Processes** > **Approval Process Settings** to go to the "Approval Process Settings" page. You can add multiple approval processes for a single project.
2. Go to **Continuous Deployment** > **Release Process** > **Associate Approval** to associate the release process with an approval process. Then, when you submit a release order, the system will automatically determine which approval process is executed in advance.

### Do release orders have to go through an approval process?
No, if you do not associate any approval process with a release process, the release process requires no approval. In this case, the release order is executed immediately after it is submitted.
