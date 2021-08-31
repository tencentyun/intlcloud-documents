

>?To provide more stable and powerful code building, image building, container image services, TCR and CODING DevOps have now realized the interconnection of container DevOps related features. Please go to [TCR console](https://console.cloud.tencent.com/tcr) and [CODING DevOps](https://console.cloud.tencent.com/coding) to use them. Creating image building and trigger in Personal Edition are not supported. The existing configurations will be retained and be effective.





### Overview
TKE offers continuous integration for containers, enabling users to build container images automatically and manually.

### Auto building
Container images can be automatically built based on GitHub or GitLab code repository that **contains Dockerfile files**. You need to register the token of the Github/Gitlab server first. If the code repository is GitLab, **the GitLab server used for the code repository must be accessible through internet**. You can configure an auto building rule for a specific code repository. When you push code to the code repository, if the auto building rule is matched, an container image is automatically built on the TKE Platform and then automatically pushed to the Tencent Cloud TKE image repository.
Configuring auto-building of images:
- Step 1: [authorize the source code repository](https://intl.cloud.tencent.com/document/product/457/35656)
- Step 2: [configure building rules](https://intl.cloud.tencent.com/document/product/457/35577)
- Step 3: submit code for auto building

### Manual building
You can manually build an image in two ways:

- **Based on GitHub and GitLab code repositories**
Similar to auto building, the code repository also needs to contain Dockerfile files. If the code repository is in GitLab, GitLab must support internet access. Different from auto building rules in which a container image is automatically built when code is pushed to the repository, manual building requires you to build an image on the console by clicking **Build**.

- **Based on an uploaded Dockerfile**
On the image repository console, you can upload a Dockerfile based on which the TKE builds a container image.

### Build description
- For Dockerfile that is in a Git repository or manually uploaded, if Dockerfile depends on external resource, the external resource must also be accessible through the internet.
- Both manual building and auto building are performed on the TKE platform, so you do not need to provide a build environment or server resources.

