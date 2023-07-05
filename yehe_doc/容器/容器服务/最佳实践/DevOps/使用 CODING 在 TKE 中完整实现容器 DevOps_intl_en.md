## Agile Development and DevOps
In the Internet industry, the concepts of agile development and DevOps are being adopted by more and more enterprises. As a kind of collaborative culture, agile development and DevOps work to break down barriers and increase the sense of common responsibility among members. At the same time, they also reduce handover work and improve the speed of delivery to customers.  
DevOps not only implements process tools (such as CI, CD, and containers) in enterprises, but also transforms the process of development and team collaboration. CICD tools are particularly important for small- and medium-sized enterprises (SMEs). By using mature tools and container technologies, enterprises can save costs and develop capabilities for rapid iteration and rapid response to business changes.  
The following figure shows the relationships between CI/CD and agile development and DevOps:
![](https://qcloudimg.tencent-cloud.cn/raw/1fb95025d669798082dc2e82e9437586.png)

## Overview
Based on native Kubernetes, Tencent Cloud TKE provides a container-based solution that solves environmental issues in the processes of development, testing, and OPS and helps users to reduce costs and improve efficiency. Implementing DevOps requires many tools and underlying services, and completing closed-loop linkage requires long-term investment and the establishment of a complex toolchain system, which will consume a lot of time and resources and can even affect R&D efficiency and delivery efficiency and delay business development. The combination of Coding and cloud advantages provides a unified collaboration platform and R&D toolchain. When the workflow is run on the Coding integrated R&D efficiency platform, the data will evolve into team knowledge accumulated in the process of project implementation. Because the data becomes collective experience, it will facilitate the continuous self-improvement of the team. Coding can also be used to implement full lifecycle management for software R&D and save the trouble of complex infrastructure OPS hosting.  
Coding can seamlessly interwork with TKE. This document describes how to implement CI/CD on Coding and deploy services to TKE clusters.  


## Concepts

### CI (Continuous Integration)

Continuous Integration is called CI for short. In the CI environment, developers frequently change and merge code, and the system will automatically build an application and run different levels of automated testing to verify the changes and ensure that the changes will not damage the application. The test items cover everything from classes and functions to the different modules that constitute the whole application. If automated testing finds conflicts between new code and existing code, CI can fix errors easily and quickly. See the figure below:
![](https://qcloudimg.tencent-cloud.cn/raw/56d1bd72ad6004dc76a372bad59bf38c.png)


### CD (Continuous Delivery and Continuous Deployment)
> ? The difference between Continuous Delivery and Continuous Deployment: Continuous Delivery is a capability, whereas Continuous Deployment is a method.  

#### Continuous Delivery
Continuous Delivery is called CD for short. After the CI process is completed, CD supports the following operations:
- Automatic publication of verified code to the repository  
- Pre-production environment deployment  
- Delivery to the quality team or users  

The following figure shows the detailed process:
![](https://qcloudimg.tencent-cloud.cn/raw/5d64bb1129a365d17c1e660763dc90ca.png)

#### Continuous Deployment
Continuous Deployment is called CD for short. It is the last stage of CICD. Continuous Deployment automatically deploys all changes, including Continuous Delivery, to the production environment. Generally, due to business considerations, you can choose not to perform the deployment. If deployment is needed, Continuous Delivery must be implemented first. The following figure shows the detailed process:
![](https://qcloudimg.tencent-cloud.cn/raw/5d64bb1129a365d17c1e660763dc90ca.png)



### CI/CD tools[](id:CICD)

Currently, the two types of CI/CD tools are provided: **On-Premise** and **Hosted tool-type SaaS service**.

#### On-Premise
Users need to establish a server to run the CI/CD tools.  

#### Hosted tool-type SaaS service
Users do not need to establish a server.
The advantages of hosted tools are as follows:
Low maintenance costs: As the operation environment is hosted by services, there are no maintenance costs. In contrast, on-premise tools require a great deal of time for server deployment and maintenance.  
Clean operation environment: When using Python as the project programming language, you need to continuously integrate different versions of Python (2.7, 3.6, and 3.7), whereas Hosted CI/CD can create a new operation environment each time and allow you to make version adjustments at any time.  
Pre-installed software and runtime environments: The continuous integration of a project requires the use of different runtimes and toolchains. Hosted CI/CD Service has already been pre-installed with a lot of common software and runtime environments, thus reducing the time it takes to establish an environment.  

### Coding
Coding is a tool for implementing the CI/CD process. Coding provides a complete set of R&D process management systems (including the complete CI/CD process). The whole process from requirement submission to product iteration, product design, code management, automated testing, continuous integration, build management, and continuous deployment is completed in Coding. The use of Coding can achieve the standardization of production line operations and automatic version recording, thus simplifying enterprise R&D management and improving R&D efficiency.  
- Coding supports both hosted and on-premise [CI/CD tools](#CICD) (supporting private deployment).  
- Coding supports Jenkins, code management (as well as GitHub and GitLab), agile development management, and Kubernetes containerized deployment. It also seamlessly supports TKE.  
- SMEs can use hosted tools to achieve quick product delivery and implement fast business iteration.  

## Directions
### Activating the DevOps service
> ! The steps here are an example intended for a root account user who uses the DevOps service for the first time. If you have activated the service, you can skip these steps and proceed to [Creating a project and a code repository](#createProduct).  

1. Log in to the TKE console, and select **[DevOps](https://console.cloud.tencent.com/coding/container-devops)** in the left sidebar.  
2. The "Container DevOps" page is displayed.
3. Select **Activate service** > **Go to CAM** to go to the "Role management" page.   
4. Click **Grant**, and you will be redirected to the **Activate service** page.
5. Complete the team information and click **OK** to activate the DevOps service.  

### Creating a project and code repository[](id:createProduct)
1. Log in to the TKE console, and select **[DevOps](https://console.cloud.tencent.com/coding/container-devops)** in the left sidebar.  
2. The "Container DevOps" page is displayed.
3. Click **Use now** to enter the **CODING DevOps** page.  
4. Select **Project** in the left sidebar to go to the project details page.  
5. On the project details page, click **+Create project** in the upper right corner.
6. In the "Choose project template" step, click the "DevOps project" to go to the next page.  
7. In the "Enter basic project information" step, enter the basic information of the project. Here, the project name coding-test is used as an example.
8. Click **Complete** to create the project. After the project is created, the project overview page will be displayed.  
9. On the overview page, click **Code repository** in the left sidebar to go to the details page of the code repository.
10. Click **Create code repository** and set the basic information of the repository. Here, a code repository named coding-test is created as an example.
11. Click **OK**.  

### Creating a product repository
Software products refer to binary files generated through source code compilation and packaging. Binary files in different programming languages have different formats, and they usually can be directly run on a server.  

#### Creation process
1. Log in to CODING DevOps and select **[Project](https://tencent-test.coding.net/user/projects)** in the left sidebar to enter the project management page.  
2. On the "Project management" page, click the name of the project for which you want to create an artifact repository to go to the project details page.  
3. Select **Artifact repository** > **Create repository** in the left sidebar to enter the **Create repository** page.
4. On the "Create repository" page, set the key information as needed.
5. Click **OK** to complete the creation process. The repository details page will be automatically displayed, as shown in the figure below:
6. Click **Use access token to generate configuration** to perform configuration after authentication.  
> ! After setting the access token, save it properly for future TKE image pulling.  
> 


### Continuous Integration
> ! Before executing the building plan, you must run the following command to add the docker registry account of Coding to the TKE cluster for image pulling authorization.  
```
kubectl  create secret docker-registry coding --docker-server=coding registry address --docker-username=user name --docker-password=password --docker-email=email address
```

1. Log in to CODING DevOps and select **[Project](https://tencent-test.coding.net/user/projects)** in the left sidebar to enter the project management page.  
2. On the "Project management" page, click the name of the project for which you want to create an artifact repository to go to the project details page.  
3. In the left sidebar, click **Continuous Integration** > **Build Plan** > **Create Build Plan**.
4. Choose a building plan template as needed, confirm the default settings of the template, and click **OK**.  
This document takes the Golang+Gin+Docker template as an example to demonstrate a Go project.


### Continuous Deployment

1. Log in to CODING DevOps and select **[Project](https://tencent-test.coding.net/user/projects)** in the left sidebar to enter the project management page.  
2. On the "Project management" page, click the name of the project for which you want to create an artifact repository to go to the project details page.  
3. On the left sidebar, select **Continuous Deployment** > **Kubernetes** and click **Configure Now**.
4. On the **Deployment console** page, select the desired Tencent Cloud account type for configuration. Then, you can proceed to subsequent steps such as configuring applications and processes, associating projects and applications, and starting deployment.  


## References
This document briefly introduces how Coding implements basic CI/CD operations based on TKE. For more information, refer to the [documentation on the official website of Coding](https://help.coding.net/).  

