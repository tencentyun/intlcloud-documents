### How do I deploy if my development environment is outside the Chinese mainland?
Serverless Framework will check whether the user is in the Chinese mainland by default during deployment. If your development environment is outside the Chinese mainland and you want to use Serverless Framework in the Chinese mainland edition, you can add the configuration item `SERVERLESS_PLATFORM_VENDOR=tencent` in the `.env` file to start the Chinese mainland edition by default.

### What should I do if I'm redirected to the global version during deployment?
If your deployment environment is configured with a proxy, this problem may occur. Please check whether your development environment is in the Chinese mainland and then add the configuration item `SERVERLESS_PLATFORM_VENDOR=tencent` to the `.env` file.

### What should I do if deployment is slow in my development environment outside the Chinese mainland?
The Serverless Framework deployment engine is currently in the Chinese mainland; therefore, for overseas deployment, file upload may be very slow. You can enable global acceleration by adding the configuration item `GLOBAL_ACCELERATOR_NA=true` to the `.env` file.

### How do I deploy if my environment does not have permission to access the public network and can access the public network only through a proxy?
Add the following configuration to the `.env` file:
```
HTTP_PROXY=http://127.0.0.1:12345  # Replace "12345" with your proxy port
HTTPS_PROXY=http://127.0.0.1:12345  # Replace "12345" with your proxy port
```

### What should I do if I have no permissions when using Windows PowerShell for deployment?
The permission control of Windows PowerShell is very stringent. You need to run the `set-executionpolicy remotesigned` command before you can deploy normally. In addition, we recommend you use the `serverless deploy` method to deploy in the Windows environment.
