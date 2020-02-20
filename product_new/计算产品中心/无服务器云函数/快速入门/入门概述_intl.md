This section briefs how to use Serverless Cloud Function (SCF). SCF helps you quickly build applications without having to purchase and manage servers. All you need to do is write the core code using the languages supported by the platform and set the conditions for code execution.

### How to Use

Before using SCF, you need to activate the service on the product details page. The flowchart below shows the basic steps for using SCF:
![](https://main.qcloudimg.com/raw/00846a864b53d5c2e21e27aa72b6b71d.png)

### Usage Examples

We provide examples for users who are new to SCF, and you can familiarize yourself with the usage of SCF based on the examples:
- Create and test a simple Hello World function.
- Create and test a function linked to COS by configuring the file upload action in a COS bucket as the trigger. For example, when there is a file uploaded to the COS bucket, the file can be downloaded to the local disk's /tmp directory of the function environment.
- Implement a simple web backend by configuring API Gateway as the trigger. For example, when an HTTPS domain name is entered in the browser, the result of function execution can be obtained.

You can learn how to perform basic operations in the SCF console through these three examples, including:
- Use the blank function template and demo function template. Each template provides sample code and configuration that implement certain logic, and you can easily create a function that already contains the sample code by simply selecting the template as needed.
- Create and update function configuration information.
- Test a function and view its execution log and monitoring.

After reading the getting started guide, you can also read how SCF works, how to build a function, and best practices to learn more about building a production system using SCF.
