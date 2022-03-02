本文为您详细介绍如何自定义设置 CODING 项目管理中的事项类型。

## 进入项目

1. 登录 [CODING 控制台](https://console.cloud.tencent.com/coding)，单击**立即使用**进入 CODING 使用页面。
2. 单击页面右上角的 <img src ="https://main.qcloudimg.com/raw/d94a8e60dd3a41d0af07d72ae0e9d70e.png" style ="margin:0">，进入项目列表页面，单击项目图标进入目标项目。
3. 单击进入左侧菜单栏中的**项目协同**功能。

## 功能介绍[](#intro)

事项类型是项目协同中的主体，例如需求与任务都可以被抽象为**事项类型**。您可以新增如**运维**事项类型、修改类型图标、定义其在项目中的 [属性](https://intl.cloud.tencent.com/document/product/1133/44767) 与 [工作流](https://intl.cloud.tencent.com/document/product/1133/44768)。事项类型依照场景分为团队全局类型与项目级类型，需先行定义全局事项类型，再在项目内应用生效。

## 全局事项类型[](#global)

全局事项类型列表将展示团队内所有的事项类型。分为系统内置类型与自定义类型，系统类型不可修改图标与名称（例：史诗、需求、任务、缺陷、用户故事和与工作项）。

**用户故事**是新增的系统内置类型，其是敏捷框架中最小的工作单元，旨在从用户角度描述软件如何为其带来特定的价值。
![](https://qcloudimg.tencent-cloud.cn/raw/e349dfa40ac29c49888165f9563243fc.png)

>?新建自定义事项类型时可以选择类型图标与添加相关描述，事项类型创建后支持复制并自动创建副本。
>
自定义事项类型支持创建自定义需求与自定义任务；允许自行删除，删除事项前需解除与项目的关联。
![](https://qcloudimg.tencent-cloud.cn/raw/8be37bb6186bc153951fed7a31989bc9.png)

## 项目级事项类型[](#project)

在**项目设置** > **项目协同**中添加已设置的全局事项类型。
![](https://qcloudimg.tencent-cloud.cn/raw/747707706573ada56d374cb1066ffd35.png)

>! [敏捷模式](https://intl.cloud.tencent.com/document/product/1133/44754) 下将自动引入子工作项类型，[经典模式](https://intl.cloud.tencent.com/document/product/1133/44744) 下无法使用史诗与子工作项类型。
>


## 事项类型配置[](#config)

您可以为事项类型设置层级关系、属性与工作流。

### 层级关系[](#level)

经典协同模式下的**用户故事**、**需求**与**自定义需求**三种事项类型支持设置层级关系。
![](https://qcloudimg.tencent-cloud.cn/raw/502e029a1e28b2e221b834c81d80abf0.png)

设置层级关系后，在向下分解需求时能够选择多种事项类型，灵活满足团队实际的工作流。
![](https://qcloudimg.tencent-cloud.cn/raw/1b730df218d3a64bf8c3b566c71b440f.png)

### 配置属性[](#attributes)

属性可以理解为事项的**描述信息**，用于快速说明此事项目前的状态、截止日期、处理人、优先级等信息，但不包含基本属性信息（标题、描述、附件、关联资源等）。 属性配置页的所有属性将会在事项的详情页展示，并且可用于搜索控件和筛选器。详情请参见 [自定义事项属性](https://intl.cloud.tencent.com/document/product/1133/44767)。
![](https://qcloudimg.tencent-cloud.cn/raw/8b0045f76b2a605848caba1d4fa55f81.png)

### 配置工作流[](#workflow)

自定义工作流能够满足不同团队的个性化需求，既能够构建敏捷开发工作流，也可以适应经典项目协同模式。更重要的是，通过定义全局工作流状态，能够实现状态定义的一致性，提高跨项目与跨部门协作的效率。详情请参见 [自定义工作流](https://intl.cloud.tencent.com/document/product/1133/44768)。
![](https://qcloudimg.tencent-cloud.cn/raw/1d2c0eafd0226e3899f5a2202943a9f1.png)
