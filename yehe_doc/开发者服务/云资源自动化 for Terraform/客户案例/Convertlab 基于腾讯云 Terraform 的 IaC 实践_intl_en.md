This document is a summary given by the Convertlab DevOps team on how they leverage Tencent Infrastructure Automation for Terraform to manage cloud infrastructure, accelerate business innovations, reduce costs, and improve efficiency.

## Convertlab overview

Established in 2015, Convertlab (Shanghai Xin Zhaoyang Information Technology Co., Ltd.) is dedicated to building a digital marketing hub and one-stop marketing middleend that make marketing simple and growth natural.

Convertlab specializes in the integration of "marketing technology" and "operation art" and provides professional, convenient, and intelligent integrated marketing cloud solutions based on the DM Hub product developed innovatively. With the help of internet big data, AI, and other technologies, it helps companies build portrait insights that are close to the real behavior of users. Through marketing automation, precise reach, and interaction, customer experience is improved, and new data-driven marketing is implemented to achieve super growth in performance.

Convertlab aims to provide enterprises with an innovative SaaS-based digital marketing hub service, so that their marketing personnel can identify and convert customers on an open and integrated platform and comprehensively measure the marketing effect. So far, Convertlab has served 400 enterprises with best practices.

## IaC import

Terraform is an Infrastructure as Code (IaC) tool. IaC is an infrastructure automation method based on software development practices. It allows you to write and execute code to define, deploy, update, and terminate infrastructure. In this way, you can use software development tools to manage infrastructure, such as versioning systems, automation tests, and deployment and orchestration tools.

Convertlab innovates based on actual customer needs. IaC is imported for two purposes. On the one hand, manual operations are not allowed in the production environment of many foreign enterprises, and cloud resources are purchased and changed only by writing Terraform code. On the other hand, improving the product line means more development environments and larger infrastructure are to be managed, calling for a more efficient method.

## Significant improvement of the delivery efficiency

Convertlab products are big data analysis applications, which rely on rich cloud products such as K8s clusters, EMR big data clusters, ES clusters, different types of databases, message middleware, and object storage. In addition to cloud products required by product running, log and monitoring products are also involved.



Although Convertlab offers SaaS services, some large and mid-sized customers require on-premises deployment, i.e., product deployment under their cloud accounts. Manual resource purchase is time-consuming and error-prone. Purchasing a cloud product in the Tencent Cloud console usually involves cumbersome configuration before order submission. After the successful purchase, configuration is also necessary. In case of an operation error, product running will be affected, and troubleshooting is time-consuming and laborious, even for experienced personnel. If the customer's IT personnel are responsible for purchase and configuration, countless rounds of communication will need to be devoted to cloud resource preparation.



The Convertlab DevOps team has developed Terraform code and automated product deployment tools for DM Hub, covering cloud resource purchase, product deployment, and installation testing. The time to deploy an environment is shortened from days to hours, greatly accelerating the process from purchase to launch. Managing cloud infrastructure with software development practices is what makes Terraform superior. In this way, all infrastructure changes are incorporated into the versioning system to be automated, repeatable, consistent, and easy to test. They can also be continuously iterated and written with self-documenting code.

## Daily deployment for product quality enhancement

Environment differences are usually what make it impossible to promptly spot and hard to reproduce and locate software defects. A manually prepared environment tends to suffer configuration drift, data inconsistency, and other issues after running for long. With customized Terraform code, the DevOps team no longer needs to manually prepare and clear the environment. Environment creation is repeatable and consistent from development and testing to delivery.



By integrating Terraform and other automation tools such as Ansible and Helm, Convertlab automates product deployment, eliminating manual intervention from cloud resource preparation and check and environment initialization to deployment. In an internal test environment, the HTTPS certificate and DNS will be automatically configured to allow for access to the deployed product in the browser.



With automated deployment capabilities, daily deployment, or end-to-end installation testing, starts. The workflow is executed on schedule every day to prepare a new environment, deploy the product, and terminate the environment hours later. The WeCom group will be notified of any failure for troubleshooting. Then, the automated installation test is added to the workflow, which checks whether the main features of the deployed product work properly. Daily deployment can discover many issues that tend to emerge only after frequent running. They are everywhere, for example, in the Terraform code, product deployment script, product data, and initialization/upgrade/migration tools. This enhances the product release quality.

## Architecture evolution acceleration for greater security compliance

Infrastructure security is the foundation of application security. Enabling a security feature in the cloud involves many configuration and verification tasks. Security configurations in a manually configured environment often fail expectations due to project progress, the experience of Ops personnel, or other problems. Terraform supports automated execution, despite many environment configurations.



The entire cloud architecture is set up based on the best practices of cloud vendors, and more and more security baselines and best practices of the architecture will be incorporated into code.

For example:
- Multi-AZ allocation of cloud resources

- Independent key pairs in different environments

- Strong and random passwords for all cloud products

- Fine-grained IAM authorization

- The principle of least privilege by port for security groups




The component upgrade and compatibility test are simpler, for example, K8s version upgrade, ES version upgrade, and testing the compatibility with other Tencent Cloud products (such as TencentDB for Redis and TencentDB for MongoDB). An environment is pulled and tested, and new Terraform code is released after the test is passed. The infrastructure architecture is constantly reviewed and improved through Terraform software development, and experience is reflected in the code.

## Creation of a temporary environment

Development teams may need the same environment or temporary environments to deploy a specified product version for some test tasks.

Based on the experience of daily deployment, Convertlab defines a workflow for task execution. Simply check the specification and number of cloud resources and the product version to be deployed before the workflow starts. When the workflow ends, you can get the product URL and login credentials in the environment. Then, perform a few simple operations on the workflow, and you can have the environment automatically terminated after the process ends, incurring no additional fees. As it is easy to get an environment, you can terminate an environment on Fridays or before holidays and create one on workdays, which saves cloud resource fees.

## Scale application

With the successful experience in DM Hub, its automation capabilities are gradually applied to other product lines. Specifically, Data Hub and AI Hub are equipped with Terraform code and automated deployment tools. Many Tencent Cloud products and parameter configurations used by Convertlab products are reusable. Some Terraform module libraries are set up and maintained, so that Terraform code can be quickly provided for other products and even temporary environments. The application scenario of automated deployment is expanding from the single-product to multi-product mode where multiple products share cloud resources.



Importing a new technology always brings along learning costs, and so is the case with Terraform. With some development experience and Terraform module libraries, if you need to set up a temporary environment, you will find that it's faster to write Terraform code than to manually log in to the console and purchase resources.

## Summary and outlook

IaC is the foundation of DevOps. Only with IaC can there be an end-to-end closed loop in the real sense and cost-effective performance stress tests, a variety of automated tests, and disaster recovery drills.



Convertlab's experience of more than one year has shown that Tencent Cloud and its IaC team can get you well started with infrastructure automation and you don't need to wait until everything is ready. The sooner you act, the sooner you enjoy the fruits.



Developing Terraform code in Tencent Cloud was not always easy though. When Terraform TencentCloud Provider was released, the resource capabilities, parameter values, and output values of certain cloud products did not meet the business requirements, certain steps needed to be manually performed in the console, and some cloud products or configuration operations had no resources or data sources. As a result, the automation workflow could not be run.



At that time, Tencent Cloud IaC team promptly offered resources and released a new provider version in a short time. They also well supported our new requirements that kept coming out. Terraform capabilities were improved and issues were solved in a very responsive and smooth atmosphere. That's how the two parties managed to create Terraform resources for EMR, TKE, and ES.



Much more can be done for infrastructure automation, for example, Terraform cross-region disaster recovery capabilities and deep integration of log and monitoring into Tencent Cloud products. Convertlab will keep updating and iterating products based on Tencent Cloud for greater benefits and win-win results.