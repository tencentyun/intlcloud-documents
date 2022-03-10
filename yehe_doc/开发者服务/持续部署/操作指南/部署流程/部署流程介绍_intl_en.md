This document describes the deployment pipeline in CODING Continuous Deployment (CODING-CD).

## Prerequisites

You must activate the CODING DevOps service for your Tencent Cloud account before you can use CODING Project Management (CODING-PM). 

## Open Project

1. Log in to the [CODING Console](https://console.cloud.tencent.com/coding) and click **Use Now** to go to CODING page.
2. On the Workspace homepage, click <img src ="https://main.qcloudimg.com/raw/12230547b45d5eae85ad1c4fa86fba68.png" style ="margin:0" data-nonescope="true"> on the left to go to the CODING-CD Console.

## Function Overview

The deployment pipeline is the core module of Continuous Deployment. It enables arbitrary combination of stages in any sequence, while maintaining excellent flexibility, consistency, and repeatability.

- Flexibility: Supports serial or parallel control
- Consistency: Supports multiple deployment strategies and rollback, ensuring the release results as expected
- Repeatability: Deployment pipelines can be executed repeatedly, and the stages can be copied to other pipelines.

You can configure a fully automated pipeline or add manual judgment conditions at certain stages. In addition, the pipeline can be triggered automatically by various events, such as webhooks and other pipelines.

## Create Deployment Pipeline

Go to CODING-CD Console, and then click the deployment pipeline icon in the lower-right corner of the application card.

![](https://qcloudimg.tencent-cloud.cn/raw/4ddc682c3bcebda9daf23b87b057476e.png)

1. Click the **Create Pipeline** button in the upper-right corner.
![](https://qcloudimg.tencent-cloud.cn/raw/dc51fd45991ee1a255dcb4017a91b373.png)
2. You can copy any pipelines created in other applications, or create a new one. CODING also offers sample pipeline templates for Kubernetes and Tencent Cloud Auto Scaling.
![](https://qcloudimg.tencent-cloud.cn/raw/7aa628a2fa00ed118aae1b2de5ed4588.png)

## Basic Configurations

Basic configurations of an application can be regarded as the starting point for a full build. This allows you to set trigger conditions, or configure the notifications for a pipeline.

![](https://qcloudimg.tencent-cloud.cn/raw/43536778c6cd104bfaacd1f8115c368c.png)

### Auto Trigger

The auto trigger supports CODING Docker Repository Trigger, TCR Personal Repository Trigger, and Git Repository Trigger.

![](https://qcloudimg.tencent-cloud.cn/raw/f2e5d1bbde7eb62274cf92ec8e23c4cc.png)

### Add deployment pipeline parameters

Go to the Deployment Pipeline Configuration page, and then click **Add Startup Parameters**.

![](https://qcloudimg.tencent-cloud.cn/raw/dccb548c5afdac2960d010b9c1b21e73.png)

### Add stage

On the Deployment Pipeline Configuration page, click **+** to add a new stage, and select the stage type from the list on the right.
![](https://qcloudimg.tencent-cloud.cn/raw/e6a1bf1defe6883427188d19368c53e5.png)

## Execute Deployment Pipeline

After the pipeline configuration is complete, you can use the preset trigger to execute the pipeline automatically, or manually trigger the pipeline by submitting a release order in Continuous Deployment.

![](https://qcloudimg.tencent-cloud.cn/raw/b4de188f629b5e3438454fc3ea2a3470.png)

## Deployment Pipeline Configuration

You can delete, disable, or lock a deployment pipeline, view its earlier versions, and edit JSON configuration.

![](https://qcloudimg.tencent-cloud.cn/raw/d08efa52feae739abd7ba8269bcb6acd.png)

### Delete pipeline

If you click "Delete", the pipeline will be deleted.

### Disable deployment pipeline

If you click "Disable", the pipeline can neither be launched via any trigger nor triggered manually. You can disable a pipeline for the team or a certain project.

![](https://qcloudimg.tencent-cloud.cn/raw/7e33280a84311cf5ce2ec0fe020edcdd.png)

### Lock deployment pipeline

If you click "Lock", the pipeline cannot be edited through the CODING-CD Console. You can specify whether the pipeline can be updated through API.

![](https://qcloudimg.tencent-cloud.cn/raw/d3fb49d5bd092eaaebf83996c82516ce.png)

### View revision history

When a new pipeline configuration is saved, the previous version will be added to revision history. On the Revision History page, you can make a comparison between different versions, and restore to any earlier version.
![](https://qcloudimg.tencent-cloud.cn/raw/a7912b8d24d038cf4e109ddcd5dadb84.png)

### Edit JSON configuration

Any changes made in the CODING-CD Console are saved in JSON files. You can add new fields to a pipeline, or edit the JSON content to customize configuration items not displayed in UI.

>! This allows you to edit a deployment pipeline in the text box, but it may affect the availability of the pipeline. We support restoring to any specific version in the revision history.

![](https://qcloudimg.tencent-cloud.cn/raw/b67161f563142b0efb95153ee2d9feb3.png)
