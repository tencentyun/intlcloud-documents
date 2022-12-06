This guide introduces how to access Customer Identity Access Management (CIAM) and APIs in the application system. You can use CIAM to quickly implement features such as user login, logout, and sign-up, and take full advantage of CIAM's flexible and powerful configuration and management capabilities.

## Applications

CIAM supports the following types of applications:

### Web applications

Web applications are application systems on the backend web server. Web applications are developed in languages​or frameworks such as Java, .NET, PHP, Node.js, and Express. Users can access them through a browser. Generally, backend applications are running on protected servers. Therefore, these applications can securely store sensitive information such as application passwords, and protect tokens from being leaked.

### Single page applications

Single page applications (SPAs) are frontend applications running in the browser. SPAs are developed using HTML, CSS and JavaScript technologies based on React, Vue, and Angular frameworks. SPAs can directly initiate requests to service APIs without forwarding by backend applications. But the applications and data exist in "user-agent" (such as browsers), so SPA applications are not suitable for storing or processing sensitive data that requires protection.

### Mobile applications

Mobile applications are applications installed and run on user devices (such as mobile phones, tablets, PCs, and smart devices). Mobile applications are generally developed using specialized application development languages, such as Objective-C, Swift, and Kotlin. These applications are not suitable for storing sensitive information such as application passwords, but can protect tokens from being leaked.

### Machine-to-machine applications

Machine-to-machine (M2M) applications are applications running on the backend (such as backend services, command line programs, and daemons). M2M applications implement services by calling APIs without user participation. This way, they can better protect sensitive information from being leaked.

## Integration Guide

Web, single page, and mobile applications can quickly access CIAM as OpenID Connect (OIDC) or OAuth clients. OIDC and OAuth protocols are widely used on the Internet. Leveraging their abundant development resources, you can find the desired development libraries for various applications for quick integration.

- M2M applications [get the Access Token via client credential mode](https://www.tencentcloud.com/document/product/1148/51483), and then carry the Access Token to access APIs.

>! The APIs in this guide are accessed through the HTTPS protocol. The prefix of the access address is​your user directory's domain name, which can be viewed on the [Domain Settings page](https://console.cloud.tencent.com/ciam/custom-domain-name). In this guide, `https://sample.portal.tencentciam.com` is used as the prefix of the access address.