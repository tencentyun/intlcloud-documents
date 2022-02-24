## Continuous Integration Overview

Continuous integration (CI) plays an important role in modern software development. In normal projects, some of the work is mechanical and repetitive, but prone to errors (such as during packaging and deployment). Users can instruct machines to complete this work with the click of a mouse and then take a break while the CI build plan automatically performs unit testing, code inspections, compilation and building, contract testing, and even deployment. This significantly reduces the workload of developers while improving code quality and development efficiency.


## CODING Continuous Integration (CODING-CI)

CODING Continuous Integration (CODING-CI) is fully compatible with Jenkins' continuous integration services. It supports popular programming languages, such as Java, Python, and Node.js, and building Docker images. Its graphical orchestration, high-spec clusters, and multi-plan parallel builds help you comprehensively accelerate your build tasks. It supports mainstream Git code repositories, including CODING Code Repositories (CODING-CR), GitHub, and GitLab. In terms of build dependency pull, it has dedicated network optimizations for major image sources such as Maven and npm to ensure a high pull speed and further accelerate the build process.

## Function Guide

The core components of continuous integration are build plans, which are displayed in cards. The buttons are described below:
![](https://qcloudimg.tencent-cloud.cn/raw/b74969b3e97b09509ead4b9cb653e5d9.png)
Hover your cursor over a chart to display button descriptions.
![](https://qcloudimg.tencent-cloud.cn/raw/559341967b3c519f66f95f917386ab7b.png)
On the build records page, users can conveniently set build plans and filter build records.
![](https://qcloudimg.tencent-cloud.cn/raw/5107dd726f32c1b4e3d381bdb3aae564.png)
In a single build record, you can follow the link to quickly go to the build branch and revision version. In the **Quick View** area, you can follow the link to view the build process, build snapshot, and change history.
![](https://qcloudimg.tencent-cloud.cn/raw/b6bdfe2e298e7dac5ad2eccf585163d2.png)

### Build plans

Build plans (jobs) are the basic units of continuous integration. You can open a build plan to set its code source, build process, trigger rules, environment variables, and notifications. In the future, this plan will be triggered based on the set rules to implement an automated build pipeline.

### Build tasks

After configuring a build plan, each build execution generates a specific build task. You can go to a build task to see its build process, change history, test reports, build artifacts, build snapshot, and other execution information.

### Jenkinsfiles

A Jenkinsfile defines a continuous integration pipeline, which implements stream encapsulation and management of steps. Pipelines are the basic units in continuous integration. Pipelines can be executed in series or parallel.

