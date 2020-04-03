## Common exceptions
- LogListener is installed successfully but failed to report data.
- An error occurs while LogListener is reporting data.

## Troubleshooting steps

1. Change the log level for LogListener.
Open the `etc/loglistener.conf` configuration file, set `level` to `DEBUG` and restart LogListener.
![](https://main.qcloudimg.com/raw/05bc0bec901147c2b9e6550a85fa7d82.png)
In the installation directory, run the following command to restart LogListener.
```shell
cd loglistener/tools && ./start.sh
```
>Restarting LogListener does not cause log loss.
2. Check that logs are successfully reported.
In the installation directory, run the following commands:
```shell
cd loglistener/log
tail -f loglistener.log | grep "ClsFileProc::readFile" | grep send
```
If log information similar to that shown in the following is displayed, logs are successfully reported to the service backend.
![](https://main.qcloudimg.com/raw/109530d249ed468b5ae2c43b3b1e2341.png)
>If logs are reported through HTTP, you can capture packets from port 80 to identify whether logs are successfully reported.

 If logs are not successfully reported to the backend, perform the following steps to locate the cause:
 1. Run the following commands in the installation directory to check whether the LogListener collection configuration is correct.
```shell
cd loglistener/log
tail -f loglistener.log | grep "ClsServerConf::load"
```	
	If the configuration has been delivered, log information is as follows:	
![](https://main.qcloudimg.com/raw/d8b24591c6f601af31e57cab8995fd52.png)
	In the delivered configuration, check whether the information of `log_type` and `path` is correct:	
	- `log_type` indicates the log parsing type. Its values include `minimalist_log` (full text in a single line), `delimiter_log` (separator), `json_log` (JSON logs), and `regex_log` (full text in multi lines).	
	- `path` indicates the log collection directory.
 2. Run the following command in the installation directory to check whether files are correctly listened to:
```shell
cd loglistener/log && grep [Name of the reported log file] loglistener.log
```
    - If log information shown in the following figure is displayed, the file is being listened to:
   ![](https://main.qcloudimg.com/raw/1c073b7ff908ab125a45be5849f2e9fe.png)
    - If no log information is displayed, run `grep regex_match loglistener.log` to search for log information and check whether the regular expression is correctly configured in the console. If the content shown in the following figure is displayed, the file name match based on the regular expression fails, and you need to log in to the console to change the regular expression.
![](https://main.qcloudimg.com/raw/8b9756fc97dc9fe38e49ddde4fb20335.png)
    - If the file is not listened to successfully, check whether the log mount point is a NAS, CIFS, or NFS shared directory. LogListener does not support log collection from such directories.

 3. Check whether the log regular expression parse is correct.
	For the extraction modes of full regular expression and full text in multi lines, regular expressions need to be specified. For full text in multi lines, the first line regular expression must match the entire content of the first line, instead of the beginning part of the first line.
	Use the log content shown in the following figure as an example. Lines beginning with `INFO`, `ERROR`, and `WARN` are the first lines of logs. In addition to `(INFO|ERROR|WARN)`, the characters following `INFO`, `ERROR`, and `WARN` also need to be matched.
![](https://main.qcloudimg.com/raw/c43a440e46ca0ff82d21275d90557e44.png)
    -  Incorrect configuration: `^(INFO|ERROR|WARN)`
    -  Correct configuration: `^(INFO|ERROR|WARN).*`
