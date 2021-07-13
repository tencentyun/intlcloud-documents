Tencent Cloud Serverless Cloud Function (SCF) is a serverless execution environment that enables you to build and run applications without having to purchase and manage servers. Simply code in a supported language and set the execution conditions, and your code can be run on the Tencent Cloud infrastructure elastically and securely.
This document describes the usage process of SCF and provides multiple examples for function creation, deployment, and testing as well as service building through the SCF Console, SCF CLI, and SCF VS Code plugin.


## Directions
The following is the flow chart and basic steps of using SCF:
![](https://main.qcloudimg.com/raw/d91172398b2f460417837fb64be85734.png)
1. **Prepare**: [sign up for a Tencent Cloud Account](https://intl.cloud.tencent.com/document/product/378/17985), activate the SCF service, configure a basic development environment, etc.
2. **Write function**: a function is the basic unit of scheduling and operation, and you must follow the function API specifications when writing a function.
3. **Test locally**: you can debug the code locally and then deploy it in the cloud.
4. **Deploy function (including configuring trigger)**: after the code is deployed in the cloud, SCF can execute the function after a triggering condition are configured. The execution condition of a function is called a trigger. You can configure various types of triggers, such as timer, API Gateway, and COS triggers.
5. **Test in cloud**: after the function is deployed in the cloud, you can test it through the configured trigger.
6. **View log**: SCF supports displaying historical or real-time function logs in various ways.
7. **View monitoring information**: you can stay on top of the function running status by viewing monitoring metrics.
8. **Configure alarm**: alarming is critical for online production business. After an alarm is configured, you can receive alarm messages promptly when an exceptional situation occurs in the business.



## Getting Started

The getting started document can guide you through the complete process of using SCF. You can further familiarize yourself with SCF and developer tools through the following examples:

- [Creating Functions in Console](https://intl.cloud.tencent.com/document/product/583/32742)
- [Creating Functions on Serverless Framework CLI](https://intl.cloud.tencent.com/document/product/1040/33164) (recommended)







## Developer Tools

The Tencent Cloud Serverless team provides a wide variety of developer tools to help you use SCF:

- [SCF Console](https://console.cloud.tencent.com/scf)
- [Serverless Framework CLI](https://intl.cloud.tencent.com/document/product/1040/33164)


You can also see [How SCF Works](https://intl.cloud.tencent.com/document/product/583/9694), [Development Guide](https://intl.cloud.tencent.com/document/product/583/9210), and [Best Practice](https://intl.cloud.tencent.com/document/product/583/9739) to learn more about how to use SCF to build production systems.
