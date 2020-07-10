## Development Mode
Serverless Framework CLI supports the development mode (`dev` mode). For projects in development mode, you can write their code and develop and debug them more easily, as you can continuously focus on the process from development to debugging while minimizing the interruptions caused by other tasks such as packaging and update.

### Entering development mode<span id="joinDev"></span>
Under a project, you can run `serverless dev` to enter the development mode as shown below:
>Currently, `serverless dev` is supported by only the Node.js 10 & 12.16 runtime environment.
>
```
$ serverless dev
serverless ⚡ framework
Dev Mode - Watching your Component for changes and enabling streaming logs, if supported...
Debugging listening on ws://127.0.0.1:9222.
For help see https://nodejs.org/en/docs/inspector.
Please open chorme, and visit chrome://inspect, click [Open dedicated DevTools for Node] to debug your code.
--------------------- The realtime log ---------------------
17:13:38 - express-api-demo - deployment
region: ap-guangzhou
apigw:
  serviceId:   service-b77xtixx
  subDomain:   service-b77xtixx-12539702xx.gz.apigw.tencentcs.com
  environment: release
  url:         http://service-b77xtixx-12539702xx.gz.apigw.tencentcs.com/release/
scf:
  functionName: express_component_6r6xkh60k
  runtime:      Nodejs10.15
  namespace:    default
express-api-demo › Watching
```
After you enter the development mode, the Serverless tool will output the deployed content and start continuous file monitoring. When a code file is updated, it will be automatically deployed again to sync the local file to the cloud.



### Exiting development mode
You can press `Ctrl+C` to exit the development mode, and the following result will be returned:
```
express-api-demo › Disabling Dev Mode & Closing ...
express-api-demo › Dev Mode Closed
```


## In-cloud Debugging

You can enable in-cloud debugging for projects whose runtime environment is Node.js 10. You can use a debugging tool such as Chrome DevTools or VS Code Debugger to connect to the remote environment for debugging.

### Notes
SCF in-cloud debugging is currently in beta test. You are recommended to try it out and share your questions and suggestions with us.
Before using SCF in-cloud debugging, you need to note the following:

- In-cloud debugging uses an actually running SCF instance for debugging.
- Because of the randomness of event triggering, if there are multiple instances, an event may be triggered on a random instance. Therefore, not all requests can hit the debugging instance and trigger debugging.
- When debugging is paused at a breakpoint:
	- If it stops running for a long period of time and there is no return, the trigger such as API gateway may prompt timeout.
	- If the instance is still in countdown status and continues running until the execution is completed after debugging completion, the total consumed time will be recorded as the function execution duration.
- The maximum duration of a single execution from triggering of instance execution to debugging completion is 900 seconds. If the debugging is interrupted for over 900 seconds, the execution will be forcibly ended, and 900 seconds will be used as the function execution duration for statistics and measurement.
- The debugging capability on the current version will set the function timeout period to 900 seconds. If you exit debugging properly, the timeout period will be reset to a normal value. If you forcibly end debugging or exit debugging exceptionally, the function timeout period will fail to be set to a normal value. In this case, you can deploy the function again (on the CLI) or manually edit it (in the console) to adjust the timeout configuration.



### Enabling in-cloud debugging
When you [enter the development mode](#joinDev), if the project is a function whose runtime environment is Node.js 10 or above, in-cloud debugging will be automatically enabled and debugging information will be output.
For example, when you enable the development mode, if the output result contains information similar to the following content, in-cloud debugging has been enabled for this project.
```plaintext
Debugging listening on ws://127.0.0.1:9222.
For help see https://nodejs.org/en/docs/inspector.
Please open chorme, and visit chrome://inspect, click [Open dedicated DevTools for Node] to debug your code.
```

### Using Chrome DevTools
The following steps are used as an example to describe how to use DevTools in Chrome to connect to a remote environment for debugging:
1. Start the Chrome browser.
2. Enter `chrome://inspect/` in the address bar to access it.
3. You can open DevTools in two ways as shown below:
![](https://main.qcloudimg.com/raw/a731827f731370cce0a245ef7252e4ea.png)
 1. (Recommended) Click **Open dedicated DevTools for Node** under "Devices".
 2. Select **inspect** under a specific target in "Remote Target #LOCALHOST".
If you cannot open the target or there are no targets, please check whether configuration of `localhost:9229` or `localhost:9222` exists in "Configure" under "Devices", which corresponds to the output after in-cloud debugging is enabled.
4. In DevTools opened after you click **Open dedicated DevTools for Node**, you can click the **Sources** tab to view the remote code. The actual code of the function is in the `/var/user/` directory.
On the **Sources** tab, the code that you want to view may be loaded. More remote files will be displayed as the debugging proceeds.
5. Open a file as needed and set a breakpoint at the specified position in it.
6. If you trigger the function in any means such as URL access, page, command, or API, the remote environment will start running and be interrupted at the breakpoint to wait for further operations.
8. On the tool bar on the right of DevTools, you can continue the execution of an interrupted program or perform other operations such as step-over, step-into, and step-out on it. You can also directly view the current variables or set the variables that you want to track. For more information on how to use DevTools, please see the DevTools user guide.

### Exiting in-cloud debugging

When you exit the development mode, in-cloud debugging will be disabled automatically.
