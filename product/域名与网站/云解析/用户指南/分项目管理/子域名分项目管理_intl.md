## Overview
Tencent Cloud DNS supports assigning subdomain names under a top-level domain name to different projects for management. For example, qcloud.com is a default project. You can assign cloud.tencent.com to project A and test.qcloud.com to project B for management.

Below are some points that need your attention:
- The project assigning of a subdomain name is effective only for itself, and there is no project affiliation among domain names at different levels. For example, if qcloud.com belongs to the default project, assigning cloud.tencent.com to project A will not assign a.cloud.tencent.com to project A, instead, it still belongs to the default project.
- A collaborator with permissions to a subdomain name can only resolve the subdomain name itself. For example, qcloud.com belongs to the default project. After cloud.tencent.com is assigned to project A, the collaborator can only add resolutions records like `www.qlcoud.com` > A record > 8.8.8.8 (host can only be www) but cannot add resolution records for qcloud.com or a.cloud.tencent.com (host cannot be @ or a.www).
- Assigning and moving domain names across projects won't affect existing resolutions.

## Operations Guide
### Assigning a Subdomain Name with Resolutions
1. Method 1
On the record management page of the domain name, select a resolution record to assign to a project, so that the corresponding subdomain name will be affiliated to the specified project for management. For example, select `www.qcloud-example.com` to assign it to a project as shown in the figure below.
![](//mc.qcloudimg.com/static/img/60ca6fd590a8c607bfd47df84a362270/image.png)
2. Method 2
Select a top-level domain name, click **Batch operation** -> **Assign its subdomain names to a project** and enter the subdomain name in the pop-up to assign them.
![](//mc.qcloudimg.com/static/img/73e344ba533817ca84623d23158dc359/image.png)
![](//mc.qcloudimg.com/static/img/8dc6737c5e6508cf161d19f2776b1f59/image.png)
For example, if "www" is entered, the resolution record corresponding to the host www will be loaded. Assigning a subdomain name to a project doesn't affect the resolution record, which follows the subdomain name to the corresponding item.
![](//mc.qcloudimg.com/static/img/3ec9f9375d56f8e73241c697b4efcb48/image.png)
### Assigning a Subdomain Name Without Resolutions
A subdomain name that has no resolutions records can also be assigned. For example, enter "test" and you can see no resolution has been added for `test.qcloud-example.com`, but it can still be assigned for management.
![](//mc.qcloudimg.com/static/img/a5f791477e5bd07ef4be8ce80f80bfb8/image.png)
### Project Permissions
In the protocol subdomain name list, a collaborator of project 123 can resolve the subdomain names under this project.
![](//mc.qcloudimg.com/static/img/da641d70cf664895938a8e0e302c4aab/image.png)
However, resolutions can be added only for the subdomain names in the **Collaborative subdomain names** list. For example, only resolution records of "www" and "test" can be added as shown in the figure below.
![](//mc.qcloudimg.com/static/img/2118da62aa76deeaf1d7b1d9ed395163/image.png)
Similarly, a collaborator of project 123 can also assign subdomain names of the project 123 to another project, and if the collaborator has permissions to project 456 at the same time, they can move the subdomain names to project 456.
![](//mc.qcloudimg.com/static/img/7071d7046f4aefb376545d77d3cbe6bd/image.png)
A global collaborator can filter the resolution records of a top-level domain name by projects to see what resolutions are added in different projects.
![](//mc.qcloudimg.com/static/img/cd42f9711c42ea0884873a6818aa1e69/image.png)
