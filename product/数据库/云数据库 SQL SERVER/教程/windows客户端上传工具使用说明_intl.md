## Tool Usage

>Note: Official support for this upload tool has been terminated. You are recommended to use COS for data migration.

1. After downloading the [Windows Client Upload Tool](https://mc.qcloudimg.com/static/archive/ef1dec9f9a72cbafdc707915475a368e/upload.zip) to the local storage, decompress it to any folder (note: no Chinese characters are allowed in the path). The decompressed directory structure is as follows:
![](https://mc.qcloudimg.com/static/img/716da8b5ece00ca2be062e2b637ff40d/1-1.png)

2. In order to protect the security of your data, before the backup is uploaded, you need to edit the configuration file etc\conf.json and enter your own API key ([secretId and secretKey](https://console.cloud.tencent.com/cam/capi)). Please be sure to keep your API key private and avoid disclosure. To ensure the stability of the transfer process, this tool now supports transfer resuming;
Note: Please save the conf.json file in "UTF-8 without BOM" (it is recommended to convert the code with Notepad++ in Windows).

![](https://mc.qcloudimg.com/static/img/8cd149b24b1be3df87371081fa8cad39/1-2.png)

3. Open Windows Command Prompt by entering "cmd" in the search box in the Start menu.

![](https://mc.qcloudimg.com/static/img/57dadbb324f56172f7a5c0f825e91d9b/1-3.png)

4. In Windows Command Prompt, go to the decompressed "Windows Client Upload Tool" directory and call upload-tool.exe in the bin directory to complete the upload operation. upload-tool.exe has two parameters: -r and -p. -p indicates the absolute local path of the backup file; -r indicates the region where the transit storage is located (please select the region where your TencentDB is located);
![](https://mc.qcloudimg.com/static/img/a4390e737e6367d860e2037c7b5068f3/1-4.png)

## Region Details

| Region | -r parameter |
|---------|---------
| Guangzhou | gz | 
| Shanghai | sh |
| Hong Kong | hk | 
| Shanghai Financial | shjr | 
| Beijing | bj | 
| Shenzhen Finance | szjr | 

Note: The identifier is case-sensitive.
